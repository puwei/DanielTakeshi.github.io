---
title: My Williams College Mathematics Colloquium Talk
author: Daniel Seita
layout: post
permalink: /?p=1410
geo_public:
  - 0
  - 0
dsq_thread_id:
  - 3755963143
categories:
  - Computer Science
tags:
  - colloquium
  - graphical models
  - math majors
  - statistics
---
Williams College requires that all senior math majors give an acceptable 30-minute colloquium talk on the topic of their choice. Virtually all seniors who give their talk &#8220;pass&#8221; as long as their topic is relatively new, interesting, and isn&#8217;t nontrivial. The senior majors have to attend 20 of these student talks, not including their own, so the typical audience consists of other students as well as most of the faculty.

Back in May, I volunteered to give my colloquium talk early, and I was fortunate that the colloquium chair assigned me to be in the first student slot. (It&#8217;s always nice to set the trend!) For my colloquium, which I just delivered today, I chose to talk about *probabilistic graphical models *(PGMs). It wasn&#8217;t a difficult decision for me to pick this topic. This past summer, as part of my &#8220;moral duty&#8221; as a machine learning student, I skimmed a wide variety of recent articles published by the highly prestigious International Conference in Machine Learning. Many of the articles I read incorporated PGMs, and there was one article in particular that struck my eye: using PGMs in crowd-sourcing to [grade a test without knowing the answers][1].

That got me a little interested in PGMs, so I read a little more and learned that these are often considered part of the intersection between computer science and statistics. Effectively, these are graphs that describe their own probability distributions (incorporating statistics) by representing nodes as random variables. By exploiting graph theoretic algorithms (incorporating computer science), it&#8217;s possible to efficiently model a scenario that might otherwise be too intractable to analyze directly, e.g. in medical analysis when we&#8217;re dealing with thousands of random variables. Needless to say, I figured I should explore PGMs in depth, both for my computer science senior thesis and for my colloquium.

Thus, my colloquium talk first gave an introduction to PGMs, and then described the application in crowd-sourcing as described in the paper I linked to earlier. If you&#8217;re interested in learning more about these, feel free to check out the slides I used for my talk. You can view them [here][2]. (Side note: for something as important as this, always have at least one backup of your slides &#8230; try using Dropbox.) Have fun with PGMs!

 [1]: http://research.microsoft.com/pubs/164692/MLIQ-CR.pdf
 [2]: https://www.dropbox.com/s/qtzdjwyv1op6o21/Final_Colloquium_Daniel_Seita.pdf