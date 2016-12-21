---
layout: post
title:  "Review of Algorithmic Human-Robot Interaction (CS 294-115) at Berkeley"
date:   2016-12-20 23:00:00
permalink: 2016/12/20/review-of-algorithmic-human-robot-interaction-cs-294-115-at-berkeley/
---

In addition to [taking STAT 210A][3] this semester, I took CS 294-115,
[Algorithmic Human-Robot Interaction][1], taught by Professor Anca Dragan.  I
will first provide a summary of what we did in class, roughly in chronological
order. Then I would like to discuss what could be improved for future
iterations.

The first day presented, as usual, [the enrollment surge][5], which is either a
good thing or a bad thing. But for being able to find a chair in the classroom,
it's a bad thing. I arrived a few minutes before class started (which is
actually *late* for the first day) and found a packed room, but fortunately my
two sign language interpreters had booked a seat for me. 

I felt bad for that. If I'm the last to arrive and all the chairs are taken, I
have no problem sitting on the floor or standing up. It's OK. Fortunately, the
number of students eventually dropped to 34 by the end of the course, but for
the first few weeks, we had a lot of students sitting on the floor or standing
by the door. The two sign language interpreters took up two seats, so I worried
that I was inconveniencing the other students. Fortunately, no one seemed to be
angry, and Professor Dragan seemed to be OK with it. In fact, at the start of
the semester, she sent me an email asking how the course was going, if she was
talking too fast, etc. I remember two other professors contacting me that way:
[Sarah Jacobson][6] for Microeconomics and [Wendy Wang][7] for Bayesian
Statistics, and I like it when professors do that.  I responded saying that she
was doing just fine and that any limitation in my ability to understand material
was mostly out of her control.

In CS 294-115, much of the first half of the semester consisted of lectures on
standard robotics topics, particularly motion planning and trajectory
optimization. This is also an HCI course, and we had lectures on experimental
design and learning from demonstrations (which are often human-led). The most
concise way to describe this class is probably a cross between [CS 287, Advanced
Robotics][8], and CS 260, the Human-Computer Interaction course at Berkeley. I
think a lot of computer science PhD students took CS 294-115 to satisfy their
PhD breadth requirements. I would, of course, take it even if it *didn't*
satisfy my requirements.

As I quickly learned, one of the most controversial aspects of CS 294-115 are
the quizzes. Every few classes, Professor Dragan would set the first 5-10
minutes aside for a quiz, which typically asked basic questions about topics
covered in the previous lectures. Each quiz was graded on a three-point scale:
minus, check, and plus. I earned one plus and three checks on the four "normal"
quizzes we had.

For one of the quizzes, the class as a whole did poorly (a third minus, a third
check, and a third plus). Probably the reason for this is that the question was
about the *reading* for the class, specifically, the Maximum-Entropy Inverse
Reinforcement Learning paper. Before the quiz, Professor Dragan smiled and said
something similar to: "if you didn't do the reading, try to say *anything*
relevant." Gee, it looks like the do-your-readings rule doesn't even apply to
Berkeley graduate courses!

We had a make-up quiz, but I still only earned a check.  Ugh.

Regardless of whether this class turns into a seminar or a lecture (which I'll
discuss later in this article) I personally think the quizzes should be
abolished. Professor Dragan also commented in class that some students thought
quizzes did not belong in a class like this. We're "not in high school," as some
succinctly put it.

As one can tell from reading the syllabus online, aside from the lectures, we
also had a lot of classes devoted to student presentations about research
papers. For each paper, we had a PRO and a CON presenter. Their names are
self-explanatory: the PRO presenter talks about the paper as if he/she had
written it, while the CON presenter provides constructive criticism.  I liked
this part of the class, though there are some inherent weaknesses, such as
scalability.

I had to wait a while; it wasn't until November 15 that I got to present. I was
assigned to be the CON presenter for a *very* interesting (and award-winning!)
paper [*Asking for Help Using Inverse Semantics*][10].

In every talk, I always need to think of several jokes to say.  The logic is as
follows: I am at the bottom of the social hierarchy when it comes to anything
related to popularity. Thus, when I'm giving a talk to a class or some audience,
*this is one of the few times where people are actually going to bother to
listen to what I have to say*. In other words, I *really* can't afford to waste
my chance to give a positive impression. One way to make a good impression is to
give a talk about something really positive, such as if I came up with a really
new algorithm that people will love. Unfortunately, aside from the really
top-tier stuff, I think it's hard to distinguish oneself with the *content* of
the talk (especially if it's not about work I did!) so the next best thing that
really helps is being reasonably funny.

Thus, I came up with the following tentative plan: since it's election season,
let's have "Anca for President"!  I would include an image like the following in
my slides, where going from left to right correlates with how much respect I
have for that person.

<p style="text-align:center;">
<img src="{{site.url}}/assets/politicians_respect.png" 
alt="politicians">
</p>

Again, this is a *rough draft* of what a figure might look like, and I'm not
saying this would have been finalized. I might have shifted a few of these faces
around, or added/removed a few. There are indeed a lot of leaders who I think
are worse than Putin, after all ...

I *think* if I showed this in class, it would elicit considerable laughter and
raise talks of "Anca for President!" even though she's not Constitutionally
eligible.  Unfortunately, the paper I presented didn't really make this joke fit
in the talk well. Combined with the fact that the candidate who everyone opposed
won the election ... never mind.

Instead, I made a joke about how humans differ in their "level of altruism." In
[CS 294-129, for which I was the GSI][9], a student asked a question on Piazza
about how to use Jupyter Notebook. It was a really stupid and shallow question,
but I couldn't resist answering it to the best of my ability. But then Professor
Canny responded with a far stricter (but also far more helpful!) answer, along
the lines of "no one can help you with that much information [...] saying this
is a waste of time [...]". It was pretty clear that Professor Canny and I have
drastically different styles, and I tried to put that in a humorous perspective.
I think it worked well, but the text was admittedly too small to see well, and
Professor Dragan docked me for it during her email to me immediately after the
talk.

Unfortunately I was scheduled as the *fourth* presenter that day, which is
easily the worst slot to be in for this class. As luck would have it, the
other three presenters went over their time (I sarcastically thought: "big
surprise"), meaning that I got to be the first presenter during the following
class.

The class after my *actual* presentation was the one before Thanksgiving, and it
was a special one where Professor Dragan ran an experiment. Rather than have the
usual PRO/CON presenters, we would instead split into small groups for
discussion. You can imagine how much I "liked" that. To the surprise of no one,
my sign language interpreters could not understand or follow the discussion
well, and neither could I. But maybe I'm just a lonely Luddite. It seemed like
the other students enjoyed that class.

After the Thanksgiving "break", we had class presentations during the final
week. I'm not sure if there's something about the aura in our class, but there's
*so much more humor* compared to the [Deep Neural Networks presentations from CS
294-129][4].  Seemingly everyone had a joke or did something that caused
laughter. Here are a few that I remember:

- Explicitly saying a joke. These are the best kind and the ones I try to do
  every time, for reasons described earlier.
- Showing a funny video.
- Performing a funny gesture.
- Complaining about the 4-minute time limit and watching as Professor Dragan
  sneaked closer and closer to the presenter to cut off the talk.
- Having multiple phones time the talks (Professor Dragan's and the presenter's)
  and having them both ring after 4 minutes.
- Grabbing Professor Dragan's laptop after the talk was over, thinking it was
  theirs.

The laughter was contagious and this is definitely something positive about the
class. My project presentation, incidentally, was about human gameplay to boost
Atari game play agents. I have some code that I'll hopefully release soon.

After the project presentations, we had to work on our final reports (5 page
maximum).  Here's a tip for those who need more space, which should be
everybody: use IEEE Conference-Style papers. The font size is small, and when
you expand the LaTeX coding to reach the maximum margins, you get *a lot* of
information packed into five pages.

All right, that was the class, but now what about some feedback? Professor
Dragan said she plans to teach this class again under the new "CS 287H" label.
What could be better for future semesters? In my opinion, the most important
question to ask is whether the class should be structured as a seminar or a
lecture. Doing it half-seminar, half-lecture as we had is really awkward.

I am inclined towards turning CS 294-115 into a standard lecture course, [given
my problematic history with seminars][11]. Yes, I know I've complained a lot
about not being able to follow technical lectures, but seminars are *still*, on
average, worse. 

The decision is obviously up to Professor Dragan. If she wants to keep it as a
seminar, I would highly encourage:

- establishing a strict enrollment limit with no more than 30 students and
  requiring prospective students to fill out a detailed form describing how they
  can contribute to the class. There are several classes which do this already
  so it's not unusual. The enrollment limit is necessary because far more
  students will sign up next year. Why? It's simple: robotics is very popular
  and Professor Dragan is very popular.
- enforcing time limits better. There were many times when students, for both
  PRO/CON presentations and final project presentations, exceeded their allotted
  time.

If CS 294-115 turns into a normal lecture, then:

- introduce problem sets and a midterm to test knowledge instead of relying on
  shallow quizzes. This will require GSIs, but by now there are plenty of
  students who can do that job. This will mean more work for the students, but
  CS 294-115 probably needs more work anyway. It's listed as 3 credits, but I
  think it's more accurate to call it a 2.5-credit class.

Regardless of the class style, I have an idea if quizzes have to remain in CS
294-115. To fix the problem of students not reading papers beforehand, let's
have quizzes for *all* the paper readings. In fact, the student presenters can
create them! They can do the grading and then forward the results to Professor
Dragan to minimize her workload.

Don't misunderstand what I'm saying. Throughout the class, I looked at all the
papers, but I mostly read only the abstract plus the first few introductory
sections. I *wanted* to read these papers in detail, but there's a tradeoff. If
I can spend four hours the night before class working towards important
research, I'm going to prefer doing that over reading a paper without
hesitation.

My final suggestion for the class is about the project presentation sign-up
process. We had a class spreadsheet and had to sign up for one of the two days.
Instead, let's randomly assign students to presentation times and make slides
due on the same night for everyone.

Well, that's all I want to say about CS 294-115 now. This is just one person's
opinion and others will no doubt have their own thoughts about the class. I'll
check the future course websites now and then to see if there are any
interesting changes from the version I just took.

Professor Dragan, thanks for a fun class!

[1]:https://people.eecs.berkeley.edu/~anca/AHRI.html
[2]:https://danieltakeshi.github.io/2016/12/19/mitt-romney-should-be-secretary-of-state/
[3]:https://danieltakeshi.github.io/2016/12/20/review-of-theoretical-statistics-stat-210a-at-berkeley/
[4]:https://danieltakeshi.github.io/2016/12/19/reflections-on-being-a-gsi-for-deep-neural-networks-cs-294-129-at-berkeley/
[5]:https://danieltakeshi.github.io/2016-01-10-the-enrollment-surge-in-graduate-courses/
[6]:http://econ.williams.edu/profile/saj2/
[7]:http://www.wellesley.edu/math/faculty/wangw#mQ6j7FM7E4Vg0jLS.97
[8]:https://danieltakeshi.github.io/2015-12-21-review-of-advanced-robotics-cs-287-at-berkeley/
[9]:https://danieltakeshi.github.io/2016/12/19/reflections-on-being-a-gsi-for-deep-neural-networks-cs-294-129-at-berkeley/
[10]:http://cs.brown.edu/courses/csci2951-k/papers/tellex14.pdf
[11]:https://danieltakeshi.github.io/2013/11/10/the-problem-with-seminars/
