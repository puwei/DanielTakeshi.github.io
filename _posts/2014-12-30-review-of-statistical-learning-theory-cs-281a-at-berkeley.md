---
title: Review of Statistical Learning Theory (CS 281a) at Berkeley
author: Daniel Seita
layout: post
permalink: /2014/12/30/review-of-statistical-learning-theory-cs-281a-at-berkeley/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - probability
  - statistical learning theory
  - statistics
---

<img src="{{site.url}}/assets/statistical_learning_theory.png" alt="slt">

Now that I&#8217;ve finished my first semester at Berkeley, I think it&#8217;s time for me to review
how I felt about the two classes I took: Statistical Learning Theory (CS 281a) and Natural Language
Processing (CS 288). In this post, I&#8217;ll discuss CS 281a, a class that I&#8217;m extremely
happy I took even if it was a bit stressful to be in lecture (more on that later).

First of all, what is statistical learning theory? I view the subject as one that principally deals
with the problem of finding a predictive function of data that minimizes a loss function (e.g.,
squared loss) on training data, and analyzes this problem in a framework that conflates machine
learning and probability methods. Whereas a standard machine learning course might primarily
describe various learning algorithms, statistical learning theory focuses on the subset of these
that are most well-suited to statistical analysis. For instance, *regression* is a common learning
algorithm, and *regularization* is a common (statistical?) technique we use to improve our
predictors.

At Berkeley, statistical learning theory is a popular course that attracts an unusually diverse
audience of students (by graduate-course standards), not just machine learning theorists. It
attracts students from all computer science and statistics research areas, as well as students from
mathematics, psychology, and various engineering disciplines. For some reason, this year it was even
more popular than usual &#8212; we had over 100 at the start (overflowing the largest room in the
electrical engineering building). I would have thought that since the popular Professor Michael I.
Jordan taught it last spring, that would have pulled away some of the students in this year&#8217;s
cycle, but I guess not.

In past years, I think CS 281a focused almost exclusively on graphical models. My class seemed
different: I had Professor Ben Recht, who was teaching it for the first time, and he changed the
material so that we only discussed graphical models for about four lectures, giving us time to go
over detection theory, hypothesis testing, and other fields. He told me personally that he dislikes
graphical models (and also the EM-algorithm!) so I&#8217;m assuming that&#8217;s the reason why. We
didn&#8217;t even get to talk about the junction tree algorithm.

We had five problem sets, which were each challenging but not impossible, and the workload got
easier as the class went on. I probably spent an average of 15-20 hours on each problem set,
including the &#8220;LaTeX-ing&#8221; process, but not including general mathematical review, of
which I had to do a *lot* because of some shocking gaps in my linear algebra and probability
intuition.

Digression: this semester gave me my first experience with [Piazza][2], a private online forum where
students can ask and answer questions related to the class material. (Students can be anonymous to
other classmates if desired.) Even though it has some obvious shortcomings, I enjoyed it because it
gave me a chance to discuss some of the homework problems &#8220;virtually.&#8221; Combined with a
few in-person collaborations, CS 281a gave me a collaboration experience that I never had at
Williams in my math courses. Having Piazza would have made some of those classes much easier!

Back to CS 281a: somewhat unexpectedly, we had a midterm! It was a 25.5-hour take-home midterm, open
note, and open internet (!). At first, I was disappointed about having to take a midterm because I
think I have proven my ability to understand concepts and describe them under timed exam
constraints, but I ended up enjoying the test and benefited from it. I didn&#8217;t check, but
I&#8217;m pretty sure none of these questions could be found online. 24-hour take home exams are the
norm at Williams so I had tons of experience with this exam format. In lieu of a final exam, we had
a final project, which I [described in a previous post][3].

In terms of the lectures themselves, Professor Recht would alternate between discussing a concept at
a high level and then writing some math on the blackboard. Unfortunately, the technical terms in
this class made the captioning difficult, as [I discussed earlier this semester][4]. (Here&#8217;s a
sample: Gaussians, Kullback-Liebler Divergence, Baum-Welch, Neyman-Pearson, and Lagrangians. Pretend
you don&#8217;t know any math beyond calculus and try to spell these correctly.) And also, I
didn&#8217;t mention this earlier, but for a large lecture course, we had a surprisingly high number
of question-answer exchanges, which made it tougher on the captioner, I think, because of the need
to listen to multiple people talking. The result was that the screen I looked at, which was supposed
to contain the captions, had a lot of gibberish instead, and I bet the students sitting behind me
were wondering what was going on. (I sat in the front row.)

I was still able to learn a lot of the material in part because I did a *lot* of reading &#8212;
both from the assigned list and from random online sources &#8212; to really understand some of this
material. I probably need to rely on out-of-class reading more than most (Berkeley computer science
graduate) students, so I don&#8217;t mind that, and it&#8217;s something that graduate students are
supposed to do: if you don&#8217;t understand something, then learn about it yourself (at first).

Overall verdict: I&#8217;m happy I took it. It&#8217;s a good introduction to what graduate courses
are like, and I will *probably* take the sequel, CS 281B, the next time it&#8217;s offered.

 [1]: https://seitad.files.wordpress.com/2014/12/statistical_learning_theory.png
 [2]: http://piazza.com
 [3]: http://seitad.wordpress.com/2014/12/18/detection-theory-adventures-a-k-a-a-final-project/
 [4]: http://seitad.wordpress.com/2014/10/05/after-a-few-weeks-of-cart-why-do-i-feel-dissatisfied/
