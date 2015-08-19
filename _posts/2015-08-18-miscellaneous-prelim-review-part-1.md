---
layout: post
title:  "Miscellaneous Prelim Review (Part 1)"
date:   2015-08-18 12:0:00
permalink: miscellaneous-prelim-review-part-1
---

Here is a random assortment of notes I created to wrap up some of the remaining material I need to
know. It's "part 1" because I have another part coming up later.

## Information Theory 

This part, Chapter 2 from Cover and Thomas, is a bunch of definitions and straightforward theorems
(i.e., those that *follow directly* from definitions):

- **Entropy**: $$E(X) = -\sum_{x} p(x)\log_2 p(x) = -\mathbb{E}[\log_2 p(X)]$$, where $$x$$ is a
  *realization* of variable $$X$$.  It's the amount of uncertainty inherent in a random variable.
  For a fixed variable $$X$$ with some probability distribution that we can create, the entropy is
  highest if we make the distribution relatively uniform, and lowest if we make it "peaked." In the
  extreme case, if we set $$Pr(X = 0) = 1$$, then $$E(X) = 0$$.

- **Mutual Information**: $$I(X;Y) = E(X) - E(X|Y)$$. It's the *decrease* in entropy (upon obtaining
  the value of $$Y$$), for variable $$X$$. Note that $$I(X;X) = E(X)$$ since the second term will be
  zero. Alternatively, we represent it as

  $$I(X;Y) = \sum_x \sum_y p(x,y) \log_2 \left(\frac{p(x,y)}{p(x)p(y)}\right)$$

  Note that $$I(X;Y) = I(Y;X)$$, so it *does* commute.

- **Relative Entropy (KL-divergence)**: $$D(p || q) = \sum_{x} p(x)\ln \left( \frac{p(x)}{q(x)}
  \right)$$. This is a *non-symmetric* measure of the difference between distributions $$p$$ and
  $$q$$. We can also interpret it as the number of *additional bits* we will need to represent $$p$$
  if we are using the (inferior) approximation of $$q$$. It is infinity if there exists an $$x$$
  such that $$p(x) > 0$$ but $$q(x) = 0$$.

All three of the above quantities are non-negative.

Another concept that plays a huge role in information theory is the following:

- **Jensen's inequality**: for a convex function $$f$$, $$f(\mathbb{E}[X]) \le \mathbb{E}[f(X)]$$.
  For a *concave* function, like the logarithm, we flip the sign (actually for logs, we can drop the
  equality case). I find it easiest to remember this rule by expanding out the equations for binary
  random variables. Let's say they taken on values 0 and 1 with probability a half each. Then we
  have $$f(\mathbb{E}[X]) = f(.5 \times 0 + .5 \times 1)$$ and $$\mathbb{E}[f(X)] = .5 \times f(0) +
  .5 \times f(1)$$ and can directly relate this to the definition of convexity.

Based on the previous discussion, we can define and infer things like:

- Joint entropy $$H(X,Y) = - \sum_x \sum_y p(x,y) \log_2 p(x,y) = H(X) + H(Y\mid X)$$.

- Conditional entropy, conditional KL divergence, conditional mutual information. For the sake of
  simplicity, I will not write all the rules here, but here is the one for conditional entropy:
  $$H(Y\mid X) = -\sum_x p(x) H(Y \mid X=x) = -\mathbb{E}_p [\log_2 p(Y\mid X)]$$. Note that
  $$H(Y\mid X) \ne H(X\mid Y)$$.

- The chain rule for entropy, relative entropy, and mutual information. Unlike normal probability,
  these *sum* the components rather than multiply, which makes sense because all three cases involve
  logarithms. Again, I won't write all the rules here, but will note that entropy is the easiest to
  relate to probability because we *literally* copy formulas from probability, but use sums instead
  of products. For the chain rule with mutual information, just pretend we don't have $$Y$$ and
  follow the probability convention (but sum up). Then stick the $$Y$$'s after the *semicolon*, but
  before the *conditioning bar*. For KL-divergence, it's the same (split up the joint into a marginal
  and product, but do this for *both* distributions, then use two "D" terms.

- A theorem: $$H(X) \le \log_2|\mathcal{X}|$$, where $$\mathcal{X}$$ represents the range of
  variable $$X$$, and equality here holds if and only if $$X$$ is a uniform random variable.

- Also one thing that tricked me up the first time I saw it was this consequence of Jensen's
  inequality:

  $$\sum_{x \in A} p(x) \log\left( \frac{q(x)}{p(x)}\right) \le \log \left( \sum_{x \in A} p(x) \frac{q(x)}{p(x)} \right)$$

  where $$A$$ is the domain for $$p$$. I am assuming this really means
  
  $$\mathbb{E}_p\left[\log \left(\frac{q(x)}{p(x)}\right)\right] \le \log \left(
  \mathbb{E}_p\left[ \frac{q(x)}{p(x)} \right] \right)$$

A final thought on this section: an alternative interpretation of entropy is that it is a *lower
bound* on the average number of bits required to represent the random variable. It's not "the
minimum number of bits" because random variables take on different values with different
probabilities, so we may wish to allocate more bits for the low probability events. And we also need
to make it clear *how* we encode, so that we can compare different encodings. Example 1.1.2 from
Cover and Thomas will clarify: here, we have eight horses, and they each win with some specified
probability. If we wanted to encode the random variable $$H$$ indicating the horse that won, we
could use three bits in the standard way. But this is suboptimal if the distribution is
$$(1/2,1/4,1/8,1/16,1/64,1/64,1/64,1/64)$$, like it is in the example, because we should allocate
*fewer* digits to the higher probability horses, and *more* towards the ones that are less likely to
win. It's possible to encode $$H$$ so that the average number of bits to represent it is two, which
exactly matches the entropy.

## Decision Trees

Decision trees are one of the simplest nontrivial classifiers[^legal] that have strong performance in
practical tasks. The hypothesis space is the set of trees. For each $$n$$-dimensional sample $$x$$,
we classify it by propagating $$x$$ down the tree. At each node, we test an attribute $$x_i$$, and
depending on that value, send the sample left or right. Once we send it down the tree far enough, it
will land in some "classifier" node that labels the class of that element.

Great, so how do we *train* such trees from labeled data $$\{(x^{(i)} =
(x_1,x_2,\ldots,x_n)^{(i)},y^{(i)})\}_{i=1}^n$$? For that, we invoke some information theory
criteria: we want to select the attribute to test that will result in the most amount of *purity* in
the resulting trees, where purity is defined based on entropy. Formally, at each point of the tree,
we have a set of data and a candidate set of attributes. We pick the attribute that maximizes the
*information gain* of the data.

Let's precisely define this for boolean decision trees. At a decision tree's node, we have $$p$$
positive and $$n$$ negative samples. The entropy of the random variable describing the output is the
entropy of a binary random variable with probability $$p/(p+n)$$; to simplify the subsequent
notation, denote this as $$B(p/(p+n))$$. We define the gain of attribute $$A_k$$ that splits the
data into $$d$$ subsets as follows:

$$Gain(A_k) = B\left(\frac{p}{p+n}\right) - \sum_{i=1}^d \left( \frac{p_k+n_k}{p+n}\right) B\left(\frac{p_k+n_k}{p+n}\right)$$

For each subset, we weigh its entropy probabilistically. Otherwise, you could think of a useless
attribute that keeps the same proportion of positive and negative examples in each subset. Without
the probability weighting, splitting on $$A_k$$ would *increase* the entropy of the goal test on the
data.

There are other impurity measures, such as the Gini impurity measure $$\sum_{k=1}^K
p(x_k)(1-p(x_k))$$ if the output takes on $$K$$ realizations. This is *not* the same as the measure
of income inequality! I think the "CART" category of decision trees uses the Gini measure, whereas
the "C4.5" and "C5" trees use entropy to measure impurity, though I think the boundaries between
those categories is a bit blurry. Misclassification error is not an appropriate measure because it
-- unlike Gini impurity and entropy -- does not give higher weight to branches with purer solutions.

Here are some things to think about:

- Trees can overfit, so what happens in most realistic algorithms is that we build the large tree
  first, *then* prune away nodes *with only leaf descendants* that do not contribute much to the
  information gain (e.g., using tests of statistical significance to see if the gain is significant
  enough). This is *not* the same as building a tree and deciding to prune away early. The classic
  example is the XOR data.  If we have a lot of XOR data that we want to split, we will find that
  the information gain of both attributes is *zero*. We do *not* want to prune away early because
  the next step will involve splitting on the second part of the XOR, which splits the data
  perfectly.

- In practice, information gain might not be a good value of the amount of information in an
  attribute, because there might be an attribute that maps each element to a unique value.

- We may have missing data. A simple but bad strategy is to ignore all training data points that
  have missing data. An alternative is to "fill in" those values probabilistically based on the
  distribution of values of those variables in the other samples considered for a particular
  decision tree.

- We may want to use decision trees for *regression* if the output is continuous-valued.  One option
  is to use a decision tree normally up to a certain depth, and then after that, we fit (linear)
  regression on only those data points that manage to reach that particular leaf node, and only the
  subset of variable attributes yet to be tested.
   
  How would we *train* such a regression tree? HTF suggest a greedy algorithm (which also assumes
  continuous *attributes*, by the way): at each node, find the attribute and a split point that
  minimizes the sum of squared errors of the two resulting regions. HTF *also* assume that once we
  get to a region, we will approximate the samples with just *one* value, rather than doing a
  full-blown regression on it, which makes the problem a lot easier since the sum of squared errors
  criterion means we pick the mean of the elements considered at that node. To avoid overfitting,
  they suggest *weakest link pruning*. We iteratively pick the *internal* (non-leaf) node that, upon
  its removal (and subsequent collapsing of the tree) results in the *smallest* increase in the sum
  of squared errors criterion. This is pretty cool, and it' similar to what Russell and Norvig
  describe.

Finally, here's a rather interesting connection between boolean decision trees and propositional
logic that I failed to realize at first: we can label various paths throughout the tree as
$$Path_i$$, and so the goal is expressed as:

$$Goal \iff (Path_1 \vee Path_2 \vee \cdots )$$

Thus, any function in propositional logic can be expressed as a decision tree!

## Nearest Neighbor

This classifier is easy to describe: for each test point, we look at the $$k$$ nearest points
according to Euclidean (or other) distance matrices and classify the test point as the majority
class among those $$k$$. This is a problem in high dimensions, since the notion of "distance" as a
measure of similarity becomes less reliable due to a combination of (1) noisy and irrelevant
features, and (2) the rather intriguing fact that the higher we go in dimensions, the more likely it
is our points are farther away from each other. As we increase the dimension of the unit hypercube
with our fixed $$k$$-nearest neighbor classifier, we will need to traverse an extra amount for each
dimension to reach the $$k$$ nearest neighbors.

Let's now restrict our focus to the 1-nearest-neighbor case. On the surface, this might seem to be
unreliable, since we're only using one closest point and it might *overfit* the data (see examples
of plots showing 1-nearest neighbor versus 5-nearest neighbor). But a famous result called the
**Cover-Hart Theorem** provides a different story, saying that the asymptotic error rate of the
1-nearest neighbor classifier is never more than twice the error of the Bayes' classifier (according
to HTE), where the Bayes' classifier assigns $$\arg_y \max P(y\mid X=x)$$. While it sounds nice, it
assumes that new points have to exactly coincide with a point in the training data, which is true in
the limit, but not true in general.

Here's another interesting fact about nearest neighbors that I found surprising.  Researchers used
nearest neighbors to achieve the best performance (at that time) on the MNIST handwritten digit
recognition problem. The digits themselves are points in $$\mathbb{R}^{256}$$-space. A classifier
would have to work in high dimensional space and be invariant to rotations, scaling, etc. They way
they did this was by *defining manifolds* in $$\mathbb{R}^{256}$$-space. For instance, there is a
one-dimensional curve where points on that curve represent different rotated versions of the "3"
digit[^skeptical]. Then there can be another curve representing a different three. One idea is to
*take the Euclidean distance of the two closest points* $$p_1$$ and $$p_2$$ which lie on separate
curves. Unfortunately, this may result in heavily rotated images being equivalent (the classic
disaster: confusing a "6" with a "9"), so the ingenious solution is to use *tangent* lines. That's
the intuition: in reality, the "one-dimensional curves" would be *manifolds* taking into account
additional invariance factors.

Having motivated nearest neighbors, let's discuss some of its drawbacks. One problem is that it
needs to store *all* the training instances, and for each new test point to classify, it needs to
*iterate* through all of those to find the $$k$$ closest neighbors. If $$O(n^2)$$ time is
unacceptable, then we can speed up the process of finding nearest neighbors with the following two
strategies:
 
* We can use $$k$$**-d trees**, or more accurately, $$n$$-d trees if our data is $$n$$-dimensional,
  so that we don't confuse this with the $$k$$ in the $$k$$-nearest neighbors. At each node, this
  tree will pick a dimension $$i$$ and split the examples according to their median point so that
  all $$x_i$$ such that $$x_i < m$$ will go the *left* sub-tree, and the rest go to the right
  subtree. The dimensions are typically chosen based on the widest spread of values.
  
  Thus, if we are doing 1-nearest neighbor, for a given new point $$x$$, we find its nearest
  neighbor by querying the $$k$$-d tree to see where it would be located (i.e., it's like we are
  inserting it in the tree). We proceed until we hit a leaf, and declare that as the best node found
  *given the current information*. But we have to be careful.  The nearest neighbor of $$x$$ might
  not be in the same hyperplane after a split! We need to "backtrack" and then measure the distance
  between $$x$$ and the hyperplanes at each step, to see if there are nearest neighbor candidates on
  the *other* side.  Check the [Wikipedia page](https://en.wikipedia.org/wiki/K-d_tree) for more
  details. They have a nice description and an animation.

  The downside with $$k$$-d trees is that with many dimensions, we will need to keep track of
  numerous subtrees that could potentially have "that nearest neighbor," and we would iterate
  through the entire tree. To extend this algorithm for multiple neighbors, we use a *list* of
  nearest neighbor points.

* We can use **locality sensitive hashing**, which hashes "similar" values in high dimensional
  spaces to the same hash buckets. *Then*, using *only* the elements remaining in that bucket, we
  can perform exact nearest neighbor via brute force comparisons. Since hash functions are hard to
  create, we can try $$M$$ hash functions independently to get $$M$$ buckets, then take the union of
  all those elements to arrive at the set which we will use for exact comparisons. Russell and
  Norvig seem to suggest that each of those $$M$$ hash functions be a projection down to a line, and
  the buckets would be a line segment. I guess that makes sense.

  The downside with locality sensitive hashing is that it, unlike the use of $$k$$-d trees, is an
  *approximate* nearest neighbors search.

Nearest neighbors has an interesting tradeoff with perceptrons. Kernelized perceptrons learn similar
to the way nearest neighbors learn, especially with Gaussian kernels that weigh a probability
distribution about each point. In other words, distance-weighted nearest neighbors *are* kernelized
perceptrons. Nearest neighbors, unlike plain (non-kernelized) perceptrons, can use fancy similarity
functions, as exemplified by the handwritten digit recognition example.

HTE also emphasize the connection between nearest neighbors and least squares.


## (Artificial) Neural Networks

Neural networks are a natural extension of the perceptron that I've written about in detail before,
since perceptrons form the basic building blocks for each node. Like the perceptron (and regression,
for that matter), we develop a classifier by updating weights. For neural networks, we use
**backpropagation** to update the weights. At a high level, this means for each training instance,
we "feed" it to the network so that it classifies it. Then, we propagate the "error" *backwards*
through the network to update weights. The weight update for those connecting to the *output* layer
is the same for that of logistic regression[^derivative], assuming we're using the sigmoid nonlinear
function. The real challenge comes when we compute weight updates for those connecting input or
hidden layers to other hidden layers. But in fact, the gradient for the loss at inner nodes is the
same as the computation for the gradient at the output layer, except we apply the chain rule
multiple times. I'm not going to write the derivation here since it would take too much time; I just
did it by hand.

Neural networks have an intriguing fact: provided that there are sufficiently many nodes and layers,
they can represent *any continuous function* (of the input) with arbitrarily high accuracy. It needs
multiple layers with non-linear activation functions at each node. Otherwise, if a NN just has an
input layer directly connected to an output layer, it fails to learn even a simple XOR function.

There are many extensions to NNs. We could use recurrent NNs, convolutional NNs (popular for
computer vision now), etc. We can use thresholding functions other than sigmoids, such as ReLUs,
which avoid the "vanishing gradient" problem of sigmoids. Note that we focus on the problem of
learning from a *fixed structure*, i.e., like parameter estimation for a graphical model with the
nodes and edges fixed. Learning the *structure* is much more complicated.

## Principal Components Analysis

Principal Components Analysis (PCA) is a way of mapping high dimensional data into a reduced
dimensional space, where the reduction is a "best approximation" of the original data. Formally, if
$$x_i \in \mathbb{R}^n$$ but we really think they lie in $$\mathbb{R}^k$$ where $$k \ll n$$, then
there is probably a process such that $$x_i = \Lambda z_i + \mu_i$$ for $$z_i \in \mathbb{R}^k$$ but
$$\mu_i \in \mathbb{R}^n$$ is some noise added.

Obviously, there are many advantages to dimensionality reduction, so the question is *how* we do
this in a sound way. PCA will do this by iteratively "mapping" points to a line characterized by the
vector which *preserves as much variance* in the data, not including vectors already
chosen[^pca_clarification]. In other words, we'd like to project the data onto a subspace so that
the variance is maximized. To do this, PCA uses an eigendecomposition, which can make it expensive,
but it does not need Expectation-Maximization. (The dimensionality reduction technique that uses E-M
is called "factor analysis.")

It's easiest to derive PCA in the two dimensional case with $$N$$ data points
$$\{(x_1,x_2)^{i}\}_{i=1}^N$$ where the data have zero mean and each coordinate has unit variance.
In the first step, we solve for the (unit) direction vector $$u$$: 

$$\max_u \sum_{i=1}^N (u^Tx^{(i)})^2 = \max_u \|Xu\|_2^2 = \max_u u^T(X^TX)u$$

where $$X$$ is the matrix where each row is a training instance $$x^{(i)}$$. Note that $$X^TX =
\sum_{i=1}^N x^{(i)}(x^{(i)})^T$$, and also, if the data are centered, then it is the sample
covariance matrix.

In fact, this is a standard optimization problem, where we have a quadratic form $$z^TAz$$ that we
are maximizing w.r.t. $$z$$ subject to the fact that $$\|z\|_2 = 1$$. It is a well known fact that
this problem is solved by finding the $$u$$ that corresponds to the *eigenvector* of $$A = X^TX$$
that has the *largest eigenvalue*. After all, $$X^TX$$ is a symmetric matrix of reals, so its
eigenvectors can be chosen to be of unit norm *and* orthogonal to each other.

Given $$u_1$$, the best vector so far, we know that $$x_i = u_1 z_i + \mu_i$$ is our "process",
where $$z_i$$ is a scalar. Since $$u_1^Tu_1 = 1$$ it follows that to project all the $$x_i$$ points
down to the one dimensional space characterized by $$u$$, we do $$u_1^Tx_i$$.

But normally we need more dimensions than that. How do we find the "best" set of vectors
$$u_1,\ldots,u_k$$ for that? We take those eigenvectors that had the largest $$k$$ eigenvalues.
These form the principal components of the data, and are mutually uncorrelated. (I'm not actually
sure why this works -- intuitively it does, but I don't have a proof.) And when we need to project
our data, we remember our "process" and add the new eigenvectors as columns of a matrix $$U$$ so
that $$x_i = Uz_i + \mu_i$$, where $$z_i \in \mathbb{R}^k$$, and $$k$$ is the number of columns of
$$U$$. Again, $$U$$ is orthogonal so ignoring the noise (which is deliberate, since it's noise!) our
projection is $$U^Tx_i$$ for all $$x_i$$ points.

We can find those eigenvectors by diagonalization or SVD of $$X^TX$$. SVD would work since that's a
real, symmetric matrix, so the eigenvalues will be the same as the singular values, and we can thus
rank them easily.

There is an alternative way we can derive PCA, using the "process" I explained earlier. We can
define $$f(z_i) = Vz_i + \mu_i$$ and use that as our approximation of $$x_i$$. Thus, our objective
would be to find

$$\min_{V} \sum_{i=1}^N \|x_i - f(z_i) \|_2^2 = \min_{V} \sum_{i=1}^N \|x_i - V(V^Tx_i) \|_2^2$$

where I just put the $$(V^Tx_i)$$ to represent the lower dimensional approximation data. To find
$$U$$, we can again resort to SVD: $$X = UDV^T$$, where $$X$$ is again the matrix with rows as
training instances. Then the *columns* of $$V$$ form the vectors of the principal components. (Sorry
for the $$U$$ and $$V$$ confusing; Ng and HTE use different formulations.) Technically, we only take
the first $$K$$ columns from $$V$$ if we want a set of $$K$$ vectors for the projections, which I
find is neat (if we want more, just add more columns!). Since $$XV = UD$$, then $$UD$$ consists of
the *projected* points of $$x_i$$, one for each row (and $$UD$$ will usually have fewer columns than
the full number of components of the $$x_i$$s). There's a lot of matrix stuff going on here; draw
this on a piece of paper to understand better.

HTE present an example of PCA using the Procrustes Transformation, but I don't really understand how
PCA relates to it. I guess because both involve rotations and scaling of the data?

***

[^derivative]: Recall how we do a stochastic gradient update of a single weight $$w_j$$ in logistic
    regression. For a given training instance, $$(x,y)$$, where $$x$$ is $$N$$-dimensional and $$y$$
    is a scalar, we do

    $$\frac{\partial}{\partial w_i}(y-h_w(x))^2 = \frac{\partial}{\partial w_i}\left(y - \frac{1}{1 + e^{w^Tx}} \right)^2$$

    assuming we're using the $$L_2$$ loss function. Then we eventually get

    $$w_j \leftarrow w_j + \alpha (y-h_w(x))h_w(x)(1-h_w(x))x_i$$

    which uses the fact that the derivative of the logistic function is itself multiplied by the
    quantity "one minus itself."

[^skeptical]: Admittedly, I am skeptical of how they can claim that a one-dimensional curve
    represents various rotated aspects of a digit, but if you buy that argument, then everything
    else follows from that.

[^legal]: In fact, the ability to describe the classifier to lawyers means that companies can use
    these classifiers to "discriminate" without concern. What companies would have to do is explain
    the classifier and their rationale (e.g., if a person is in X category, we have to do Y due to
    previous data, etc.).

[^pca_clarification]: The easiest way to understand this is to look for figures that plot data along
    with vectors that indicate the PCA dimensions. Typically there will be two vectors chosen,
    incidating two "best directions" that capture the data.


