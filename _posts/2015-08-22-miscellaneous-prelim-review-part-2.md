---
layout: post
title:  "Miscellaneous Prelim Review (Part 2)"
date:   2015-08-22 23:00:00
permalink: miscellaneous-prelim-review-part-2
---

This will probably be my last prelim review post. The topics I'll cover in this post are convex
optimization, statistical learning theory (broadly), and logic/planning.  Actually, I wanted to
write about Kalman filtering, but I think I've done more than enough here, and there are too many
equations involved to write that quickly.

## Convex Optimization

This part is based on sections 9.1 through 9.5 of [Boyd and Vandenberghe's book, freely available
online](http://stanford.edu/~boyd/cvxbook/). Stephen Boyd also has a [lecture video on YouTube that I
watched](https://www.youtube.com/watch?v=sTCtkkqrY8A), which I found to be very helpful. (I can also
understand Professor Boyd's speech well.) The book is fine, I suppose, but is really hard for me to
read so I made embarrassingly slow progress as I learned this material.

The main purpose of sections 9.1 through 9.5 is to discuss iterative algorithms for minimization.
Formally, we have the problem of minimizing a *convex* function $$f(x)$$ and need to find the
optimal $$x = x^*$$. As in almost all cases, we have to remember that $$x$$ is *not* generally a
scalar but a *vector*, but $$f$$ is *real-valued*, so $$f : \mathbb{R}^n \to \mathbb{R}$$. I had to
keep reminding myself of this.

In most cases, we need to use *iterative* algorithms to find $$x^*$$. The class of algorithms we use
are known as *descent* algorithms because they generate points $$\{x^1,x^2,\ldots \}$$ such that
$$f(x^k) > f(x^{k+1})$$ unless we are at the optimum. Actually, a little side-note: there *is*
exactly one optimal $$x^*$$ because we are actually assuming that $$f$$ is *strictly* convex, not
just convex (and strict convexity is not the same as strong convexity!). By strong convexity, we
assume that there is a constant $$m > 0$$ such that $$\nabla^2 f(x) \ge mI$$, which means $$\nabla^2
f(x) - mI$$ is positive semidefinite.

A lot of our future analysis will depend on a concept known as the *condition number* of a matrix or
a set. For a matrix, the condition number is the ratio of the largest singular value to the smallest
singular value. Alternatively, we can use eigenvalues if the matrix is positive semidefinite, which
actually happens here since the second-order characterization of convexity states that the Hessian
of $$f$$ is positive semidefinite. The condition number of a set is defined as the ratio of the
largest width to smallest width. High condition numbers result in highly skewed/stretched data.

Here's the descent algorithm. We repeat the following until some stopping criterion:

- Compute a (descent) direction to change $$x$$, denoted $$\Delta x$$
- Compute a length or step size $$t$$ to go in that direction using some form of line search
- Compute $$x \leftarrow x + t (\Delta x)$$

There are two main ways to choose $$t$$: exact search (find $$\arg_t \min f(x + t (\Delta x))$$) or
backtracking search. For some reason, it took me a really long time to understand backtracking line
search, but after looking at that figure in Boyd's book for ages, I understand what it does now. We
have to keep decrementing $$t$$ until our function $$f(x + t (\Delta x))$$ lies below a given upper
bound. Backtracking line search is important because it's more efficient and in practice, it often
works just as well (or better!) than exact line search.

But the real difference in the various gradient algorithms comes when we pick $$\Delta x$$. There
are three options:

- Use $$-\nabla f(x)$$. I mean, the gradient $$\nabla f(x)$$ points in the direction of *greatest
  increase* of $$f$$ at $$x$$ (by definition) so why on earth would we not use the negative of
  that? This is *gradient descent*. 
- Use the direction that maximizes the negative gradient in the direction determined by a
  pre-specified norm. TODO I didn't quite describe this clearly. This is *steepest descent*, and
  equals gradient descent when we are using the $$\ell_2$$ norm.
- use $$-(\nabla^2 f(x))^{-1}\nabla f(x)$$, i.e., the negative of the *inverse* of the Hessian,
  multiplied by the gradient. Whew! This comes from the second order approximation of $$f(x + \Delta
  x)$$ -- just take the gradient with respect to $$x$$, then solve. This is *Newton's Method*. TODO
  confirm this computation?

Gradient descent is simple, and works perfectly (i.e., converges in one step) when the data are
"isotropic," that is to say, roughly "equal in all directions." It's bad when the condition number
of the Hessian or the sublevel sets is high. The classic example is the ellipsoid "bowl" where we
have a 3-D bowl that is much wider in one direction than the other. Gradient descent with exact line
search will always "overshoot" the optimal location and keeps going back and forth, zig-zagging to
the center.

Steepest descent is a generalization of gradient descent in that we get the option of picking the
norm that we want to use as a metric of our "gradient" here.

TODO more things about norms, e.g, quadratic norm, and if we use l-1, it's coordinate ascent,
modifying one coordinate at a time.

Newton's method is a step up from gradient descent in that we use a *second-order* approximation of
$$f$$. The way I think of it is that gradient descent will produce a plane in 3-D (e.g., for a 3-D
"bowl" that we're trying to reach the minimum of) but Newton's method will produce *another* bowl,
though this bowl will usually be entirely above of the original one, save for the tangent point.

More facts about Newton's method:

- If the original bowl was already quadratic, Newton's method converges in one step.
- The *downside* of Newton's method compared to gradient or steepest descent is that (1) we have to
  compute the Hessian, and (2) we have to store it -- remember that the Hessian will be $$n \times
  n$$, whereas the *gradient* will only be $$n \times 1$$.
- Affine invariant, transformation of coordinates
- Damped phase versus pure phase (I think?), after the damped phase, the number of accurate digits
  *doubles*.

The usual disclaimers apply in that we don't really know various constants that get involved in the
proof, unfortunately.

TODO Read through ALL FORTY pages and fill in any missing gaps above. Don't get too heavy on math.


## Statistical Concepts and Logistic Regression

This part is closely related to what I wrote about [linear regression and the least mean squares
algorithm](http://danieltakeshi.github.io/the-least-mean-squares-algorithm/). I will be discussing
logistic regression as well (for classification, not regression), but first we take a brief detour
to discuss the third major class of problem known as *density estimation*.

The problem is, given data, to find the appropriate model for it. The relatively easy case is if we
assume we already have an idea of the distribution (e.g., Gaussian) and we just need to find the
parameters (here, the mean and variance). We find the parameters via maximum likelihood. So in the
IID Gaussian case, of which the graphical model is represented as $$N$$ independent shaded circles
in a graphical model, we take the sample mean and sample covariance as our MLEs. With the Bayesian
approach, where we have a new $$\mu$$ node pointing to all samples, we put a *Gaussian* prior on
mean $$\mu$$ so that the result is a weighted estimate (and the same for the variance, actually),
because of conjugate priors. In the case of discrete data $$x$$, we model these with multinomials.
The resulting MLEs, which require Lagrange multipliers to solve (which gave me a *huge* headache at
first), are just the sample proportions. For the Bayesian version, we use a Dirichlet prior. To
extend the class of distributions we want to model, we can assume a mixture model, where $$p(x\mid
\theta) = \sum_{i=1}^{k}\alpha_i f_i(x\mid \theta_i)$$, where the $$\alpha_i$$s are mixing
proportions that sum to one. This time, we have a *hidden* node that points to its own observed
data point $$x$$.

There is an alternative strategy of estimation known as nonparametric density estimation. Here, we
do not assume we have a fixed parameter $$\theta$$ and as our data grows, the nonparametric model
will grow to represent a wider class of distributions. We have kernels, where each data point takes
some probability mass, and we add them up and normalize. In the case of Gaussian kernels, the
nonparametric case for a fixed number of samples really reduces to the mixture model case, but they
differ as the number of instances grow.

Tip: use the nonparametric case if we do not have a good idea of the model and lots of data, but use
the parametric version when we have little data and a good idea of its underlying distribution (it
will converge faster). The line between the two methods does blur somewhat, for instance, when we
have a mixture modeling problem where we have to dynamically estimate the number of components
$$K$$.

Finally, we can turn our attention towards the *regression* and *classification* problems. In both
cases, we model $$p(y_n\mid x_n,\theta)$$, where the $$n$$ here indicates that we assume IID data.
For *linear* regression, we assume $$y_n = \beta^Tx_n + \epsilon_n$$, and have to find $$\beta$$.
The choice of $$\epsilon_n$$ is what really determines the distribution -- here we assume Gaussians,
so this is linear regression, and that means the MLE of $$\beta$$ is the OLS estimate. Another way
of extending linear regression to be more flexible is to use (conditional) mixtures. Here, the
graphical model looks like that of the density estimation mixture model, except we also need the
$$X_n$$ node (which may or may not be connected to the mixture node $$Z_n$$). And, of course, we
could always treat these from a Bayesian perspective, perhaps by endowing that $$\epsilon_n$$ error
term for Gaussians (in linear regression) with Gaussian priors for its mean and variance (well,
probably variance only if we want the mean to be zero).

We can also use nonparametric regression, if we do not want to restrict our conditional mean
functions. Actually, Russell and Norvig cover this a bit in their nonparametric methods section in
the textbook; each predicted new $$y$$ is based on the weighted prediction of the other, "nearest"
$$y_n$$s.

In the classification case, the distinction between generative and discriminative cases is more
apparent. I remember the way the arrows point in the model just by remembering the discriminative
case, and then realizing that the generative is the opposite one. Use the generative case if we want
a full probabilistic model, and use discriminative classification if we only care about the boundary
point. The full model in the generative case also may help combat overfitting, so it is better with
limited and partially observed data. Discriminative models have less bias because they make fewer
assumptions, so they work better with lots of data (in fact, it's a lot like how nearest neighbor
will work best with lots of data).

These approaches are important to understand the *logistic regression* algorithm, where we assume
that the posterior probability $$p(y=0\mid x, \theta)$$ for a binary classification problem is
logistic or arrives at that form. That we have the inner product there means the posterior
"boundaries" of equal probability are *hyperplanes*. In the generative case, we estimate means and
covariances, which *define* $$\theta$$ (and these are density estimation problems!) and the boundary
*implicitly*, while in the discriminative case, we estimate $$\theta$$ "directly," possibly choosing
an arbitrarily complex boundary. In fact, "discriminative = logistic regression", "generative =
Naive Bayes", and *both* are for classification. In fact, that's *why* they are in the same chapter
of Mike Jordan's notes!

Again, logistic regression assumes we have the sigmoid function as the form for our posterior
probability. We can assume this from the outset (discriminative) but we can also "inspire" this
generatively. Here's how: assume that we have two classes, and the class conditionals[^cc] are
*Gaussian* with, and this is important, *the same covariance matrices*. Then the posterior $$P(Y = 0
\mid X, \theta)$$ can be expressed as $$(1+e^{-\beta^Tx - \gamma})^{-1}$$, i.e., the exponent has an
affine function of $$x$$, which means that the boundaries of equal probability are *hyperplanes*. In
the special case of equal *mixing proportions*, we have equidistant boundaries. A skewed mixing
proportion will shift the boundaries towards or away one of the classes.

In fact, the assumption of a Gaussian class conditional is not even necessary. We can get away with
multinomials (this is another way of viewing the Naive Bayes classifier), or in fact, anything in
the exponential family[^expfam]! When I was learning about these in my undergraduate Bayesian
statistics course, I never really *got* why the exponential families were that important. But here
is one reason, I suppose. Note that these are still *assumptions* that add bias to the generative
case.

We can extend the previous analysis to the general classification case with $$K$$ outputs. In that
case, we use the softmax: $$e^{\beta_i^Tx}/\sum_j e^{\beta_j^Tx}$$, which also results in linear
boundaries, though that's kind of stretching the definition; imagine a "pie-chart" where the
"slices" represent boundaries.  Also, if we wanted to find maximum likelihood estimation, we could
do that, because we have $$P(x\mid y,\theta)$$ and $$P(y\mid \theta)$$. Just combine those to get
the joint and differentiate the log of it. For instance, in the two Gaussian case, the MLE for
the means $$\mu_1$$ and $$\mu_2$$ are just the sample means of the elements in their respective
classes (remember, we assume we *know* the training data labels), and the covariance is weighted
among the two. In the general case, we again write the formula and then separate the terms
appropriately. Note: we will use $$\theta$$ to represent a generic vector of weights. To be safe,
whenever we write probabilities, add a conditioned $$\theta$$.

Whew! Now we can talk about logistic regression, where the class dependency is fixed to be a sigmoid
function. How do we find the best $$\theta$$? As usual, take logs, and maximize. This actually leads
us to an LMS-like algorithm, and the only difference is the class expectation. For the batch
version, we use *iteratively reweighted least squares*, which is basically Newton's method for
optimizing the (nearly) quadratic log likelihood function. In fact, there is a close connection
between this method and the "normal" weighted least squares method, which started by assuming that
each training input/output had an attached "weight" to it: this method can be written as

$$\theta \leftarrow (X^TWX)^{-1}X^TWz$$

for what I thought was a pretty convoluted $$z$$, but actually turns out to be a first order
approximation of $$y$$. Interesting ... I don't really understand the full details of this, but
having the knowledge of convex optimization at the top of this post really helped me.

For extending discriminative learning to multiple classes, again assume that $$P(Y = ? \mid
X,\theta)$$ is represented by the softmax function, and a lot of our math follows for what is known
as *softmax regression*.

Finally, thanks to Andrew Ng I have a bit of a better idea on the connection between the logistic
regression update (in the LMS-like form) versus the perceptron: just change the sigmoid part in the
update to be the "sign" function, and then the update turns into the perceptron.

## More Statistical Learning Theory

Here's a random assortment of notes from Mike Jordan's book (which I think he has abandoned now).

First, let's consider the multivariate Gaussian is one of the most important distributions to
understand, and I did not have an easy time learning about it. Fortunately, by now I can write out
the formula and reason about it quite easily. Unfortunately, I don't know how to derive it from
first principles. I can explain "roughly" what it does, e.g., that $$|\Sigma|^{1/2}$$ in the
normalizing constant comes from how each component of the random vector contributes some amount of
variance equal to its eigenvalue, and the determinant of a matrix is the product of its eigenvalues.

But anyway, there are a few important facts worth discussing about the multivariate Gaussian.

- There is a *moment* parameterization and the *canonical* parameterization. The former is what I
  always use, but we can transform it into the latter with the rules $$\Lambda = \Sigma^{-1}$$ and
  $$\eta = \Sigma^{-1}\mu$$ to get $$p(X\mid \eta, \Lambda)$$.

- Given a matrix $$M$$ where we partition it into components $$E,F,G,$$ and $$H$$, the goal of
  *block diagonalization* is to find matrices $$A$$ and $$B$$ such that $$A \times M \times B$$ is
  diagonal in the corresponding locations of $$F$$ and $$G$$. After a lot of algebra, we can arrive
  at the derivative of the partitioned matrix $$M$$, and also derive a bunch of useful identities
  (the "matrix inversion lemma") that I refuse to memorize.

- The reason why we go through this tedious algebra is that it gives us identities we can use when
  partitioning the multivariate Gaussian to get *formulas* for marginal and conditional
  probabilities involving multivariate Gaussians. Specifically, we have $$x\in \mathbb{R}^n$$ split
  into $$x_1$$ and $$x_2$$, and we want $$p(x_2)$$ and $$p(x_1\mid x_2)$$, where I'm eliding the
  parameters for simplicity. We obviously have the joint $$p(x_1,x_2)$$, so we need to figure out
  how to split them cleverly. Once we've gone through the derivation, we will find that the moment
  parameterization lends to easy computations of marginals but hard ones for conditionals, and the
  reverse is true for the canonical parameterization. Importantly, these formulas preserve the fact
  that our variables are Gaussian.

In addition to knowing that the marginals and the conditionals are Gaussian, the sum of independent
Gaussians is Gaussians.

TODO mixture models, and give an example of an EM derivation?

TODO Kalman filtering


## Logic and Planning

I [discussed this earlier](http://danieltakeshi.github.io/reading-russell-and-norvig/) and had a
chance to re-read all of that stuff. My main purpose in this section is to highlight *how everything
in this section connects with each other*. I don't want to just learn propositional logic, then
first order logic, etc., I want to *describe* then in terms of each other, and to discuss all the
similarities and differences among them (and the algorithms they inspire). But this won't be long
because Stuart Russell isn't on the prelim committee this time (hint hint...).

But first, a laundry list of facts that *really* confused me the first time:

- Propositions consist of **literals**, which are just like the atomic elements of propositions, but
  they *can* have a "negation" symbol. That's it: think of literals as either $$A$$ or $$\neg A$$.
- Predicates are really functions that output a True or a False. Predicates are -- in my opinion --
  the backbone of first order logic.
- Be sure to realize that $$\alpha \Rightarrow \beta$$ is the same thing as $$\neg \alpha \vee
  \beta$$. This is probably *the* most important thing to remember to understand Horn and definite
  clauses, and why we can apply Modus Ponens to them.

Now we can talk about the *connections*. Here they are:

- One can convert from first order logic to propositional logic by extending universal and
  existential quantifiers.

- Forward and backward chaining play a role in both propositional and first order logic. They are
  algorithms for determining *entailment* when we assume that our knowledge base consists of Horn
  clauses (prop.) or first order definite clauses (FOL). This is a simplifying assumption, but it is
  often easy to convert databases to this format. The reason why Horn or definite clauses are needed
  is that their truth values are equivalent to $$\alpha \Rightarrow \beta$$ (and we need "or"s not
  "and"s), and that exactly fits the description of the Modus Ponens and Generalized Modus Ponens
  rule format. Note: we use these when we *do not* want to use the full power of resolution.

- As an alternative, say we do not have definite clauses and are just looking for a satisfying
  assignment to a disjunction of clauses. Then in *both* types of logics, we have the option of
  backtracking and local search. Both of these have their similarities in the Constraint
  Satisfaction Problem domain. In backtracking search, we have similar versions of "minimum
  remaining values" and "least constraining value" heuristics. In local search, that is when we are
  starting with a *full*, though not typically *satisfactory*, assignment to a problem in CNF form,
  and we pick clauses to shift, and this is the same as in CSPs when we start with a full assignment
  and use the minimum conflicts heuristics to adjust values.

- The PDDL language (Chapter 10) is about a simplified language that *uses* first-order logic
  "materials" (e.g., predicates, quantifiers, etc.) to encode a *search* problem (remember Chapter
  3!)[^pushingit]. Since we're encoding a search problem, we need to define the actions we can take,
  and those must have preconditions and effects, which involve adding or removing some fluents. The
  *fluent*, by the way, is the atomic set whose values represent a state. Again, the really
  important thing to know about Chapter 10 is that it is really another case of the general search
  problems. One can also make plans using a logical agent.

- Knowledge representation (Chapter 12) is all about *encoding* "real-world" stuff in first order
  logic. Our strategy to represent these is formally called ontological engineering. They discuss
  categorizing *objects*, *categories* (make them into objects!), and *events*.

- Let's go over the different *kinds* of algorithms:

    - Backtracking search: when we incrementally look for assignments to stuff, and then "backtrack"
      when we have seen some "problems", e.g., impossible situations (and this can be used for
      entailment as well!). There are heuristics for this. We do this in CSPs and searching for
      satisfying assignments in propositional logic. We can also transform a classical planning case
      to a propositional case and turn it over to the backtracking solver, but this is not
      practical.
    - Local search: we start with a complete assignment, and move variables around until we get to
      a solution. We do this with CSPs, propositional logic.
    - Forward chaining and backward chaining are algorithms for deciding *entailment* in the two
      logics. We do not use these in CSPs or classical planning. The FOL case is more complicated
      due to the need to perform unification (among other factors), but we have general heuristics
      for improving them.
    - In PDDLs, we do forward *searching* and backward *searching* to search for a satisfying
      sequence of actions. The forward searching part is similar to the backtracking search in that
      we can search for actions with heuristics and backtrack if needed. Backward search can avoid
      irrelevant states, though.

***

[^pushingit]: The book never really makes this clear, but PDDL is *not* actually First Order Logic,
    but it *reminds* me of it because the syntax was designed apparently to be similar.

[^cc]: These are $$p(x\mid y)$$ because we are *conditioning* on the *class* $$y$$.

[^expfam]: A distribution that can be expressed as $$p(x\mid \eta) = h(x) \exp\{\eta^Tx - a(\eta)\}$$
    is in the exponential family.

