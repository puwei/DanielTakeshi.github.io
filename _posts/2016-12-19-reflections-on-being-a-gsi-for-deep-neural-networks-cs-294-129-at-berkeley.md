---
layout: post
title:  "Reflections on Being a GSI for Deep Neural Networks (CS 294-129) at Berkeley"
date:   2016-12-19 15:00:00
permalink: 2016/12/19/reflections-on-being-a-gsi-for-deep-neural-networks-cs-294-129-at-berkeley/
---

This semester, [as I mentioned in an earlier blog post][2], I was one of two
GSIs[^gsi] for [the Deep Neural Networks course at Berkeley][1], taught by
Professor John Canny. This was a surprise, because I was not planning on being a
GSI for any class until Fall 2017. I wanted to have time to carefully think
about and plan my GSI experience beforehand, perhaps by talking to previous GSIs
or learning more about becoming an effective teacher.  In addition, I was hoping
to write a few technical articles here, and maybe some students would find them
helpful.  They would have to search for my blog themselves, though, since I
usually don't actively tell people about this website.

Well, so much for that. I got appointed several weeks into the course, *after* I
had done the first assignment as a normal student. How did it happen? After [Yang
You][4] (the other GSI) got appointed, he talked to me after class to ask about
the possibility of being a GSI, since he knew that I was one of John Canny's
students. I thought about it and decided to join. John was a little hesitant at
first and worried that I would spend too much time trying to help out the
students, but after I promised him "not to spend more than 15 hours a week on
this course" John agreed to have me appointed as a 10-hour GSI.[^hours] This
process was certainly rushed and I had to scramble through Berkeley's annoying
administrative requirements.

Fortunately, things soon settled down as normal. My first set of duties
consisted of grading homework and providing comments on Piazza. I contacted the
Stanford CS 231n team, but did not get a response which contained a rubric, so
Yang and I had to create our own for the assignments.  After I figured out a
good workflow to downloading and managing Jupyter Notebooks, I was usually able
to grade relatively quickly by running a select subset of the Notebook cells and
spot-checking the plots.

There were four programming assignments in this course. The first three were
adapted from CS 231n at Stanford, and the fourth one was a reinforcement
learning homework assignment which John and I had to create. It asked questions
regarding [Deep-Q Networks][5] and Policy Gradients. Some of the homework was
unclear, and we only had two reinforcement learning lectures in the course ---
neither of which mentioned DQN --- so I think in future iterations of the
course, either the lecture arrangement or the fourth assignment (or both) should
be substantially revised.

CS 294-129 also contained an in-class midterm (80 minutes). Professor Canny
created the midterm and I helped to revise and clarify it. One regret I have is
that I didn't create any questions. While the midterm was OK and fair, I would
have designed it in a slightly different way and would have made it more
challenging. Grading was easy due to [Gradescope][6].

I also made a mistake just before the midterm.  Professor Canny had said that
students were allowed to use "one page of notes". A student asked a question on
Piazza inquiring about whether this was one-sided or two-sided. I had always
thought one page meant two-sided, and the day before the midterm, I provided an
answer: "two-sided". Oops.  Professor Canny almost immediately replied saying
*one-sided*. To the students who had to rewrite their cheat sheet for the exam
due to this, I am genuinely sorry. After that, I made sure not to jump the gun
on administration questions.

While the class has programming assignments and a midterm as mentioned earlier,
the most important part of CS 294-129 is the student project assignment, done in
groups of 1-4 students. We set aside *four lectures* for student project
presentations, two in the week before the midterm and two in the last week of
classes. (I think this is a bit too much, and would probably have set the first
presentation week to be more about DQN and some other core Deep Learning
concept.)

The 83 students who took the midterm collectively formed 36 project teams. Thus,
18 teams presented each day. We set aside 3 minutes for the first presentation
week and 5 minutes for the second presentation week, since we started class 30
minutes earlier. The course staff graded both sets of presentations, and I was
responsible for collecting all our feedback together to give a final grade along
with written feedback. Here is a list containing some common feedback I gave:

- Please respect the time limits.

- Please use large text *everywhere* on figures: title text, axes text, legend
  text, etc. Come on everyone, [this is really easy due to matplotlib][7].

- Please don't clog your slides with a long list of text. If I want to read the
  text, I can read the final report. (And students in the audience who may want
  more detail are free to contact the presenters.)

- Please look at the audience when talking and project your voice while speaking
  with confidence. One might wonder if it is appropriate for a deaf person to
  provide comments on this material. In my case, it is OK for the following
  reasons: the other GSI and the professor also wrote comments about this, and
  my sign language interpreters can tell me if there's a student who speaks too
  softly. 

- Please respect the time limits.

I also noticed an interesting contrast between the presentations in this class
versus those of CS 294-115, the Algorithmic Human-Robot Interaction class. Our
presentations did not contain that much humor, and I don't think we laughed a
lot. In contrast, the CS 294-115 presentations were *substantially* more
humorous. Why is that??

As I said, I combined the feedback from the course staff to provide grades for
the presentations. I learned more about the students and the exciting work they
were doing, but the process of grading these presentations took about a full
day. Indeed, grading tends to be one of the more cumbersome aspects of being a
GSI/TA, but putting things in perspective, I think my grading experience was
"less bad" than those of other GSIs. I was pleasantly surprised that I didn't
get too many grading complaints. This is a graduate course, and the undergrads
who lasted the entire semester are also probably more skilled than the average
undergraduate EECS student, so the students would generally have produced better
work. It also helps that the grading curve for EECS graduate courses provides
more As by default.

There was something far worse than grading, however. The worst part of being a
GSI was, without question, that *not a single student attended my office hours*!
I know I started late as a GSI, but I still had about seven or eight weeks of
office hours. I guess I really am unpopular.

Sadly, this course will not be offered next semester, but there is [an
alternative in CS 294-112][3], which I expect to be popular. Professor Canny
*might* be willing to teach CS 294-129 again next fall, and I *might* also be
willing to be the GSI again, so we'll see if that happens. If it does, I hope to
be more popular with the students while also demanding strong work effort. If
not, well, I think I enjoyed the GSI experience overall and I'm happy I did it.
I hope the students enjoyed the class!

***

[^gsi]: GSI stands for "Graduate Student Instructor" and is the same thing as a
    Teaching Assistant.

[^hours]: As far as I can tell, during the semester students can sign up to be a
    10-hour or a 20-hour GSI, with 40-hour GSIs reserved for summer courses. Of
    course, by now I've learned to treat any "X-hour job" with skepticism that
    it's actually an "X-hour" job.

[1]:https://bcourses.berkeley.edu/courses/1453965
[2]:https://danieltakeshi.github.io/2016-09-24-gsi-for-berkeleys-deep-neural-networks-class/
[3]:http://rll.berkeley.edu/deeprlcourse/
[4]:https://people.eecs.berkeley.edu/~youyang/
[5]:https://danieltakeshi.github.io/2016/12/01/going-deeper-into-reinforcement-learning-understanding-dqn/
[6]:https://gradescope.com/
[7]:https://danieltakeshi.github.io/2016-01-16-ipython-jupyter-notebooks-and-matplotlib/
