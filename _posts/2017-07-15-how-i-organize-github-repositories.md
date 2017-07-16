---
layout:     post
title:      "How I Organize My GitHub Repositories"
date:       2017-07-15 21:00:00
permalink:  2017/07/15/how-i-organize-my-github-repositories/
---

I've been putting more of my work-related stuff [in GitHub repositories][1] and
by now I have more or less settled on a reasonable workflow for utilizing
GitHub. For those of you who are new to this, GitHub helps us easily visualize
and share *code repositories* online, whether in public (visible to everyone) or
private (visible only to those with permissions), though technically
repositories don't have to be strictly code-based. GitHub uses version control
in combination with *git*, which is what actually handles the technical
machinery.  It's grown into the de facto place where computer scientists ---
particularly those in Artificial Intelligence --- present their work.  What
follows is a brief description of what I use GitHub for; in particular, I have
many *public* repositories along with a few *private* repositories.

For *public* repositories, I have the following:

- A **Paper Notes** repository, where I [write notes for research papers][2]. A
  few months ago, [I wrote a brief blog post][10] describing why I decided to do
  this. Fortunately, I have come back to this repository several times to see
  what I wrote for certain research papers. The more I'm doing this, the more
  useful it is! The same holds for running a blog; the more I find myself
  rereading it, the better!
- A repository for **coding various algorithms**. I actually have two
  repositories which carry out this goal: one for [reinforcement learning][4]
  and another for [MCMC-related stuff][5]. The goal of these is to help me
  understand existing algorithms; many of the state-of-the-art algorithms are
  tricky to implement precisely because they are state-of-the-art.
- A repository for **miscellaneous personal projects**, such as one for [Project
  Euler problems][7] (yes, I'm still doing that ... um, barely!) and another for
  [self-studying various][9] courses and textbooks.
- A repository for **preparing for coding interviews**. I thought it might be
  useful to post [some of my solutions to practice problems][8].
- A repository for my **vimrc** file. Right now [my vimrc file is only a few
  lines][6], but it might get more complex. I'm using a number of computers
  nowadays (mostly via ssh), so one of the first steps to get started with a
  machine is to clone the repository and establish my vimrc.
- Lastly, but certainly not least, don't forget that [there's a repository][3]
  for **my blog**. That's obviously the most important one!
 
On the other hand, there are many cases when it makes sense for individuals to
use private repositories. (I'm using "individuals" here since it should be clear
that all companies have their "critical" code in private version control.) Here
are some of the private repositories I have:

- **All ongoing research projects** have their own private repository. This
  should be a no-brainer. You don't want to get scooped, particularly with a
  fast-paced field such as Artificial Intelligence. Once such papers are ready
  to be posted to arXiv, that's when the repository can be released to the
  public, or copied to a new public one to start fresh.
- I also have one repository that I'll call a **research sandbox**. It contains
  multiple random ideas I have, and I run smaller-scale experiments here to test
  ideas. If any ideas look like they'll work, I start a new repository to
  develop them further. On a side note, running quick experiments to test an
  idea before scaling it up is a skill that I need to work on!
- Finally, I have a repository for **homework**, which also includes class final
  projects. It's particularly useful for when one has laptops that are
  relatively old (like mine) since the computer might die and thus all my work
  LaTeX-ing statistics homework might be lost. At this point, though, I think
  I'm done taking any real classes so I don't know if I'll be using this one
  anymore.

Well, this is a picture of how I manage my repositories. I am pleased with this
configuration, and perhaps others who are starting out with GitHub might adapt
some of these repositories for themselves.

[1]:https://github.com/DanielTakeshi
[2]:https://github.com/DanielTakeshi/Paper_Notes
[3]:https://github.com/DanielTakeshi/DanielTakeshi.github.io
[4]:https://github.com/DanielTakeshi/rl_algorithms
[5]:https://github.com/DanielTakeshi/MCMC_and_Dynamics
[6]:https://github.com/DanielTakeshi/vimrc
[7]:https://github.com/DanielTakeshi/Project_Euler_in_C
[8]:https://github.com/DanielTakeshi/Interview_Practice
[9]:https://github.com/DanielTakeshi/Self_Study_Courses
[10]:https://danieltakeshi.github.io/2017/03/23/keeping-track-of-research-articles-my-paper-notes-repository/
