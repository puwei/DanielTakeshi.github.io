---
layout:     post
title:      "Review of Theoretical Statistics (STAT 210B) at Berkeley"
date:       2017-06-26 12:00:00
permalink:  2017/06/26/review-of-theoretical-statistics-stat-210b-at-berkeley/
---

After taking STAT 210A last semester (and [writing way too much about it][2]),
it made sense for me to take STAT 210B, the continuation of Berkeley's
theoretical statistics course aimed at PhD students in statistics and related
fields.

## The Beginning

Our professor was [Michael I. Jordan][1], who is colloquially called the
"Michael Jordan of machine learning."  Indeed, how does one begin to describe
his research? Yann LeCun, himself an extraordinarily prominent Deep Learning
researcher and considered as one of the three leaders in the
field[^schmidhuber], said this[^interview] in a [public Facebook post][5]:

> Mike's research direction tends to take radical turns every 5 years or so,
> from cognitive psychology, to neural nets, to motor control, to probabilistic
> approaches, graphical models, variational methods, Bayesian non-parametrics,
> etc. Mike is the "Miles Davis of Machine Learning", who reinvents himself
> periodically and sometimes leaves fans scratching their heads after he changes
> direction.

And Professor Jordan responded with:

> I am particularly fond of your "the Miles Davis of machine learning" phrase.
> (While "he's the Michael Jordan of machine learning" is amusing---or so I'm
> told---your version actually gets at something real).

As one would expect, he's extremely busy, and I think he had to miss four
lectures for 210B.  Part of the reason might be because, as he mentioned to us:
"I wasn't planning on teaching this course ... but as chair of the statistics
department, I assigned it to myself. I though it would be fun to teach." The TAs
were able to substitute, though it seemed like some of the students in the class
decided to skip those lectures.

Just because him teaching 210B was somewhat "unplanned" doesn't mean that it was
easy --- far from it! In the first minute of the first lecture, he said that
210B is the hardest course that the statistics department offers. Fortunately,
he followed up with saying that the grading would be lenient, that he didn't
want to scare us, and so forth. Whew. We also had two TAs (or "GSIs" in Berkeley
language) who we could ask for homework assistance.

Then we dived into the material. One of the first things we talked about was
*U-Statisics*, a concept that can often trick me up because of my lack of
intuition in internalizing expectations of expectations and how to rearrange
related terms in clever ways. Fortunately, we had a homework assignment question
about U-Statistics in 210A so I was able to follow some of the material. We also
talked about the related *Hájek projection*.


## Diving into High-Dimensional Statistics

We soon delved into to the meat of the course. I consider this to be the
material in our textbook for the course, Professor Martin Wainwright's recent
book *High-Dimensional Statistics: A Non-Asymptotic Viewpoint*.

For those of you who don't know, Professor Wainwright is a faculty member in the
Berkeley statistics and EECS departments who won the 2014 COPSS "Nobel Prize in
Statistics" award due to his work on high dimensional statistics.  [Here's the
transcript of his interview][12], where he says that serious machine learning
students *must* know statistics. As a caveat, the students he's referring to are
the kind that populate the PhD programs in schools like Berkeley, so he's
talking about the best of the best. It's true that *basic* undergraduate
statistics courses are useful for a broad range of students --- and I wish I had
taken more when I was in college --- but courses like 210B are not needed for
all but a handful of students in specialized domains.

First, what is "high-dimensional" statistics? Suppose we have parameter $$\theta
\in \mathbb{R}^d$$ and $$n$$ labeled data points $$\{(x_i,y_i)\}_{i=1}^n$$ which
we can use to estimate $$\theta$$ via linear regression or some other procedure.
In the classical setting, we can safely assume that $$n > d$$, or that $$n$$ is
allowed to increase while the data dimension $$d$$ is typically held fixed. This
is not the case in high-dimensional (or "modern") statistics where the
relationship is reversed, with $$d > n$$. Classical algorithms end up running
into brick walls into these cases, so new theory is needed, which is precisely
the main contribution of Wainwright's research. It's also the main focus of STAT
210B.

The most important material to know from Wainwright's book is the stuff from the
second chapter: sub-Gaussian random variables, sub-Exponential random variables,
bounds from Lipschitz functions, and so on. We referenced back to this material
*all* the time.

We then moved away from Wainwright's book to talk about entropy, the Efron-Stein
Inequality, and related topics. Professor Jordan criticized Professor Wainwright
for not including the material in this book. I somewhat agree with him, but for
a different reason: I found this material harder to follow compared to other
class concepts, so it would have been nice to see Professor Wainwright's
interpretation of it.

Note to future students: get the book by Boucheron, Lugosi, and Massart, titled
*Concentration Inequalities: a Nonasymptotic Theory of Independence*. I think
that's the book Professor Jordan was reviewing when he gave these
non-Wainwright-related lectures, because he was using the same exact notation as
in the book. 

How did I know about the book, which amazingly, *wasn't even listed on the
course website*? Another student brought it to the class and I peeked over the
student's shoulder to see the title. Heh. I memorized the title and promptly
ordered it online. Unfortunately, or perhaps fortunately, Professor Jordan then
moved on to exclusively material from Professor Wainwright's book.

If any future students want to buy off the Boucheron et al book from me, send me
an email.

After a few lectures, it was a relief to me when we returned to material from
Wainwright's book, which included:

- Rademacher and Gaussian Complexity (these concepts were briefly discussed in a
  [Deep Learning paper I recently blogged about][11])
- Metric entropy, coverings, and packings
- Random matrices and high dimensional covariance matrix estimation
- High dimensional, sparse linear models
- Non-parametric least squares
- Minimax lower bounds, a "Berkeley specialty" according to Professor Jordan

I obtained a decent understanding of how these concepts relate to each other.
The concepts appear in many chapters outside the ones when they're formally
defined, because they can be useful as "sub-routines" or as part of technical
lemmas for other problems.

Despite my occasional complaint about not understanding details in Wainwright's
book --- which I'll bring up later in this blog post --- I think
the book is above-average in terms of clarity, relative to other textbooks aimed
at graduate students. There were often enough high-level discussions so that I
could see the big picture. One thing that needs to be fixed, though, are the
typos. Professor Jordan frequently pointed these out during lecture, and would
also sometimes ask us to confirm his suspicions that something was a typo.

Regarding homework assignments, we had seven of them, each of which was about
five or so problems with multiple parts per problem. I was usually able to
correctly complete about half of each homework by myself. For the other half, I
needed to consult the GSIs, other students, or perform extensive online research
to assist me with the last parts. Some of the homework problems were clearly
inspired by Professor Wainwright's research papers, but I didn't have much
success translating from research paper to homework solution.

For me, some of the most challenging homework problems pertained to material
that wasn't in Wainwright's textbook. In part this is because some of the
problems in Wainwright's book have a similar flavor to exercises in the main
text of the book, which were often accompanied with solutions.


## The Final Exam

In one of the final lectures of the class, Professor Jordan talked about the
final exam --- that it would cover a range of questions, that it would be
difficult, and so forth --- but then he also mentioned that he could complete it
*in an hour*.  (Final exams in Berkeley are in three-hour slots.) While he
quickly added "I don't mean to disparage you...", unfortunately I found
the original comment about completing the exam in an hour quite disparaging. I'm
baffled by why professors say that; it seems to be a no-win solution for the
students. Furthermore, no student is going to question a Berkeley professor's
intelligence; I certainly wouldn't.

That comment aside, the final exam was scheduled to be Thursday at 8:00AM (!!)
in the morning. I was hoping we could keep this time slot, since I am a morning
person and if other students aren't, then I have a competitive advantage.
Unfortunately, Professor Jordan agreed with the majority in the class that he
hated the time, so we had a poll and switched to Tuesday at 3:00PM. Darn. At
least we know now that professors are often more lenient towards graduate
students than undergrads.

On the day of the final exam, I felt something really wrenching. And it wasn't
something that had to do with the actual exam, though that of course was also
"wrenching." It was this:

> It looked like my streak of having all professors know me on a first-name
> basis was about to be snapped. 

For the last *seven years* at Williams and Berkeley, I'm pretty sure I managed
to be known on a first-name basis to the professors from *all* of my courses.
Yes, all of them. It's easier to get to know professors at Williams, since the
school is small and professors often make it a point to know the names of every
student. At Berkeley it's obviously different, but graduate-level courses tend
to be better about one-on-one interaction with students/professors. In addition,
I'm the kind of student who frequently attends office hours. On top of it all,
due to my deafness, I get some form of visible accommodation, either captioning
(CART providers) or sign language interpreting services.

Yes, I have *a little bit* of an unfair advantage in getting *noticed* by
professors[^sadly], but I was worried that my streak was about to be snapped.
It wasn't for lack of trying; I had indeed attended office hours once with
Professor Jordan (who promptly criticized me for my lack of measure theory
knowledge) and yes, he was obviously aware of the sign language interpreters I
had, but as far as I can tell he didn't really *know* me.

So here's what happened just before we took the final. Since the exam was at a
different time slot than the "official" one, Professor Jordan decided to take
attendance.

My brain orchestrated an impressive mental groan. It's a pain for me to figure
out when I should raise my hand.  I did not have a sign language interpreter
present, because why? It's a three hour exam and there wouldn't be (well, there
better not be!) any real discussion. I also have bad memories because one time
during a high school track practice, I gambled and raised my hand when the team
captains were taking attendance ... only to figure out that the person being
called at that time had "Rizzuto" as his last name. Oops.

Then I thought of something. *Wait* ... why should I even raise my hand?  If
Professor Jordan knew me, then surely he would indicate to me in some way (e.g.
by staring at me). Furthermore, if my presence was that important to the extent
that my absence would cause a police search for me, then another student or TA
should certainly point me out.

So ... Professor Jordan took attendance. I kept turning around to see the
students who raised their hand (I sat in the front of the class. Big surprise!).
I grew anxious when I saw the raised hand of a student whose last name started
with "R". It was the moment of truth ...

A few seconds later ... Professor Jordan looked at me and checked something off
on his paper --- *without* consulting anyone else for assistance. I held my
breath mentally, and when another student whose last name was after mine was
called, I grinned.

My streak of having professors know me continues! Whew!

That personal scenario aside, let's get back to the final exam. Or, maybe not. I
probably can't divulge too much about it, given that some of the material might
be repeated in future iterations of the course. Let me just say two things
regarding the exam:

- Ooof. Ouch. Professor Jordan wasn't kidding when he said that the final exam
  was going to be difficult. Not a single student finished early, though some
  were no doubt quadruple-checking their answers, right?
- Professor Jordan wasn't kidding when he said that the class would be graded
  leniently.

I don't know what else there is to say.


## I am Dying to Know

Well, STAT 210B is now over, and in retrospect I am *really* happy I took the
course. Even though I know I won't be doing research in this field, I'm glad
that I got a taste of the research frontier in high-dimensional statistics and
theoretical machine learning. I hope that understanding some of the math here
can transfer to increased comprehension of technical material more directly
relevant to my research.

Possibly more than anything else, STAT 210B made me really appreciate the
enormous talent and ability that Professor Michael I. Jordan and Professor
Martin Wainwright exhibit in math and statistics. I'm blown away at how fast
they can process, learn, connect, and explain technically demanding material.
And the fact that Professor Wainwright wrote the textbook solo, and that much of
the material there *comes straight from his own research papers* (often
co-authored with Professor Jordan!) surely attests to why those two men are
award-winning statistics and machine learning professors.

It makes me wonder: *what do I lack compared to them*? I know that throughout my
life, being deaf has put me at a handicap, which my white male privilege (even
though I'm not white) can't completely overcome. But if Professor Jordan or
Professor Wainwright and I were to sit side-by-side and each read the latest
machine learning research paper, they would be able to process and understand
the material far faster than I could. Reading a research paper theoretically
means my disability shouldn't be a strike on me.

So what is it that prevents me from being like those two?

I tried doing as much of the lecture reading as I could, and I truly understood
a lot of the material. Unfortunately, many times I would get bogged down by some
technical item which I couldn't wrap my head around, or I would fail to fill in
missing steps to argue why some "obvious" conclusion is true. Or I would miss
some (obvious?) mathematical trick that I needed to apply, which was one of the
motivating factors for me writing [a lengthy blog post about these mathematical
tricks][3].

Then again, after one of the GSIs grinned awkwardly at me when I complained to
him during office hours about not understanding one of Professor Wainwright's
incessant "putting together the pieces" comment without any justification
whatsoever ...  maybe even advanced students struggle from time to time? And
Wainwright *does* have this to say in the first chapter of his book:

> Probably the most subtle requirement is a certain degree of mathematical
> maturity on the part of the reader. This book is meant for the person who is
> interested in gaining a deep understanding of the core issues in
> high-dimensional statistics. As with anything worthwhile in life, doing so
> requires effort. This basic fact should be kept in mind while working through
> the proofs, examples and exercises in the book.

(I'm not sure if a "certain degree" is a good description, more like "very high
degree" wouldn't you say?)

Again, I am dying to know: 

> What is the difference between me and Professor Jordan? For instance, when we
> each read Professor Wainwright's textbook, why is he able to process and
> understand the information at a much faster rate? Does his brain simply work
> on a higher plane?  Do I lack his intensity, drive, and/or focus? Am I
> inherently less talented?

I just don't know.


## Random Thoughts

Here are a few other random thoughts and comments I have about the course:

- The course had recitations, which are once-a-week events when one of the TAs
  leads a class section to discuss certain class concepts in more detail.
  Attendance was optional, but since the recitations conflicted with one of my
  research lab meetings, I didn't attend a single recitation. Thus, I don't know
  what they were like. However, future students taking 210B should at least
  attend one section to see if such sessions would be beneficial.

- Yes, I had sign language interpreting services, which are my usual class
  accommodations. Fortunately, I had a [consistent group][13] of two
  interpreters who attended almost every class. They were quite kind enough to
  bear through such technically demanding material, and I know that one of the
  interpreters was sick once, but came to work anyway since she knew that
  whoever would be substituting would be scarred to life from the class
  material. Thanks to both of you[^i_am_told], and I hope to continue working
  with you in the future!
  
- To make things easier for my sign language interpreters, I showed up early to
  every class to arrange two seats for them. (In fact, beyond the first few
  weeks, I think I was the first student to show up to every class, since in
  addition to rearranging the chairs, I used the time to review the lecture
  material from Wainwright's book.) Once the other students in the class got
  used to seeing the interpreters, they didn't touch the two magical chairs.

- We had a class Piazza. As usual, I posted way too many times there, but it was
  interesting to see that we had a lot more discussion compared to 210A. 

- The class consisted of mostly PhD students in statistics, mathematics, EECS,
  and mechanical engineering, but there were a few talented undergrads who
  joined the party.

## Concluding Thoughts

I'd like to get back to that Facebook discussion between Yann LeCun and Michael
I. Jordan in the beginning of his post. Professor Jordan's final paragraph was a
pleasure to read:

> Anyway, I keep writing these overly-long posts, and I've got to learn to
> do better. Let me just make one additional remark, which is that I'm really
> proud to be a member of a research community, one that includes Yann Le Cun,
> Geoff Hinton and many others, where there isn't just lip-service given to
> respecting others' opinions, but where there is real respect and real
> friendship.

I found this pleasing to read because I often find myself thinking similar
things. I too feel proud to be part of this field, even though I know I don't
have a fraction of the contributions of those guys. I feel
privileged[^privilege] to be able to learn statistics and machine learning from
Professor Jordan and all the other professors I've encountered in my education.
My goal is to become a far better researcher than I am now so that I feel like I
am giving back to the community. That's indeed one of the reasons why I started
this blog way back in August 2011 when I was hunched over my desk in the eighth
floor of a dorm at the University of Washington. I wanted a blog in part so that
I could discuss the work I'm doing and new concepts that I've learned, all while
making it hopefully accessible to many readers.

The other amusing thing that Professor Jordan and I have in common is that we
both write overly long posts, him on his Facebook, and me on my blog.  It's time
to get back to research.

***

[^interview]: This came out of [an interview that Professor Jordan had with IEEE
    back in 2014][7]. However, it didn't quite go as well as Professor Jordan
    wanted, and he criticized the title and hype (see the featured comments
    below at the article).

[^schmidhuber]: The other two are Geoffrey Hinton and Yoshua Bengio. Don't get
    me started with Jürgen Schmidhuber, though he's admittedly a clear fourth.

[^last_day]: Also on the last day, just before we gave him an applause for the
    class, he said he often sits down in classes just to learn more and to try
    and see what's worth investigating rather than following the hype. (He
    didn't specify the hype, but I know what he meant.) "Never stop learning,"
    he said. I know it's a cliche, but he is right. I will heed his advice.

[^sadly]: Sadly, this "unfair advantage" has not translated in "getting noticed"
    in other respects, such as friendship, dating, and so forth.

[^i_am_told]: While I don't advertise this blog to sign language interpreters, a
    few years ago one of them said that there had been "some discussion" of my
    blog among her social circle of interpreters. Interesting ...

[^privilege]: Even though that word has gotten a bad rap from the Social Justice
    Warriors, it's the right word here.


[1]:https://people.eecs.berkeley.edu/~jordan/
[2]:https://danieltakeshi.github.io/2016/12/20/review-of-theoretical-statistics-stat-210a-at-berkeley/
[3]:https://danieltakeshi.github.io/2017/05/06/mathematical-tricks-commonly-used-in-machine-learning-and-statistics
[4]:https://danieltakeshi.github.io/2017/04/22/following-professor-michael-jordans-advice-your-brain-needs-exercise
[5]:https://www.facebook.com/yann.lecun/posts/10152348155137143
[6]:https://www.reddit.com/r/MachineLearning/comments/2fxi6v/ama_michael_i_jordan/
[7]:http://spectrum.ieee.org/robotics/artificial-intelligence/machinelearning-maestro-michael-jordan-on-the-delusions-of-big-data-and-other-huge-engineering-efforts
[8]:https://en.wikipedia.org/wiki/Ronald_Reagan
[9]:http://civilization.wikia.com/wiki/Gandhi_(Civ4)
[10]:https://stanford.edu/class/stats311/
[11]:https://danieltakeshi.github.io/2017/05/19/understanding-deep-learning-requires-rethinking-generalization-my-thoughts-and-notes
[12]:https://simplystatistics.org/2014/08/18/interview-with-copss-award-winner-martin-wainright/
[13]:https://danieltakeshi.github.io/2015-10-31-the-benefits-of-having-the-same-group-of-interpreters/
