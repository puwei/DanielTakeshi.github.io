---
layout: post
title:  "Following Professor Michael I. Jordan's Advice: \"Your Brain Needs Exercise\""
date:   2017-04-22 20:00:00
permalink: 2017/04/22/following-professor-michael-jordans-advice-your-brain-needs-exercise
---

The lone class I am taking this semester is STAT 210B, the second course in the
PhD-level theoretical statistics sequence. I took STAT 210A last semester, and I
briefly [wrote about the class here][2]. I'll have more to say about STAT 210B
in late May, but in this post I'd first like to present an interesting problem
that our professor, [Michael I. Jordan][1], brought up in lecture a few weeks
ago.

The problem Professor Jordan discussed was actually an old homework question,
but he said that it was so important for us to know this that he was going to
prove it in lecture anyway, *without* using any notes whatsoever. He also
stated:

> "Your brain needs exercise."

He then went ahead and successfully proved it, and urged us to do the same
thing.

OK, if he says to do that, then I will follow his advice and write out my answer
in this blog post. I'm probably the only student in class who's going to be
doing this, but I'm already a bit unusual in having a long-running blog. If any
of my classmates are reading this and have their own blogs, let me know!

By the way, for all the students out there who say that they don't have time to
maintain personal blogs, why not take baby steps and start writing about stuff
that accomplishes your educational objectives, such as doing practice exercises?
It's a nice way to make yourself look more productive than you actually are,
since you would be doing those anyway.

Anyway, here at last is the question Professor Jordan talked about:

> Let $$\{X_i\}_{i=1}^n$$ be a sequence of zero-mean random variables, each
> sub-Gaussian with parameter $$\sigma$$ (No independence assumptions are
> needed). Prove that 
>
> $$\mathbb{E}\Big[\max_{i=1,\ldots,n}X_i\Big] \le \sqrt{2\sigma^2 \log n}$$ 
>
> for all $$n\ge 1$$.

This problem is certainly on the easier side of the homework questions we've
had, but it's a good baseline and I'd like to showcase the solution here. Like
Professor Jordan, I will do this problem (a.k.a. write this blog post) without
any form of notes. Here goes: for $$\lambda \in \mathbb{R}$$, we have

$$
\begin{align}
e^{\lambda \mathbb{E}[\max\{X_1, \ldots, X_n\}]} \;&{\overset{(i)}{\le}}\;\mathbb{E}[e^{\lambda \max\{X_1,\ldots,X_n\}}] \\
\;&{\overset{(ii)}{\le}}\; \max\left\{\mathbb{E}[e^{\lambda X_1}],\ldots,\mathbb{E}[e^{\lambda X_n}]\right\} \\
\;&{\overset{(iii)}{\le}}\; \sum_{i=1}^n\mathbb{E}[e^{\lambda X_i}] \\
\;&{\overset{(iv)}{\le}}\; ne^{\frac{\lambda^2\sigma^2}{2}}
\end{align}
$$

where:

- **Step (i)** follows from Jensen's inequality. Yeah, that inequality is
  *everywhere*.
- **Step (ii)** follows from noting that the term inside the expectation is
  just picking out the maximal exponential term. One can also analyze by cases
  with $$\lambda < 0$$ and $$\lambda > 0$$.
- **Step (iii)** follows from the classic union bound, which can be pretty bad
  but we don't have much else to go on here. The key fact is that the
  exponential makes all terms in the sum positive.
- **Step (iv)** follows from applying the sub-Gaussian bound to all $$n$$
  variables, and then summing them together.

Next, taking logs and rearranging, we have

$$
\mathbb{E}\Big[\max\{X_1, \ldots, X_n\}\Big] \le \frac{\log n}{\lambda} + \frac{\lambda\sigma^2}{2}
$$

Since $$\lambda \in \mathbb{R}$$ is isolated on the right hand side, we can
differentiate it to find the *tightest* lower bound. Doing so, we get
$$\lambda^* = \frac{\sqrt{2 \log n}}{\sigma}$$. Plugging this back in, we get

$$
\begin{align}
\mathbb{E}\Big[\max\{X_1, \ldots, X_n\}\Big] &\le \frac{\log n}{\lambda} + \frac{\lambda\sigma^2}{2} \\
&\le \frac{\sigma \log n}{\sqrt{2 \log n}} + \frac{\sigma^2\sqrt{2 \log n}}{2 \sigma} \\
&\le \frac{\sqrt{2 \sigma^2 \log n}}{2} + \frac{\sqrt{2 \sigma^2 \log n}}{2}  \\
\end{align}
$$

which proves the desired claim.

I have to reiterate that this problem is easier than the others we've done in
STAT 210B, and I'm sure that over 90 percent of the students in the class could
do this just as easily as I could. But this problem makes clear the *techniques*
that are often used in theoretical statistics nowadays, so at minimum students
should have a firm grasp of the content in this blog post.


[1]:https://people.eecs.berkeley.edu/~jordan/
[2]:https://danieltakeshi.github.io/2016/12/20/review-of-theoretical-statistics-stat-210a-at-berkeley/
