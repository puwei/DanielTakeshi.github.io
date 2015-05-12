---
title: Wrapping Up my Summer Research
author: Daniel Seita
layout: post
permalink: /?p=269
categories:
  - Computer Science
tags:
  - Bard College
  - machine learning
  - research
  - summer
---
I&#8217;ve written my final report to the National Science Foundation for my summer work at the 2012 [Bard College Mathematics & Computation Research Experience for Undergraduates][1]. My project focused on *text simplification*, which can be broadly defined as the process of making (English) text easier to read while maintaining as much underlying content as possible. I would consider it to be a subfield of *machine learning*, which is a branch of artificial intelligence.

The primary objective of my work was to improve on existing results of text simplification. There is no standard way to measure the quality of simplification, so my research team &#8212; consisting of me, another undergraduate, and two Bard college professors &#8212; decided to use [BLEU scores][2]. The advantage to using those scores is that, in the summer of 2011, another research group used it as a measure of their level of simplification. Our goal was to beat their BLEU scores.

To carry out the translation process, we used the open-source [Moses][3] software. To train the system to simplify text, we used aligned, parallel data from Wikipedia and [Simple English Wikipedia][4]. Moses is designed to be able to translate across different languages, but we considered &#8220;Simple English&#8221; as its own language. Thus, we viewed the project as encompassing an English-to-English translation problem, where the &#8220;foreign&#8221; language is derived from Wikipedia, and the &#8220;simple&#8221; language is derived from Simple English Wikipedia. Our hope was that Moses would be able to understand the steps involved in making English text simpler and act as an effective means of translation.

We soon discovered, though, that our parallel data was of low quality. We therefore used the [LIBSVM][5] and [LIBLINEAR][6] classification softwares to improve the data by switching or deleting certain pairs of lines from the parallel corpus. For instance, if there was a short sentence in the Wikipedia data that was aligned to an obviously more complex sentence from the Simple English Wikipedia data, it made sense to switch those two sentences so they were in the more appropriate data set. After all, the data was made by random people contributing to the two Wikipedias, so there were bound to be a few bad samples here and there.

Our group successfully classified a random sample of sentences as belonging to the Wikipedia set or the Simple English Wikipedia set with a higher degree of accuracy than previous researchers did. My professors are still performing some experiments, so it remains to be seen if we can get higher BLEU scores.

Overall, I&#8217;m glad I had the chance to participate in the Bard REU, and I&#8217;m optimistic that we will produce a strong research paper. I thank the professors there for accepting me into their program, and the National Science Foundation, which has now sponsored my second straight summer program.

 [1]: http://seitad.wordpress.com/2012/06/03/summer-at-bard/
 [2]: http://en.wikipedia.org/wiki/BLEU
 [3]: http://www.statmt.org/moses/index.php?n=Main.HomePage
 [4]: http://simple.wikipedia.org/wiki/Main_Page
 [5]: http://www.csie.ntu.edu.tw/~cjlin/libsvm/
 [6]: http://www.csie.ntu.edu.tw/~cjlin/liblinear/