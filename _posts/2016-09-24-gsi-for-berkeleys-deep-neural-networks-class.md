---
layout: post
title:  "GSI-ing for Berkeley's Deep Neural Networks Class"
date:   2016-09-24 10:00:00
permalink: 2016-09-24-gsi-for-berkeleys-deep-neural-networks-class/
---

In news that might be welcome to the students taking CS 294-129, "[Designing,
Visualizing, and Understanding Deep Neural Networks][1]" this semester, I got
recruited as the second GSI (Graduate Student Instructor, a.k.a. Teaching
Assistant) for the class.

Why do I say this might be good news for the students? First, I hope they
realize how much I enjoy teaching. I like to provide hints (but not complete
solutions) to students when they need it, because it feels good when students
are able to learn and benefit from my presence. I'm also tolerant of students
who have to come to office hours frequently, because quite frankly, *I* was one
of those students for a brief time in undergrad (thankfully, since outgrown).

Probably the biggest reason why I think students will like my new GSI position
is that, in news that will surprise no one, the class was substantially
over-enrolled at the start of the semester. My guess is that we had around a
*hundred* students[^piazza] who wanted to take the class ... but *no* GSI.
Fortunately, the class got one GSI a few weeks into the semester, which meant
everyone (I hope) on the waitlist got in. Then I became a GSI. The irony is that
both of us started as normal students. I like to think of it as "getting
promoted as a GSI." With two of us, it means that students will get their
homeworks graded faster. The first one was already due a week ago, and the
second one is due next Friday. Gulp.

So what is this class about? It was a last-minute addition to the curriculum for
the semester, but fortunately, the class is based on [CS 231n from Stanford
University][2], which has already been offered twice. This means we can borrow
their three homework assignments, as well as the style of their midterm
questions (though I hope we don't use the *exact* same questions ...). In
addition, since we are on a semester system and Stanford is on a quarter system,
we can cover slightly more material[^deep_learning], such as Deep Reinforcement
Learning, Monte Carlo methods, and current research directions with Deep
Learning, which do not appear to be on the [CS 231n syllabus][6].

Incidentally, by looking at the Stanford CS 231n offering for Winter 2016, they
had *three* instructors and *eleven* teaching assistants. There were apparently
200 final projects for the class, and since students could pair up for those,
that corresponds to about *300-400 students total* (wow!). We certainly don't
have nearly as many students, but there still is not enough course staff to make
the student-to-staff ratio match.

Our homework assignments, as mentioned earlier, are borrowed from the Stanford
version. I did the first one and am almost done with the second. The assignments
are based on Jupyter Notebooks ([awesome!][4]) and done entirely in Python. And
I'd like to give my congratulations to the CS 231n staff, because the
assignments are *awesome*. They are challenging enough to stimulate the deepest
parts of my brain (pun intended), but not so hard enough that I have to
constantly ask someone for help, which would be a bit embarrassing for a GSI.
One of the things I really like about the assignments is that they give me a
taste for how *real* deep network systems are implemented. In my undergraduate
machine learning class, I implemented backpropgation for a very simple, fully
connected neural network, but that was a "naive" version, with me iterating
through arrays and following a formulaic definition. That worked out fine, but
in practice, neural network code must be modular enough (and vectorized!) to
allow for effective training on *deep* networks. Oh, and did I mention that most
networks for image recognition are not fully connected but *convolutional* nets?
That makes the implementation much more challenging!

I'm excited to be joining the course staff for CS 294-129, and I hope that I and
the rest of the students will enjoy the course. Probably the one downside to
being a GSI is that I may have to face student complaints (moreso than [when I
was TA-ing in undergrad][5]) since GSIs have more grading responsibility.

***

[^piazza]: It's a bit tough to say how many students we have exactly, since some
    join after the start date and others drop. The Piazza website says that
    there are 165 people enrolled, but that also includes students who have
    dropped the class.

[^deep_learning]: Our textbook is based on the [online book by Goodfellow et
    al][3]. I was hoping to read through the full book at some point, so this
    class gives me a great opportunity to do that!

[1]:https://bcourses.berkeley.edu/courses/1453965
[2]:http://cs231n.stanford.edu/
[3]:http://www.deeplearningbook.org/
[4]:https://danieltakeshi.github.io/2016-01-16-ipython-jupyter-notebooks-and-matplotlib/
[5]:https://danieltakeshi.github.io/2013/04/26/whats-it-like-being-an-undergraduate-teaching-assistant/
[6]:http://cs231n.stanford.edu/syllabus.html
