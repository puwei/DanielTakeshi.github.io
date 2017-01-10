---
layout: post
title:  "Some Interesting Artificial Intelligence Research Papers I've Been Reading"
date:   2017-01-09 19:00:00
permalink: 2017/01/09/some-interesting-artificial-intelligence-research-papers-ive-been-reading/
---

One of the advantages of having a four-week winter break between semesters is
that, in addition to [reading interesting, challenging non-fiction books][1], I
can also catch up on reading academic research papers. For the last few years,
I've mostly read research papers by downloading them online, and then reading
the PDFs on my laptop while taking notes using the Mac *Preview* app and its 
highlighting and note-taking features. For me, research papers are challenging
to read, so the notes mean I can write stuff in plain English on the PDF.

However, there are a lot of limitations with the Preview app, so I thought I
would try something different: how about making a GitHub repository which
contains a list of papers that I have read (or plan to read) and where I can
write extensive notes. [The repository is now active][2]. Here are some papers
I've read recently, along with a one-paragraph summary for each of them. All of
them are "current," from 2016.

- **Stochastic Neural Networks for Hierarchical Reinforcement Learning**, arXiv,
  by Carlos Florensa et al. This paper proposes using Stochastic Neural Networks
  (SNNs) to learn a variety of low-level skills for a reinforcement learning
  setting, particularly one which has *sparse rewards* (i.e. usually getting 0s
  instead of +1s and -1s). One key assumption is that there is a *pre-training*
  environment, where the agent can learn skills before being deployed in
  "official" scenarios. In this environment, SNNs are used along with an
  information-theoretic regularizer to ensure that the skills learned are
  *different*. For the overall high-level policy, they use a *separate* (i.e.
  not jointly optimized) neural network, trained using Trust Region Policy
  Optimization. The paper benchmarks on a swimming environment, where the agent
  exhibits different skills in the form of different swimming directions. This
  wasn't what I was thinking of when I thought about *skills*, though, but I
  guess it is OK for one paper. It would also help if I were more familiar with
  SNNs.

- **#Exploration: A Study of Count-Based Exploration for Deep Reinforcement
  Learning**, arXiv, by Haoran Tang et al. I think by *count-based reinforcement
  learning*, we refer to algorithms which explicitly keep track of $$N(s,a)$$,
  state-action visitation counts, and which turn that into an exploration
  strategy. However, these are only feasible for small, finite MDPs when states
  will actually be visited more than once. This paper aims to blend count-based
  reinforcement learning to the high-dimensional setting by cleverly applying a
  *hash function* to map states to hash codes, which are *then* explicitly
  counted. Ideally, states which are similar to each other should have the same
  or similar hash codes. The paper reports the surprising fact (both to me and
  to them!) that such count-based RL, with an appropriate hash code of course,
  can reach near state of the art performance on complicated domains such as
  Atari 2600 games and continuous problems in the RLLab library.

- **RL^2: Fast Reinforcement Learning via Slow Reinforcement Learning**, arXiv,
  by Rocky Duan et al. The name of this paper, RL^2, comes from "using
  reinforcement learning *to learn* a reinforcement learning algorithm,"
  specifically, by encoding it inside the weights of a Recurrent Neural Network.
  The hope is that the RNN can help encode some prior knowledge to accelerate
  the training for reinforcement learning algorithms, hence "fast" reinforcement
  learning. The slow part is the process of training the RNN weights, but *once
  this is done*, the RNN effectively encodes its own reinforcement learning
  algorithm! Ideally, learning this way will be faster than DQN-based and policy
  gradient-based algorithms, which are brute-force and require lots of samples.
  One trouble I had when reading this paper was trying to wrap my head around
  what it means to "learn a RL algorithm" and I will probably [inspect the
  source code][4] if I want to really understand it.  Some intuition that might
  help: experiments are applied on a *distribution* of MDPs, i.e., randomly
  sampling closely-related MDPs, because the high-level learning process must
  *optimize* over something, hence it optimizes over the MDP distribution.

- **Deep Visual Foresight for Planning Robot Motion**, arXiv, by Chelsea Finn et
  al. This paper takes an important step in letting robots predict the outcome
  of their own actions, rather than relying on costly human intervention, such
  as if a human were to collect data and provide feedback. In addition, models
  that are hand-engineered often fail on real, unstructured, open-world
  problems, so it makes sense to abstract this all away (i.e. pull humans out of
  the loop) and *learn* everything. There are two main contributions of the
  paper. The first is a deep predictive model of videos which, given a current
  frame and a sequence of future actions, can predict the *future* sequence of
  frames. Naturally, it uses LSTMs. (Note that these "frames" are --- at least
  in this paper --- images of a set of objects cluttered together.) The second
  contribution is a Model Predictive Control algorithm which, when provided raw
  pixels of the environment and the goal, can determine the sequence of actions
  that maximizes the probability of the designated pixel(s) moving to the goal
  position(s). The experiments test *nonprehensile motion*, or motion which does
  not rely on grasping but pushing objects, and show that their algorithm can
  successfully learn to do so with minimal human intervention.

- **Value Iteration Networks**, NIPS 2016 (Best Paper Award), by Aviv Tamar et
  al. This introduces the *Value Iteration Network*, which is a neural network
  module that learns how to plan by computing an approximate version of value
  iteration via convolutional neural networks. I *think* I understand it: the
  number of actions is the number of channels in a convolutional layer, which
  themselves represent $$\bar{Q}(s,a)$$ values, so by max-pooling over that
  channel, we get $$\bar{V}(s)$$. VINs are differentiable, so by inserting it
  inside a larger neural network somewhere, it can be trained using *end-to-end*
  backpropagation. The motivation for VINs is from an example where they sample
  MDPs from a *distribution* of MDPs, specifically for Grid-World scenarios
  where start/goal states and obstacles are randomly assigned. When training on
  a fixed Grid-World, a DQN or similar algorithm can learn how to navigate it,
  but it will be unlikely to generalize on a newly sampled Grid-World.  Hence,
  the agent is not *learning how to plan* to solve "Grid-World-like" scenarios;
  it doesn't understand the goal-directed nature of the problem. More generally,
  agents need to plan on some model of the domain, rather than a fixed MDP. This
  is where VINs help, since they enable the entire agent architecture to map
  from observations to not only actions, but to *planning computations*. Another
  contribution of their paper is the idea of using another MDP, which they
  denote as $$\bar{M}$$ along with the subsequent $$\bar{s}, \bar{\pi}$$, etc.,
  and then utilizing the solution to that for the original MDP $$M$$.

- **Principled Option Learning in Markov Decision Processes**, EWRL 2016, by Roy
  Fox et al. This paper is about hierarchical reinforcement learning, where the
  "sub-policies" at the base of the hierarchy are called "options", and the
  higher-level policy is allowed to pick and execute them. This paper assumes a
  prior policy on an agent, and then uses information theory to develop options.
  For instance, in a two room domain, if we constrain the number of options to
  two, then one option should automatically learn to go from left to right, and
  another should go from right to left. The hardest part about understanding
  this paper is probably that there is no clear algorithm that connects it with
  the overall MDP environment. There's an algorithm there that describes how to
  learn the options, but I'm still not sure how it works from start-to-finish in
  a clean MDP.

- **Taming the Noise in Reinforcement Learning via Soft Updates**, UAI 2016, by
  Roy Fox et al.  This paper introduces the *G-learning* algorithm for
  reinforcement learning, which I've correctly implemented (I hope) in my
  [personal reinforcement learning GitHub][3] repository. The central motivation
  is that the popular Q-learning algorithm learns *biased estimates* of the
  state-action values due to taking the "max" operator (or "min" in the case of
  costs). Therefore, it makes sense to use "soft updates" where, instead of
  taking the single best "successor action" as in the standard Q-learning
  temporal difference update, we use *all* of the actions, weighted according to
  probability. This is, I believe, implemented by imposing a *prior policy* on
  the agent, and then formulating an appropriate cost function, and *then*
  deriving a $$\pi(a'|s')$$ which enforces the "softness." The G-learning
  algorithm relies on a tuning parameter which at the start of training values
  the prior more, and then as time goes on, G-learning gradually shifts to a
  more deterministic policy. The G-learning update is similar to the Q-learning
  update, except it uses information-theory to mitigate the effect of bias. I
  haven't been able to do the entire derivation.

Aside from these papers being Artificial Intelligence-related, one aspect that
seems to be common to these papers is the need for either *hierarchical
learning* or *increased abstraction*. The former can probably be considered a
subset of the latter since we "abstract away" lower-level policies in lieu of
focusing on the higher-level policy. We can also abstract away the process of
choosing MDPs or a pipeline and just *learn* them (e.g., the Deep Visual
Foresight and the RL^2 papers). That might be something useful to keep in mind
when doing research in this day and age.

[1]:https://danieltakeshi.github.io/2016/12/31/all-the-books-i-read-in-2016-plus-my-thoughts-long
[2]:https://github.com/DanielTakeshi/Paper_Notes
[3]:https://github.com/DanielTakeshi/rl_algorithms
[4]:https://github.com/openai/gym/pull/416
