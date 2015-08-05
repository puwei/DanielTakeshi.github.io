---
layout: post
title:  "The Least Mean Squares Algorithm"
date:   2015-07-29 21:00:00
permalink: the-least-mean-squares-algorithm
---


After [reviewing some linear
algebra](http://danieltakeshi.github.io/stanfords-linear-algebra-review/), the Least Mean Squares
(LMS) algorithm is a logical choice of subject to examine, because it combines the topics of linear
algebra (obviously) and graphical models, the latter case because we can view it as the case of a
single, continuous-valued node whose mean is a linear function of the value of its parents.
(Admittedly, I do not find this intuitively helpful.)

## The High-Level Problem

We are going to be analyzing LMS in the context of linear regression, i.e., we will have some input
features $$x_n = (x_1, x_2, \ldots, x_k)^{(n)}$$ along with their (scalar-valued) output $$y_n$$ as
our data, and the goal is to estimate a parameter vector $$\theta$$ such that $$y_n = \theta^T x_n +
\epsilon_n$$, where the $$\epsilon_n$$ is admitting that we do not expect to exactly match
$$y_n$$.

When we have ordinary linear regression, we often express the data all together in terms of
matrices. Thus, we could have $$X$$ be our $$m \times n$$ matrix of features, where there are $$m$$
samples and $$n$$ variables per sample, $$\theta$$ be the $$n\times 1$$ column vector of parameters,
and the goal would be to find a solution $$\theta$$ to the problem $$X\theta = Y$$, where $$Y$$ is the
column vector of actual outputs. The problem is *linear* because the equations are linear in
$$\theta$$ ($$X$$ itself can actually be input to a more complicated function). In the rare case
that $$X$$ is square and that all columns are linearly independent, this immediately reduces to
$$\theta = X^{-1}Y$$. Most of the time, though, $$X$$ is a "tall" matrix and the data vector $$Y$$
lies *outside* the column space of $$X$$.

The most natural solution, it seems, is to find the projection of $$Y$$ onto the subspace of
$$Col(X)$$, as that intuitively should minimize all our $$\epsilon_n$$ terms. Thus, we have the
normal equations, the most important one in statistics: $$(X^TX)\theta = X^TY$$. In most
cases[^intro], we can invert $$(X^TX)$$. If not, we can use the *pseudo-inverse*[^pseudoinverse].

There are several ways of getting to the normal equations. One can appeal geometrically, by using
geometry and linear algebra. Alternatively, we can derive it based on the following cost function:

$$\begin{align}
J(\theta) &= \frac{1}{2}\sum_{n=1}^N \epsilon_n^2\\
&= \frac{1}{2} \sum_{n=1}^N (y_n - \theta^Tx_n)^2 \\
&= \frac{1}{2} (y - X\theta)^T(y - X\theta)\\
&= \frac{1}{2} \|y - \theta^TX\|_2^2
\end{align}$$

If someone asks you about what LMS (which we will discuss shortly) is supposed to optimize, it is
this cost function. We want to minimize the sum of squared errors.

So, under the assumption that we can get $$\theta$$ by inverting $$X^TX$$, we can solve this via
direct methods (e.g., Gaussian elimination) or iterative methods. The latter is our focus, *as the
LMS algorithm is an example of an iterative method. Put another way, it is a steepest descent
algorithm for solving the normal equations*.

## The LMS Algorithm

The gradient of the cost function over all the data (i.e., the "batch" case, not the "online" case)
leads to the update rule:

$$\theta^{(t+1)} = \theta^{(t)} + \rho \underbrace{\sum_{n=1}^N(y_n - (\theta^{(t)})^T x_n)x_n}_{\nabla J(\theta)}$$ 

We just initialize some $$\theta^{(0)}$$ and run this until convergence. But this is bad because we
are summing up over the entire set of samples. Thus, we use the following *single-case update*,
which is indeed what we mean by the **LMS algorithm**:

$$\theta^{(t+1)} = \theta^{(t)} + \rho \underbrace{(y_n - (\theta^{(t)})^T x_n) x_n}_{\nabla_{x_n} J(\theta)}$$

In other words, the idea is that we take each data point stochastically[^sg], which provides an
approximation of the gradient, in the hopes that $$\theta$$ will converge to whatever is implied by
the normal equations. The above equation is the LMS update. While LMS is technically an
approximation, it is in fact often superior to the batch version equation update written earlier.

This update rule has the following neat, intuitive interpretation courtesy of Michael I. Jordan.
Suppose we are given $$(x_n,y_n)$$; what update should we perform on $$\theta$$? If this is our only
data, then we have vectors $$x_n$$ and $$\theta$$ in some space. To map $$\theta^Tx_n$$ perfectly
onto $$y_n$$, we must figure out a way to project[^dotprod] $$\theta$$ onto $$x_n$$. In general,
there will be a *line* of possible solutions for $$\theta$$, but the two "natural" ways to update
$$\theta$$ are by extending $$\theta$$ in either (1) the "$$\theta$$ direction" or (2) the "$$x_n$$
direction." The second case is easiest to do because the error associated with the projection of
$$\theta$$ is precisely $$x_n - y_n$$, and by projecting $$\theta$$ by this amount *in the direction
of $$x_n$$*, we will get $$y_n = \theta^Tx_n$$ with no error term. In general, the rule will be:

$$\theta^{(t+1)} = \theta^{(t)} + \frac{1}{\|x_n\|_2^2}(y_n - (\theta^{(t)})^Tx_n)x_n$$

and this nicely maps to the LMS algorithm (in fact, it *is* the LMS algorithm update!) as we can
turn the reciprocal of the norm term into $$\rho$$. If we have multiple data points, we should
expect the "jumping $$\theta$$" to eventually land at the solution, if there is one, or converge
under certain conditions. The above equation means that we update $$\theta$$ by moving it some
distance in "the $$x_n$$ direction."

What I found especially interesting is that we can literally treat the parameter estimation
$$\theta$$ problem as a geometric problem, where each data point $$(x_n,y_n)$$ presents a
*constraint*, and the overall goal is to solve a *constraint satisfaction problem*, a popular
subfield in classic Artificial Intelligence.

It is possible to prove that LMS converges to a vector that satisfies the normal equations. I will
not put the proofs here[^benrecht], but it is important to understand these to see how much
flexibility we have with the step size $$\rho$$. 

## Side Notes

If we want to do *weighted least squares*, where each point is assigned a weight $$w_n$$ that
indicates its importance, then the cost function is $$J(\theta) = (1/2)(y-X\theta)^TW(y-X\theta)$$,
meaning that the normal equations turn into $$X^TWX\theta = X^TWy$$. Our new matrix $$W$$ is a
diagonal matrix of weights.

We can connect our geometric treatment of LMS with probability. Suppose we endow the errors
$$\epsilon_n$$ as IID zero-mean Gaussians with variance $$\sigma^2$$. Then, if we try to compute
$$p(Y\mid X,\theta)$$ for the entire data, *what happens is that the log likelihood of this
expression is equivalent to the least squares cost function* $$J(\theta)$$! Said another way,
maximizing the log likelihood with $$\theta$$ is the same as minimizing the least-squares cost
function, and all we assumed are IID sampling and Gaussian errors. Thus, we can avoid most of our
geometric, constraint satisfaction approaches in favor of just computing the data log likelihood,
since they evidently get the same results. This is assuming we stay in the maximum likelihood
framework, by the way; the least-squares cost function can lead to a frequentist "estimator",
*regardless* of whether or not the data errors are Gaussian, and then that estimator and the MLE
would not coincide. But here, they do.

It's interesting to consider the question as to whether we can use LMS for classification. As it is,
it's not a good fit for the classification case, but if we wanted to, we could adapt it into
*logistic regression*. Then what this means is our hypothesis will *still* involve some form of
$$\theta^Tx_n$$, but we will instead use the logistic function:

$$h_\theta(x) = \frac{1}{1 + e^{-\theta^Tx_n}}$$

I hope to discuss logistic regression in more detail in a future blog post. Note that this is suited
for binary problems, but we can do 1-vs-all for general classification. (EDIT: No, we would use the
softmax function.)

Finally, [here is another source about the LMS
algorithm](http://cs229.stanford.edu/notes/cs229-notes1.pdf), courtesy of Andrew Ng. A lot of his
notes really make things clear!

***

[^intro]: At least in introductory statistics courses...

[^pseudoinverse]: After reading more about Singular Value Decomposition (SVD), in addition to
    knowing about SVD and the four fundamental subspaces, I *finally* feel like I have a solid grasp
    of what the heck pseudoinverses do.  The four fundamental subspaces are $$Col(A), Null(A^T),
    Col(A^T)$$, and $$Null(A)$$, where for an $$m \times n$$ matrix $$A$$, the first two I listed
    combined will take up the entire $$\mathbb{R}^m$$ space, and the latter two will combine for
    $$\mathbb{R}^n$$ space. In other words, *any* $$m$$-dimensional vector $$x$$ can be broken up
    into $$x = x_1 + x_2$$ where $$x_1 \in Col(A)$$ and $$x_2 \in Null(A^T)$$. What SVD does is that
    for an arbitrary $$m\times n$$ matrix $$A$$, it splits it into $$A = U\Sigma V^T$$. Suppose
    $$A$$ has rank $$r$$.  Then the first $$r$$ columns of $$U$$ are the basis for $$Col(A)$$, the
    last $$n-r$$ are the basis for $$N(A^T)$$, and similar conditions apply for the $$V$$ matrix.
    When we take pseudoinverses, we get them *via* the SVD, so $$A^+ = V\Sigma^+U^T$$ (where
    $$\Sigma^+$$ is the transpose of $$\Sigma$$ with all the nonzero diagonals inverted) and one can
    verify that $$AA^+ = I$$. Thus, finally, by looking at the normal equations $$(A^TA)x = A^Tb$$,
    the obvious thing to do to solve for $$x$$ is to multiply both sides by $$(A^TA)^+$$. At long
    last, I finally understand what to do if $$A^TA$$ is not invertible! (This happens when $$A$$
    has linearly dependent columns, say if we repeated measurements somehow, not a far fetched
    possibility.  If that happens, then $$A^TA$$ is an $$n\times n$$ matrix with rank less than
    $$n$$.) Also, sorry for the abnormally long footnote here! We are not actually doing this here.
    This is the "batch" form of solving the problem, and we want the iterative form.

[^sg]: The LMS algorithm is also known sometimes as the stochastic gradient method, I think.

[^benrecht]: Ben Recht, on analyzing the convergence of LMS: "There are whole books written on
    this!"

[^dotprod]: Recall that $$\|a\| \|b\| \cos \theta = a \cdot b$$. It took me a surprisingly long time
    to verify that the projection actually worked, so it might be worth it to go through the math
    and trigonometry involved, if necessary.

