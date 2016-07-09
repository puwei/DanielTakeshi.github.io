---
layout: post
title:  "Review of Applications of Parallel Computing (CS 267) at Berkeley"
date:   2016-05-27 10:00:00
permalink: 2016-05-27-review-of-applications-of-parallel-computing-cs-267-at-berkeley/
---

Last semester, I took [Applications of Parallel Computing (CS 267)][1], taught by Jim Demmel. This
is one of those graduate courses that we can expect will be offered every year for the near future.
In fact, CS 267 has been offered *almost every year since 1994*, and strangely enough, it seems to
have always been in the spring semester. Amazingly, [the website for the 1994 class is still
active][4]!

The reason why CS 267 continues to be offered is because parallel programming has become more
important recently. I can provide two quick, broad reasons why: because virtually *all* computers
nowadays are parallel (i.e., have parallel processors), and because [Moore's Law][9][^moores] has
[started to slow down][10], so that future speed-ups will not "come for free" as it did with Moore's
Law, but will come with *parallelism*. But parallelizing existing code is hard.  Hence why this
class exists.

CS 267 is aimed at a broad audience, so the student body is *very* diverse. There are computer
scientists of course, but also mechanical engineers, environmental engineers, bioengineers,
political scientists, etc. The slides on the first day of class said that we had 116 (yes, 116, you
can tell how popular things are getting) students enrolled, including 16 undergrads and 64 EECS
students. Computer scientists, especially those in graphics/AI/theory like to take this course to
fulfill prelim breadth requirements. See the following screenshot for why:

<img src="{{site.url}}/assets/prelim_courses.png" alt="course_requirements">

We have to take at least one course in three out of the six areas above, with one "above the line"
and one "below the line." CS 267 is in the "Programming" category and "below the line," making it a
good match for AI people, which is why you see a lot of those in the class. Incidentally, our
"Homework 0" was to write a short summary about ourselves, and these were posted on the website. I
wish more classes did this.

Due to its popularity, CS 267 has video lectures. I [talked about this earlier][3] when I explained
why I didn't show up to lectures. (Actually, I'm still catching up on watching the video lectures
... sorry.) Fortunately, the captioners did a better job than I expected with getting captions on
the videos.

Regarding the workload in the class, there were four main things: three homeworks and a final
project.

**Homework 1: Optimize Matrix Multiplication**. We had to implement [matrix multiplication][6]. We
were judged by the speed of $$C = AB$$ for dense, random matrices $$A$$ and $$B$$, on a nearby
supercomputer. The naive $$O(n^3)$$ algorithm is easy to describe and implement, but is unacceptably
slow. To speed it up, we had to use low-level techniques such as compiler intrinsics, loop
unrolling, blocking, etc. The thing I probably learned the most out of this assignment is how to use
these operations to make better use of the cache. I also credit this assignment for giving me a
glimpse into how real, professional-grade matrix libraries work. We had assigned teams on this
homework; the course staff paired us up based on a course survey. It's probably best to say you're a
bad C programmer in the survey so you can get paired up with an "expert".

**Homework 2: Parallelize Particle Simulation**. It's helpful to look at the GIF of the particle
simulation:

<p style="text-align:center;">
<img src="{{site.url}}/assets/cs267_animation.gif" alt="animation">
</p>

This is implemented by having an array of particles (which themselves are C structs). During each
iteration, the particle positions are updated based on simple forces that cause particles to repel.
We were provided an $$O(n^2)$$ serial (i.e., not parallel) implementation, where $$n$$ is the number
of particles. This assignment involved four parts: implementing (1) an $$O(n)$$ serial version, (2)
an $$O(n)$$ OpenMP version (i.e., shared memory), (3) an $$O(n)$$ MPI version (i.e., distributed
memory), and (4) an $$O(n)$$ GPU-accelerated version.  For this assignment, obviously do (1) first,
since the others are based on that. But don't use linked lists, which I tried in my first version.
For (2), OpenMP isn't as hard as I thought, and most of it involves adding various ```pragma omp```
statements before for loops. For (3), MPI can be challenging, so do yourself a favor and [read these
excellent blog posts][2]. For (4) ... unfortunately, one of my partners did that, not me.  I did
(1), (2), and (3), but I wish I had done some GPU coding.

**Homework 3: Parallelize Graph Algorithms**. We needed to parallelize de Novo Gene Assembly. No
biology background is needed, because the assignment description is self-contained. Our job was to
parallelize their provided serial algorithm, which constructs and traverses over something called a
*De Brujin graph*. We had to use an [extension of the C language called UPC][8], developed by
researchers here in Berkeley, but fortunately, it's not that much more complicated than MPI, and
there are some guides and long presentation slides online that you can read and digest. UPC tries to
provide both shared and distributed memory, which can be a little hard to think about, so you really
want to make sure you know exactly what kind of data is being transferred when you write UPC
statements. Don't assume things work as you expect!
 
For all three assignments, a write-up is needed, so be sure to have time before the deadline to
write it. In terms of debugging, my best advice is to keep running the code with a bunch of
```printf(...)``` statements.  Sorry for lack of better ideas. But a fair warning --- there's a
limit to how often we can use the supercomputer's resources! This is something I wish the course
staff had clarified *early* in the semester, rather than waiting until a few people had exceeded
their quotas.

**Final Projects**. As usual, we had final projects. Our format was somewhat unusual, though: we
gathered in the Wozniak Lounge from 8:10AM to 11:00AM (early for some people, but not for me). The
first half of this time slot consisted of a series of 1.5-minute presentations. For my talk, I
discussed an ongoing research project about parallel Gibbs sampling, but my slide probably had too
much stuff in it for a 1.5-minute talk. (I also didn't realize how low the screen resolution would
be until the presentation date.) I was tempted to add some humor by starting out with one separate
slide that said "MAKE GIBBS SAMPLING GREAT AGAIN", but for some reason I decided against it. Perhaps
that was mistaken, since I think the presentations could have been a little funnier. After this, we
had the usual poster session.

Overall, I wouldn't say that CS 267 is among the more challenging CS courses[^assignments], but it
can be difficult for those with limited C programming experience. Some students, especially
undergrads, might be somewhat annoyed at the lack of grading information, because we didn't get
grades on our final project, and I don't even know what grade I got on the third homework. The
grading is lenient as usual, though, so I wouldn't worry much about it. Also, during the homeworks,
it can be easy to not do much work if you rely on your partners; don't do that! You get more out of
the class if you take the lead on the homeworks and do as much as you can.

***

[^moores]: Roughly speaking, Moore's Law states that the number of transistors in an integrated
    circuit increases at a fixed rate, usually stated as doubling every 1.5 years.
 
[^assignments]: I'm talking about the assignments here, not the lectures. The assignments are
    generally doable, but the lectures are impossible to follow.

[1]:http://www.cs.berkeley.edu/~demmel/cs267_Spr16/
[2]:http://mpitutorial.com/
[3]:http://danieltakeshi.github.io/2016-02-05-why-i-reluctantly-dont-show-up-to-class/
[4]:http://people.eecs.berkeley.edu/~demmel/cs267/
[5]:http://danieltakeshi.github.io/2015-09-01-my-prelims/
[6]:https://en.wikipedia.org/wiki/Matrix_multiplication
[7]:http://people.eecs.berkeley.edu/~mme/cs267-2016/hw1/index.html
[8]:http://upc.lbl.gov/
[9]:https://en.wikipedia.org/wiki/Moore%27s_law
[10]:http://www.nature.com/news/the-chips-are-down-for-moore-s-law-1.19338
