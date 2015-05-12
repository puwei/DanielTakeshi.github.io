---
title: Detection Theory Adventures (a.k.a. a Final Project)
author: Daniel Seita
layout: post
permalink: /?p=2126
geo_public:
  - 0
  - 0
categories:
  - Computer Science
tags:
  - detection theory
  - final project
  - ICML
  - NIPS
  - statistical learning theory
  - writing
---
Whew! I just spent the past week in a mad dash to finish up my Statistical Learning Theory final project (CS 281a at Berkeley). My [write-up is online][1], in case you want to check it out. The overall goal of my project was to explore the area of [detection theory][2], an important mathematical field that *does* have practical implications. I know every field likes to say that (and in a sense, maybe it&#8217;s true for all fields anyway) but seriously &#8212; detection theory is about trying to distinguish the signal from the noise. Suppose we see a bunch of data points that are generated from some underlying process. This goes on for a while, but then at some point, the chart we see spikes up. That could indicate that something&#8217;s wrong. There are tons of examples that match this kind of situation. The example I used in my report was monitoring a patient&#8217;s body temperature. If I&#8217;m taking my temperature every 12 hours, for instance, and I see the following numbers: 98.6, 98.6, &#8230; (a long time) &#8230;, 98.6, 99.1, 99.5, 99.7, 100.2, 100.0, 101.1, by the time I&#8217;m getting even past 99.5 I should be a little suspicious and think that the underlying process for my body temperature indicates that I have a fever.

I learned *a lot* from my final project, since I read about 15 academic papers (which are not easy to read) and skimmed over many others. Despite this, I am not that happy with how it ended up, because my experiments were not extensive or groundbreaking. On the other hand, perhaps this kind of work is what I should expect if I&#8217;ve got only four weeks for a class project. It wouldn&#8217;t be the first time that I&#8217;ve been excessively harsh on myself.

By the way, my report is written in the style and formatting of the [Neural Information Processing Systems ][3](NIPS) conference. NIPS is one of the top two academic machine learning research conferences, with the other one being the Internal Conference on Machine Learning (ICML). Their papers have a nine-page limit, with the ninth one reserved for references only, but I&#8217;ve noticed that in practice a lot of researchers end up putting a ton of proofs and other information in appendices or supplementary material after the first nine pages. I have seen supplementary material sections that were 30 pages long! This is allowed, because NIPS guidelines say that extra material after nine pages is fine with the understanding that reviewers are not obligated to read them. I found the eight page limit to be easy to reach with this simple project, which is funny because I&#8217;ve long viewed eight page papers/reports to be long for a high school or college class. Furthermore, many of my previous class papers had to be double-spaced in 12-point font, whereas in NIPS they cram everything down with single-spaced, 10-point font*.* I had to fiddle around with a lot of the text to get everything to squish into eight pages, and as my last step, I used the LaTeX command vskip -10pt to condense the &#8220;Acknowledgments&#8221; subsection heading with its text. I guess that&#8217;s what academic writing is like?

 [1]: https://www.dropbox.com/s/tppfr6gyq7cbv1l/daniel_seita_281a_final_project.pdf?dl=0
 [2]: http://en.wikipedia.org/wiki/Detection_theory
 [3]: http://nips.cc/Conferences/2014/