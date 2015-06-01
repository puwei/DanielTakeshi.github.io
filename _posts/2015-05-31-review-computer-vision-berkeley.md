---
layout: post
title:  "Review of Computer Vision (CS 280) at Berkeley"
date:   2015-05-31 22:00:00
permalink: 2015-05-31-review-computer-vision-berkeley
---

Last semester, I took Berkeley's graduate-level computer vision class (CS 280) as part of my course
requirements for the Ph.D. program. My reaction to this class in three words: it was great.

Compared to what happened in classes I took last semester, there were a lot fewer cases of
head-bashing, mental struggles, and nagging doubts in CS 280. One reason for this favorable outcome
is that I eschewed captioning in favor of sign language interpreting, which is the accommodation
type I'm most used to experiencing. What may have played an even bigger role than that, however, was
the professor himself.  The one who taught my class was Professor Jitendra Malik, a senior faculty
member who's been at Berkeley since 1986 and was [recently elected to the National Academy of
Sciences](http://newscenter.berkeley.edu/2015/04/28/five-berkeley-scientists-named-to-national-academy/)
(congratulations). I realized after the first few classes that he *really takes his time* when
lecturing. He talks relatively slowly, explains things at a high level, and repeatedly asks "Does
this make sense?" He is slowest when dissecting math he's scribbled on the whiteboard. In fact, I
was often hoping he would *speed up* when he was strolling through basic linear algebra review that
should have been a prerequisite for taking CS 280. If someone like *me* wants a faster class pace,
that means *everyone else* must have wanted the same thing!

For obvious reasons, the slow lecture pace was well-suited for the two sign language interpreters
who worked during lectures. They sat near where the power point slides were displayed, which made it
relatively easy to move my eyes back and forth across the front of the room. As usual, I hope no one
else got distracted by the interpreters. Unfortunately, the seat next to mine (I sat on the edge of
the first row, no surprise) would remain suspiciously empty for a long time, and would only fill up
once all the other seats were occupied save for a few hard-to-reach center ones.

I should warn future CS 280 students: this is a *popular* graduate-level course, for reasons that
will be clear shortly. The auditorium we had was designed to seat about 80-90 people, and we
probably had over 100 when the class began. It did eventually drop to 80 --- aided by some forced
undergraduate drops --- but before those drops, the tardy students had to sit on the floor.  This is
a real problem with Berkeley EECS courses, but I guess the university is short on funds?

Anyway, let's discuss the work. While the lectures were informative, they did not go in great detail
on any topic. Professor Malik, when faced with an esoteric concept he didn't want to explain, would
say "but I won't explain this because you can read the [academic] paper for yourself, or Wikipedia."
Well, I *did* use Wikipedia a lot, but the thing that really helped me understand computer vision
concepts were the homework assignments. We only had three of them:

* Homework 1 was a jack-of-all-trades assignment which asked us questions on a wide variety
  of subjects. The questions were related to perspective projection, rotation analysis (e.g.,
  Rodriguez's formula), systems of equations, optical flow, and the Canny edge detector, which we
  had to implement. I think it is too hard to implement the Canny edge detector from the original
  1986 paper, and I'm pretty sure most of the students relied on a combination of Wikipedia and
  other sources to get the algorithm pseudocode. Overall, this homework took a *really* long time
  for me to finish (I blame the perspective projection questions), but we did have two weeks to do
  this, and we all got an extension of a few days.

* Homework 2 was a smaller assignment that focused on classifying hand-written digits using SVMs
  (part 1) and neural networks (part 2). The first part was not too bad, as we just had to write
  some short MATLAB scripts, but the second part, which required us to use the open-source,
  Berkeley-developed [caffe](http://caffe.berkeleyvision.org/) software, probably took everyone a
  longer time to finish. To put it politely, research software is rarely easy to use[^moses], and
  caffe is no exception. I could tell that there were a lot of headaches based on the complaints in
  Piazza! Oh, and I should also mention that caffe had a critical update happen a few days before
  the deadline, which broke some of the older data format. Be warned, everyone. To no one's
  surprise, we all got an extension for this homework after that surprise update.

* Homework 3 was another small assignment, and it was about reconstructing a 3-D scene using points
  measured from multiple cameras with different centers. We had to implement a matching algorithm
  that would match the different coordinate systems to determine the true coordinates of a point.
  Our online textbook went through the algorithm in detail, so it wasn't too bad to read the
  textbook and apply what was there (and possibly supplement with external sources). Unfortunately,
  this homework's due date was originally set to be on the *same day* as the midterm! After some
  more Piazza complaints (none from me!), we all got *yet another* extension[^ext].

One thing I didn't quite like was that Homework 1 took significantly longer than the second one,
which took significantly longer than the third one. There wasn't quite much balance, it seems. On
the other hand, we could work in groups of two, which made it easier.

Aside from the homeworks, the other two aspects of our grade were the midterm and the final project.
The midterm was in-class, set to be eighty minutes, but the administrative assistant was a little
late in printing the tests, so we actually started ten minutes late. Fortunately, Professor Malik
gave us five extra minutes, and told us we didn't have to answer one of the questions
(unfortunately, it was one that I could have answered easily). As for the midterm itself, I didn't
like it that much. I felt like it had too many subjective multiple-choice questions (there were some
"select the best answer out of the following..."). I don't mind a few of those, but it's a little
annoying to see thirty percent of the points based on that and to see that you lost points because
you didn't interpret the question correctly. The average score appeared to be about 60 percent.

With regards to my final project, I did enjoy it, even if what I produce almost always falls under
initial expectations. I paired up with another student to focus on extracting information from
videos, but we basically did two separate projects in parallel and tried to convince the course
staff that they could be combined in "future work" in our five-page report. What I did was take
YouTube video frames from Eclipse, Excel, Photoshop, or SketchUp videos and trained a neural network
(using caffe, of course) to recognize, for a given frame, to which movie it belonged. Thus, the
neural network had to solve a four-way classification problem for each frame. The results were
impressive: my network got over 95 percent accuracy!

The final project was also enjoyable because each group had to give a five minute presentation to
the class.  This is better than a poster session because I don't have to go through the hassle of
going to people and saying "Hi, I'm Daniel, can I look at what you did?" One amusing benefit of
these class presentations is that I get to learn the names of people in this class; it's definitely
nothing like Williams where we are expected to know our classmates' names. When I see names that are
familiar from Piazza, I think: whoa, *that* was the person who kept criticizing me!

To wrap it up, I'd like to mention the increasing importance of computer vision as a research field,
which is one of the reasons why I took this class. Computer vision is starting to have some
life-changing impacts to real life. It has long been used for digit recognition, but with recent
improvements, we've been able to do better object detection and scene
reconstruction. In the future, we will actually have automated cars that use computer vision to
track their progress. It's exciting! (One of my interpreters was *terrified* at this thought,
though, so there will be an "old guard" that tries to stop this.) A lot of progress, as Professor
Andrew Ng [mentions in this
article](http://www.huffingtonpost.com/2015/05/13/andrew-ng_n_7267682.html), is due to the power of
combining the ages-old technique of neural networks with the massive amounts of data we have. One of
the things that motivated this line of thinking was a 2012 paper published at NIPS, called [ImageNet
Classification with Deep Convolutional Neural
Networks](http://www.cs.toronto.edu/~fritz/absps/imagenet.pdf), that broke the ImageNet
classification record. It spawned a huge interest in the application of neural networks to solving
object detection and classification problems, and hopefully we may end up seeing *neural networks*
become a household name in the coming years.

***

[^ext]: If there had been a fourth homework assignment, I would have been tempted to say the
    following on Piazza: "To the TAs/GSIs: I would like to ask in advance how long the incoming
    homework extension will be for homework four?"

[^moses]: Moses, for statistical machine translation, is also not an exception. It is [extremely hard
    to install and
    use](http://danieltakeshi.github.io/2014/11/19/brain-dump-successfully-installing-and-running-the-moses-statistical-machine-translation-system/),
    as I discussed last November.

