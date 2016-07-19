---
layout: post
title:  "Review of Deep Reinforcement Learning (CS 294-112) at Berkeley"
date:   2015-12-17 23:59:00
author: Daniel Seita
permalink: 2015-12-17-review-of-deep-reinforcement-learning-cs-294-112-at-berkeley/
---

**Update July 18, 2016**: This post seems to have gotten a considerable amount of attention, at
least compared to my normal blog posts, so I would like to answer some of the common questions that
I've received in either the comments or by private email.

1. If you're looking for homework assignments, I first want to warn you that, as I emphasize in the
my review, the assignments are probably not going to be as educational as you would want them to be.
If you're still interested, our TA for the class [posted a github repository on the Berkeley RLL][1]
page with the homework for this class. The homeworks are iPython notebooks (now called Jupyter
notebooks, I think). If there's code in the "YOUR CODE HERE" sections, then you're probably reading
the solutions; I'm not sure if there's a clean version of the assignments there.

2. Unfortunately, we did not have any video lectures, slides, or readings outside of what you can
see on the class website. A note for those who are reading the comments after this update: the class
website was originally pulled down due to "some tyrants" (according to the course staff), but it's
happily now up.

3. If you're looking for other resources to learn about deep reinforcement learning, I have several
recommendations. In terms of courses, check out [David Silver's reinforcement learning course][4]
and the recent [Machine Learning Summer School][8]; the latter had our class instructor as part of the course
staff, so the material is probably going to be similar to what we covered. (Coming up in a few weeks
is the [Deep Learning Summer School][5], something you might also want to check out.) I have all these courses
bookmarked and am trying to carve out some time to read the slides. In terms of code, I would
strongly recommend starting with either [the deep_q_rl library][3] or [OpenAI Gym][7]. The former is
a super easy-to-read Python library that allows you to replicate DeepMind's results in their 2013
and 2015 papers on Atari games. The latter was recently launched, and I don't have experience with
it, but it sounds really cool as we can compare our reinforcement learning implementations.

4. This is more of a comment than an answer, but I thought I'd mention it anyway: my blog's comments
are handled by Disqus, and in the moderation panel I can see the emails of the commenters. Thus,
there is no need to post your email publicly as I can see it regardless.

Thanks everyone, and that's all! After this paragraph is the original post as I had written it. But
one more thing: after rereading this post, I think I was a little too harsh on the class.
Furthermore, even though people have said they liked this post, I don't think I gave reinforcement
learning its due. So to rectify my regrets, **I'm planning on launching a new series of deep
reinforcement learning posts on this blog**, similar to the style of [Andrej Karpathy's excellent
blog post][6]. I've [already written a post on basic reinforcement learning][2], so I'm hoping to
progress towards more advanced topics. My goal is to have the first post up sometime in August.
Hopefully those will be a good resource for some enthusiasts out there.

***

At the start of the semester, [Pieter Abbeel](http://www.cs.berkeley.edu/~pabbeel/) told me, "If you
want to know more about the work we do, take the deep reinforcement learning class."

"Which course is that? The one taught by John?" I asked.

"Yes, take that." Pieter said. "Hope to see you there."

I somewhat reluctantly agreed to join late, knowing that I had missed the first two lectures, and
furthermore, that I would have to sit through the first one I *did* attend without sign language
interpreting. In retrospect, however, interpreting services provided the *least benefit* for me in
this class compared to *any other class I had ever taken*. Given my history of taking highly
technical, difficult-to-interpret courses, that's saying a lot!

So what was this course? It was a new two-credit class called [Deep Reinforcement Learning (CS
294-112)](http://rll.berkeley.edu/deeprlcourse/) and taught by Pieter's graduate student, [John
Schulman](http://www.eecs.berkeley.edu/~joschu/).  It seemed like a cross between a research seminar
and a normal lecture course. The former tend to be one or two credits and are principally about
relevant research results; the latter tend to be three or four credits and have lectures, homeworks,
exams, and projects.

In AI and robotics, reinforcement learning is a standard way of framing a problem. For example, if a
robot needs to learn how to play a game, it must engage in "reinforcement learning" to try out
different actions, get rewards, and then modify its policy. The word "deep" refers to how *deep
neural networks* have recently become the workhorse of state-of-the-art reinforcement learning.
(This is why the class wasn't taught until now.) The broader category of *deep learning* involves
the use of deep neural networks in other applications, such as image classification and speech
recognition.  Deep learning has become so popular that Google even paid $400 million to buy a deep
learning company, [DeepMind](http://deepmind.com/).

The class had about eighty students, so to avoid getting into trouble with the building managers
about stuffing too many people in one room, John gave two identical lectures for each class day. I
remained in the afternoon session to make it easy on the interpreters' schedules, but unfortunately,
most of the other students picked the afternoon session, but hey, they don't have my excuse ...
perhaps they can't wake up early?  So *once again*, a graduate level class had some of its students
sitting on the floor.  Seems like that's a
[common](http://danieltakeshi.github.io/2014/12/30/review-of-statistical-learning-theory-cs-281a-at-berkeley/)
[problem](http://danieltakeshi.github.io/2015-05-31-review-computer-vision-berkeley/) here, huh?

Anyway, back to the class discussion. The first few lectures were about Markov Decision Processes
and neural networks, so if there were *any* classes to miss, it would be those because I already
knew the material.

The remaining lectures were, to be frank, difficult, and I often felt mentally stressed in class.
Most of the content was pure math, and the derivations were a long sequence of sums, expectations,
and other terms, each of which were *more* sums and expectations. For instance, look at the formula
for *policy gradients*:

$$g = \mathbb{E}\left[\sum_{t=1}^T \Psi_t \nabla_\theta \log \pi_\theta (a_t \mid s_t)\right]$$

To understand this, one has to process lots of material, such as what it means to take the gradient
of the log of a policy, and that $$\Psi_t$$ isn't just a simple scalar but can represent concepts
like the advantage function, which involves *another* sequence of expectations and sums of rewards.
Connecting this material is challenging in real time, and I felt that the lectures did not provide
sufficient intuition. My sign language interpreters tried to repeat the exact words John uttered,
but despite this, I could not translate this process into clear mathematical comprehension.

Given that the lectures were difficult for me to follow, I hoped that homeworks would be more
useful. The homeworks in this class were provided as IPython/Jupyter notebooks. We had starter code
and needed to fill in the "YOUR CODE HERE" sections.

The first homework was nearly trivial for people who knew about the basics of Markov Decision
Process, Value Iteration, Policy Iteration, and Q-Learning. I wrote about thirty lines of Python
code for the entire assignment.

The second homework, on policy gradients, was more interesting, but the release date kept getting
postponed. It soon became a running joke in class whenever John said: "Oh, and about that second
homework, we plan to release it in a few days...". It was finally released on October 11. (John on
Piazza: "You may have given up hope that this day would ever come, but behold, HW2 is finally
here.") To put this in perspective, the first homework assignment was *due* on September 7.

Fortunately, the second assignment was more challenging than the first, and I had to be careful in
implementing formulas since math from research papers doesn't always translate neatly into code.  I
was pleased to see that the homework was designed so naive implementations of formulas would take
too long to test. (I believe AI assignments should require code to be reasonably optimized.)

We were going to have homeworks on approximate dynamic programming and supervised learning, but
since the second homework got delayed so much and the third one would have taken too long to create,
the staff canceled all future assignments.

To be honest, the main deep reinforcement learning material I learned this semester *didn't even
come from this class*. In Pieter's Advanced Robotics (CS 287) class, which I also took this
semester, my final project was about deep learning for Atari games. I had time to sufficiently read
and absorb the Atari deep learning research papers, which helped me to better understand some of the
material in this class (CS 294-112). Consequently, my recommendation for someone who wants to take
this class in the future is to, if possible, take CS 287  concurrently and do a project that uses
neural networks. That way, one gets to *do* deep reinforcement learning.

To recap, here are some of the positive aspects of the class:

- It covers a popular and interesting research area.
- It presents many relevant research papers, including those from Berkeley students.
- For a class that is almost like a research seminar, there are many online resources one can
  consult for additional background. Unfortunately, a lot of the written references are *also* hard
  to understand.
- It is easy to obtain homework help on Piazza.

Here are some of the negative ones:

- The lectures were not polished and involved lots of math without intuition. This issue is
  understandable because it was a first time course taught by a graduate student.
- There did not seem to be much advance preparation for the course in terms of lecture material. The
  course website had a brief outline of lectures, but we had to change some of that on short notice.
- It did not provide sufficiently many or sufficiently difficult homework assignments. Having more
  in-depth assignments would let me deeply reinforce my understanding (pun **fully** intended).

Ultimately, this course allowed me to scratch the surface of deep reinforcement learning, though it
was immensely frustrating for me to try and understand the material directly from the lecture, and
the haphazard nature of the course did not help.  I suspect that future iterations of the course
will proceed more smoothly, and yes, even though no one's told me personally, this class *will* be
offered again (in some form) so long as deep learning remains the king of machine learning. 

[1]:https://github.com/rll/deeprlhw2
[2]:http://danieltakeshi.github.io/2015-08-02-markov-decision-processes-and-reinforcement-learning/
[3]:https://github.com/spragunr/deep_q_rl
[4]:http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching.html
[5]:https://sites.google.com/site/deeplearningsummerschool2016/home
[6]:http://karpathy.github.io/2016/05/31/rl/
[7]:https://gym.openai.com/
[8]:http://learning.mpi-sws.org/mlss2016/
