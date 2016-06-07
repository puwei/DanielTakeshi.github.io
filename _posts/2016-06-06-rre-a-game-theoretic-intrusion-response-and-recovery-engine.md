---
layout: post
title:  "RRE: A Game-Theoretic Intrusion Response and Recovery Engine"
date:   2016-06-06 21:00:00
permalink: 2016-06-06-rre-a-game-theoretic-intrusion-response-and-recovery-engine/
---

During the past two months, I have been reading more research papers after not doing so for much of
the spring 2016 semester. One paper I recently read is *[RRE: A Game-Theoretic Intrusion Response
and Recovery Engine][1]*, a February 2014 IEEE Transactions on Parallel and Distributed Systems
paper written by four computer engineering researchers. As suggested by the publication venue, it's
a systems and networking paper, but there's an interesting connection to Artificial Intelligence. It
also looks like it has had a noticeable impact, with 106 Google Scholar citations today, which is
good for a 2014 paper.  In this post, I'll provide a brief summary of the RRE paper.

The paper considers the scenario of defending a computer network system from outside intrusions,
which for many reasons is *very* common and *very* important nowadays. The traditional way to do
this is to have some administrators and IT staff inspect the system and respond to attacks.
Unfortunately, this is slow and hard to scale, and attackers are becoming increasingly
sophisticated, meaning that we need *automated* responses to preserve the availability and integrity
of computer systems. Hence, we have the Response and Recovery Engine (RRE) as a possible solution.

Their proposed RRE uses a two-tiered design for handling local and global situations.  At the local
level, individual computers have their own RREs, which take as input [Intrusion Detection System][3]
(IDS) alerts and Attack Response Trees (ARTs). IDS alerts are a well-known computer networking
concept, but ARTs are part of their new research contribution. ARTs analyze possible combinations of
attack consequences that lead to some intrusion of system assets (e.g., SQL servers) and are
designed offline by experts. ARTs allow RREs to (a) understand the cause and effects of different
system problems and (b) decide on appropriate security responses. Another important aspect of ARTs 
is that its root node, denoted $$\delta_g$$, represents the probability that the overall security
property it represents has been compromised. The value of $$\delta_g$$ can be computed using
straightforward probability recurrence rules, so long as nodes in the ARTs are assumed independent.
The recurrence starts at the leaves of the ART, which each take as input a set of IDS alerts and use
a Naive Bayes binary classifier to determine the probability that the leaf node property has
happened or not.

Using these ARTs, the authors nicely transform the security problem into a *Partially Observed
Markov Decision Process* (POMDP), which they technically call a Partially Observed *Competitive*
Markov Decision Process (POCMDP). First, an ART with $$n$$ leaf nodes is automatically converted to
a *standard* (i.e., fully observed) Markov Decision Process. The states $$s$$ are $$n$$-dimensional
binary vectors, with one element for each leaf, and the value matching whatever the leaf node has in
the ART. The set of *actions* $$A$$ for this MDP is split into sets $$A_r$$ and $$A_a$$,
representing the set of actions for the RRE and the attacker, respectively. These actions have the
effect of changing the values in the ART leaves; responses generally result in more zeros, and
attacks typically result in more ones. (ARTs are designed so that nodes tend to represent *negative*
events, hence we want more zeros.) The transition probabilities are determined from prior data, and
the reward function $$r(s,a,s')$$ is customized so that it takes into account the probability
difference in the security property (i.e., $$(\delta_g(s) - \delta_g(s'))^{\tau_1}$$ for $$0\le
\tau_1 \le 1$$), as well as the cost of executing the action. Here's a brief exercise left to the
reader: why is $$\delta_g(s') \le \delta_g(s)$$?

After formulating the MDP, the paper suddenly reminds us that we don't actually have full knowledge
of our states $$s$$ (which makes sense in reality). Thus, we are in the *partially observed* case.
According to their formulation, the probability of being in a state $$s$$, denoted as $$b(s)$$, is

$$b(s) = \prod_{l \in \mathcal{L}}(1_{[s_l = 1]}\delta(l) + 1_{[s_l=0]}(1-\delta(l)))$$

This makes sense and is consistent with the paper's notation; I will leave it to the reader to
review the paper if he or she wishes to verify this formula. They then outline how to solve the
POMDP (based on their MDP formulation) using standard value iteration techniques. Note that they
call their formulation a POCMDP (as stated earlier) because they add the "Competitive" word to the
name, but I don't think that is necessary. As [I discussed near the end of this blog post on
reinforcement learning][2], one can formulate a standard MDP in terms of a two-player adversarial
game. They are simply making the distinction between action sets clearer here, perhaps for the
benefit of the reader who is not familiar with Artificial Intelligence.

Another interesting note about their POCMDP formulation is that *we do not actually need ARTs* ---
the *POCMDPs* are all that is necessary, but they are harder to design and they have an exponential
state space compared to the ARTs, so it is best to let experts design ARTs and automatically build
the POCMDPs from it. This certainly makes sense from a practical perspective.

The process above is similar for the *global* case. The global RRE takes as input the recursively
computed $$\delta_g$$ values for each local RRE, the probability that the security property of the
local assets have been compromised. It then uses these to automatically formulate a CMDP to help
guide overall network priorities. To add finer-grained control over the states, the authors augment
the system with *fuzzy logic*, allowing partial memberships. (See the [Fuzzy Sets Wikipedia page][4]
for background on fuzzy sets.) This means they can combine information from local engines to
determine a probability for a global security property. Their canonical example of the latter: *is
the network secure?* Overall, this section of the paper is not as clear as the one describing local
RREs, and while I understood the basics on how they used fuzzy logic, I wish there was enough space
in the paper for a clearer explanation of how they form the global CMDP.

After their global RRE description, the authors present some brief experimental results on how long
it takes to form the MDP models and on the runtime for RREs to compute an optimal response action.
In general, their experiments are short and not that informative since they rely on randomly
generated networks. To be fair, it is probably harder to run benchmarks in networking papers as
compared to machine learning papers. In the latter case, we have standard datasets on which to test
our algorithms.

The disappointing experiments notwithstanding, I enjoyed this paper. I fortunately did not need much
networking or systems background to understand it, and it is nice to see different ways of how MDPs
get formulated. It certainly falls prey to lots of simplifying assumptions, but I don't see how that
can be avoided for a research paper.

[1]:http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=6583161&url=http%3A%2F%2Fieeexplore.ieee.org%2Fiel7%2F71%2F4359390%2F06583161.pdf%3Farnumber%3D6583161
[2]:http://danieltakeshi.github.io/2015-08-02-markov-decision-processes-and-reinforcement-learning/
[3]:https://en.wikipedia.org/wiki/Intrusion_detection_system
[4]:https://en.wikipedia.org/wiki/Fuzzy_set
