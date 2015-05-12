---
title: Git and Git Immersion
author: Daniel Seita
layout: post
permalink: /?p=1791
geo_public:
  - 0
  - 0
categories:
  - Computer Science
tags:
  - git
  - Git Immersion
  - version control
---
One critical skill I acquired this past year was how to use [git][1]. It&#8217;s a distributed version control system that is often used by programmers and software companies to manage their code. The reason why git and other version/revision control systems are so useful is that they allow multiple people to easily work together on a project by means of a shared code repository. Rather than have one person work on a small part of a project and email any updates to everyone else, he or she can instead &#8220;push&#8221; their modifications to the repository, and other collaborators can &#8220;pull&#8221; the updated code so that they are working with the latest version. (I use &#8220;push&#8221; and &#8220;pull&#8221; since these are git-related terms, but other systems have different terminologies for adding and getting repository code.)

If the current code has serious issues, it is possible to roll back to a previous version, which is just like having a bunch of backup files. This is one of the main benefits of using version control systems, even for a project managed by just one person. For instance, I used git for my undergraduate thesis and the related code, so whenever I wanted to work on it, I would just pull from the current repository, make my changes, and then push at the end. Git turned out to be a lifesaver when, two weeks before I had to send my thesis to the rest of the department, I accidentally deleted a chapter. The solution? Pull the latest version of that chapter from the repository.

Git is very common among computer science students, and possibly even more popular among computer science Ph.D. students, so it&#8217;s a good skill to have in one&#8217;s toolkit. I learned git largely by trial and error and having other people tell me what to do, but one resource I found that might be useful to beginners is [Git Immersion][2]. This is a tutorial that walks you through the basic commands of git. It was mostly review for me, but I did learn a few things, such as &#8220;git mv&#8221; which will save me time when moving files in my repositories. In the past, I would move files, then delete the original files from git, then add the new ones (in the different location), then commit everything, but git mv does all that at once. My one qualm is that I wish they incorporated [GitHub][3] in the tutorial, but it&#8217;s technically not part of git, so I can see the reason for excluding it.

Say, I wonder how non-computer scientists write their theses, or more accurately, those who don&#8217;t employ version control systems. I would hate having to save countless backups for a variety of files. In addition, another key benefit of git is that each time you make a change, you can record the high-level idea of this modification, and it will appear in the log for future reference. This makes it easy to go back and search for an old version of a file.

 [1]: http://git-scm.com/
 [2]: http://gitimmersion.com/index.html
 [3]: github.com