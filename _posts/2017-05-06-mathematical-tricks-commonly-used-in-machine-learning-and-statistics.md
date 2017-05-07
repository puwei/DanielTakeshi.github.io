---
layout: post
title: "Mathematical Tricks Commonly Used in Machine Learning and Statistics"
date:   2017-05-06 10:00:00
permalink: 2017/05/06/mathematical-tricks-commonly-used-in-machine-learning-and-statistics
---

I have passionately studied various machine learning and statistical concepts
over the last few years. One thing I've learned from all this is that there are
many mathematical "tricks" involved, whether or not they are explicitly stated.
(In research papers, such tricks are often used without acknowledgment since it
is assumed that anyone who can benefit from reading the paper has the
mathematical maturity to fill in the details.) I thought it would be useful for
me, and hopefully for a few interested readers, to catalogue a set of the common
tricks here, and to see them applied in a few examples.

The following list, in alphabetical order, is a non-exhaustive set of tricks
that I've seen:

- Cauchy-Schwarz
- Integrating Probabilities into Expectations
- Introducing an Independent Copy
- Jensen's Inequality
- Law of Iterated Expectation
- Lipschitz Functions
- Markov's Inequality
- Norm Properties
- Series Expansions (e.g. Taylor's)
- Stirling's Approximation
- Symmetrization
- Take a Derivative
- Union Bound
- Variational Representations

If the names are unclear or vague, the examples below should clarify.  All the
tricks are used except for the law of iterated expectation and Markov's
inequality. (No particular reason for those omissions; it just turns out the
exercises I'm interested in didn't require them.)





## Example 1: Maximum of (Not Necessarily Independent!) sub-Gaussians

I covered this problem in [my last post here][1] so I will not repeat the
details. However, there is one extension to that problem which I thought would
be worth noting. To prove an upper bound for the random variable $$Z =
\max_{i=1,2,\ldots,n}|X_i|$$, it suffices to proceed as we did earlier in the
non-absolute value case, but *augment* our sub-Gaussian variables
$$X_1,\ldots,X_n$$ with the set $$-X_1,\ldots,-X_n$$. It's OK to do this because
no independence assumptions are needed. Then it turns out that an upper bound
can be derived as

$$\mathbb{E}[Z] \le 2\sqrt{\sigma^2 \log n}$$

This is the same as what we had earlier, except the "2" is now outside the
square root.

Tricks used:

- Jensen's Inequality
- Take a Derivative
- Union Bound

**Comments**: My earlier blog post shows what I mean when I say "take a
derivative." It typically happens when there is an upper bound on the left hand
side and we have a free parameter $$\lambda \in \mathbb{R}$$ (or $$\lambda \ge
0$$) which we can optimize to get the *tighest* possible bound. Often times,
such a $$\lambda$$ is *explicitly introduced* via Markov's Inequality. Note the
use of convexity of the exponential function. It is *very common* to see
Jensen's inequality applied with the exponential function. Always remember that
$$e^{\mathbb{E}[X]} \le \mathbb{E}[e^X]$$!! Finally, the procedure that I refer
to as the "union bound" when I bound a maximum by a sum isn't exactly the
canonical way of doing it, since that typically involves probabilities, but it
has a similar flavor. More formally, the [union bound][6] states that 

$$\mathbb{P}\left[\cup_{i=1}^n A_i\right] \le \sum_{i=1}^n \mathbb{P}\left[A_i\right]$$

for countable sets of events $$A_1,A_2,\ldots$$. When we define a set of events
based on a maximum of certain variables, that's the same as taking the union of
the individual events.





## Example 2: Bounded Random Variables are Sub-Gaussian

This example is really split into two parts. The first is as follows:

> Prove that Rademacher random variables are sub-Gaussian with parameter
> $$\sigma = 1$$.

The next is:

> Prove that if $$X$$ is a zero-mean and has support $$X \in [a,b]$$, then $$X$$
> is sub-Gaussian with parameter (at most) $$\sigma = b-a$$.

To prove the first part, let $$\varepsilon$$ be a Rademacher random variable.
For $$\lambda \in \mathbb{R}$$, we have

$$\begin{align}
\mathbb{E}[e^{\lambda \epsilon}] \;&{\overset{(i)}{=}}\; \frac{1}{2}\left(e^{-\lambda} + e^{\lambda}\right) \\
\;&{\overset{(ii)}{=}}\; \frac{1}{2}\left( \sum_{k=0}^\infty \frac{(-\lambda)^k}{k!} + \sum_{k=0}^\infty \frac{\lambda^k}{k!}\right) \\
\;&{\overset{(iii)}{=}}\; \sum_{k=0}^\infty \frac{\lambda^{2k}}{(2k)!} \\
\;&{\overset{(iv)}{\le}}\; \sum_{k=0}^\infty \frac{\lambda^{2k}}{2^kk!} \\
\;&{\overset{(v)}{=}}\; e^{\frac{\lambda^2}{2}},
\end{align}$$

and thus the claim is satisfied by the definition of a sub-Gaussian random
variable. In (i), we removed the expectation by using facts from
Rademacher random variables, in (ii) we used the series expansions of the
exponential function, in (iii) we simplified by removing the odd powers, in (iv)
we used the clever trick that $$2^kk! \le (2k)!$$, and in (v) we *again* used
the exponential function's power series.

To prove the next part, observe that for any $$\lambda \in \mathbb{R}$$, we have

$$\begin{align}
\mathbb{E}_{X}[e^{\lambda X}] \;&{\overset{(i)}{=}}\; \mathbb{E}_{X}\Big[e^{\lambda (X - \mathbb{E}_{X'}[X'])}\Big] \\
\;&{\overset{(ii)}{\le}}\; \mathbb{E}_{X,X'}\Big[e^{\lambda (X - X')}\Big] \\
\;&{\overset{(iii)}{=}}\; \mathbb{E}_{X,X',\varepsilon}\Big[e^{\lambda \varepsilon(X - X')}\Big] \\
\;&{\overset{(iv)}{\le}}\; \mathbb{E}_{X,X'}\Big[e^{\frac{\lambda^2 (X - X')^2}{2}}\Big] \\
\;&{\overset{(v)}{\le}}\; e^{\frac{\lambda^2(b-a)^2}{2}},
\end{align}$$

which shows by definition that $$X$$ is sub-Gaussian with parameter $$\sigma =
b-a$$. In (i), we cleverly introduce *an extra independent copy* $$X'$$ inside
the exponent. It's zero-mean, so we can insert it there without issues.[^miller]
In (ii), we use Jensen's inequality, and note that we can do this with respect
to just the random variable $$X'$$. (If this is confusing, just think of the
expression as a function of $$X'$$ and ignore the outer expectation.) In (iii)
we apply a clever *symmetrization* trick by multiplying a Rademacher random
variable to $$X-X'$$. The reason why we can do this is that $$X-X'$$ is already
symmetric about zero. Hence, inserting the Rademacher factor will maintain that
symmetry (since Rademachers are only +1 or -1). In (iv), we applied the
Rademacher sub-Gaussian bound with $$X-X'$$ held fixed, and then in (v), we
finally use the fact that $$X,X' \in [a,b]$$.

Tricks used:

- Introducing an Independent Copy
- Jensen's Inequality
- Series Expansions (twice!!)
- Symmetrization

**Comments**: The first part is a classic exercise in theoretical statistics,
one which tests your ability to understand how to use the power series of
exponential functions. The first part involved converting an exponential
function to a power series, and then later doing *the reverse*. When I was doing
this problem, I found it easiest to start by stating the conclusion --- that we
would have $$e^{\frac{\lambda^2}{2}}$$ somehow --- and then I worked backwards.
Obviously, this only works when the problem gives us the solution!

The next part is also "classic" in the sense that it's often how students (such
as myself) are introduced to the symmetrization trick. The takeaway is that one
should be on the lookout for anything that seems symmetric. Or, failing that,
perhaps *introduce* symmetry by adding in an extra independent copy, as we did
above.  But make sure that your random variables are zero-mean!!





## Example 3: Concentration Around Median and Means

Here's the question:

> Given a scalar random variable $$X$$, suppose that there are positive
> constants $$c_1,c_2$$ such that 
>
> $$\mathbb{P}[|X-\mathbb{E}[X]| \ge t] \le c_1e^{-c_2t^2}$$ 
>
> for all $$t \ge 0$$.
>
> (a) Prove that  $${\rm Var}(X) \le \frac{c_1}{c_2}$$
> 
> (b) Prove that for any median $$m_X$$, we have 
>
> $$\mathbb{P}[|X-m_X| \ge t] \le c_3e^{-c_4t^2}$$
>
> for all $$t \ge 0$$, where $$c_3 = 4c_1$$ and $$c_4 = \frac{c_2}{8}$$.

To prove the first part, note that

$$
\begin{align}
{\rm Var}(X) \;&{\overset{(i)}{=}}\; \mathbb{E}\Big[|X-\mathbb{E}[X]|^2 \Big]  \\
\;&{\overset{(ii)}{=}}\; 2 \int_{t=0}^\infty t \cdot \mathbb{P}[|X-\mathbb{E}[X]| \ge t]dt  \\
\;&{\overset{(iii)}{\le}}\; \frac{c_2}{c_2} \int_{t=0}^\infty 2t c_1e^{-c_2t^2} dt  \\
\;&{\overset{(iv)}{=}}\; \frac{c_1}{c_2},
\end{align}
$$

where (i) follows from definition, (ii) follows from the "integrating
probabilities into expectations" trick (which I will describe shortly), (iii)
follows from the provided bound, and (iv) follows from standard calculus (note
the multiplication of $$c_2/c_2$$ for mathematical convenience). This proves the
first claim.

This second part requires some clever insights to get this to work. One way to
start is by noting that:

$$\frac{1}{2} = \mathbb{P}[X \ge m_X] = \mathbb{P}\Big[X-\mathbb{E}[X] \ge
m_X-\mathbb{E}[X]\Big] \le c_1e^{-c_2(m_X-\mathbb{E}[X])^2}$$

and where the last inequality follows from the bound provided in the question.
For us to be able to apply that bound, assume without loss of generality that
$$m_X \ge \mathbb{E}[X]$$, meaning that our $$t = m_X-\mathbb{E}[X]$$ term is
positive and that we can increase the probability by inserting in absolute
values. The above also shows that

$$m_X-\mathbb{E}[X] \le \sqrt{\frac{\log(2c_1)}{c_2}}$$

We next tackle the core of the question. Starting from the left hand side of the
desired bound, we get

$$
\begin{align}
\mathbb{P}[|X-m_X| \ge t] \;&{\overset{(i)}{=}}\; \mathbb{P}\Big[|X + \mathbb{E}[X] - \mathbb{E}[X]-m_X| \ge t\Big]  \\
\;&{\overset{(ii)}{\le}}\; \mathbb{P}\Big[|X + \mathbb{E}[X] | \ge t - |\mathbb{E}[X] - m_X|\Big] \\
\;&{\overset{(iii)}{\le}}\; c_1e^{-c_2(t - |\mathbb{E}[X] - m_X|)^2} 
\end{align}
$$

where step (i) follows from adding zero, step (ii) follows from the Triangle
Inequality, and (iii) follows from the provided bound based on the expectation.
And yes, this is supposed to work only for when $$t-|\mathbb{E}[X]-m_X| > 0$$. The
way to get around this is that we need to assume $$t$$ is greater than some
quantity. After some algebra, it turns out a nice condition for us to enforce is
that $$t > \sqrt{\frac{8\log(4c_1)}{c_2}}$$, which in turn will make
$$t-|\mathbb{E}[X]-m_X| > 0$$. If $$t < \sqrt{\frac{8\log(4c_1)}{c_2}}$$, then the
desired bound is attained because 

$$\mathbb{P}[|X-m_X| \ge t] \le 1 \le 4c_1 e^{-\frac{c_2}{8}t^2}$$

a fact which can be derived through some algebra. Thus, the remainder of the
proof boils down to checking the case that when $$t >
\sqrt{\frac{8\log(4c_1)}{c_2}}$$, we have

$$
\mathbb{P}[|X-m_X| \ge t] \le  c_1e^{-c_2(t - |\mathbb{E}[X] - m_X|)^2} \le 4c_1 e^{-\frac{c_2}{8}t^2}
$$

and this is proved by analyzing roots of the quadratic and solving for $$t$$.


Tricks used:

- Integrating Probabilities into Expectations
- Triangle Inequality

**Comments**: The trick "integrating probabilities into expectations" is one
which I only recently learned about, though one can easily find it (along with
the derivation) on the [Wikipedia page for the expected values][5]. In
particular, note that for a positive real number $$\alpha$$, we have

$$\mathbb{E}[|X|^\alpha] = \alpha \int_{0}^\infty t^{\alpha-1}\mathbb{P}[|X| \ge t]dt$$

and in the above, I use this trick with $$\alpha=2$$. It's quite useful to
convert between probabilities and expectations!

The other trick above is using the triangle inequality in a clever way.  The key
is to observe that when we have something like $$\mathbb{P}[X\ge Y]$$, if we
*increase* the value of $$X$$, then we increase that probability. This is
another common trick used in proving various bounds.

Finally, the above also shows that when we have constants $$t$$, it pays to be
clever in how we assign those values. Then the remainder is some brute-force
computation. I suppose it also helps to think about inserting $$1/2$$s whenever
we have a probability and a median.





## Example 4: Upper Bounds for $$\ell_0$$ "Balls"

Consider the set

$$T^d(s) = \{\theta \in \mathbb{R}^d \mid \|\theta\|_0 \le s, \|\theta\|_2 \le 1\}$$

We often write the number of nonzeros in $$\theta$$ as $$\|\theta\|_0$$ like
this even though $$\|\cdot\|_0$$ is not technically a norm. This exercise
consists of three parts:

> (a) Show that $$\mathcal{G}(T^d(s)) = \mathbb{E}[\max_{\mathcal{S}}
> \|w_S\|_2]$$ where $$\mathcal{S}$$ consists of all subsets $$S$$ of 
> $$\{1,2,\ldots, d\}$$ of size $$s$$, and $$w_S$$ is a sub-vector of $$w$$ (of
> size $$s$$) indexed by those components. Note that by this definition, the
> cardinality of $$\mathcal{S}$$ is equal to $${d \choose s}$$.
>
> (b) Show that for any fixed subset $$S$$ of cardinality $$s$$, we have
> $$\mathbb{P}[\|w_S\|_2 \ge \sqrt{s} + \delta] \le e^{-\frac{\delta^2}{2}}$$.
>
> (c) Establish the claim that $$\mathcal{G}(T^d(s)) \precsim \sqrt{s \log
> \left(\frac{ed}{s}\right)}$$.

To be clear on the notation, $$\mathcal{G}(T^d(s)) =
\mathbb{E}\left[\sup_{\theta \in T^d(s)} \langle \theta, w \rangle\right]$$ and
refers to the *Gaussian complexity* of that set. It is, roughly speaking, a way
to measure the "size" of a set.

To prove (a), let $$\theta \in T^d(s)$$ and let $$S$$ indicate the support of
$$\theta$$ (i.e. where its nonzeros occur). For any $$w \in \mathbb{R}^d$$
(which we later treat to be sampled from $$N(0,I_d)$$, though the immediate
analysis below does not require that fact) we have

$$
\langle \theta, w \rangle = 
\langle \tilde{\theta}, w_S \rangle \le
\|\tilde{\theta}\|_2 \|w_S\|_2 \le
\|w_S\|_2,
$$

where $$\tilde{\theta}\in \mathbb{R}^s$$ refers to the vector taking only the
nonzero components from $$\theta$$. The first inequality follows from
Cauchy-Schwarz.  In addition, by standard norm properties, taking $$\theta =
\frac{w_S}{\|w_S\|_2} \in T^d(s)$$ results in the case when equality is
attained. The claim thus follows. (There are some technical details needed
regarding which of the maximums --- over the set sizes or over the vector
selection --- should come first, but I don't think the details are critical for
me to know.)

For (b), we first claim that the function $$f_S : \mathbb{R}^d \to \mathbb{R}$$
defined as $$f_S(w) := \|w_S\|_2$$ is Lipschitz with respect to the Euclidean
norm with Lipschitz constant $$L=1$$. To see this, observe that when $$w$$ and
$$w'$$ are both $$d$$-dimensional vectors, we have

$$
|f_S(w)-f_S(w')| =
\Big|\|w_S\|_2-\|w_S'\|_2\Big| \;{\overset{(i)}{\le}}\;
\|w_S-w_S'\|_2 \;{\overset{(ii)}{\le}}\;
\|w-w'\|_2,
$$

where (i) follows from the reverse triangle inequality for normed spaces and
(ii) follows from how the vector $$w_S-w_S'$$ cannot have more nonzero terms
than $$w-w'$$ but must otherwise match it for indices lying in the subset $$S$$.

The fact that $$f_S$$ is Lipschitz means that we can apply a theorem regarding
tail bounds of Lipschitz functions of Gaussian variables. The function $$f_S$$
here doesn't *require* its input to consist of vectors with IID standard
Gaussian components, but we have to assume that the input is like that for the
purposes of the theorem/bound to follow. More formally, for all $$\delta \ge 0$$
we have

$$
\mathbb{P}\Big[\|w_S\|_2 \ge \sqrt{s} + \delta\Big] \;{\overset{(i)}{\le}}\;
\mathbb{P}\Big[\|w_S\|_2 \ge \mathbb{E}[\|w_S\|_2] + \delta \Big]\;{\overset{(ii)}{\le}}\;
e^{-\frac{\delta^2}{2}}
$$

where (i) follows from how $$\mathbb{E}[\|w_S\|_2] \le \sqrt{s}$$ and thus we
are just decreasing the threshold for the event (hence making it more likely)
and (ii) follows from the theorem, which provides an $$L$$ in the denominator of
the exponential, but $$L=1$$ here.

Finally, to prove (c), we first note that the previous part's theorem guaranteed
that the function $$f_S(w) = \|w_S\|_2$$ is sub-Gaussian with parameter
$$\sigma=L=1$$.  Using this, we have

$$
\mathcal{G}(T^d(s)) = \mathbb{E}\Big[\max_{S \in \mathcal{S}} \|w_S\|_2\Big]
\;{\overset{(i)}{\le}}\; \sqrt{2 \sigma^2 \log {d \choose s}}
\;{\overset{(ii)}{\precsim}}\; \sqrt{s \log \left(\frac{ed}{s}\right)}
$$

where (i) applies the bound for a maximum over sub-Gaussian random variables
$$\|w_S\|_2$$ for all the $${d\choose s}$$ sets $$S \in \mathcal{S}$$ (see
Example 1 earlier), each with parameter $$\sigma$$, and (ii) applies an
approximate bound due to Stirling's approximation and ignores the constants of
$$\sqrt{2}$$ and $$\sigma$$. The careful reader will note that Example 1
required *zero*-mean sub-Gaussian random variables, but we can generally get
around this by, I believe, subtracting away a mean and then re-adding later.

Tricks used:

- Cauchy-Schwarz
- Jensen's Inequality
- Lipschitz Functions
- Norm Properties
- Stirling's Approximation
- Triangle Inequality

**Comments**: This exercise involves a number of tricks. The fact that
$$\mathbb{E}[\|w_S\|_2] \le \sqrt{s}$$ follows from how 

$$
\mathbb{E}[\|w_S\|_2] = \mathbb{E}\Big[\sqrt{\|w_S\|_2^2}\Big] \le
\sqrt{\mathbb{E}[\|w_S\|_2^2]} = \sqrt{s}
$$ 

due to Jensen's inequality and how $$\mathbb{E}[X^2]=1$$ for $$X \sim
N(0,1)$$. Fiddling with norms, expectations, and square roots is another common
way to utilize Jensen's inequality (in addition to using Jensen's inequality
with the exponential function, as explained earlier). Moreover, if you see norms
in a probabilistic bound statement, you should immediately be thinking of the
possibility of using a theorem related to Lipschitz functions.

The example also uses the (reverse!) triangle inequality for norms: 

$$\Big| \|x\|_2-\|y\|_2\Big| \le \|x-y\|_2$$

This can come up quite often and is the non-canonical way of viewing the
triangle inequality, so watch out! 

Finally, don't forget the trick where we have $${d \choose s} \le
\left(\frac{ed}{s}\right)^s$$. This comes from [an application of Stirling's
approximation][7] and is seen frequently in cases involving *sparsity*, where
$$s$$ components are "selected" out of $$d \gg s$$ total. The maximum over a
finite set should also provide a big hint regarding the use of a sub-Gaussian
bound over maximums of (sub-Gaussian) variables.





## Example 5: Gaussian Complexity of Ellipsoids

> Recall that the space $$\ell_2(\mathbb{N})$$ consists of all real sequences
> $$\{\theta_j\}_{j=1}^\infty$$ such that $$\sum_{j=1}^\infty \theta_j^2 \le
> \infty$$. Given a strictly positive sequence $$\{\mu_j\}_{j=1}^\infty \in \ell_2(\mathbb{N})$$,
> consider the associated ellipse 
> 
> $$\mathcal{E} := \left\{\{\theta_j\}_{j=1}^\infty \in \ell_2(\mathbb{N}) \;\Big|
> \sum_{j=1}^\infty \frac{\theta_j^2}{\mu_j^2} \le 1\right\}$$
> 
> (a) Prove that the Gaussian complexity satisfies the bounds
>
> $$\sqrt{\frac{2}{\pi}}\left(\sum_{j=0}^\infty \mu_j^2 \right)^{1/2} \le
> \mathcal{G}(\mathcal{E}) \le  \left(\sum_{j=0}^\infty \mu_j^2 \right)^{1/2}$$
>
> (b) For a given radius $$r > 0$$, consider the truncated set
>
> $$ \tilde{\mathcal{E}} := \mathcal{E} \cap \left\{\{\theta_j\}_{j=1}^\infty
> \;\Big| \sum_{j=1}^\infty \theta_j^2 \le r^2 \right\}$$
>
> Obtain upper and lower bounds on its Gaussian complexity that are tight up to
> universal constants independent of $$r$$ and $$\{\mu_j\}_{j=1}^\infty$$.

To prove (a), we first start with the upper bound. Letting $$w$$ indicate a
sequence of IID standard Gaussians $$w_i$$, we have

$$
\begin{align}
\mathcal{G}(\mathcal{E}) \;&{\overset{(i)}{=}}\; \mathbb{E}_w\left[ \sup_{\theta \in \mathcal{E}}\sum_{i=1}^\infty w_i\theta_i \right]  \\
\;&{\overset{(ii)}{=}}\; \mathbb{E}_w\left[ \sup_{\theta \in \mathcal{E}}\sum_{i=1}^\infty \frac{\theta_i}{\mu_i}w_i\mu_i \right]  \\
\;&{\overset{(iii)}{\le}}\; \mathbb{E}_w\left[ \sup_{\theta \in \mathcal{E}} \left(\sum_{i=1}^\infty\frac{\theta_i^2}{\mu_i^2}\right)^{1/2}\left(\sum_{i=1}^\infty w_i^2 \mu_i^2\right)^{1/2} \right] \\
\;&{\overset{(iv)}{\le}}\; \mathbb{E}_w\left[ \left(\sum_{i=1}^\infty w_i^2 \mu_i^2 \right)^{1/2} \right] \\
\;&{\overset{(v)}{\le}}\; \sqrt{\mathbb{E}_w\left[ \sum_{i=1}^\infty w_i^2 \mu_i^2 \right]} \\
\;&{\overset{(vi)}{=}}\; \left( \sum_{i=1}^\infty \mu_i^2 \right)^{1/2}
\end{align}
$$

where (i) follows from definition, (ii) follows from multiplying by one, (iii)
follows from a clever application of the [Cauchy-Schwarz inequality][3] for
sequences (or more generally, [Holder's Inequality][2]), (iv) follows from the
definition of $$\mathcal{E}$$, (v) follows from Jensen's inequality, and (vi)
follows from linearity of expectation and how $$\mathbb{E}_{w_i}[w_i^2]=1$$.

We next prove the lower bound. First, we note a well-known result that
$$\sqrt{\frac{2}{\pi}}\mathcal{R}(\mathcal{E}) \le \mathcal{G}(\mathcal{E})$$
where $$\mathcal{R}(\mathcal{E})$$ indicates the *Rademacher* complexity of the
set. Thus, our task now boils down to showing that $$\mathcal{R}(\mathcal{E}) =
\left(\sum_{i=1}^\infty \mu_i^2 \right)^{1/2}$$. Letting $$\varepsilon_i$$ be
IID Rademachers, we first begin by proving the *upper* bound

$$
\begin{align}
\mathcal{R}(\mathcal{E}) \;&{\overset{(i)}{=}}\; \mathbb{E}_\varepsilon\left[ \sup_{\theta \in \mathcal{E}}\sum_{i=1}^\infty \varepsilon_i\theta_i \right]  \\
\;&{\overset{(ii)}{=}}\; \sup_{\theta \in \mathcal{E}}\sum_{i=1}^\infty \Big|\frac{\theta_i}{\mu_i}\mu_i\Big|  \\
\;&{\overset{(iii)}{\le}}\; \sup_{\theta \in \mathcal{E}} \left(\sum_{i=1}^\infty\frac{\theta_i^2}{\mu_i^2}\right)^{1/2}\left(\sum_{i=1}^\infty \mu_i^2\right)^{1/2} \\
\;&{\overset{(iv)}{=}}\; \left( \sum_{i=1}^\infty \mu_i^2 \right)^{1/2}
\end{align}
$$

where (i) follows from definition, (ii) follows from the symmetric nature of the
class of $$\theta$$ (meaning that WLOG we can pick $$\varepsilon_i = 1$$ for all
$$i$$) and then multiplying by one, (iii), follows from Cauchy-Schwarz again,
and (iv) follows from the provided bound in the definition of $$\mathcal{E}$$.

We're not done yet: we actually need to show *equality* for this, or at the very
least prove a *lower* bound instead of an upper bound.  However, if one chooses
the valid sequence $$\{\theta_j\}_{j=1}^\infty$$ such that $$\theta_j =
\mu_j^2 / (\sum_{j=1}^\infty \mu_j^2)^{1/2}$$, then equality is attained since we
get

$$
\frac{\sum_{i=1}^\infty \mu_i^2}{\left(\sum_{i=1}^\infty \mu_i^2\right)^{1/2}} = 
\left( \sum_{i=1}^\infty \mu_i^2 \right)^{1/2}
$$

in one of our steps above. This proves part (a). 

For part (b), we construct two ellipses, one that contains
$$\tilde{\mathcal{E}}$$ and one which is contained inside it. Let $$m_i :=
\min\{\mu_i, r\}$$. Then we claim that the ellipse $$\mathcal{E}_{m}$$ defined
out of this sequence (i.e. treating "$$m$$" as our "$$\mu$$") will be contained
in $$\tilde{\mathcal{E}}$$. We moreover claim that the ellipse
$$\mathcal{E}^{m}$$ defined out of the sequence $$\sqrt{2} \cdot m_i$$ for all
$$i$$ contains $$\tilde{\mathcal{E}}$$, i.e. $$\mathcal{E}_m \subset
\tilde{\mathcal{E}} \subset \mathcal{E}^m$$. If this is true, it then follows
that

$$
\mathcal{G}(\mathcal{E}_m) \le
\mathcal{G}(\tilde{\mathcal{E}}) \le \mathcal{G}(\mathcal{E}^m)
$$

because the definition of Gaussian complexity requires taking a maximum of
$$\theta$$ over a set, and if the set grows larger via set containment, then the
Gaussian complexity can only grow larger. In addition, the fact that the upper
and lower bounds are related by a constant $$\sqrt{2}$$ suggests that there
should be extra lower and upper bounds utilizing universal constants independent
of $$r$$ and $$\mu$$.

Let us prove the two set inclusions previously described, as well as develop the
desired upper and lower bounds. Suppose $$\{\theta_j\}_{j=1}^\infty \in
\mathcal{E}_m$$. Then we have

$$
\sum_{i=1}^\infty \frac{\theta_i^2}{r^2} \le \sum_{i=1}^\infty \frac{\theta_i^2}{(\min\{r,\mu_j\})^2} \le 1
$$

and

$$
\sum_{i=1}^\infty \frac{\theta_i^2}{\mu_i^2} \le \sum_{i=1}^\infty \frac{\theta_i^2}{(\min\{r,\mu_j\})^2} \le 1
$$

In both cases, the first inequality is because we can only decrease the value in
the denominator.[^downstairs] The last inequality follows by assumption of
membership in $$\mathcal{E}_m$$. Both requirements for membership in
$$\tilde{\mathcal{E}}$$ are satisfied, and therefore,
$$\{\theta_j\}_{j=1}^\infty \in \mathcal{E}_m$$ implies
$$\{\theta_j\}_{j=1}^\infty \in \tilde{\mathcal{E}}$$ and thus the first set
containment. Moving on to the second set containment, suppose
$$\{\theta_j\}_{j=1}^\infty \in \tilde{\mathcal{E}}$$. We have

$$
\frac{1}{2}\sum_{i=1}^\infty \frac{\theta_i^2}{(\min\{\mu_i,r\})^2}
\;{\overset{(i)}{\le}}\;
\frac{1}{2}\left( \sum_{i=1}^\infty \frac{\theta_i^2}{r^2}+\sum_{i=1}^\infty
\frac{\theta_i^2}{\mu_i^2}\right)
\;{\overset{(ii)}{\le}}\; 1
$$

where (i) follows from a "union bound"-style argument, which to be clear,
happens because for every term $$i$$ in the summation, we have either
$$\frac{\theta_i^2}{r^2}$$ or $$\frac{\theta_i^2}{\mu_i^2}$$ added to the
summation (both positive quantities). Thus, to make the value *larger*, just add
*both* terms! Step (ii) follows from the assumption of membership in
$$\tilde{\mathcal{E}}$$. Thus, we conclude that $$\{\theta_j\}_{j=1}^\infty \in
\mathcal{E}_m$$, and we have proved that

$$
\mathcal{G}(\mathcal{E}_m) \le
\mathcal{G}(\tilde{\mathcal{E}}) \le \mathcal{G}(\mathcal{E}^m)
$$

The final step of this exercise is to develop a lower bound on the left hand
side and an upper bound on the right hand side that are close up to universal
constants. But we have reduced this to an instance of part (a)! Thus, we simply
apply the lower bound for $$\mathcal{G}(\mathcal{E}_m)$$ and the upper bound for
$$\mathcal{G}(\mathcal{E}^m)$$ and obtain

$$
\sqrt{\frac{2}{\pi}}\left(\sum_{i=1}^\infty m_i^2 \right)^{1/2}
\le \mathcal{G}(\mathcal{E}_m) \le
\mathcal{G}(\tilde{\mathcal{E}}) \le \mathcal{G}(\mathcal{E}^m) \le
\sqrt{2}\left(\sum_{i=1}^\infty m_i^2 \right)^{1/2}
$$

as our final bounds on $$\mathcal{G}(\tilde{\mathcal{E}})$$. (Note that
as a sanity check, the constant offset $$\sqrt{1/\pi} \approx 0.56$$ is less
than one.) This proves part (b).

Tricks used:

- Cauchy-Schwarz
- Jensen's Inequality
- Union Bound

**Comments**: This exercise on the surface looks extremely challenging. How does
one reason about multiple infinite sequences, which furthermore may or may not
involve squared terms?  I believe the key to tackling these problems is to
understand how to apply Cauchy-Schwarz (or more generally, Holder's Inequality)
for infinite sequences.  More precisely, Holder's Inequality for sequences
spaces states that

$$
\sum_{k=1}^\infty |x_ky_k| \le \left(\sum_{k=1}^\infty x_k^2 \right)^{1/2}\left( \sum_{k=1}^\infty y_k^2 \right)^{1/2}
$$

(It's actually more general for this, since we can assume arbitrary positive
powers $$p$$ and $$q$$ so long as $$1/p + 1/q=1$$, but the easiest case to
understand is when $$p=q=2$$.)

Holder's Inequality is *enormously helpful* when dealing with sums (whether
infinite or not), and *especially* when dealing with two sums if one does *not*
square its terms, but the other one *does*.

Finally, again, think about Jensen's inequality whenever we have expectations
and a square root!





## Example 6: Pairwise Incoherence

> Given a matrix $$X \in \mathbb{R}^{n \times d}$$, suppose it has normalized
> columns ($$\|X\|_2/\sqrt{n} = 1$$ for all $$j = 1,...,d$$) and pairwise
> incoherence upper bounded as $$\delta_{\rm PW}(X) < \gamma$$.
>
> (a) Let $$S \subset \{1,2,\ldots,d\}$$ be any subset of size $$s$$. Show that
> there is a function $$\gamma \to c(\gamma)$$ such that $$\lambda_{\rm
> min}\left(\frac{X_S^TX_S}{n}\right) \ge c(\gamma) > 0$$ as long as $$\gamma$$
> is sufficiently small, where $$X_S$$ is the $$n\times s$$ matrix formed by
> extracting the $$s$$ columns of $$X$$ whose indices are in $$S$$.
>
> (b) Prove, from first principles, that $$X$$ satisfies the restricted
> nullspace property with respect to $$S$$ as long as $$\gamma < 1/3$$.

To clarify, the *pairwise incoherence* of a matrix $$X \in \mathbb{R}^{n \times
d}$$ is defined as

$$\delta_{\rm PW}(X) := \max_{j,k = 1,2,\ldots, d} 
\left|\frac{|\langle X_j, X_k \rangle|}{n} - \mathbb{I}[j\ne k]\right|$$

where $$X_i$$ denotes the $$i$$-th *column* of $$X$$. Intuitively, it measures
the correlation between any columns, though it subtracts an indicator at the end
so that the maximal case does not always correspond to the case when $$j=k$$. In
addition, the matrix $$\frac{X_S^TX_S}{n}$$ as defined in the problem looks like:

$$
\frac{X_S^TX_S}{n} = 
\begin{bmatrix}
\frac{(X_S)_1^T(X_S)_1}{n} & \frac{(X_S)_1^T(X_S)_2}{n} & \cdots & \frac{(X_S)_1^T(X_S)_s}{n} \\
\frac{(X_S)_1^T(X_S)_2}{n} & \frac{(X_S)_2^T(X_S)_2}{n} & \cdots & \vdots \\
\vdots & \ddots & \ddots & \vdots \\
\frac{(X_S)_1^T(X_S)_s}{n} & \cdots & \cdots  & \frac{(X_S)_s^T(X_S)_s}{n} \\
\end{bmatrix} = 
\begin{bmatrix}
1  & \frac{(X_S)_1^T(X_S)_2}{n} & \cdots & \frac{(X_S)_1^T(X_S)_s}{n} \\
\frac{(X_S)_1^T(X_S)_2}{n} & 1 & \cdots & \vdots \\
\vdots & \ddots & \ddots & \vdots \\
\frac{(X_S)_1^T(X_S)_s}{n} & \cdots & \cdots  & 1 \\
\end{bmatrix}
$$

where the 1s in the diagonal are due to the assumption of having normalized columns.

First, we prove part (a). Starting from the *variational representation* of the
minimum eigenvalue, we consider any possible $$v \in \mathbb{R}^s$$ with
Euclidean norm one (and thus this analysis will apply for the *minimizer*
$$v^*$$ which induces the minimum eigenvalue) and observe that

$$
\begin{align}
v^T\frac{X_S^TX_S}{n}v \;&{\overset{(i)}{=}}\; \sum_{i=1}^sv_i^2 + 2\sum_{i<j}^s\frac{(X_S)_i^T(X_S)_j}{n}v_iv_j   \\
\;&{\overset{(ii)}{=}}\; 1 + 2\sum_{i<j}^s\frac{(X_S)_i^T(X_S)_j}{n}v_iv_j \\
\;&{\overset{(iii)}{\ge}}\; 1 - 2\frac{\gamma}{s}\sum_{i<j}^s|v_iv_j| \\
\;&{\overset{(iv)}{=}}\; 1 - \frac{\gamma}{s}\left((|v_i| + \cdots + |v_s|)^2-\sum_{i=1}^sv_i^2\right) \\
\;&{\overset{(v)}{\ge}}\; 1 - \frac{\gamma}{s}\Big(s\|v\|_2^2)-\|v\|_2^2\Big)
\end{align}
$$

where (i) follows from the definition of a quadratic form (less formally, by
matrix multiplication), (ii) follows from the $$\|v\|_2 = 1$$ assumption, (iii)
follows from noting that 

$$
-\sum_{i<j}^s\frac{(X_S)_i^T(X_S)_j}{n}v_iv_j  \le  \frac{\gamma}{s}\sum_{i<j}^s|v_iv_j|
$$

which in turn follows from the pairwise incoherence assumption that
$$\Big|\frac{(X_S)_i^T(X_S)_j}{n}\Big| \le \frac{\gamma}{s}$$. Step (iv) follows
from definition, and (v) follows from how $$\|v\|_1 \le \sqrt{s}\|v\|_2$$ for
$$s$$-dimensional vectors.

The above applies for any satisfactory $$v$$. Putting together the pieces, we
conclude that

$$
\lambda_{\rm min}\left(\frac{X_S^TX_S}{n}\right) = \inf_{\|v\|_2=1} v^T\frac{X_S^TX_S}{n}v
\ge \underbrace{1 - \gamma \frac{s-1}{s}}_{c(\gamma)} \ge 1-\gamma,
$$

which follows if $$\gamma$$ is sufficiently small.

To prove the restricted [nullspace property][10] in (b), we first suppose that
$$\theta \in \mathbb{R}^d$$ and $$\theta \in {\rm null}(X) \setminus \{0\}$$.
Define $$d$$-dimensional vectors $$\tilde{\theta}_S$$ and
$$\tilde{\theta}_{S^c}$$ which match components of $$\theta$$ for the indices
within their respective sets $$S$$ or $$S^c$$, and which are zero
otherwise.[^time] Supposing that $$S$$ corresponds to the subset of indices of
$$\theta$$ of the $$s$$ largest elements in absolute value, it suffices to show
that $$\|\tilde{\theta}_{S^c}\|_1 > \|\tilde{\theta}_S\|_1$$, because then we
can *never* violate this inequality (and thus the restricted nullspace property
holds).

We first show a few facts which we then piece together to get the final result.
The first is that

$$
\begin{align}
0 \;&{\overset{(i)}{=}}\; \|X\theta \|_2^2 \\
\;&{\overset{(ii)}{=}}\; \|X\tilde{\theta}_S + X\tilde{\theta}_{S^c}\|_2^2 \\
\;&{\overset{(iii)}{=}}\; \|X\tilde{\theta}_S\|_2^2 + \|X\tilde{\theta}_{S^c}\|_2^2 + 2\tilde{\theta}_S^T(X^TX)\tilde{\theta}_{S^c}\\
\;&{\overset{(iv)}{\ge}}\; n\|\theta_S\|_2^2 \cdot \lambda_{\rm min}\left(\frac{X_S^TX_S}{n}\right) - 2\Big|\tilde{\theta}_S^T(X^TX)\tilde{\theta}_{S^c}\Big|
\end{align}
$$

where (i) follows from the assumption that $$\theta$$ is in the kernel of $$X$$,
(ii) follows from how $$\theta = \tilde{\theta}_S + \tilde{\theta}_{S^c}$$,
(iii) follows from expanding the term, and (iv) follows from carefully noting
that

$$
\lambda_{\rm min}\left(\frac{X_S^TX_S}{n}\right) = \min_{v \in \mathbb{R}^d}
\frac{v^T\frac{X_S^TX_S}{n}v}{v^Tv} \le
\frac{\theta_S^T\frac{X_S^TX_S}{n}\theta_S}{\|\theta_S\|_2^2}
$$

where in the inequality, we have simply chosen $$\theta_S$$ as our $$v$$, which
can only make the bound worse. Then step (iv) follows immediately. Don't forget
that $$\|\theta_S\|_2^2 = \|\tilde{\theta}_S\|_2^2$$, because the latter
involves a vector that (while longer) only has extra zeros. Incidentally, the
above uses the variational representation for eigenvalues in a way that's more
convenient if we don't want to restrict our vectors to have Euclidean norm one.

We conclude from the above that

$$
n\|\theta_S\|_2^2 \cdot \lambda_{\rm min}\left(\frac{X_S^TX_S}{n}\right) \le 2\Big|\tilde{\theta}_S^T(X^TX)\tilde{\theta}_{S^c}\Big|
$$

Next, let us upper bound the RHS. We see that

$$
\begin{align}
\Big|\tilde{\theta}_S^T(X^TX)\tilde{\theta}_{S^c}\Big|\;&{\overset{(i)}{=}}\; \Big|\theta_S^T(X_S^TX_{S^c})\theta_{S^c}\Big|\\
\;&{\overset{(ii)}{=}}\; \left| \sum_{i\in S, j\in S^c} X_i^TX_j (\tilde{\theta}_S)_i(\tilde{\theta}_{S^c})_j \right| \\
\;&{\overset{(iii)}{\le}}\; \frac{n\gamma}{s} \sum_{i\in S, j\in S^c} |(\tilde{\theta}_S)_i(\tilde{\theta}_{S^c})_j |\\
\;&{\overset{(iv)}{=}}\; \frac{n\gamma}{s}\|\theta_S\|_1\|\theta_{S^c}\|_1
\end{align}
$$

where (i) follows from a little thought about how matrix multiplication and
quadratic forms work. In particular, if we expanded out the LHS, we would get a
sum with lots of terms that are zero since $$(\tilde{\theta}_S)_i$$ or
$$(\tilde{\theta}_{S^c})_j$$ would cancel them out. (To be clear, $$\theta_S \in
\mathbb{R}^s$$ and $$\theta_{S^c} \in \mathbb{R}^{d-s}$$.) Step (ii) follows
from definition, step (iii) follows from the provided Pairwise Incoherence bound
(note the need to multiply by $$n/n$$), and step (iv) follows from how

$$
\|\theta_S\|_1\|\theta_{S^c}\|_1 = \Big(|(\theta_S)_1| +\cdots+ |(\theta_S)_s|\Big) 
\Big(|(\theta_{S^c})_1| +\cdots+ |(\theta_{S^c})_{d-s}|\Big)
$$

and thus it is clear that the product of the $$L_1$$ norms consists of the sum
of all possible combination of indices with nonzero values.

The last thing we note is that from part (a), if we assumed that $$\gamma \le
1/3$$, then a lower bound on $$\lambda_{\rm min}
\left(\frac{X_S^TX_S}{n}\right)$$ is $$2/3$$. Putting the pieces together, we
get the following three inequalities

$$
\frac{2n\|\theta_S\|_2^2}{3} \;\;\le \;\;
n\|\theta_S\|_2^2 \cdot \lambda_{\rm min}\left(\frac{X_S^TX_S}{n}\right) \;\;\le \;\;
2\Big|\tilde{\theta}_S^T(X^TX)\tilde{\theta}_{S^c}\Big| \;\; \le \;\;
\frac{2n\gamma}{s}\|\theta_S\|_1\|\theta_{S^c}\|_1
$$

We can provide a lower bound for the first term above. Using the fact that
$$\|\theta_S\|_1^2 \le s\|\theta_S\|_2^2$$, we get
$$\frac{2n\|\theta_S\|_1^2}{3s} \le \frac{2n\|\theta_S\|_2^2}{3}$$. The final
step is to tie the lower bound here with the upper bound from the set of three
inequalities above. This results in

$$
\begin{align}
\frac{2n\|\theta_S\|_1^2}{3s} \le \frac{2n\gamma}{s}\|\theta_S\|_1\|\theta_{S^c}\|_1 \quad &\iff \quad
\frac{\|\theta_S\|_1^2}{3} \le \gamma \|\theta_S\|_1\|\theta_{S^c}\|_1 \\
&\iff \quad \|\theta_S\|_1 \le 3\gamma \|\theta_{S^c}\|_1 
\end{align}
$$

Under the same assumption earlier (that $$\gamma < 1/3$$) it follows directly
that $$\|\theta_S\|_1 < \|\theta_{S^c}\|_1$$, as claimed. Whew!

Tricks used:

- Cauchy-Schwarz
- Norm Properties
- Variational Representation (of eigenvalues)

**Comments**: Actually, for part (a), one can prove this more directly by using
the [Gershgorin Circle Theorem][9], a *very* useful Theorem with a surprisingly
simple proof. But I chose this way above so that we can make use of the
variational representation for eigenvalues. There are also variational
representations for *singular values*.

The above uses a *lot* of norm properties. One example was the use of $$\|v\|_1
\le \sqrt{s}\|v\|_2$$, which can be proved via Cauchy-Schwarz. The extension to
this is that $$\|v\|_2 \le \sqrt{s}\|v\|_\infty$$. These are quite handy.
Another example, which is useful when dealing with specific subsets, is to
understand how the $$L_1$$ and $$L_2$$ norms behave. Admittedly, getting all the
steps right for part (b) takes a *lot* of hassle and attention to details, but
it is certainly satisfying to see it work.



## Closing Thoughts

I hope this post serves as a useful reference for me and to anyone else who
might need to use one of these tricks to understand some machine learning and
statistics-related math.

***

[^miller]: One of my undergraduate mathematics professors, [Steven J.
    Miller][4], would love this trick, as his two favorite tricks in mathematics
    are *adding zero* (along with, of course, multiplying by one).

[^downstairs]: Or "downstairs" as professor [Michael I. Jordan][8] often puts it
    (and obviously, "upstairs" for the numerator).

[^time]: It can take some time and effort to visualize and process all this
    information. I find it helpful to draw some of these out with pencil and
    paper, and also to assume without loss of generality that $$S$$ corresponds
    to the first "block" of $$\theta$$, and $$S^c$$ therefore corresponds to the
    second (and last) "block." Please contact me if you spot typos; they're
    really easy to make here.

[1]:https://danieltakeshi.github.io/2017/04/22/following-professor-michael-jordans-advice-your-brain-needs-exercise
[2]:https://en.wikipedia.org/wiki/H%C3%B6lder%27s_inequality
[3]:https://en.wikipedia.org/wiki/Cauchy%E2%80%93Schwarz_inequality
[4]:https://web.williams.edu/Mathematics/sjmiller/public_html/williams/welcome.html
[5]:https://en.wikipedia.org/wiki/Expected_value
[6]:https://en.wikipedia.org/wiki/Boole%27s_inequality
[7]:https://math.stackexchange.com/questions/132625/n-choose-k-leq-left-fracen-k-rightk
[8]:https://people.eecs.berkeley.edu/~jordan/
[9]:https://en.wikipedia.org/wiki/Gershgorin_circle_theorem
[10]:https://en.wikipedia.org/wiki/Nullspace_property
