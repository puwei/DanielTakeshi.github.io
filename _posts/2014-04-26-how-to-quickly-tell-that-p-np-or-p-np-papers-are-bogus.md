---
title: How to Quickly Tell That P = NP or P =/= NP Papers are Bogus
author: takeshidanny@gmail.com
layout: post
permalink: /?p=2403
geo_public:
  - 0
dsq_thread_id:
  - 3755962160
categories:
  - Computer Science
tags:
  - academic papers
  - famous problems
  - P vs NP
---
&nbsp;

[<img class="aligncenter size-large wp-image-1770" src="http://www.seitad.com/wp-content/uploads/2014/04/pvsnp1.png?w=460" alt="PvsNP" width="460" height="292" />][1]

For one of my final projects this semester, I&#8217;m working on something that&#8217;s loosely based off of the [traveling salesman problem][2] (TSP) and the P vs NP question, the latter of which is arguably the most famous open problem in all of computer science. Whoever proves that P = NP, P =/= NP, or that the problem cannot be proved/solved for whatever reason, gets a $1,000,000 prize from the Clay Mathematics Institute.

As part of my pre-project research, I&#8217;ve had the chance to look at a few papers about the TSP and the P vs NP question. Some papers have been great to skim, if only to gather insights about the TSP&#8217;s integer programming formulation, but others (typically those that claim to *solve* P vs NP) are clearly mockeries. In this post, I&#8217;d like to discuss the ways one can quickly tell that papers claiming to solve this question &#8212; or in fact, any other famous open problem &#8212; are bogus. Let&#8217;s do this under the assumption that you&#8217;re looking at a *pre-print* of the paper before it has been reviewed by a preeminent conference or journal.

For reference and amusement, [here&#8217;s a page][3] that lists (as of this writing) *one hundred and five papers/proofs* that (mostly) claim to solve this question. The author of this page states that only *one* of these papers has appeared in a peer-reviewed journal. And of course, it doesn&#8217;t solve the problem:

> <span style="color:#000000;">Note: The following paragraphs list many papers that try to contribute to the P-versus-NP question. Among all these papers, there is only </span>**a single paper**<span style="color:#000000;"> that has appeared in a peer-reviewed journal, that has thoroughly been verified by the experts in the area, and whose correctness is accepted by the general research community: The paper by Mihalis Yannakakis. (And this paper does not settle the P-versus-NP question, but &#8220;just&#8221; shows that a certain approach to settling this question will never work out.)</span>

Before we begin, let me just start with a disclaimer. Yes &#8230; this problem *may *be solved throughout my lifetime. So the title of this blog post *may* be changed to &#8220;How to Quickly Tell That *All* *but One* P = NP or  P =/= NP Papers are Bogus&#8221; &#8230; but for now it is safe, as the Clay Mathematics Institute has yet to recognize a solution. Furthermore, by definition, if P = NP, then the papers claiming that P =/= NP are erroneous, and vice versa. So, under the assumption that (for whatever reason) you&#8217;re skimming a paper claiming to solve the P vs NP question (or another famous open problem), what are three quick signs that the paper is not worth reading?

<span style="text-decoration:underline;"><strong>Reason #1</strong></span>: The author isn&#8217;t a top theoretical computer scientist (or, if there is more than one author, then none are top theoretical computer scientists) The logic is pretty simple. The top theoretical computer scientists are more likely to be at the forefront of the P vs NP question. Thus, they will know the relevant background work, understand why previous approaches failed, and may have ideas or new techniques to bring to the field. If you don&#8217;t know the name of an author, then a good proxy is the prestige of the university he or she resides. Again, the logic is simple: ranking of universities correlates with quality of professors.

*But *&#8230; an unknown mathematician made the biggest academic result in all of science, technology, engineering, and mathematics in 2013. I&#8217;m referring to when Yitang Zhang made [groundbreaking progress][4] on the Twin Primes Conjecture. (If I was writing this post last year, I&#8217;d be talking about the [Higgs Boson][5] result in 2012, which was from several established scientists. But I find Zhang&#8217;s case to be more interesting to discuss, as some may consider it as a counterexample to Reason #1.) On the other hand, Zhang&#8217;s paper, which is available on the Internet somewhere, satisfies my two other reasons.

<span style="text-decoration:underline;"><strong>Reason #2</strong></span>: The paper isn&#8217;t written using LaTeX. Oh yes &#8230; [LaTeX is awesome][6]. And it&#8217;s a shame that some people who write up these proofs do not even take the time to make their papers look nice. All top computer scientists will use LaTeX for their papers, and about 99% of the non-top ones will. Yet some of the papers I saw on that linked page were clearly written using a different (and inferior) word processor.

The use of LaTeX is important to give the impression that one is serious about his or her work by presenting it cleanly to readers. But there&#8217;s another easily-identifiable characteristic of bogus papers that can make it clear that the paper isn&#8217;t worth reading. That is &#8230;

<span style="text-decoration:underline;"><strong>Reason #3</strong></span>: The paper is short. This can vary from discipline to discipline, and whether the paper was written using LaTeX or not (with non-LaTeX papers tending to take up more pages due to poor formatting/spacing). I would suggest that any paper that is shorter than the equivalent of about 40 *double*&#8211;*spaced*, 12-pt font, normal-margin pages cannot contain enough information to really resolve the P vs NP question. For that kind of paper, the authors would almost certainly need a full section of more than 10 pages just to discuss the background work. Then it&#8217;s another 20 or more pages to discuss the new techniques or ideas the paper brings to the field. Then it&#8217;s 20 more to set up the lemmas to prove it. Then 20 more to prove the theorem. Then 20 more to show why common counter-arguments are false. And so on.

Only one of the papers I checked on that P vs NP page were long enough to my liking. I didn&#8217;t have the time to see all of them, so maybe I am missing a few others. It is worth noting that Zhang&#8217;s paper was around 50 pages.

 [1]: http://www.seitad.com/wp-content/uploads/2014/04/pvsnp1.png
 [2]: http://en.wikipedia.org/wiki/Travelling_salesman_problem
 [3]: http://www.win.tue.nl/~gwoegi/P-versus-NP.htm
 [4]: http://www.simonsfoundation.org/quanta/20130519-unheralded-mathematician-bridges-the-prime-gap/
 [5]: http://en.wikipedia.org/wiki/Higgs_boson
 [6]: http://seitad.wordpress.com/2013/07/12/its-time-to-ditch-powerpoint-and-word-in-favor-of-latex/