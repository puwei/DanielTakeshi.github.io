---
layout: post
title:  "Notes on the Generalized Advantage Estimation Paper"
date:   2017-04-02 06:00:00
permalink: 2017/04/02/notes-on-the-generalized-advantage-estimation-paper/
---

This post serves as a continuation of [my last post on the fundamentals of
policy gradients][1]. Here, I continue it by discussing the *Generalized
Advantage Estimation* ([arXiv link][2]) paper from ICLR 2016, which presents and
analyzes more sophisticated forms of policy gradient methods.

Recall that raw policy gradients, while unbiased, have *high variance*. This
paper proposes ways to dramatically reduce variance, but this unfortunately
comes at the cost of introducing bias, so one needs to be careful before
applying tricks like this in practice.

The setting is the usual one which I presented in my last post, and we are
indeed trying to maximize the sum of rewards (for now, assume no discount). I'm
happy that the paper includes a concise set of notes summarizing policy
gradients:

<p style="text-align:center;"> <img src="{{site.url}}/assets/gae_paper_pg_basics.png" alt="policy_gradients"> </p>

If the above is not 100% clear to you, I recommend reviewing the basics of policy
gradients. I covered five of the six forms of the $$\Psi_t$$ function in my last
post; the exception is the temporal difference residual, but I will go over
these later here. 

Somewhat annoyingly, they use the infinite-horizon setting. I find it easier to
think about the *finite* horizon case, and I will clarify if I'm assuming that.


# Proposition 1: $$\gamma$$-Just Estimators.

One of the first things they prove is Proposition 1, regarding $$\gamma$$-just
advantage estimators. Suppose $$\hat{A}_t(s_{0:\infty},a_{0:\infty})$$ is an
estimate of the advantage function.  A $$\gamma$$-just estimator (of the
advantage function) results in 

$$
\mathbb{E}_{s_{0:\infty},a_{0:\infty}}\left[\hat{A}_t(s_{0:\infty},a_{0:\infty}) \nabla_\theta \log \pi_{\theta}(a_t|s_t)\right]=
\mathbb{E}_{s_{0:\infty},a_{0:\infty}}\left[A^{\pi,\gamma}(s_{0:\infty},a_{0:\infty}) \nabla_\theta \log \pi_{\theta}(a_t|s_t)\right]
$$

This is for *one time step* $$T$$. If we sum over all time steps, by linearity
of expectation we get

$$
\mathbb{E}_{s_{0:\infty},a_{0:\infty}}\left[\sum_{t=0}^\infty \hat{A}_t(s_{0:\infty},a_{0:\infty}) \nabla_\theta \log \pi_{\theta}(a_t|s_t)\right]=
\mathbb{E}_{s_{0:\infty},a_{0:\infty}}\left[\sum_{t=0}^\infty A^{\pi,\gamma}(s_t,a_t)\nabla_\theta \log \pi_{\theta}(a_t|s_t)\right]
$$

In other words, we get an *unbiased* estimate of the discounted gradient. Note,
however, that this discounted gradient is *different* from the gradient of the
actual function we're trying to optimize, since that was for the *undiscounted*
rewards. The authors emphasize this in a footnote, saying that they've *already*
introduced bias by even assuming we're using the discounted version.  (I'm
somewhat pleased at myself for catching this in advance.)

The proof for Proposition 1 is based on proving it for one time step $$t$$,
which is all that is needed. The resulting term with $$\hat{A}_t$$ in it splits
into two terms due to linearity of expectation, one with the $$Q_t$$ function
and another with the baseline. The second term is zero due to the baseline
causing the expectation to zero, which I derived in my previous post in the
finite-horizon case. (I'm not totally sure how to do this in the infinite
horizon case, due to technicalities involving infinity.) 

The first term is unfortunately a little more complicated. Let me use the finite
horizon $$T$$ for simplicity so that I can easily write out the definition. They
argue in the proof that:

$$
\begin{align}
&\mathbb{E}_{s_{0:T},a_{0:T}}\left[ \nabla_\theta \log \pi_{\theta}(a_t|s_t) \cdot Q_t(s_{0:T},a_{0:T})\right] \\
&= \mathbb{E}_{s_{0:t},a_{0:t}}\left[ \nabla_\theta \log \pi_{\theta}(a_t|s_t)\cdot \mathbb{E}_{s_{t+1:T},a_{t+1:T}}\Big[Q_t(s_{0:T},a_{0:T})\Big]\right] \\
&= \int_{s_0}\cdots \int_{s_t}\int_{a_t}\Bigg[ p_\theta((s_0,\ldots,s_t,a_t)) \nabla_\theta \log \pi_{\theta}(a_t|s_t) \cdot \mathbb{E}_{s_{t+1:T},a_{t+1:T}}\Big[ Q_t(s_{0:T},a_{0:T}) \Big]\Bigg] d\mu(s_0,\ldots,s_t,a_t)\\
\;&{\overset{(i)}{=}}\; \int_{s_0}\cdots \int_{s_t} \left[ p_\theta((s_0,\ldots,s_t)) \nabla_\theta \log \pi_{\theta}(a_t|s_t) \cdot A^{\pi,\gamma}(s_t,a_t)\right] d\mu(s_0,\ldots,s_t)
\end{align}
$$

Most of this proceeds by definitions of expectations and then "pushing"
integrals into their appropriate locations.  Unfortunately, I am unable to
figure out how they did step (i). Specifically, I don't see how the integral
over $$a_t$$ somehow "moves past" the $$\nabla_\theta \log \pi_\theta(a_t|s_t)$$
term. Perhaps there is some trickery with the law of iterated expectation due to
conditionals? If anyone else knows why and is willing to explain with detailed
math somewhere, I would really appreciate it.

For now, I will assume this proposition to be true. It is useful because if we
are given the form of estimator $$\hat{A}_t$$ of the advantage, we can
immediately tell if it is unbiased.


# Advantage Function Estimators

Now assume we have some function $$V$$ which attempts to approximate the true
value function $$V^\pi$$ (or $$V^{\pi,\gamma}$$ in the undiscounted setting).

- **Note I**: $$V$$ is *not* the true value function. It is only our estimate of
  it, so $$V_\phi(s_t) \approx V^\pi(s_t)$$. I added in the $$\phi$$ subscript
  to indicate that we use a function, such as a neural network, to approximate
  the value.

- **Note II**: we *also* have our policy $$\pi_\theta$$ parameterized by
  parameters $$\theta$$, typically a neural network nowadays. For now, assume
  that these are *separate* parameters. The combination of $$\pi_{\theta}$$ and
  $$V_{\phi}$$ with a policy estimator and a value function estimator is known
  as the **actor-critic** model with the policy as the actor and the value
  function as the critic.

Using $$V$$, we can derive a *class* of advantage function estimators as
follows:

$$
\begin{align}
\hat{A}_t^{(1)} &= r_t + \gamma V(s_{t+1}) - V(s_t) \\
\hat{A}_t^{(2)} &= r_t + \gamma r_{t+1} + \gamma^2 V(s_{t+2}) - V(s_t) \\
\cdots &= \cdots \\ 
\hat{A}_t^{(\infty)} &= r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + \cdots - V(s_t)
\end{align}
$$

These take on the form of temporal difference estimators where we first estimate
the sum of discounted rewards and then we subtract the value function estimate
of it. **If** $$V = V^{\pi,\gamma}$$, meaning that $$V$$ is exact, then all of
the above are unbiased estimates for the advantage function. In practice, this
will not be the case, since we are not given the value function.

The *tradeoff* here is that the estimators $$\hat{A}_t^{(k)}$$ with small $$k$$
have **low variance but high bias**, whereas those with large $$k$$ have **low
bias but high variance**. Why? I think of it based on the number of terms. With
small $$k$$, we have fewer terms to sum over (which means low variance).
However, the bias is relatively large because it does not make use of extra
"exact" information with $$r_K$$ for $$K > k$$. Here's another way to think of
it as emphasized in the paper: $$V(s_t)$$ is constant among the estimator class,
so it does not affect the relative bias or variance among the estimators:
differences arise entirely due to the $$k$$-step returns.

One might wonder how to make use of the $$k$$-step returns in practice. The key
to doing so is to let the agent run for $$k$$ steps, and then update the return
afterwards. In normal Q-learning, for instance, we can update the return
"immediately" with the current reward, but that's only due to the specific
nature of the Q-learning update. With longer returns, we have to keep the
Q-values fixed until the agent has explored more. This is emphasized in the A3C
paper from DeepMind.


# The Generalized Advantage Estimator

It might not be so clear which of these estimators above is the most useful. How
can we compute the bias and variance?

It turns out that it's better to use *all* of the estimators, in a clever way.
First, define $$\delta_t^V = r_t + \gamma V(s_{t+1}) - V(s_t)$$. Now, here's how
the **Generalized Advantage Estimator** $$\hat{A}_t^{GAE(\gamma,\lambda)}$$ is
defined:

$$
\begin{align}
\hat{A}_t^{GAE(\gamma,\lambda)} &= (1-\lambda)\Big(\hat{A}_{t}^{(1)} + \lambda \hat{A}_{t}^{(2)} + \lambda^2 \hat{A}_{t}^{(3)} + \cdots \Big) \\
&= (1-\lambda)\Big(\delta_t^V + \lambda(\delta_t^V + \gamma \delta_{t+1}^V) + \lambda^2(\delta_t^V + \gamma \delta_{t+1}^V + \gamma^2 \delta_{t+2}^V)+ \cdots \Big)  \\
&= (1-\lambda)\Big( \delta_t^V(1+\lambda+\lambda^2+\cdots) + \gamma\delta_{t+1}^V(\lambda+\lambda^2+\cdots) + \cdots \Big) \\
&= (1-\lambda)\left(\delta_t^V \frac{1}{1-\lambda} + \gamma \delta_{t+1}^V\frac{\lambda}{1-\lambda} + \cdots\right) \\
&= \sum_{l=0}^\infty (\gamma \lambda)^l \delta_{t+l}^{V}
\end{align}
$$

To derive this, one simply expands the definitions and uses the geometric series
formula. The result is interesting to interpret: the (weighted) sum of *Bellman
residual terms*.

The above describes the estimator $$GAE(\gamma, \lambda)$$ for $$\lambda \in
[0,1]$$ where adjusting $$\lambda$$ adjusts the bias-variance tradeoff. We
usually have $${\rm Var}(GAE(\gamma, 1)) > {\rm Var}(GAE(\gamma, 0))$$ due to
the number of terms in the summation (more terms usually means higher variance),
but the bias relationship is reversed. The other parameter, $$\gamma$$, *also*
adjusts the bias-variance tradeoff ... but for the GAE analysis it seems like
the $$\lambda$$ part is more important.

To make a long story short, we can put the GAE in the policy gradient estimate
and we've got our (biased) gradient estimate. Will this work well in practice?


# Value Function Estimation

In order to be able to *use* the GAE in our policy gradient algorithm (again,
this means computing gradients and shifting the weights of the policy to
maximize an objective), we need some value function $$V_\phi$$ parameterized by
a neural network. Again, this is part of the **actor-critic** framework, where
the "critic" provides the value function estimate. 

Let $$\hat{V}_t = \sum_{l=0}^\infty \gamma^l r_{t+l}$$ be the discounted sum of
rewards. The authors propose the following optimization procedure to find the
best weights $$\phi$$:

$$
{\rm minimize}_\phi \quad \sum_{n=1}^N\|V_\phi(s_n) - \hat{V}_n\|_2^2
$$

$$
\mbox{subject to} \quad \frac{1}{N}\sum_{n=1}^N\frac{\|V_\phi(s_n) -
\hat{V}_{\phi_{\rm old}}(s_n)\|_2^2}{2\sigma^2} \le \epsilon
$$

where each iteration, $$\phi_{\rm old}$$ is the parameter vector before the
update, and 

$$\sigma^2 = \frac{1}{N}\sum_{n=1}^N\|V_{\phi_{\rm old}}(s_n)-\hat{V}_n\|_2^2$$

This is a *constrained optimization* problem to find the best weights for the
value function. The constraint reminds me of Trust Region Policy Optimization,
because it limits the amount that $$\phi$$ can change from one update to
another. The advantages with a "trust region" method are that the weights don't
change too much and that they don't overfit to the current batch. (Updates are
done in *batch* mode, which is standard nowadays.)

- **Note I**: unfortunately, the authors don't use this optimization procedure
  exactly. They use a *conjugate gradient* method to approximate it. But think
  of the optimization procedure here since it's easier to understand and is
  "ideal."

- **Note II**: remember that this is *not* the update to the policy
  $$\pi_\theta$$. That update requires an entirely separate optimization
  procedure. Don't get confused between the two. Both the policy and the value
  functions can be implemented as neural networks, and in fact, that's what the
  authors do. They actually have the same architecture, with the exception of
  the output layer since the value only needs a scalar, whereas the policy needs
  a higher-dimensional output vector.


# Concluding Thoughts

I didn't understand the implications of this paper when I read it for the first
time (maybe more than a year ago!) but it's becoming clearer now. They present
and analyze a specific kind of estimator, the GAE, which has a bias-variance
"knob" with the $$\lambda$$ (and $$\gamma$$, technically). By adjusting the
knob, it might be possible to get low variance, low biased estimates, which
would drastically improve the sample efficiency of policy gradient methods. They
also present a way to estimate the value method using a trust region method.
With these components, they are able to achieve high performance on challenging
reinforcement learning tasks with continuous control.


[1]:https://danieltakeshi.github.io/2017/03/28/going-deeper-into-reinforcement-learning-fundamentals-of-policy-gradients/
[2]:https://arxiv.org/abs/1506.02438
