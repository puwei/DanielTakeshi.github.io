---
title: 'Independent Component Analysis &#8212; A Gentle Introduction'
author: Daniel Seita
layout: post
permalink: /?p=2192
geo_public:
  - 0
  - 0
categories:
  - Computer Science
tags:
  - algorithms
  - Andrew Ng
  - gradient
  - Independent Component Analysis
  - machine learning
  - stochastic gradient descent
---
In this post, I give a brief introduction to independent component analysis (ICA), a machine learning algorithm useful for a certain niche of problems. It is not as general as, say, regression, which means many introductory machine learning courses won&#8217;t have time to teach ICA. I first describe the rationale and problem formulation. Then I discuss a common algorithm to solve ICA, courtesy of Bell and Sejnowski.

***Motivation and Problem Formulation***

Here&#8217;s a quick technical overview: the purpose of ICA is to explain some desired non-Gaussian data by figuring out a linear combination of statistically independent components. So what does that *really* mean?

This means we have some random variable &#8212; or more commonly, a random *vector* &#8212; that we observe, and which comes from a combination of different data sources. Consider the canonical cocktail party problem. Here, we have a group of people conversing at some party. There are two microphones stationed in different locations of the party room, and at time indices $latex i = {1, 2, ldots }$, the microphones provide us with voice measurements $latex x\_1^{(i)}$ and $latex x\_2^{(i)}$, such as amplitudes.

For simplicity, suppose that throughout the entire party, only two people are actually speaking, and that their speech signals are *independent* of each other (this is crucial). At time index $latex i$, they speak with signals $latex s\_1^{(i)}$ and $latex s\_2^{(i)}$, respectively. But since the two people are in different locations of the room, the microphones each record signals from a *different combination* of the two people&#8217;s voices. The goal of ICA is, given the time series data from the microphones, to figure out the original speakers&#8217; speech signals. The combination is assumed to be *linear* in that

  * $latex x\_1^{(i)} = a\_{11}s\_1^{(i)} + a\_{12}s_2^{(i)}$
  * $latex x\_2^{(i)} = a\_{21}s\_1^{(i)} + a\_{22}s_2^{(i)}$

for unknown coefficients $latex a\_{11},a\_{12},a\_{21},a\_{22}$.

Here&#8217;s a graphical version, [from a well-known ICA paper][1]. The following image shows two (unrealistic) wavelength diagrams of two people&#8217;s voices:

[<img class="aligncenter size-large wp-image-2195" src="http://www.seitad.com/wp-content/uploads/2015/01/ica1.png?w=460" alt="ica1" width="460" height="186" />][2]The data that is observed from the two microphones is in the following image:

[<img class="aligncenter size-large wp-image-2196" src="http://www.seitad.com/wp-content/uploads/2015/01/ica2.png?w=460" alt="ica2" width="460" height="191" />][3]The goal is to recover the original people&#8217;s wavelengths (i.e., the two graphs in the first of the two images I posted) when we are only given the observed data (i.e., the two graphs from the second image). Intuitively, it seems like the first observed wavelength must have come from a microphone closer to the first person, because its shape more closely matches person 1&#8217;s wavelength. The opposite is true for the second microphone.

More generally, consider having $latex n$ microphones and $latex n$ independent speakers; the numerical equality of microphones and speakers is for simplicity. In matrix form, we can express the ICA problem as $latex x^{(i)} = As^{(i)}$ where $latex A$ is an *unknown, square, invertible* mixing matrix that does not depend on the time interval. Like the assumptions regarding $latex n$, the invertibility of $latex A$ is to make our problem simple to start. We also know that all $latex x^{(i)}$ and $latex s^{(i)}$ are $latex n$-dimensional *random* vectors. The goal is to recover the unseen sources $latex s^{(i)}$. To simplify the subsequent notation, I omit the $latex i$ notation, but keep in mind that it&#8217;s there.

How does the linear combination part I mentioned earlier relate to this problem formulation? When we express problems in $latex x = As$ form, that can be viewed as taking linear combinations of components of $latex s$ along with the appropriate row of $latex A$. For instance, the *first component* (remember, there are $latex n$ of them) of the vector $latex x$ is the dot product of the first row of $latex A$ and the full vector $latex s$. This is a linear combination of independent source signals $latex s\_1,s\_2,ldots,s\_n$ with coefficients $latex a\_{11},a\_{12}, ldots, a\_{1n}$ based on the first row of $latex A$.

Before moving on to an algorithm that can recover the sources, consider the following insights:

  1. What happens if we know $latex A$? Then multiply both sides of $latex x = As$ by $latex A^{-1}$ and we are done. Of course, the point is that we *don&#8217;t* know $latex A$. It is what computer scientists call a set of *latent* variables. In fact, one perspective of our problem is that we need to get the optimal $latex A^{-1}$ based on our data.
  2. The following ambiguities regarding $latex A$ will always hold: we cannot determine the variance of the components of $latex s$ (due to scalars canceling out in $latex A$) and we also cannot determine ordering of $latex s$ (due to permutation matrices). Fortunately, these two ambiguities are not problematic in practice.
  3. One additional assumption that ICA needs is that the independent source components $latex s\_1, s\_2, ldots, s_n$ are *not* Gaussian random variables. If they are, then the rotational symmetry of Gaussians means we cannot distinguish among the distributions when analyzing their combinations. This requirement is the same as ensuring that the $latex s$ vector is *not* multivariate Gaussian.

Surprisingly, as long as the source components are non-Gaussian, ICA will typically work well for a range of practical problems! Next, I&#8217;d like to discuss *how* we can &#8220;solve&#8221; ICA.

***The Bell and Sejnowski ICA Algorithm  
***

We describe a simple stochastic gradient descent algorithm to learn the parameter $latex A^{-1}$ of the model. To simplify notation, let $latex W = A^{-1}$ so that its rows can be denoted by $latex w_i^top$. Broadly, the goal is to figure out some way of determining the *log-likelihood *of the training data that depends on the parameter $latex W$, and then perform updates to iteratively improve our estimated $latex W$. This is how stochastic gradient descent typically works, and the normal case is to take logarithms to make numerical calculations easier to perform. Also, we will assume the data $latex x_i$ are zero-mean, which is fine because we can normally &#8220;shift&#8221; a distribution to center it at 0.

For ICA, suppose we have $latex m$ time stamps $latex i = {1, 2, ldots, m}$. The log-likelihood of the data is

$latex ell(W) = sum\_{i=1}^{m} left( log |W| + sum\_{j=1}^{n} log g'(w_j^top x^{(i)}) right)$,

where we note the following:

  1. $latex |W|$ is the determinant of $latex W$
  2. $latex g&#8217;$ is the *derivative* of the sigmoid function $latex g$ (*not *the sigmoid function itself!)

Let&#8217;s explain why this formula makes sense. It comes from taking logarithms of the density of $latex x^{(i)}$ at each time stamp. Note that $latex x = As$ so if we let $latex p$ denote the *density* function of $latex x^{(i)}$, then $latex p(x^{(i)}) = |W| prod\_{j=1}^{n} p\_j(w\_j^top x^{(i)})$, where $latex p\_j$ is the density of the individual source $latex j$. We can split the product this way due to the independence among the sources, and the $latex w_j$ terms are just (vector) constants so they can be separated as well. For a more detailed overview, see Andrew Ng&#8217;s lecture notes; in particular, we need the $latex |W|$ term due to the effect of linear transformations.

Unfortunately, we don&#8217;t know the density of the individual sources, so we approximate them with some &#8220;good&#8221; density and make them equal to each other. We can do this by taking the derivative of the sigmoid function:

[<img class="aligncenter size-large wp-image-2209" src="http://www.seitad.com/wp-content/uploads/2015/01/logistic-curve.png?w=460" alt="Logistic-curve" width="460" height="307" />][4]The reason why this works is that the sigmoid function satisfies the properties of a *cumulative distribution function*, and by differentiating such a function, we get a *probability density function*. And since it works well in practice (according to Andrew Ng), we might as well use it.

Great, so now that we have the log-likelihood equation, what is the stochastic gradient descent update rule? It is (remember that $latex g$ is the sigmoid function):

$latex W\_{t} = W\_{t-1} + alpha left( begin{bmatrix} 1-2g(w\_1^top x^{(i)}) \ 1-2g(w\_2^top x^{(i)}) \ vdots \ 1-2g(w\_n^top x^{(i)}) end{bmatrix} (x^{(i)})^top + ((W\_{t-1})^top)^{-1} right)$,

where $latex alpha$ is the standard learning rate parameter, and the $latex i$ that we pick for each iteration update varies (ideally sampling from the $latex m$ training data pieces uniformly). Notice that the term in the parentheses is a matrix: we&#8217;re taking an outer product and then adding another matrix. To get that update rule from the log-likelihood equation, we take the gradient $latex nabla_W ell(W)$, though I think we omit the first summation over $latex m$ terms. Matrix calculus can be tricky and one of the best sources I found for learning about this is (surprise) [another one of Andrew Ng&#8217;s lecture notes][5] (look near the end). It took a while for me to verify but it should work as long as the $latex m$ summation is omitted, i.e., we do this for a fixed $latex x^{(i)}$. To find the correct outer product vectors to use, it may help to use the sigmoid&#8217;s nice property that $latex g'(x) = g(x) (1-g(x))$. Lastly, don&#8217;t forget to take the logarithm into account when taking the derivatives. I can post my full gradient calculation later if there&#8217;s enough demand.

There are whole books written on how to decide when to stop iterating, so I won&#8217;t get into that. Once it converges, perform $latex s^{(i)} = Wx^{(i)}$ and we are done, assuming we just wanted the $latex s$ vectors at all times.

Well, that&#8217;s independent component analysis. Remember that this is just one way to solve related problems, and it&#8217;s probably on the easier side.

***References and Further Reading  
***

  1. [Independent Component Analysis: Algorithms and Applications][1]
  2. [Andrew Ng&#8217;s lecture notes][6]

Let me know if you found this article useful.

 [1]: http://www.cs.helsinki.fi/u/ahyvarin/papers/NN00new.pdf
 [2]: http://www.seitad.com/wp-content/uploads/2015/01/ica1.png
 [3]: http://www.seitad.com/wp-content/uploads/2015/01/ica2.png
 [4]: http://www.seitad.com/wp-content/uploads/2015/01/logistic-curve.png
 [5]: http://cs229.stanford.edu/section/cs229-linalg.pdf
 [6]: http://cs229.stanford.edu/notes/cs229-notes11.pdf