---
layout: post
title:  "Review of Convex Optimization (EE 227BT) at Berkeley"
date:   2015-12-22 23:59:00
permalink: 2015-12-22-review-of-convex-optimization-ee-227bt-at-berkeley
---

The third class I took this semester was Convex Optimization (EE 227BT), which was also my first
time wading into electrical engineering.  There are three convex optimization courses at Berkeley:
EE 227A, EE 227B, and EE 227C. (Note: I say 227BT in this title because the course had a "T" for
"Temporary," but that should go away soon.) I did not take the first course, EE 227A, and I think
that may have been a reason for my struggles in this class.

To do well in EE 227B, I think one needs to be highly skilled in the following two areas: linear
algebra and problem solving. If a student lacks one or both of these skills, he or she is in
serious trouble. For a linear algebra concept, consider this problem: $$\max_{\{x : \|x\|_2=1\}}
x^TAx$$ for symmetric $$A$$. We encountered this at the start of the semester and would see it *over
and over again*.  The professor, [Laurent El Ghaoui][4], said: "If you didn't immediately know that
the answer to this was the maximum eigenvalue of $$A$$, or $$\lambda_{\max}(A)$$, then run away to
EE 227A. This is all linear algebra." I *did* know that, in fact, but the class material was
nonetheless very difficult for me to understand.

We had five problem sets, and I think they were among the hardest ones I've ever had, and also more
challenging than [those from CS 281A][1]. After spending 30 to 40 hours on the first few homeworks,
I realized I needed to seriously start reaching out to other students to get more than two-thirds of
the homework done correctly, and I [*did* do that this semester][3].

Each problem set contained three to five questions, each of which had some number of sub-problems.
Their difficulty varied considerably, with some parts following directly from the definition of
Cauchy-Schwarz, $$x^Ty \le \|x\|_2\|y\|_2$$ (*not* Cauchy-Schwartz ... I don't know why people keep
misspelling that), and others requiring some ridiculously complicated insights. The hardest one was
to prove Theorem 4 and Corollary 3 from Laurent's paper [Sparse Learning via Boolean
Relaxations][5]. Yes, we had to do that, and no, we were not given this paper reference and had to
start some of that from scratch. I found out about this paper from another student.  Also, the paper
was published in 2015, so it must have been difficult since no one else did this until now.  Setting
the boolean relaxation problem aside, the homework questions were challenging but doable with some
problem solving insights (one might need help for these, though), and they were *brutally
educational*. 

In terms of homework *logistics*, we had a paid grader who graded the homeworks, which is different
from the previous iteration of the course (Fall 2014) when students had to *self-grade* their
submissions. Note that Laurent's EE 227BT website is (currently) incorrect; I think he recycles the
same links for his classes, so some of it is out of date for the Fall 2015 edition. Our grader was
surprisingly generous with points but did not offer detailed feedback and also took three or four
weeks before providing grades. In part, this was because of the large class size. We had perhaps
eighty students at the start before setting to fifty or sixty. 

One of the "less-awesome" aspects of this class, in my opinion, was that we barely followed the
projected outline. We were *supposed* to get five homework assignments, released every other
Thursday, which meant we would get two weeks to do each assignment. However, because the lectures
quickly fell behind from the outline, Laurent delayed the second homework by a week, which caused a
few more subsequent delays for other assignments. This meant that homeworks eventually spilled over
into time that was originally designated for us to do final project work. I think it would be best
to design homeworks conservatively so that even if the lectures get delayed, there's no need to put
off the homework due dates.

We had a midterm, but that was *also* delayed, by a week. It was in-class for 80 minutes, open note
(but not open laptop or Internet). It had three questions, each with multiple parts, and was out of
40 points total. Judging from the distribution of scores, I think most students got somewhere
between 15 and 30 points. It was definitely a challenging midterm, but in retrospect, I thought it
was *fair*, and was of higher quality compared to the [CS 280 midterm][2].

The third part of our grade was based on the final project. We started final project discussions
*really early*, in September! Almost from the beginning, Laurent designed lectures so that we would
cover standard concepts (e.g., Lagrange duality) for 75 minutes, and then the last 5 minutes would
be an open discussion of final project ideas. Despite the early focus of final projects in the
lectures, in reality we didn't have *that* much time to work on them due to the homeworks and
midterm getting delayed and cutting into project time. I think the course staff should address this
in future iterations of the course.

I worked in a group of four in my final project, where we investigated various properties of neural
networks. We read a lot of research papers (the "literature review" that Laurent kept saying in
lecture) and ran experiments using CAFFE and CVX. We wrote this up in a forty-page final project
report. Going through and editing that at the end was a lot of work! A quick warning to future
students: the project report date was set *before* RRR week, which I think is unusual for most
graduate courses, which allow students to work on reports through mid-December.

In addition to a report, we had project *presentations*, which I was happy about since it's fun to
give talks. Not all students would agree with me. During the presentations, my sign language
interpreters would comment on some of the students who appeared to be really nervous. To make
matters worse, Laurent brought a hand-held microphone to the class, and about half of the students
*actually held the microphone when they were talking*. No, I'm serious! And it's not like we were on
stage at Broadway --- we were in a normal-sized classroom!  I don't like holding a microphone
because *it would make it completely obvious to the rest of the class that I was nervous about
public speaking*!  I think Laurent had good intentions about bringing the microphone, but to future
students, please don't use microphones when talking.

When it was my turn to present, I put the microphone away after someone handed it to me (sorry, not
using it!) and immediately started off with a planned joke. I told the class to pretend that Laurent
and I were "trapped in a world that represents the loss function of the neural network." (Don't ask
why!) I continued the story: I led Laurent to a *local* minimum, but he got angry and wanted the
*global* minimum. I calmly responded that local minima are just as good as the global minimum in
neural networks. I added a little acting and tried to cleverly alter my tone of voice. The class
roared in laughter, and I think that was probably the most successful joke I have ever pulled off in
a class presentation.

To wrap up my thoughts on EE 227B, I think it is similar to most classes I've taken in the sense
that it is *challenging*, but very *educational*. I now feel like I have a much better understanding
of concepts in linear algebra, especially those about norms, eigenvectors, and matrix decomposition.
Many students who take this course do research in Artificial Intelligence fields, and EE 227B
enables students to read AI research papers without getting bogged down by the notation and
definitions.  This was a *huge* problem for me when I first started to read machine learning papers
a few years ago. I couldn't even consistently remember what $$\|x\|$$ meant! Thanks to EE 227B, and
some of my own independent linear algebra studying, I've cleared a lot of that initial "notation
hurdle".

Finally, to future students who are considering this class, the best advice I have is to make sure
that your linear algebra skills are sharp. In particular, be sure you know about matrix norms,
eigenvectors, and other forms of matrix decomposition (e.g., Singular Value Decomposition).

If you're weak in those areas, then in the words of Laurent, "run away to EE 227A."

[1]:http://danieltakeshi.github.io/2014/12/30/review-of-statistical-learning-theory-cs-281a-at-berkeley/
[2]:http://danieltakeshi.github.io/2015-05-31-review-computer-vision-berkeley/
[3]:http://danieltakeshi.github.io/2015-11-21-thoughts-on-isolation-how-often-do-students-work-together-on-homework/
[4]:http://www.eecs.berkeley.edu/~elghaoui/
[5]:http://www.eecs.berkeley.edu/~elghaoui/Pubs/SparseLearningBoolean.pdf
