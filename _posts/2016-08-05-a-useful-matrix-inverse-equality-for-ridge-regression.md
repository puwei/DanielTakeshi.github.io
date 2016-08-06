---
layout:     post
title:      "A Useful Matrix Inverse Equality for Ridge Regression"
date:       2016-08-05 10:00:00
permalink:  2016/08/05/a-useful-matrix-inverse-equality-for-ridge-regression/
---

I was recently reading [Stephen Tu's blog][1] and stumbled upon his [matrix inverse equality
post][2] which brough back some memories. Here's the equality: let $$X$$ be an $$n \times d$$
matrix, let $$\lambda > 0$$, and let $$I_k$$ represent the $$k \times k$$ identity matrix. Then

$$X(X^TX + \lambda I_d)^{-1}X^T = XX^T(XX^T + \lambda I_n)^{-1}$$

Note that both sides are left-multipled by $$X$$, so for the purposes of checking equality, there's
no need to have it there, so instead consider

$$(X^TX + \lambda I_d)^{-1}X^T = X^T(XX^T + \lambda I_n)^{-1}$$
 
I was asked to prove this as part of a homework assignment in [my CS 281A class with Professor Ben
Recht][3] a while back. Stephen Tu already has an excellent proof based on Singular Value
Decomposition, but I'd like to present an alternative proof that seems even simpler to me. I also
want to explain why this equality is important.

First, start with $$\lambda X^T = \lambda X^T$$. Then left-multiply the left hand side (LHS) by
$$I_d$$ and right-multiply the right hand side (RHS) by $$I_n$$ to obtain

$$\lambda I_d X^T = \lambda X^TI_n$$

Note that this doesn't change the equality, because multiplying a matrix with the identity will not
change it, regardless of the multiplication ordering. As a sanity check, the LHS is $$(d \times
d)\times (d \times n)$$ and the RHS is $$(d\times n)\times (n\times n)$$ and both result in an $$(n
\times n)$$-dimensional matrix so the dimensions match up. Next, add $$X^TXX^T$$ to both sides and
get

$$X^TXX^T + \lambda I_d X^T = X^TXX^T + \lambda X^TI_n$$

We now "distribute out" an $$X^T$$, though the particular $$X^T$$ to use is different on both sides.
We obtain

$$(X^TX + \lambda I_d)X^T = X^T(XX^T + \lambda I_n)$$

Next, left-multiply both sides by $$(X^TX + \lambda I_d)^{-1}$$ and right-multiply both sides by
$$(XX^T + \lambda I_n)^{-1}$$:

$$(X^TX + \lambda I_d)^{-1}(X^TX + \lambda I_d)X^T(XX^T + \lambda I_n)^{-1} = 
(X^TX + \lambda I_d)^{-1}X^T(XX^T + \lambda I_n)(XX^T + \lambda I_n)^{-1}$$

$$X^T(XX^T + \lambda I_n)^{-1} = (X^TX + \lambda I_d)^{-1}X^T$$

Thus proving the identity.

Now, you can leave it like that and in some cases you'll be OK. But strictly speaking, you should
show that the two inverses above *actually exist* before using them. When I was writing up this
for my homework, I said "the problem implies the inverses exist" because the inverse was already
written in the problem statement. In retrospect, however, that was a mistake. Fortunately, the TA
didn't take off any points, though he marked "No, but w/e ..." 

To make things extra clear, we now show that the inverses exist. Consider $$(X^TX + \lambda I_d)$$.
We claim its inverse exist because it is positive definite (and all positive definite matrices are
invertible). This is straightforward because for any nonzero $$z \in \mathbb{R}^d$$, we have

$$z^T(X^TX + \lambda I_d)z = z^TX^TXz + \lambda zI_dz = (Xz)^T(Xz) + \lambda z^Tz = \|Xz\|_2^2 + \lambda \|z\|_2^2 > 0$$

where we use the standard $$w^Tw = \|w\|_2^2$$ trick, which is *everywhere* in machine learning and
optimization. If you don't believe me, [take EE 227B as I did][4] and you'll never be able to forget
it. By the way, the above shows why we needed $$\lambda > 0$$, because $$\|Xz\|_2^2$$ is not
necessarily greater than zero; it could be zero! This is because $$X^TX$$ could be positive
*semi*-definite, but not positive *definite*.

A similar proof applies for the other inverse, which uses $$\|X^Ty\|_2^2$$ for $$y \in \mathbb{R}^n$$.

Having proved the equality, why do we care about it? The reason has to do with ridge regression and
duality. The problem formulation for ridge regression is

$${\rm minimize}_w \quad \|Xw - y\|_2^2 + \lambda \|w\|_2^2$$

where $$y$$ is the $$n$$-dimensional vector of targets and $$\lambda > 0$$. Taking the gradient we
get

$$
\begin{align*}
\nabla_w ((Xw - y)^T(Xw - y) + \lambda w^Tw) &= \nabla_w (w^TX^TXw - 2y^TXw + \lambda w^Tw) \\
    &= 2X^TXw - 2X^Ty + 2 \lambda w \\
\end{align*}
$$

Setting to zero, we find $$w^*$$ as

$$
\begin{align*}
2X^TXw^* - 2X^Ty + 2\lambda w^* = 0 &\iff (X^TX + \lambda I_d)w^* - X^Ty = 0 \\
&\iff (X^TX + \lambda I_d)w^* = X^Ty  \\
&\iff w^* = (X^TX + \lambda I_d)^{-1}X^Ty.
\end{align*}
$$

Gee, does this formulation of $$w^*$$ look familiar? Yep! The above is one way of finding $$w^*$$,
but another way is by invoking the equality to get what is known as the *dual form* of $$w^*$$:

$$ w^* = (X^TX + \lambda I_d)^{-1}X^Ty = X^T\underbrace{(XX^T + \lambda I_n)^{-1}y}_{\alpha^*}$$

Why do we like this new perspective? First, like any dual solution, it provides us with an
alternative method if the "other" way (technically called the *primal* solution) is harder to compute.
In this case, however, I don't think that's the main reason why (because this is fairly
straightforward either way). I think we like this representation because $$w^*$$ is a linear
combination of the rows of $$X$$, with coefficients specified by the vector $$\alpha^* \in
\mathbb{R}^n$$! The rows of $$X$$ are the elements in our data $$\{x_i\}_{i=1}^n$$, so this gives
the intuitive interpretation of the optimal solution being some combination of the data elements.

[1]:https://people.eecs.berkeley.edu/~stephentu/blog/
[2]:https://people.eecs.berkeley.edu/~stephentu/blog/matrix-analysis/2016/06/03/matrix-inverse-equality.html
[3]:http://danieltakeshi.github.io/2014/12/30/review-of-statistical-learning-theory-cs-281a-at-berkeley/
[4]:http://danieltakeshi.github.io/2015-12-22-review-of-convex-optimization-ee-227bt-at-berkeley/
