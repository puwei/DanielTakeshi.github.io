---
layout: post
title:  "The Expectation of the Minimum of IID Uniform Random Variables"
date:   2016-09-25 20:00:00
permalink: 2016/09/25/the-expectation-of-the-minimum-of-iid-uniform-random-variables/
---

In my [STAT 210A class][1], we frequently have to deal with the minimum of a
sequence of independent, identically distributed (IID) random variables. This
happens because the minimum of IID variables tends to play a large role in
sufficient statistics.

In this post, I'll briefly go over how to find the minimum of IID uniform
random variables. Specifically, suppose that $$X_1,\ldots,X_n \sim {\rm
Unif}(0,1)$$ and let $$T = \min_i X_i$$. How do we find $$\mathbb{E}[T]$$? To
compute this, observe that

$$
\begin{align}
P\left(\min_i X_i \le t\right) &= 1 - P\left(\min_i X_i \ge t\right) \\
&= 1 - P(X_1 \ge t, \ldots, X_n \ge t) \\
&= 1 - \prod_{i=1}^n P(X_i \ge t) \\
&= 1 - \prod_{i=1}^n [1 - P(X_i \le t)] \\
&= 1 - [1 - P(X_i \le t)]^n,
\end{align}
$$

so the next step is to determine $$P(X_i \le t)$$. Due to the IID assumption, it
doesn't matter which $$X_i$$ we use. Note also that to avoid adding cumbersome
indicator functions, assume that $$t \in [0,1]$$.

The value $$P(X_i \le t)$$ is easier to compute because it directly relates to
the cumulative distribution function (CDF) of a uniform random variable. For
$${\rm Unif}(0,1)$$, the CDF is simply $$F_X(x) = x$$ if $$x \in (0,1)$$. This
means

$$
P\left(\min_i X_i \le t\right) =  1 - [1 - P(X_i \le t)]^n = 1 - [1 - t]^n,
$$

so that by differentiating with respect to $$t$$, the density function is
$$f_T(t) = n(1-t)^{n-1}$$ (the notation here with the $$T$$ as the subscript is
to denote the variable whose density is being defined).

The reason why we need the density is because of the definition of the
expectation:

$$
\mathbb{E}[T] = \int_0^1 t f_T(t) dt = n \int_0^1 t(1-t)^{n-1}dt.
$$

To compute this, we integrate by parts. Set $$u=t, du=dt$$ and $$dv =
(1-t)^{n-1}dt, v = -(1-t)^{n}/n$$. We get

$$
\begin{align}
\int_0^1 t(1-t)^{n-1}dt &= \left(-\frac{t(1-t)^n}{n} \Big|_{t=0}^{t=1}\right) - \int_0^1 -\frac{(1-t)^n}{n}dt \\
&= \left[-\frac{(1)(1-(1))^n}{n} - -\frac{(0)(1-(0))^n}{n} \right] + \frac{1}{n} \int_0^1 (1-t)^ndt \\
&= \frac{1}{n} \left[ -\frac{(1-t)^{n+1}}{n+1}\Big|_{t=0}^{t=1}\right] \\
&= \frac{1}{n} \left[ -\frac{(1-(1))^{n+1}}{n+1}- -\frac{(1-(0))^{n+1}}{n+1}\right] \\
&= \frac{1}{n} \frac{1}{n+1}.
\end{align}
$$

Combining this with the extra $$n$$ factor we left out (you didn't forget that,
did you?) we get $$\mathbb{E}[T] = \frac{1}{n+1}$$. Notice that as $$n \to
\infty$$ the expected value of the minimum of these uniform random variables
goes to zero. In addition, this expectation is always in $$(0,1/2]$$ for $$n \ge
1$$. Thus, the answer passes the smell test and seems reasonable.

[1]:http://www.stat.berkeley.edu/~wfithian/courses/stat210a/

