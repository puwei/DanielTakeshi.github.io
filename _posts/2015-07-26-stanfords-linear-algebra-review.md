---
layout: post
title:  "Stanford's Linear Algebra Review"
date:   2015-07-26 23:00:00
permalink: stanfords-linear-algebra-review
---

I'll take a break from the recent discussion on graphical models to go over some old linear algebra
concepts. While there are many references on linear algebra designed to help a student re-learn what
he or she may have forgotten, I found the [handout from Stanford's CS 229 (Machine Learning)
class](http://cs229.stanford.edu/section/cs229-linalg.pdf) to be one of the best when considering
the content, size, and clarity together. And despite being advertised as a review, it actually *did*
teach me a lot. In college, I only took one linear algebra class, a basic introductory and proofs-based
course[^williams].  While I found it difficult when I was taking it, in retrospect, we did not go
over that much material. Two things that really tricked me up when I first arrived in Berkeley were

* Positive Definite Matrices (and related to that, Singular Value Decomposition)
* Matrix Calculus (with gradients, Hessians, etc.)

These two concepts are used all the time in AI, and I really wish I could know them better. Thus, in
this post, I'll quickly go over some of the basic review concepts of linear algebra as presented in
the Stanford handout, and then spend a little more time on those previously mentioned topics.

## Basic Concepts and Matrix Multiplication

A few years ago, I kept getting confused between column and row vectors when I was reading machine
learning literature, but now I know that all vectors are assumed to be *columns* by default. Also,
when denoting row vectors, be careful that the transpose sign does not necessarily mean we are
taking the corresponding column and then transposing it (as the notes say, the definitions of
$$a_1$$ and $$a_1^T$$ are ambiguous).

Matrix multiplication is at the heart of linear algebra and what we do in AI. I find it easiest to
reason about matrix multiplication by always checking the number of rows and columns of the matrices
involved, and making sure they align correctly. But this handout made it easier for me to think of
other ways to view how multiplication works. They describe four interesting ways of looking at
matrix multiplication, of which the most interesting to me is when the product $$AB$$ is expressed
as the *sum* of *outer* products (between vectors).

## Operations and Properties

Some interesting operations and properties of matrices:

* Any square matrix $$A \in \mathbb{R}^{n\times n}$$ can be represented as a sum of a symmetric
  matrix and an anti-symmetric matrix, since $$A = .5 (A + A^T) + .5 (A - A^T)$$.

* The **trace** is the sum of the diagonal elements of a matrix. Despite its seeming simplicity, the
  trace operator will actually be very useful in matrix calculus (the "trace trick") and in the
  study of eigenvalues and eigenvectors, since the sum of the eigenvalues of a matrix equals the
  trace, even though the individual components being summed up generally have no relation.

* The **norm** of a vector $$\|x\|$$ is like an informal measure of the distance. For some reason,
  these kept confusing me when I was trying to work on my undergraduate thesis, so it's nice to see
  it formally treated here. There are several properties of norms, but in general, I tend to view
  norms of vectors as just the $$\ell_p$$ norm. Also, when working with norms, make sure I know the
  Cauchy-Schwarz inequality: $$|x \cdot y | \le \|x\| \|y\|$$.

* The **rank** of a matrix is equal to the number of its linearly independent columns (or rows).
  There are many implications of the rank; for me, the one I remember the best is that in order for
  an inverse to exist, a (square) matrix has to be *full rank*. If we generated a square matrix by
  filling in its values from a random number generator, then it will almost always have full rank.

* A square matrix $$U$$ is  **orthogonal** if $$U^TU = I$$. This requires the columns of $$U$$ to be
  **orthonormal**[^terminology]. A nice property: $$\|Ux\|_2 = \|x\|_2$$, which we can prove by
  squaring them, thus considering $$(Ux)^T(Ux)$$ and $$x^Tx$$.

* The **range**, i.e., column space, of a matrix $$A \in \mathbb{R}^{m \times n}$$ is
  $$\mathcal{R}(A) = \{v \in \mathbb{R}^m \: : \: v = Ax, x \in \mathbb{R}^n \}$$. The **null
  space** is $$\mathcal{N}(A) = \{x \in \mathbb{R}^n \: : \: Ax = 0\}$$[^right]. Vectors in the
  former set have length $$m$$, those in the latter have length $$n$$, and we can get the complement
  of each of those sets by considering $$\mathcal{R}(A^T)$$ and $$\mathcal{N}(A^T)$$. For instance,
  considering the sets $$\mathcal{R}(A^T)$$ and $$\mathcal{N}(A)$$, it turns out that the
  intersection of those two sets is empty, and that *every* vector in $$\mathbb{R}^n$$ can be
  expressed as the sum of two vectors, one in each of those two sets. Thus, they are *orthogonal
  complements*. The two column spaces, combined with the two column spaces (using $$A$$ and $$A^T$$)
  form the **four fundamental subspaces**, a term popularized by Gilbert Strang. I'm not sure I
  really *get* it, though.

* The **determinant** of a square matrix $$A$$, denoted as $$det A$$ or $$|A|$$, is a mysterious
  function that maps $$A$$ to the real numbers. The three main properties it satisfies are:

  - that the identity has determinant one
  - that if we multiply a single row in $$A$$ by a scalar $$t$$, the determinant of the new matrix
    is $$t|A|$$
  - that if we exchange any two (different) rows, then the determinant of the new matrix is
    $$-|A|$$ 

  All the other properties of determinants follow from this, including the cofactor expansion, which
  I will not list here. Determinants have an intuitive interpretation in terms of volume: if we take
  the span of the rows of $$A$$, and restrict all the coefficients to be in $$[0,1]$$, then the
  determinant is the volume of this set. Also, determinants are useful for checking if $$A^{-1}$$
  exists. Finally, the **adjoint** of a matrix, $${\rm adj}(A)$$, is $$A^{-1} = {\rm adj}(A) / |A|$$.

* Given a square, *symmetric* matrix $$A$$, a **quadratic form** is a function $$f(x) = x^TAx =
  \sum_{i=1}^n \sum_{j=1}^n A_{ij}x_ix_j$$ mapping $$A$$ and $$x$$ to the reals. Our variables are
  $$x$$, so even if the dimensions of $$A$$ are large, the highest power of any $$x_i$$ (i.e., a
  component of $$x$$) that can exist in $$f(x)$$ is two, hence the intuitive name.

  Something that is related is the concept of a **positive semidefinite** matrix, which is a
  *symmetric* matrix such that $$x^TAx \ge 0$$ for all $$x$$. We can also define the obvious
  analogues for *definite*, *negative definite*, etc., matrices. Given any, not necessarily square
  matrix $$A$$, the matrix $$A^TA$$ is always positive semidefinite; prove this by using
  $$\|Ax\|_2^2$$.

  Note: quadratic forms like these are the start of an introduction to what *really* happens in
  machine learning and AI, where we have to understand matrix representations.

* For determining eigenvalues and their corresponding eigenvectors (note: eigenvectors are not
  unique), refer to $${\rm det}(A - \lambda I) = 0$$ if we are going to be solving them by hand.

  We tend to use $$\Lambda$$ (capital lambda) to represent the matrix of eigenvalues, so the matrix
  equation will result in $$AS = S\Lambda$$, implying that $$A = S\Lambda S^{-1}$$, hence $$A$$ is
  *diagonalizable*.

  Some interesting properties: the trace and determinant are the sum and product, respectively, of
  the eigenvalues. The eigenvalues of a triangular matrix are just the elements on the diagonal. If
  $$A$$ is nonsingular, then $$1/\lambda_i$$ is an eigenvalue of $$A^{-1}$$ with eigenvector
  $$x_i$$.

  If we have a symmetric matrix $$A$$, then (1) all eigenvalues are real, and (2) its eigenvectors
  can be scaled to be orthogonal to each other, so that $$S$$ above can turn orthogonal, and hence
  we have $$S^{-1} = S^T$$, a good thing because transposes are easier computationally than
  inverses. Unfortunately, I don't currently know how to prove these off the top of my head.

## Singular Value Decomposition

With a symmetric matrix $$A$$, we can set $$A = U\Lambda U^T$$ instead of using $$U^{-1}$$. It turns
out we can generalize this to *arbitrary* (not even square!) matrices $$A$$ by expressing them in
singular value decomposition form, $$A = U\Sigma V^T$$. The $$U$$ and $$V$$ matrices are square and
*orthogonal*, and represent *eigenvectors* of $$AA^T$$ and $$A^TA$$, respectively.

The $$\Sigma$$ matrix is diagonal, *possibly non-square*, and contains something called the
**singular values** (not the eigenvalues!) of matrix $$A$$. They fill the first $$r$$ diagonal
elements for a rank $$r$$ matrix $$A$$, and the rest of the elements are zero. The singular values
are the *square roots* of the nonzero eigenvalues of both $$AA^T$$ and $$A^TA$$ (which are
symmetric, so they have real eigenvalues).

For a positive definite matrix, $$U = V$$.

There are many applications of SVD, and the ones I'm familiar with happen to be in computer vision.
Some of these applications have to do with the fact that $$U$$ and $$V$$ give orthonormal bases for
all four fundamental subspaces. For instance, to use SVD to compute the null space of $$A$$, then
look at the last $$n-r$$ columns of $$V$$.

## Matrix Calculus

I really wish I had completely digested this section before taking CS 281A here because I had no
idea how matrix calculus worked until I reviewed this document. Given a function $$f : \mathbb{R}^{m
\times n} \to \mathbb{R}$$, the gradient of $$f$$ with respect to $$A$$ is a *matrix* (i.e., it's
the same size as the original matrix input to $$f$$) of partial derivatives of $$f(A)$$.

The **Hessian** is the second derivative analogue to the gradient (well, almost). Here, we assume we
are taking the Hessian with respect to a function $$f : \mathbb{R}^n \to \mathbb{R}$$, where we take
a vector as input (not a general matrix, even though that's possible).

## The Trace Trick

Here's a neat trick I learned from reading Mike Jordan's notes. Since the trace is such that
$$tr[ABC]$$ is the same no matter what the ordering of the three matrices, and since
$$\frac{\partial}{ \partial A} tr[AB] = B^T$$ (verify this by explicit computation) then we can
claim:

$$
\begin{align}
\frac{\partial}{\partial A} x^TAx &= \frac{\partial}{\partial A} tr[x^TAx] \\
&= \frac{\partial}{\partial A} tr[xx^TA] \\
&= \frac{\partial}{\partial A} [xx^T]^T = xx^T
\end{align}
$$

Intuitively, this makes sense since we just eliminated $$A$$. In the past, when I tried computing
derivatives like these, I would convert the entire expression to an enormous set of summations, and
try to reason element by element. That is way too much work.

There is a related trick involving determinants: the derivative of $$\log |A|$$ with respect to
$$A$$ is $$A^{-T}$$.

One can use these tactics to take the MLE of the covariance matrix $$\Sigma$$ of a multivariate
Gaussian distribution, since the log likelihood of that term has $$\log |\Sigma|$$ and
$$(x_n-\mu)^T\Sigma^{-1}(x_n-\mu)$$ in it.

***

[^williams]: When I took the course (with Professor Elizabeth Beazley), it was called MATH 211.
    Now it's called MATH 250 since the department put the core courses in the "50"s with their
    much-improved numbering system.

[^terminology]: Watch out with the terminology! Some people might call such matrices $$U$$ as
    *orthonormal* matrices, but I call them *orthogonal*.

[^right]: This is technically called the *right* null space, or the *kernel*, since we may wish to
    refer to the *left* null space, which uses $$A^Tx = 0 \Rightarrow x^TA = 0$$.

