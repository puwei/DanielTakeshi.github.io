---
layout: post
title:  "Closing Thoughts on Graphical Models"
date:   2015-07-15 12:00:00
permalink: 2015-07-15-closing-thoughts-on-graphical-models/
---

## The Basics

There are two main types of graphical models: directed (**Bayesian Networks**) and undirected
(**Markov Random Fields**). There are also chain graphs that mix the two, but I will ignore those
for now. Bayesian Networks are interesting because they let us model generative processes. We can
look at arrows in a diagram and think: oh, there's an arrow from $$X_1$$ to $$X_2$$, hence the
former variable must have some kind of causal relationship with the latter. Then we can continue
that line of thinking to "generate" each variable. For a Markov Random Field, we can think of there
being a local structure to the nodes.

One of the main reasons why people like graphical models is that it helps us concisely express
probability distributions. If we have a distribution $$P(X_1,X_2,\ldots,X_n)$$ where $$n$$ is in the
hundreds (a typical real-world case) a naive tabular representation of the distribution is out. But
with a Bayesian Network, what we can do is decompose the joint into node-parent conditional
probability tables (CPTs). Using the chain rule on a Bayesian Network, with nodes listed in a
topological ordering[^topological], we can decompose the joint into distributions of each node, and
then use the independence assumption to get rid of (hopefully lots of!) certain variables being
conditioned on in $$P(X_i \mid X_1, X_2, \ldots, X_{i-1})$$. For a Markov Random Field, we can
decompose the joint probability into a *product of functions on maximal cliques*,
$$P(X_1,\ldots,X_n) \propto \prod_{X_C \in \mathcal{C}} \psi_C(X_C)$$, where $$\mathcal{C}$$ is the
set of maximal cliques of the graph[^cliques]. One of the most confusing things about the clique
functions $$\psi$$ is that they are *not* (generally) probability distributions! All we require is
that they are an arbitrary, local non-negative function. To enforce non-negativity, it is common to
exponentiate functions, thus we often see these expressed in terms of exponentials[^interesting].
Note: it's important to understand the high-level idea here. In both the directed and undirected
cases, we have figured out a way to efficiently decompose the joint into the product of functions
that act on a *local* set of nodes.

Given that we have decomposed the joint distribution in terms of products of local functions, it's
important to realize that, while we've obviously imposed some "constraints" on the graph, a graphical
model still expresses a *family* of distributions. In a three-node "chain" Bayesian Network, which
means $$P(X_1,X_2,X_3) = P(X_1)P(X_2\mid X_1)P(X_3\mid X_2)$$, we are allowed to tweak the three
CPTs of our graph, so long as the product still obeys a probability distribution (i.e., non-negative
and sums to one). For a Markov Random Field, we can tweak the potentials.

There is also an equivalent way of expressing the family of distributions inherent in a graphical
model. We can do that by listing all the conditional independences enforced by the graph. This means
that for all triplets of disjoint variable sets $$X_A,X_B,X_C$$ which are a subset of all the
variables in the graph, we need to check whether $$X_A \perp X_B \mid X_C$$. By taking the set of
distributions that factor according to these independences, we find that they are equivalent to what
we would get if we started with the node-parent probabilities and "tweaked the CPTs."

It's easiest to determine whether $$X_A \perp X_B \mid X_C$$ in the undirected case, because to
determine whether such a statement is true (and therefore should be listed in that list of
independences) we delete the nodes of $$X_C$$ and check whether a path still exists from $$X_A$$ to
$$X_B$$.

The directed case is a little more complicated, but more intellectual. We run something called the
**Bayes Ball** algorithm. To explain this, we first consider three canonical graphs: a chain $$A
\rightarrow B \rightarrow C$$, a wedge $$A \leftarrow B \rightarrow C$$, and (the most interesting
case) a v-node $$A \rightarrow B \leftarrow C$$. The rules are as follows:

* In the chain, $$A \perp C \mid B$$. No other assertions are possible.
* In the wedge, $$A \perp C \mid B$$. No other assertions are possible.
* In the v-node, $$A \perp B$$. No other assertions are possible.

To explain the third case in more detail is to understand the **explaining away** phenomenon. This
happens when we have two or more competing clauses that attempt to explain the same thing. Those
clauses are independent of each other, but once we observe the $$C$$ variable, then all of a sudden
they are dependent on each other, because if one of them "caused" $$C$$, it is likely that the other
one did *not*. But without $$C$$, we can't say much. Kevin Murphy [has a nice example on his
tutorial page](http://www.cs.ubc.ca/~murphyk/Bayes/bnintro.html), where a college only admits smart
students, or athletes, and those variables are independent in the population. Then if we see that a
student is at the college, then we can "explain" this phenomenon in two ways: if the student is
smart, or an athlete.

To run the Bayes Ball algorithm, we "shade in" the nodes of $$X_C$$, which serve intuitively as
"blocking" nodes. We start with balls in nodes from $$X_A$$, and see if *any one of them* can reach
any node in $$X_B$$, subject to constraints on the movements of the balls due to the canonical
graphs. Note that there are a few other special cases that we have to consider. If we have a chain
$$A \rightarrow B$$ but $$B$$ has no other children, then the ball is allowed to "return" in the
opposite direction, *so long as* $$B$$ *is* shaded. It is as if there is a *duplicate* $$A$$ node,
which would be like applying case three with the v-node, and balls only pass in that case if the
$$B$$ node is shaded.

So, if you are ever given a Bayesian Network and have to determine whether certain conditional
independences hold, just as in the [Spring 2011 Berkeley AI
final](https://s3-us-west-2.amazonaws.com/cs188websitecontent/exams/sp11_final.pdf), just run the
Bayes Ball algorithm.

By the way, it should be clear from the above that identifying conditional independences is easier
for the undirected case, which is what tends to motivate their formulation, but for the directed
case, it's easier to think of them in terms of node-parent probabilities. But we could try thinking
of them in the opposite way.

## The Sum-Product Algorithm and Factor Graphs

In [my last post](http://danieltakeshi.github.io/notes-on-exact-inference-in-graphical-models/), I
described two ways of performing exact inference on general graphical models. That's actually not
the final word on exact inference: it is possible to develop a more useful version of variable
elimination, *under the assumption that the graphical model is a tree*. This is not that
restrictive, since we *can* express a lot of real-world problems in terms of trees.  The key
advantage of the algorithm known as the Sum-Product Algorithm[^name] is that it lets us compute *all
marginals* simultaneously. If you recall, in variable elimination, I assumed that we only had one
query node, so that algorithm would have been useful for $$P(X_i \mid e)$$, but not $$P(X_i,X_j \mid
e)$$. Fortunately, with trees, we can compute *all* of $$P(X_i)$$ for each node. Including evidence
isn't a problem; we can also compute $$P(X_i,e)$$. Remember that we should consider marginals and
conditionals as equivalent.

How does it work? Remember how in variable elimination, we would create intermediate values
$$m_i(...)$$ for node $$X_i$$ as it got eliminated? We will do a similar thing here; these $$m_i$$
are now technically called messages and we can index them as $$m_{ij}(...)$$ to describe a message
from node $$X_i$$ to $$X_j$$, where node $$X_i$$ was the one that got eliminated.

The Sum-Product algorithm begins message-passing at the leaf nodes of the graph by eliminating them
and passing their intermediate messages (the $$m_i$$ functions) to their neighbors. Then the process
repeats. The rule is that each node can only send a message to another node, as long as it has
received messages from all its *other* neighbors. Since the graph is a tree, this immediately
implies that messages have to start at the leaves (as stated earlier) and, furthermore, that *no
new edges will be created* in the elimination process.

To be precise, the formula for a message from $$X_j$$ to $$X_i$$ (hence, eliminating $$X_j$$) is:

$$m_{ji}(x_i) = \sum_{x_j} \psi^E(x_j) \psi(x_i,x_j) \prod_{k \in \mathcal{N}(j)\setminus i} m_{kj}(x_j)$$

This equation is from Michael I. Jordan's notes on graphical models. Don't worry too much about the
notation, but here is a little about it: the $$\psi^E$$ function is his way of including evidence
variables[^evidence]. The $$\psi(x_i,x_j)$$ is the potential function on the maximal clique of
$$X_i$$ and $$X_j$$; in trees, the maximal cliques are always of size two. The interesting stuff
comes when we consider the $$m_{kj}$$ functions. These are all the other *incoming* messages from
the neighbors of node $$X_j$$, *except* $$X_i$$. This should remind us of variable elimination. When
we eliminate nodes, we pass intermediate factors back to whatever node has dependency on it. Since
we are in a tree, that means the intermediate message will have a dependency on whatever neighbor is
*remaining*. That is why the $$m_{kj}$$ functions depend on $$x_j$$, but the $$m_{ji}$$ function
depends on $$x_i$$ (not $$x_j$$).

Oh, by the way, we are dealing with *undirected* graphs here, not directed ones. We can treat these
on equal footing because we have trees, so in the undirected case, $$\psi(x_i,x_j) = P(x_j \mid
x_i)$$, and the singleton potentials are either 1, or $$P(x_r)$$ for the root[^potentials].

At the root node, we can determine the marginal probability as proportional to the product of
incoming messages, where the proportionality can be resolved by iterating over the possible
states/realizations for the root node.

That's nice, but how do we determine marginal probabilities for *all* nodes? When we did this for
the root node, it was as if the messages started from the leaf nodes and *propagated inwards*
towards the root node, due to the protocol that a node couldn't send a message unless it got
messages from all other neighbors. The clever insight is that we now propagate messages *outwards*
from the root node, into all the leaves! What happens after this is that *every edge in the tree now
has two messages on it, in opposite directions*. Then, for each node, take the product of its
incoming messages. We now have marginal probabilities for all nodes! The amazing thing is that this
only requires double the amount of work it took for the first step to send messages inwards to the
root. Unfortunately, as mentioned earlier, this only works on trees. But it definitely works well.

Taking another perspective, suppose we were not interested in determining a distribution, but wanted
to do MAP inference. That means figuring out the maximum probability possible in any configuration
(or determining the actual configuration itself). To do that, just replace the "sum" operators with
"max" operators in the formulas, and things will work from there[^semiring].

Finally, let us consider factor graphs, briefly. Given an undirected graph, we can associate with it
a set of factors $$\mathcal{F}$$, where each factor $$f_i(X_{f_i})$$ is a function on a *set* of
nodes. The sets may not be unique among different factor functions, and they might not also
correspond to maximal cliques. Actually, the one thing we really want them to obey is that there is
a giant factor function $$f$$ of all the variables that can be "factorized" (hence the name) into
the individual factors, and that we can evaluate for one factor efficiently (kind of reminds one of
probabilities and potentials, huh?). Then when we draw the graph, the only edges that exist are
those from normal nodes $$X_j$$ to factor nodes $$f_i$$, and an edge exists between them if and only
if the factor function $$f_i$$ takes node $$X_j$$ as input.

Some advantages of factor graphs are that:

* Sometimes, we want to express a family of probability distributions at a finer level than is
  possible with conditional independences. Factor functions let us be arbitrarily precise in how we
  want to model the interactions between variables, while potential functions are more limited.
  With the complete graph $$\mathcal{K}_3$$, no conditional independence assertions are possible but
  we might want to endow the sole potential with some structure: $$\psi(x_1,x_2,x_3) =
  f_a(x_1,x_2)f_b(x_2,x_3)$$, but note that adding extra nodes can do the same thing[^representation].
* We can convert undirected trees that are "almost" like trees (perhaps they have just one clique of
  size three) into factor graphs that are trees, ignoring the distinction between factor and
  variable nodes.
* We can apply a similar version of the sum-product algorithm to factor trees, which uses
  messages from nodes to factors and factors to nodes, *even if* the original tree (before the
  factorization was added) was not actually a tree.

There are also *directed* graphs that are almost like trees, e.g., *polytrees*, which are trees if
we drop the orientation of edges, but they also have multiple parents to each node, which poses a
problem if we do any moralization. We can convert these to factor trees (yes, *trees*) and directly
apply the Sum-Product algorithm.

## Sampling for Graphical Models

In many cases, exact inference is intractable in graphical models, so we resort to *approximate*
methods. Here, I'll briefly review approximate inference in Bayesian Networks, with an emphasis on
**particle-based** methods, which generate samples from the network.

One confusion I originally had when I first learned about this was that it was unclear what
assumptions we were making about the information we possessed. To clarify, we're going to assume
that we know *all* the CPTs[^discrete] of the graph, but that's it.  The goal will be to generate a
*full set of samples* from this CPT. That means if there are $$n$$ variables in the Bayesian
Network, we want to obtain samples $$(X_1,X_2,\ldots,X_n)^{(i)}$$ for large $$i$$.

Using the CPTs, how do we sample? Here's an almost trivial method, often called **direct sampling**:
we iterate through the variables in a topological ordering, and for each one, sample its
*state*[^jordan] from its CPT. The parents of the node in question (if any) must be set to the value
that they were sampled at earlier, which we know happened due to the topological ordering. Once
we've gone through all samples, we repeat.

In the general case, we'll want to make use of whatever *evidence* variables we have in $$P(X \mid E
= e)$$, which direct sampling fails to consider. To do so, we can use **rejection sampling**, which
means that we do direct sampling, but only keep the full samples that are consistent with the
evidence $$E = e$$. Unfortunately, as the evidence increases, it gets increasingly unlikely that we
will ever generate a compatible sample! To fix the problem of rejecting too many samples, we can use
**likelihood weighting** which will force the evidence variables to be at their fixed values. That
is to say, given a network of $$n$$ variables where we want to sample full elements that have $$X_i
= 2$$, then we would fix that value and sample the other $$n-1$$ variables normally with the direct
sampling method.

Unfortunately, even this doesn't work out well, because we actually have to weigh the samples we get
by the value of the evidence variables! It's easiest to think of likelihood weighting as always
generating compatible samples, but *each sample is actually worth only a fraction of a sample*,
quantified by its weight $$w$$. We compute a sample's weight by multiplying the $$P(X_i = x_i \mid
X_{\pi_i})$$ values of the evidence variables together. Intuitively, evidence variables that seem to
be incompatible with the sampled variables should result in a smaller weight for the full sample.

Rejection sampling and likelihood weighting are two valid sampling methods, but they generate full
samples independently of each other. The class of **Markov Chain Monte Carlo** methods assume that
consecutive, full samples are (weakly) correlated with each other. **Gibbs Sampling** is the most
well known of these samples. Given $$(X_1,X_2,\ldots,X_n)^{(i)}$$, it goes through each variable one
by one and generates a sample for variable $$X_j$$ in the $$(i+1)$$th element by using the
conditional distribution

$$P(X_j^{(i+1)} \mid X_1^{(i+1)}, \ldots, X_{j-1}^{(i+1)}, X_{j+1}^{(i)}, \ldots, X_{n}^{(i)})$$

Thus, it relies on the newly generate samples for the first $$j-1$$ variables, but for the remaining
variables, it uses the values of the *previous* sample. Hence the correlation between consecutive
samples.

But wait, in a Bayesian Network, we can say more! The probability of a variable, conditioned on all
the other variables, is simply that conditioned on the *Markov blanket* of a variable, which
consists of itself, its parents, its children, and the parents of those children! We need to make an
important distinction: when we say that $$P(X_i \mid X_1, \ldots, X_{i-1}) = P(X_i \mid X_{\pi_i})$$
in Bayesian Networks, that is only because we list variables in a topological ordering.  If the
variable is conditioned on *all other variables* in the network, we can only simplify by eliminating
variables that are outside the Markov blanket $$mb(X_j)$$ of a node.  Precisely, Gibbs sampling
would sample from the following distribution:

$$P(X_j \mid mb(X_j)) \propto P(X_j \mid X_{\pi_j}) \prod_{Y_j \in C(X_j)} P(Y_j \mid Y_{\pi_j}),$$

where $$C(X_j)$$ denotes the set of children nodes of node $$j$$.

Note: with evidence variables, we just don't sample them in Gibbs sampling (which also applies to
other sampling methods).

Putting all this together, what does it really mean when we generate full samples? How do these
actually help us with a query? An example would clarify. If we are making the query $$P(X_1 \mid X_2
= x_2, X_3 = x_2)$$, but this is *not* a node-parent probability (i.e., it is not listed in the CPTs
anywhere) we need to sample to figure out the distribution of $$X_1$$. Thus, we would generate full
samples. We can then compute the desired distribution by looking at the value of $$X_1$$ generated
in all those samples that have $$X_2 = x_2$$ and $$X_3 = x_3$$ (i.e., that are consistent). In other
words, it's a maximum likelihood estimate.

## What I Would Study Next

If I had all the time in the world to study graphical models, here's what I would study next: the
*junction tree algorithm*. This is an extension of variable elimination and the sum-product
algorithm in that it performs exact inference on general graphical models as efficiently as
possible. To do that, it has to transform the graph into what's known as a *junction tree* (hence
the algorithm name). Unfortunately, that's about all I know about the algorithm.

***

[^topological]: When people discuss Bayesian Networks, they *almost always* assume that nodes have a
    topological ordering.

[^interesting]: In fact, even though splitting up the joint distribution for Bayesian Networks in
    terms of the product of node-parent conditional probabilities makes more sense than whatever the
    heck is going on with potentials, it's not at all clear that we are allowed to do that! But as
    shown in Michael I. Jordan's notes, the technical conditions we assume are that we can split up
    the joint in terms of a product of arbitrary, non-negative functions $$f_i(X_i,...)$$ that act
    on a local set of nodes, in which if we sum up over values of $$X_i$$, $$f_i = 1$$. To actually
    get our node-parent formalism, we assume that the $$f_i$$ functions can take the parents as
    "input," and by showing that the sum of the entire product with respect to all the variables is
    one, we can prove that the functions $$f_i(X_i,...)$$ must *exactly* correspond to the
    conditional probability functions of $$X_i$$ given its parents! Weird! Of course, things are
    different in the undirected case, in which case it is easiest for us to simply abandon
    conditional probabilities altogether when figuring out how to decompose the joint.

[^name]: Ben Recht: "You know what it's called? The Sum-Product Algorithm. [Laughs] I mean, come on,
    can't we come up with better names here?"

[^discrete]: Again, we will continue the assumption that we have discrete random variables.

[^jordan]: Michael I. Jordan seems to prefer the term *realization*.

[^potentials]: In that sense, potentials here *do* loosely correspond to probability distributions.
    In general, if there is an easy way for us to map potentials to probabilities, we do that since
    it makes understanding them easier.

[^evidence]: What happens is that he assumes we will always be summing over a variable, but that we
    will repeatedly multiply an indicator function to indicate evidence, so $$\sum_x P(x \mid
    \pi_x)$$ is really $$\sum_x P(x \mid \pi_x)\psi(x,\overline{x})$$, where $$\overline{x}$$ is a
    fixed evidence value of $$x$$. All this is really formal trickery. In practice, if we know a
    value is fixed, we just take the appropriate slice from the CPT; we would *not* sum up over its
    values if we know that the indicators will be zero everywhere. But understanding the $$\psi$$
    notation is helpful to understand the rest of his notes.

[^semiring]: The reason why replacing sums with maxes is fine is because both of those operations
    are *commutative semirings*.

[^cliques]: Sometimes, we relax the maximal assumption on cliques, such as when we discuss the
    Sum-Product algorithm.

[^representation]: Interestingly enough, factor graphs do *not* provide additional representational
    power, because adding more nodes can simulate the effect of factor functions (by acting as
    indicator functions), but Mike argues that this approach is artificial, which makes sense.

