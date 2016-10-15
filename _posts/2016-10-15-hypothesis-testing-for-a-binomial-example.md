---
layout: post
title:  "Hypothesis Testing for a Binomial Example"
date:   2016-10-15 10:00:00
permalink: 2016/10/15/hypothesis-testing-for-a-binomial-example/
---

In [STAT 210A class][1], we are now discussing *hypothesis testing*, which has
brought back lots of memories from my very first statistics course (taken in my
third semester of undergrad). Think null hypotheses, $$p$$-values, confidence
intervals, and power levels, which are often covered in introductory statistics
courses. In STAT 210A, though, we take a far more rigorous treatment of the
material. Here's the setting at a high level: we use data to infer which of two
competing hypotheses is correct. To formalize it a bit: we assume some model
$$\mathcal{P} = \{P_\theta : \theta \in \Theta\}$$ and test:

- $$H_0 : \theta \in \Theta_0$$, the null hypothesis
- $$H_1 : \theta \in \Theta_1$$, the alternative hypothesis

While it is not strictly necessary for $$\Theta_0 \cup \Theta_1 = \Theta$$ 
and  $$\Theta_0 \cap \Theta_1 = \emptyset$$, we often assume these are true for
simplicity.

We "solve" a hypothesis testing problem by specifying some *critical function*
$$\phi$$, specified as

$$
\phi(x) = \begin{cases}
0 &\text{accept $H_0$}\\
\gamma &\text{reject $H_0$ with probability $\gamma$} \\
1 &\text{reject $H_0$}
\end{cases}
$$

In other words, $$\phi$$ tells us the probability that we should reject
$$H_0$$.

The performance of the test $$\phi$$ is specified by the *power* function:

$$
\beta(\theta) = \mathbb{E}_\theta[\phi(x)] = {\rm Pr}_\theta[\text{reject $H_0$}]
$$

A closely related quantity is the *significance level* of a test:

$$
\alpha = \sup_{\theta \in \Theta_0} \beta(\theta)  = \sup_{\theta \in \Theta_0} \mathbb{E}_\theta[\phi(X)]
$$

The level $$\alpha$$ here therefore represents the *worst* chance (among all the
$$\theta$$ possibilities) of falsely rejecting $$H_0$$. Notice that $$\theta$$
is constrained to be in the null hypothesis region $$\Theta_0$$! The reason why
we care about $$\alpha$$ is because $$H_0$$ often represents the status quo, and
we only want to reject it if we are absolutely sure that our evidence warrants
it. (In fact, we technically don't even "accept" the null hypothesis; in many
courses, this is referred to as "failing to reject".)

We may often resort to a randomized test, which was suggested by my definition
of $$\phi$$ above which uses a $$\gamma$$. This is useful for technical reasons
to achieve exact significance levels.  Let's look at an example to make this
concrete. Suppose that $$X \sim Bin(\theta, n=2)$$, and that we are testing

- $$H_0 : \theta = \frac{1}{2}$$.
- $$H_1 : \theta = \frac{3}{4}$$ (so here the hypotheses do not partition).

And, furthermore, that we want to develop a test $$\phi$$ with a significance
level of $$\alpha=0.05$$. (Note: yes, this is related to the abundant usage of
0.05 as a $$p$$-value in many research articles.)

To test, it is convenient to use a *likelihood ratio* test, which have nice
properties that I will not cover here.  In our case, we have:

$$
L(X) = \frac{p(X \mid \theta = 3/4)}{p(X\mid \theta = 1/2)} = 
\frac{\left(\frac{3}{4}\right)^X\left(\frac{1}{4}\right)^{2-X}}{\left(\frac{1}{2}\right)^X\left(\frac{1}{2}\right)^{2-X}} 
= \frac{3^X}{4}
$$

where we have simply plugged in the densities for Binomial random variables and
simplified. Intuitively, if this ratio is very large, then it is more likely
that we should reject the null hypothesis because $$\theta=3/4$$ describes the
data better.

We know that $$L(X)$$ can take on only three values (because $$n=2$$) and that
*under the null hypothesis* (this is important!) the probabilities of $$L(X)$$
taking on $$1/4,3/4$$, or $$9/4$$ happen with probability $$1/4,1/2,$$ and
$$1/4$$, respectively.

Knowing this, how do we design the test $$\phi$$ with the desired significance
level? It must be the case that

$$
\begin{align*}
\mathbb{E}_\theta[\phi(X)] &= P(X=0)\phi(0) + P(X=1)\phi(1) + P(X=2)\phi(2) \\
&= \frac{1}{4}\phi(0) + \frac{2}{4}\phi(1) + \frac{1}{4}\phi(2) = 0.05
\end{align*}
$$

(There is only one $$\theta$$ possibility here, so we do not need a "sup" term.)

By using the fact that a likelihood ratio must be defined by a cutoff point
where if $$L(X)>k$$, we reject, else if $$L(X) < k$$ we accept (and with
equality, we randomize), we see that our test must be $$\phi(0)=\phi(1)=0$$ and
$$\phi(2)=1/5$$. If we were to equate this with our definitions above, this
would be:

$$
\phi(x) = \begin{cases}
0 &\text{if $L(X) = \frac{1}{4}$ or $L(X) = \frac{3}{4}$, i.e., if $L(X) < \frac{9}{4}$}\\
\frac{1}{5} &\text{if $L(X) = \frac{9}{4}$} \\
1 &\text{if $L(X) > \frac{9}{4}$}
\end{cases}
$$

with $$k=9/4$$. (The third case never happens here; I just added it to be
consistent with our earlier $$\phi$$ definition.)

And *that* is why we use randomization. This also gives us a general recipe for
designing tests that achieve arbitrary significance levels.

[1]:http://www.stat.berkeley.edu/~wfithian/courses/stat210a/

