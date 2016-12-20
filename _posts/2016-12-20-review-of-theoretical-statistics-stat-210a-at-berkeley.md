---
layout: post
title:  "Review of Theoretical Statistics (STAT 210A) at Berkeley"
date:   2016-12-20 12:00:00
permalink: 2016/12/20/review-of-theoretical-statistics-stat-210a-at-berkeley/
---

In addition to [taking CS 294-115 this semester][2], I also took STAT 210A,
Theoretical Statistics. Here's a description of the class from the [Berkeley
Statistics Graduate Student Association][3] (SGSA):

> All of the core courses require a large commitment of time, particularly with
> the homework. Taking more than two of them per semester (eight units) is a
> Herculean task.
> 
> 210A contains essential material for the understanding of statistics. 210B
> contains more specialized material. The 210 courses are less mathematically
> rigorous than the 205 courses. 210A is easier than 205A; 210B is very
> difficult conceptually, though in practice it's easy to perform adequately.
> Homework is time-consuming.
>
> 210A: The frequentist approach to statistics with comparison to Bayesian and
> decision theory alternatives, estimation, model assessment, testing, confidence
> regions, some asymptotic theory.

And on [our course website][1] we get the following description:

> Stat 210A is Berkeley's introductory Ph.D.-level course on theoretical
> statistics. It is a fast-paced and demanding course intended to prepare
> students for research careers in statistics.

Both of these descriptions are highly accurate. I saw these before the semester,
so I was already prepared to spend many hours on this course. Now that it's
over, I think I spent about 20 hours a week on it. I thought this was a lot of
time, but judging from the SGSA, maybe even the statistics PhD students have to
dedicate lots of time to this course?

Our instructor was Professor William Fithian, who is currently in his second
year as a statistics faculty member. This course is the first of two theoretical
statistics courses offered each year aimed at statistics PhD students. However,
I am not even sure if statistics PhD students were in the majority for our
class. At the start of the semester, Professor Fithian asked us which fields we
were studying, and a *lot* of people raised their hands when he asked "EECS".
Other departments represented in 210A included mathematics and engineering
fields. Professor Fithian also asked if there was anyone studying the humanities
or social sciences, but it looks like there were no such students. I wouldn't
expect any; I don't know why 210A would be remotely useful for them.  *Maybe* I
can see a case for a statistically-minded political science student, but it
seems like 215A and 215B would be far superior choices.

The number of students wasn't too large, at least compared to the crowd-fest
that's drowning the EECS department. Right now I see 41 students listed on the
bCourses website, and this is generally accurate since the students who drop
classes usually drop bCourses as well.

It's important to realize that even though some descriptions of this course say
"introduction" (e.g., see Professor Fithian's comments above), any student who
majored in statistics for undergrad, or who studied various related concepts
(computer science and mathematics, for instance) will have encountered the
material in 210A before at some level. In my opinion, a succinct description of
this course's purpose is probably: "provide a *broad review* of statistical
concepts but with lots of *mathematical rigor*, while filling in any *minor*
gaps."

I am not a statistics PhD student nor did I major in statistics during
undergrad, which at the time I was there didn't even *offer* a statistics major.
I took only three statistics courses in college: an introductory to stats course
(the easy kind, where we plug in numbers and compute standard deviations), a
statistical modeling course (a *much* easier version than STAT 215A at
Berkeley), and an upper-level Bayesian Statistics course taught by [Wendy
Wang][8]. That third course was *enormously* helpful, and I'm really starting to
appreciate taking that class. The fourth undergrad course that was extremely
beneficial was [Steven Miller's][9] Math 341 class (probability), which is also
now cross-listed into statistics. I should thank my old professors ...

Despite not majoring in statistics, I still knew a lot of concepts that were
introduced in this class, such as:

- Sufficient Statistics
- Exponential Families
- Maximum Likelihood
- Neyman's Factorization Theorem
- Jensen's Inequality and KL Divergences
- Bootstrapping
- The Central Limit Theorem

But I *didn't* know a lot:

- Rao-Blackwell Theorem
- GLRT, Wald, Score, Max tests
- Convergence in probability vs distribution
- The Delta Method
- A lot about hypothesis testing, UMP tests, UMPU tests, etc.

Even for the concepts I already knew, we went into *far* more detail in this
class (e.g. with sufficient statistics) and described the math foundations, so I
definitely got a taste as to what concepts appear in statistics research. A good
example is the [preprint about reranking in exponential families][7] written by
the professor and his graduate student Kenneth Hung, who was also the lone TA
for the course. Having taken this course, it's actually possible for me to read
the paper and remotely understand what they're doing.

The syllabus for 210A roughly proceeded in the order of Robert Keener's
textbook, a book which by itself requires significant mathematical maturity to
understand. We covered probably more than half of the book. Towards the end of
the semester, we discussed more hypothesis testing, which judging from Professor
Fithian's publications (e.g., the one I just described here) seems to be his
research area so that's naturally what he'd gravitate to.

We did *not* discuss measure theory in this class. I think the only measure
theory courses we have at Berkeley are STAT 205A and 205B? I surprisingly
couldn't find any others by searching the math course catalog (is there *really*
no other course on measure theory here???). But even [Professor Aldous' 205A
website][5] says: 

> Sketch of pure measure theory (not responsible for proofs)

Well, then, how do statistics PhD students learn measure theory if they're "not
responsible for proofs"? I assume they self-study? Or is measure theory needed
at all? Keener says it is needed to properly state the results, but it has the
unfortunate side effect of hindering understanding. And Andrew Gelman, a
prominent statistician, [says he never (properly) learned it][6].

As should be obvious, I do not have measure theory background. I know that if
$$X \sim {\rm Unif}[0,1]$$ then the event that $$X=c$$ for any constant $$c\in
[0,1]$$ has measure 0, but that's about it. In some sense this is really
frustrating. I have done a lot of differentiating and integrating, but before
taking this class, I had *no idea* there were differences between Lebesuge and
Riemannian integration. (I took real analysis and complex analysis in undergrad,
but I can't remember talking about Lebesuge integration.)

Even in a graduate-level class like this one, we made lots of simplifying
assumptions. This was the header text that appeared at the top of our problem
sets:

> For this assignment (and generally in this class) you may disregard
> measure-theoretic niceties about conditioning on measure-zero sets. Of course,
> you can feel free to write up the problem rigorously if you want, and I am
> happy to field questions or chat about how we could make the treatment fully
> rigorous (Piazza is a great forum for that kind of question as long as you can
> pose it without spoilers!)

Well, I shouldn't say I was disappointed, since I was more relieved if anything.
If I had to formalize everything with measure theory, I think I would get bogged
down with trying to understand measure this, measure that, the integral is with
respect to X measure, etc.

Even with the "measure-theoretically naive" simplification, I had to spend lots
of time working on the problem sets. In general, I could usually get about 50-80
percent of a problem set done by myself, but for the remainder of it, I needed
to consult with other students, the GSI, or the professor.  Since problem sets
were usually released Thursday afternoons and due the following Thursday, I made
sure to set aside either Saturday or Sunday as a day where I worked solely on
the problem set, which allowed me to get huge chunks of it done and LaTeX-ed up
right away.

The bad news is that it wasn't easy to find student collaborators. I had
collaborators for some (but not all of) the problem sets, and we stopped meeting
later in the semester. Man, I wish I were more popular. I also attended a few
office hours, and it could sometimes be hard to understand the professor or the
GSI if there were a lot of other students there. The GSI office hours were
a major problem, since another class had office hours *in the same room*.  Think
of overlapping voices from two different subjects. Yeah, it's not the best
setting for the acoustics and I could not understand or follow what people were
discussing apart from scraps of information I could get from the chalkboard. The
good news is that the GSI, apart from obviously knowing the material very well,
was generous with partial credit and created solutions to all the problem sets,
which were really helpful to me when I prepared for the three-hour final exam.

The day of the final was pretty hectic for me. I had to gave a talk at [SIMPAR
2016][4] in San Francisco that morning, then almost immediately board BART to
get back to Berkeley by 1:00PM to take the exam. (The exam was originally
scheduled at 8:00AM[^sorry] (!!) but Professor Fithian kindly allowed me to take
it at 1:00PM.) I did not have any time to change clothes, so for the first time
in my life, I took an exam *wearing business attire*.

Business attire or not, the exam was tough. Professor Fithian made it four broad
questions, each with multiple parts in it. I tried doing all four, and probably
did half of all four correct, roughly. We were allowed a one-sided, one-page
cheat sheet, and I crammed mine in with A LOT of information, but I almost never
used it during the exam. This is typical, by the way. Most of the time, simply
*creating* the cheat sheet actually serves as my studying. As I was also
preoccupied with research, I only spent a day and a half studying for the final.

After I had turned in the exam, Professor Fithian mentioned that he thought it
was a "hard exam".  This made me feel better, and it also made me wonder, how
well do professors generally do on their own exams? Well, assuming the exam was
the same difficulty and that they didn't directly know the questions in advance.

It was definitely a relief to finish the final exam, and I rewarded myself with
some Cheeseboard Pizza (first pizza in ages!) along with a beautiful 5.8-mile
run the following morning.

Now that I can sit back and reflect on the course, STAT 210A was enormously
time-consuming but I learned *a lot* from it.  I'm not sure whether I would have
learned more had I had more of a statistics background; it might have made it
easier to go in-depth into some of the technically challenging parts. I probably
could have spent additional focused time to understand the more confusing
material, but that applies to any subject. There's always a tradeoff: should I
spend more time understanding every aspect of the t-test derivation, or should I
learn how to not be an incompetently bad C programmer, or should I simply waste
time and blog?

One of the challenges with a technical course like this one is, as usual,
following the lectures in real time. Like most of my Berkeley classes, I used
sign language interpreting accommodations. No, they were not happy with
interpreting this material, and it was hard for them to convey information to
me. On the positive side, I had a *consistent* group so they were able to get
used to some of the terminology.

In general, if I did not already deeply understand the material, it was very
difficult for me to follow a lecture from start to finish. I can understand
math-based lectures *if* I can follow the math derivation on the board, but with
many of the proofs we wrote, we had to skip a lot of details, making it hard to
get intuition. There are also a lot of technical details to take care of for
many derivations (e.g., regarding measure theory). I wonder if the ability to
fill in gaps between math and avoid getting bogged down with technicalities is
what separates people like Professor Fithian versus the average statistics PhD
student who will never have the ability to become a Berkeley statistics faculty
member.

Regarding the quality of instruction, some might be concerned that since
Professor Fithian is a new faculty member, the teaching would be sub-par. For
me, this is not usually much of an issue. Due to limitations in sign language
and my ability to hear, I always get relatively less benefit out of lectures as
compared to other students, so direct lecture-teaching skill matters less to me
as to whether there are written sources or sufficient office hours to utilize.
(To be fair, it's also worth noting that Professor Fithian won several teaching
awards at Stanford, where he obtained his PhD.)

In case anyone is curious, I thought Professor Fithian did a fine job teaching,
and he's skilled enough such that the teaching quality shouldn't be a negative
factor for future students thinking of taking 210A (assuming he's teaching it
again). He moves at a relatively moderate pace in lectures with standard
chalkboard to present details. He doesn't use slides, but we occasionally got to
see some of his R code on his computer, as well as his newborn child on
Facebook!

I would be remiss if I didn't make any suggestions. So here they are, ordered
roughly from most important to least important:

- If there's any one suggestion I can make, it would be to increase the size of
  the chalkboard text/notes. For optimal positioning of sign language
  interpreting accommodations, I always sat in the front left corner of the
  room, and even then I often could not read what was on the far right
  chalkboard of the room. I can't imagine how much harder it would be for the
  people in the back rows. In part, this may have been due to the limitations in
  the room, which doesn't have elevated platforms for the back rows. Hopefully
  next semester they figure out better rooms for statistics courses.

- I think the pace of the class was actually *too slow* during the first part of
  the course, about exponential families, sufficiency, Bayesian estimation,
  and so on, but then it became slightly *too fast* during the details on
  hypothesis testing. My guess is that most students will be familiar with the
  details on the first set of topics, so it's probably fair to speed through
  them to get to the hypothesis testing portion, which is probably the more
  challenging aspect of the course.  Towards the end of the semester I think the
  pace was acceptable, which means it's slightly too fast for me but appropriate
  for other students.

- Finally, I hope that in future iterations of the course, the problem sets are
  provided on a consistent basis and largely free of typos.  We went off our
  once-a-week schedule several times, but still found a way to squeeze out 11
  problem sets. Unfortunately, some of the questions either had typos or worse,
  major conceptual errors. This often happens when Professor Fithian has to
  create his own questions, which is partly out of necessity to avoid repeating
  old questions and risk students looking up solutions online. I did not look up
  solutions to the problem set questions, though I used the web for the purposes
  of background material and to learn supporting concepts (Wikipedia is great
  for this, so are other class websites which use slides) for every problem set.
  I'm not sure if this is standard among students, but I think *most* would need
  to do so to do very well on the problem set.

Well, that's all I want to say now. This is definitely the longest I've written
about any class at Berkeley. Hopefully this article provides the best and most
comprehensive description of STAT 210A in the blogosphere.  There's a lot more I
can talk about but there's also a limit to how long I'm willing to write.

Anyway, great class!

***

[^sorry]: Professor Fithian: "sorry, not my idea."

[1]:http://www.stat.berkeley.edu/~wfithian/courses/stat210a/
[2]:https://danieltakeshi.github.io/2016/12/20/review-of-algorithmic-human-robot-interaction-cs-294-115-at-berkeley/
[3]:http://sgsa.berkeley.edu/prospective-students/the-department/phd-coursework
[4]:http://simpar2016.org/
[5]:http://www.stat.berkeley.edu/~aldous/205A/index.html
[6]:http://andrewgelman.com/2008/01/14/what_to_learn_i/
[7]:https://arxiv.org/abs/1610.03944
[8]:http://www.wellesley.edu/math/faculty/wangw#IA1IU6oudrHbS9iW.97
[9]:https://web.williams.edu/Mathematics/sjmiller/public_html/williams/welcome.html
