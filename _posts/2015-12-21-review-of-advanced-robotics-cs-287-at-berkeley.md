---
layout: post
title:  "Review of Advanced Robotics (CS 287) at Berkeley"
date:   2015-12-21 23:59:00
permalink: 2015-12-21-review-of-advanced-robotics-cs-287-at-berkeley
---

I took Advanced Robotics (CS 287) last semester, which is the graduate level class that [Pieter
Abbeel](http://www.cs.berkeley.edu/~pabbeel/) teaches at Berkeley. You can view the [course website
here](http://www.cs.berkeley.edu/~pabbeel/cs287-fa15/). Robotics is a vast, highly interdisciplinary
field, so to restrict the focus, CS 287 is about the math and algorithms of robot systems. No, we
didn't see giant, science-fiction style robots battle each other, but we *did* observe a research
robot tie knots (alas, through videos, not in real time).

Before the class even began, I could tell we would have some logistics issues. Like *almost every
course I have taken at Berkeley*, CS 287 was substantially over-enrolled at the start; we had
perhaps eighty students before settling down to about sixty at the end.  According to the CS 287
websites from previous years, it looks like the Fall 2009 and Fall 2012 courses had nineteen and
fifteen students, respectively. Yeah, welcome to the new normal.

Due to the class size, Pieter actually provided *two* different lecture times, one in the morning
and one in the afternoon, and I suspect he also convinced John to [do the same thing for CS
294-112](http://danieltakeshi.github.io/2015-12-17-review-of-deep-reinforcement-learning-cs-294-112-at-berkeley/).
Pieter did this to get to know the students better. During some of the class breaks, he would ask a
handful of students to introduce themselves to everyone. Since I sat in the front corner of the room
for optimal use of sign language interpreting services, I was called on first. From these
    introductions, I learned a few things from the class composition:

- There were *a lot* of mechanical engineering graduate students. So much, to the point where I was
  complaining (er, joking) about this with my interpreters midway through a long sequence of
  mechanical engineers introducing themselves.  It's a good thing that no one else in the class (I
  *think*...) can understand sign language. (PS: to mechanical engineers reading this, I *was*
  joking so please don't get angry.)

- A *lot* of the students **do not speak clearly**! Many are quiet, have heavy foreign accents, or
  exhibit both qualities. The most egregious case resulted in my interpreter *not understanding a
  single word a student said*, which I [mentioned earlier
  here](http://danieltakeshi.github.io/why-can-certain-people-understand-foreign-accents-easily/).

- A lot of the students did robotics research of some form, whether it was in computer science,
  mechanical engineering, electrical engineering, or a related field.  Then I'm confused, is it just
  this year that robotics suddenly became popular? Or is it because CS 287 wasn't offered last year
  and that this is the "overflow" year?

In terms of course material, CS 287 combined lectures on standard topics in artificial intelligence
(e.g., optimization and probability) and on more obscure, robotics research subjects. The course
lectures could be divided as follows: Markov Decision Processes, optimization, probability, and
research. Overall, I felt that the lectures were polished and of high quality. Pieter seemed like he
really knew the material and was able to offer many doses of intuition for some of the more
technical material.

I discuss this in my other reviews, so I'll continue the trend: how did the lectures mesh with sign
language interpreting services? Pieter lectured at a fast pace, which was problematic for my two
interpreters, who were often exhausted when their 20-minute shifts were up. On the positive side,
Pieter spoke *loud and clear*, to the point where I actually think he's one of the easiest people
for me to understand. Consequently, relative to other classes, I did not have much difficulty in
terms of identifying the exact words he uttered. It's also somewhat ironic that he would be the one
to mention to me about an ideal future where people had "virtual captions" projected out of their
mouths, which displays the text they say in real-time. Yes, I *would* like for that to happen.

As an added benefit, the course slides contained a lot of information. In many cases I could
understand a concept or a homework sub-problem just by reading the appropriate slides, which is
really handy for a text-heavy person like me. Incidentally, while Pieter wrote a lot of math on a
white board, in almost all cases it was math directly from the slides, and he was writing it out for
intuition. Thus, taking hand-written notes is probably unnecessary for this class.

No course is without its hiccups, however, and I'd like to bring up a few points that may (or may
not) matter to future students:

- The difficulty of lectures varied considerably, which one can probably tell by browsing some of
  the slides. I thought the easiest class was [the one on introductory
  probability](http://www.cs.berkeley.edu/~pabbeel/cs287-fa15/slides/lecture12-probability-review.pdf).
  Since the material is quite rudimentary, I think that lecture needs to be eliminated in future
  iterations of the course. Basic probability is an *ironclad requirement* for understanding the
  math of robot systems. Other lectures were more complicated.  The convex optimization and Kalman
  Filtering lectures would have been hard for me to follow had I not already had substantial
  exposure to those concepts.

- Towards the end of the semester, we had a "project speed-dating" lecture, which is when we
  gathered in small groups and shared our progress on the final project.  Ideally, students could
  get feedback and learn what others were doing. In reality, most students skipped this class, and
  I'm not sure how beneficial it was to those students who *did* attend (I didn't benefit).
  Furthermore, we eventually had final project presentations.  Thus, I think project speed-dating
  should be replaced with a "standard" robotics lecture.

- We had three class sessions where guests from industry lectured about their companies. I'm neutral
  towards these, and would suggest that these only happen when Pieter (or another future instructor,
  if applicable) is traveling and unable to lecture.

CS 287 had four problem sets which involved math and MATLAB programming.  I thought they were, on
average, less challenging compared to problem sets in other classes.  The math did not require
incredible problem-solving skills, and I think they were designed to accommodate people from other
fields (mechanical engineers ...). For instance, the fourth homework asked to prove that covariance
matrices are positive semidefinite, which is something that a lot of machine learning students can
answer in thirty seconds. For the coding, we had to fill in MATLAB code in the designated "YOUR CODE
HERE" sections. We got *a lot* of starter code for these assignments, so it's relatively easy to
understand how the code works in the overall pipeline.

To turn in homeworks, we used [Gradescope](https://gradescope.com/), a company Pieter co-founded
with Berkeley students. We only had to turn in PDFs of our answers, and the course staff can grade
code-based assignments by spot-checking our plots. (Part of the reason why we had lots of starter
code is because some of that is used to generate plots, which means that they are standardized
across all student submissions.) We had page limits for our solutions, so be sure you know how to
cram lots of figures together in LaTeX, such as by using [minipages or
subpages](http://tex.stackexchange.com/questions/37581/latex-figures-side-by-side). Oh, I should
mention: there are no solution sets to these assignments. I agree with Pieter in that there would be
too much temptation for students to search for old solutions. Well, *I* wouldn't search, but I'm not
sure about others.

In addition to regular homeworks, we had four (!) optional extra credits, plus the final project. I
only did one of the extra credit assignments, so I don't have much to comment on those.

For my final project, I worked on a deep learning project about Atari game play, but my project
ended up relating more to *human learning* since I analyzed data from humans playing Atari games on
Amazon Mechanical Turk, and I ran out of time to integrate my findings with a Q-Learning agent.
Pieter was the one who suggested this project. In fact, back in October, he and the two GSIs
actually met with *every project group in the class* for five minutes to discuss the final project.
Then, a day later, I assume Pieter sent out personalized emails to every group with project
suggestions. That must have been a lot of work!

Just like in CS 280, we had project *presentations*, *not* a project poster session. That is a good
thing. Single-student groups presented for 5.5 minutes. I tried to be funny by sprinkling in four
jokes in my talk, and went so far as to put in a picture of Bernie Sanders in one of my slides.
Unfortunately, I think my Sanders-related joke backfired since a lot of the students were
internationals or were not fluent in American politics, whereas I have very strong political
beliefs.

We then had to write the usual report to wrap up the project. I will warn future students: the
grading for the final project is somewhat stricter than the grading for homeworks, though admittedly
I think it was hard to get a *really low* grade on the project. Thus, to get an A, try to get at
least 90 percent of the homework points, and make up for lost points with the four extra credit
assignments. Pieter really makes it clear how our grades are computed, which makes the process less
stressful for students who care about grades. This is in contrast with some other professors, who
might not even return grades for final projects.

In conclusion, I enjoyed CS 287 and would highly recommend it to future students. Again, if possible
consider taking this class concurrently with Deep Reinforcement Learning or a similar two-credit
class as they would reinforce each other.
