---
layout: post
title:  "Review of Convex Optimization and Approximation (EE 227C) at Berkeley"
date:   2016-05-21 10:00:00
permalink: 2016-05-21-review-of-convex-optimization-and-approximation-ee-227c-at-berkeley/
---

This past semester, I took Convex Optimization and Approximation (EE 227C). The name of the course
is slightly misleading, because it's not clear why there should be the extra "and approximation"
text in the course title. Furthermore, EE 227C is not really a continuation of [EE 227B][2][^still]
since 227B material is not a prerequisite. Those two classes are generally orthogonal, and I would
*almost* recommend taking then in the reverse order (EE 227C, then EE 227B) if one of the midterm
questions hadn't depended on EE 227B material. More on that later.

Here's the [course website][3]. The professor was Ben Recht, who amusingly enough, calls the course
a different name: "Optimization for Modern Data Analysis". That's probably more accurate than
"Convex Optimization and Approximation", if only because "Convex Optimization" implies that
researchers and practitioners are dealing with convex functions. With neural network optimization
being the go-to method for machine learning today, however, the loss functions in reality are
*non-convex*. EE 227C takes a broader view than just neural network optimization, of course, and
this is reflected in the main focus of the course: *descent algorithms*.

Given a convex function $$f : \mathbb{R}^n \to \mathbb{R}$$, how can we find the $$x \in
\mathbb{R}^n$$ that minimizes it?  The first thing one should think of is the gradient descent
method: $$x_{k+1} = x_{k} - \alpha \nabla f(x_k)$$ where $$\alpha$$ is the step size. This is the
most basic of all the descent methods, and there are tons of variations of it, as well as similar
algorithms and/or problem frameworks that use gradient methods. More generally, the idea behind
descent methods is to iteratively update our "point of interest", $$x$$, with respect to some
function, and stop once we feel close enough to the optimal point. Perhaps the "approximation" part
of the course title is because we can't usually get to the optimal point of our problem. On the
other hand, in many practical cases, it's not clear that we *do* want to get the absolute optimal
point. In the real world, $$x$$ is usually a parameter of a machine learning model (often written
as $$\theta$$) and the function to minimize is a loss function, showing how "bad" our current model
is on a given training data. Minimizing the loss function perfectly usually leads to overfitting on
the test data.

Here are some of the most important concepts covered in class that reflect the enormous breadth of
descent methods, listed roughly in order of when we discussed them:

- **Line search**. Use these for tuning the step size of the gradient method. There are two
  main ones to know: exact (but impractical) and backtracking ("stupid," according to [Stephen
  Boyd][7], but practical).

- **Momentum and accelerated gradients**. These add in extra terms in the gradient update to
  preserve "momentum", the intuition being that if we go in a direction, we'll want to "keep the
  momentum going" rather than throwing away information from previous iterations, as is the case
  with the standard gradient method. The most well-known of these is Nesterov's method: $$x_{k+1} =
  x_k + \beta_k(x_k - x_{k-1}) - \alpha_k \nabla f(x_k + \beta_k(x_k - x_{k-1}))$$.

- **Stochastic gradients**. These are when we use approximations of the gradient that match in
  expectation. Usually, we deal with them when our loss function is of the form $$f(x) =
  \frac{1}{n}\sum_{i=1}^nf_i(x)$$, where each $$f_i$$ is a specific training data example. The
  gradient of $$f$$ is the gradient of the individual terms, but we can use a random subset each
  iteration and our performance is just as good and much, much faster.

- **Projected gradient**. Use these for constrained optimization problems, where we want to find a
  "good" point $$x$$, but we have to make sure it satisfies the constraint $$x \in \Omega$$ for some
  space $$\Omega$$. The easiest case is when we have component-wise linear constraints of the form
  $$a \le x_i \le b$$. Those are easy because the projection is as follows: if $$x_i$$ exceeds the
  range, either decrease it to $$b$$, or increase it to $$a$$, depending on which case applies.

- **Subgradient method**. This is like the gradient method, except this time we use a *subgradient*
  rather than a gradient. It is *not* a descent direction, so perhaps this shouldn't be in the list.
  Nonetheless, the performance in practice can still be good and, theoretically, it's not much worse
  than regular stochastic gradient.

- **Proximal point**. To me, these are non-intuitive. These methods combine a gradient step with a
  *proximal* method. They also perform a projection.

Then later, we had special topics, such as Newton's method and zero-order derivatives (a.k.a.,
finite differences). For the former, quadratic convergence is nice, but the method is almost useless
in practice.  For the latter, we can use it, but avoid if possible.

As mentioned earlier, Ben Recht was the professor for the class, and this is the second class he's
taught for me (the first being [CS 281A][1]) so by now I know his style well.  I generally had an
easier time with this course than CS 281A, and one reason was that we had typed-up lecture notes
released beforehand, and I could read them in great detail. Each lecture's material was contained in
a 5-10 page handout with the main ideas and math details, though in class we didn't have time to
cover most proofs. The notes had a substantial amount of typos (which is understandable) so Ben
offered extra credit for those who could catch typos. Since "catching typos" is one of my areas of
specialty (along with "reading lecture notes before class") I soon began highlighting and posting on
Piazza all the typos I found, though perhaps I went overkill on that.  Since I don't post
anonymously on Piazza, the other students in the class also probably thought it was
overkill[^extra].

The class had four homework assignments, all of which were sufficiently challenging but certainly
doable. I reached out to a handful of other students in the class to work together, which helped. A
fair warning: the homeworks also contain typos, so be sure to check Piazza. One of the students in
class told me he didn't know we had a Piazza until after the second homework assignment was due, and
that assignment had a notable typo; the way it was originally written meant it was unsolvable.

Just to be clear: I'm not here to criticize Ben for the typos. I think it's actually a good thing,
because he has to start writing these lecture notes and assignments from scratch. This isn't one of
those courses that's been taught every year for 20 years and where Ben can reuse the material. The
homework problems are also brand new questions; one student who took EE 227C last spring showed me
his assignments which were vastly different.

In addition to the homeworks, we had one midterm just before spring break. It was a 25.5-hour take
home midterm, but Ben said students should be able to finish the midterm in two hours. To state my
opinion: while I agree that there are students in the class who can finish the midterm in less than
two hours, I don't think that's the case for the majority of students. At least, it wasn't for *me*
--- I needed about six hours --- and I got a good score. The day we got our midterms back, Ben said
that if we got less than an 80 on the midterm, we shouldn't talk to him to "complain about our
grades."

Incidentally, the midterm had four questions. One question wasn't even related to the material that
much (it was about critical points) and another was about duality and Lagrange multipliers, so that
probably gave people like me who took EE 227B an advantage (these concepts were not covered much in
class).  The other two questions were based more on stuff directly from lecture.

The other major work component of EE 227C was the usual final project for graduate-level EE and CS
courses.  I worked on "optimization for robot grasping", which is one of my ongoing research
projects, so that was nice. Ben *expects* students to have final projects that coincide with their
research. We had a [poster session rather than presentations][8], but I managed to survive it as
well as I could. 

My overall thought about the class difficulty is that EE 227C is slightly easier than EE 227B,
slightly more challenging than CS 280 and CS 287, and around the same difficulty as CS 281A. 

To collect some of my thoughts together, here are a few positive aspects of the course:

- The material is interesting both theoretically and practically. It is heavily related to machine
  learning and AI research.
- Homework assignments are solid and sufficiently challenging without going overboard.
- Lecture notes make it easy to review material before (and after!) class.
- The student body is a mix of EE, CS, STAT, and IEOR graduate students, so it's possible to meet
  people from different departments.

Here are the possibly negative aspects of EE 227C:

- We had little grading transparency and feedback on assignments/midterms/projects, in part because
  of the relatively large class (around 50 students?) and only one GSI. But it's a graduate-level
  course and my GPA almost doesn't matter anymore so it was not a big deal to me.
- We started in Etcheverry Hall, but had to move to a bigger room in Donner Lab (uh ... where is
  that?!?) when more students stayed in the class than expected. This move meant we had to sit in
  cramped, auditorium-style seats, and I had to constantly work to make sure my legs didn't bump
  into whoever was sitting next to me. Am I the only one who runs into this issue?
- For some reason, we also ended class early a lot. The class was listed as being from 3:30-5:00PM,
  which means in Berkeley, it goes from 3:40-5:00PM. But we actually ran from 3:40-4:50PM,
  especially near the end of the semester. *Super* Berkeley time, maybe?

To end this review on a more personal note, convex optimization was one of those topics that I
struggled with in undergrad. At Williams, there's no course like this (or EE 227B ... or even EE
227A!![^liberalarts]) so when I was working on my undergraduate thesis, I never deeply understood
all of the optimization material that I needed to know for my topic, which was about the properties
of a [specific probabilistic graphical model architecture][5]. I spent much of my "learning" time on
Wikipedia and reading other class websites. After two years in Berkeley, with courses such as CS
281A, CS 287, EE 227B, and of course, this one, I *finally* have formal optimization education, and
my understanding of related material and research topics has vastly improved.  On our last lecture,
I asked Ben what to take after this. He mentioned that this was a terminal course, but the closest
would be a Convex *Analysis* course, as taught in the math department. I checked, and Bernd
Sturmfels's [Gemoetry of Convex Optimization][4] class would probably be the closest, though it
looks like that's not going to be taught for a while, if at all.  In the absence of a course like
that, I'm probably going to shift gears and take classes in different topics, but optimization was
great to learn. I honestly felt like I enjoyed this course more than any other in my time at
Berkeley.

Thanks for a great class, Ben!

***

[^still]: For some reason, Convex Optimization is *still* called EE 227BT instead of EE 227B. Are
    Berkeley's course naming rules really that bad that we can't get rid of the "T" there?

[^liberalarts]: One of the odd benefits of graduate school is that I can easily rebel against my
    liberal arts education.
 
[^extra]: I'm not even sure if I got extra credit for those.

[1]:http://danieltakeshi.github.io/2014/12/30/review-of-statistical-learning-theory-cs-281a-at-berkeley/
[2]:http://danieltakeshi.github.io/2015-12-22-review-of-convex-optimization-ee-227bt-at-berkeley/
[3]:http://www.eecs.berkeley.edu/~brecht/eecs227c.html
[4]:https://math.berkeley.edu/~bernd/math275old.html
[5]:http://research.microsoft.com/en-us/um/people/hoifung/papers/poon11.pdf
[6]:http://caffe.berkeleyvision.org/
[7]:http://stanford.edu/~boyd/index.html
[8]:http://danieltakeshi.github.io/2015-12-25-for-final-projects-class-presentations-are-better-than-poster-sessions/
