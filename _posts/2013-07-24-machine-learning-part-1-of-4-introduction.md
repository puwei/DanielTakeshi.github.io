---
title: 'Machine Learning (Part 1 of 4): Introduction'
author: Daniel Seita
layout: post
permalink: /2013/07/24/machine-learning-part-1-of-4-introduction/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - algorithms
  - decision stumps
  - machine learning
---
[<img class="aligncenter size-medium wp-image-1283" alt="Machine_Learning" src="http://seitad.files.wordpress.com/2013/07/machine_learning.jpg?w=300" width="300" height="199" />][1]

This summer, I&#8217;ve spent a good amount of time analyzing the content of my blog. By looking at
the composition of my computer science entries, I realized that I don&#8217;t talk about the subject
material in my *classes* a whole lot. Most of my posts in that category are related to programming,
research, and other areas. I do have four course-related posts thus far in a &#8220;theory of
computation&#8221; series, which you can access by looking at the recently-added [directory][2] of
blog entries, but other than that, there&#8217;s honestly not much.

I&#8217;m hoping to change that as the summer turns into fall. One way is to revive my theory of
computation series, which is motivated in part because I&#8217;m going to be a theory teaching
assistant this fall. Entries are currently being drafted behind the scenes.

And another way is to introduce a new series of posts relating to one of my favorite classes at
Williams, *machine learning*. This is also the subject area of my senior research thesis, so
I&#8217;ll definitely be committed to writing about the subject. This will be a four-post series,
with this one being the first.

This post will give an introduction the field and, along with the second post, will discuss the
variety of *learning algorithms* (I&#8217;ll explain what these are later) that are commonly studied
in machine learning. The third post will involve analyzing the advantages and disadvantages of the
learning algorithms and discuss scenarios where some may be preferable over others. The fourth and
final post will discuss some of my possible future research in the field.

<!--more-->

**Introduction to Machine Learning**

So what is machine learning anyway? First, let&#8217;s go over the corresponding Williams College
course description:

> Machine Learning is an area within Artificial Intelligence that has as its aim the development and
> analysis of algorithms that are meant to automatically improve a system&#8217;s performance.
> Automatic improvement might include: (1) learning to perform a new task; (2) learning to perform a
> task more efficiently or effectively; or (3) learning and organizing new facts that can be used by
> a system that relies upon such knowledge.

At the heart of machine learning, then, is dealing with the question of how to *learn from data.*
After all, our goal in this field is to figure out how to train a computer to adequately perform
some task, and those almost always involve some sort of data manipulation. Possibly the most
ubiquitous such &#8220;task&#8221; in machine learning is *classifying* *data*.* *The canonical
example of this is separating spam email from non-spam email. Somehow, someway, we must use our vast
repositories of spam and non-spam email to train an email client how to detect spam email with high
[precision and recall][3]. That way, we can be reasonably confident when deploying it in the real
world.

Needless to say, this is an important but inherently complicated task. Sure, there are some emails
that are *obviously* spam, such as ones that are filled with nothing but dangerous URLs and
non-English text. But what about those kinds of emails where someone&#8217;s writing to ask you
about money? Most would consider those as spam, but what if a relative was actually serious about
asking money, but without knowing it, wrote in a style that was similar to those guys from unknown
countries? (Perhaps the relative doesn&#8217;t use email much?) Furthermore, we can also run into
the problem of ambiguity. If there exist perplexing emails such that even knowledgeable human
readers can&#8217;t come with a consensus on spam vs non-spam, how can the computer figure out
something like this?

Fortunately, with email, we won&#8217;t usually have such confusion. Spam tends to be fairly
straightforward for the human eye to detect &#8212; but can the same be said for a computer? The key
is to take advantage of existing data that consists of *both *spam and non-spam emails. The more
recent the emails (to take into account possible changes over time) and the more diverse the emails
(to take into account the many different writing styles of people and spam engines) the better. We
can take a large subset of the data and &#8220;train&#8221; our email client. We assume that each
email will have a label stating whether it is &#8220;spam&#8221; or &#8220;not spam&#8221; (if we
relax this assumption, then things get harder &#8212; more on that later) and we must use some kind
of algorithm to teach the client to recognize the common characteristics of emails in both
categories. Then, we can take a &#8220;test&#8221; set, which might consist of all the remaining
data that we didn&#8217;t use for training, and see how well the email client performs.

The advantage with this approach is that, since we assumed the data are labeled, we can judge and
analyze the results, taking into account not just basic factors &#8212; such as percentage of emails
classified correctly &#8212; but also if there are any trends or patterns that might give us insight
as to when our learning algorithm works and doesn&#8217;t work. We can continue to modify our
learning algorithm and its parameters until we feel satisfied with its performance on the testing
set. Only then do we &#8220;deploy&#8221; it into the real world and watch it in action, where it
has to deal with unlabled email.

In fact, a good analogy of machine learning in the context of humans seems to be sports referees.
These people have to undergo a period of education and training before they can get tested on some
&#8220;practice&#8221; games. They will then get feedback before moving on to the more serious
competitions. Current NBA referees, for instance, might have been trained via this simple algorithm:
&#8220;Read Book W, Pass Written Exam X\_1 and Physical Exam X\_2, Referee Summer League Game Y, and
if performance is satisfactory, Referee Actual NBA Game Z.&#8221;

Hopefully this makes sense. As the previous example and general concepts imply, machine learning can
make an impact in many fields other than computer science. Statistics, psychology, biology,
chemistry, and many other areas have benefitted from machine learning tactics. In fact, such
learning algorithms are even used in fraud detection.

Now let&#8217;s move on to some more formal definitions.

**The Problem Setting**

We have a computer capable of performing *classification*, which is the process of assigning a given
category to each element in the data. The specific categories may or may not be known to the
learner, but in general, knowing the categories ahead of time makes for far easier machine
learning. A *learning algorithm* is something that can be used to help a machine (i.e. a computer)
better perform a task when given data. &#8220;Better perform&#8221; can obviously mean different
things depending on the circumstances or evaluation methodology used, but for the sake of
simplicity, let&#8217;s suppose we&#8217;re only focusing on *accuracy, *or *correctness*.

To carry out the machine learning and evaluate performance, we&#8217;ll need some data in the form
of *feature vectors,* which store the relevant attributes of our samples, and usually includes its
class label. For instance, with the email example earlier, the vector might include attributes such
as the number of characters present in the index zero, then the number of words present in index
one, and the email domain in index two, and so on. Attributes can be real-valued or categorical. One
element in the feature vector &#8212; possibly the last one &#8212; might be reserved for the true
classification of SPAM vs NON-SPAM. The machine will then use these feature vectors with a learning
algorithm to build a learning model.

There are multiple ways of performing this learning. Three common methods are *supervised learning,
unsupervised learning, *and *reinforcement learning. *Supervised learning involves the use of
labeled training data to build a clear model for output, while unsupervised learning has unlabeled
training data and generally performs tasks such as clustering (i.e. identifying similar elements).
Reinforcement learning is when a *grade* is given to some output. This allows the learner to know
what&#8217;s going right and wrong. A good analogy is when a young child touches a radiator and gets
burned. He will typically learn from his error and avoid touching radiators in the near future, even
if they are not actually hot.

My machine learning class did not discuss reinforcement learning, so for now we can focus on
supervised and unsupervised learning.

To allow machine learning to happen in supervised learning, it is common to divide our data
into *training, validation,* and *testing sets*.

  1. The training set's primary purpose is to build the learning model that the machine can utilize
  to classify future examples. The ideal training set is large, diverse, and is accurately labeled,
  which might involve humans hand-labeling the data.

  2. Validation sets are used to check how well a model has performed before we move on to testing.
  We may have multiple approaches and might use our validation set to pick the top candidates or
  slightly modify some parameters.

  3. Testing sets tend to be used to officially evaluate the performance of our proposed learning
  model. The learner is generally not going to have access to these elements to build the model,
  since that would defeat the point of testing.

There are different ways to partition data into those sets. It is common, in my experience, to
simply combine the validation and testing sets, but the validation set is used enough to make it
worth mentioning. If we have very little data, then we might consider omitting the validation set,
or perhaps even treating the entire data set as both training and testing as a last resort. This is
not desirable because we want to train a machine to perform well on the entire distribution of
relevant data, not just our own samples, so there&#8217;s a danger of [overfitting][4]. In other
words, we build the model so tightly towards our present data that it fails to generalize to the
larger population.

On the other hand, unsupervised learning deals with clustering. The goal here is to find groups of
examples that are similar to each other but distinct from other groups of examples. We'll get
to this more when I discuss clustering algorithms.

*<span class="Apple-style-span" style="font-style:normal;"><strong>Learning Algorithms</strong></span>*

I believe the easiest learning algorithm to discuss is *[decision stumps][5],* since it has just one
clear component. We pick an attribute and associate a rule to it. If it&#8217;s categorical, then we
can have multiple groups for each of the possible values for that attribute, and assign elements
accordingly. If it&#8217;s real-valued, we often associate a threshold to it and divide elements
based on that rule. For instance, if we have real-valued data such as the number of words in an
email message, we might set a threshold of 500 words. All emails with fewer than that quantity are
spam, and all emails with at least 500 words are not spam.

That&#8217;s it! Obviously, in our particular example, this is a *terrible *classification. The
simplicity of decision stumps is one of its major drawbacks, since we have to rely on one single
attribute to make our choice of classification; many times, it is unreasonable for this to result in
an acceptable classification. On the other hand, the fact that it&#8217;s so simple means we can
easily explain this model to a group of non-technical people. Don&#8217;t neglect this important
fact! Scientists and mathematicians must know how to communicate with people from a variety of
fields.

In the next post, I&#8217;ll discuss an obvious extension of this problem to *decision trees*, which
are not restricted to classifying after just one decision.

 [1]: http://seitad.files.wordpress.com/2013/07/machine_learning.jpg
 [2]: http://seitad.wordpress.com/detailed-directory-of-blog-entries/
 [3]: http://en.wikipedia.org/wiki/Precision_and_recall
 [4]: http://en.wikipedia.org/wiki/Overfitting
 [5]: http://en.wikipedia.org/wiki/Decision_stump
