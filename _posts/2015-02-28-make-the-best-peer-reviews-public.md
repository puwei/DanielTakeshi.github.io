---
title: Make the Best Peer Reviews Public
author: Daniel Seita
layout: post
permalink: /2015/02/28/make-the-best-peer-reviews-public/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - conferences
  - machine learning
  - NIPS
  - peer review
---
<img src="{{site.url}}/assets/nips-2014-poster-thumbnail.png" alt="nips">

The annual Neural Information Processing Systems (NIPS) conference is arguably the premier machine
learning conference along with the International Conference on Machine Learning (ICML). I read a lot
of NIPS papers, and one thing I&#8217;ve only recently found out was that NIPS actually makes the
paper reviews (somewhat) public.

As I understand it, the way NIPS works is:

  1. Authors submit papers, which are eight pages of text, and a ninth one for references. Unlimited
  supplementary material is allowed with the caveat that reviewers do not need to read it.
  2. The NIPS committee assigns reviewers to peer-review the submissions. These people are machine
  learning faculty, graduate students, and researchers. (It has to be like that because
  there&#8217;s no other qualified group of people to review papers.) One key point is that NIPS is
  *double-blind*, so reviewers do not know the identity of the papers they read while reviewing, and
  authors who submit papers do not know the identity of the people reviewing their papers.
  3. After a few months, reviewers make their preliminary comments and assign relative scores to
  papers. Then the original authors can see the reviews and respond to them during the &#8220;author
  rebuttal&#8221; phase. Naturally, during all this time, the identity of the authors and reviewers
  is a secret, though I&#8217;ve seen cases when people post submitted NIPS papers to Arxiv before
  acceptance/rejection, and Arxiv requires full author identity, so I guess it is the
  reviewer&#8217;s responsibility to avoid searching for the identity of the authors.
  4. After a few more months, the reviewers make their final decision on which papers get accepted.
  Then the authors are notified and have to modify their submitted papers to include their actual
  names (papers in submissions don&#8217;t list the authors, of course!), any acknowledgments, and
  possibly some minor fixes suggested by the reviewers.
  5. A few months *after* that (yeah, we&#8217;re getting a lot of months here), authors of accepted papers travel to the conference where they discuss their research.

This is a fairly typical model of a computer science conference, though possibly an aytpical model
when compared to other academic disciplines. But I won&#8217;t get into that discussion; what I
wanted to point out here is that NIPS, as I said earlier, makes their reviews public, though the
*identity* of the reviewers is not shown. Judging by [the list of NIPS proceedings][2], this policy
of making reviews public began in 2013, and happened again in 2014. I assume NIPS will continue with
this policy. (You can click on that link, then click on the 2013/2014 papers lists, click on any
paper, and then there&#8217;s a &#8220;Reviews&#8221; tab.) Note that the author rebuttals are also
visible.

I was pleasantly surprised when I learned about this policy. This seems like a logical step towards
transparency of reviews. Why don&#8217;t all computer science conferences do this?

On the other hand, I also see some room for improvement. To me, the obvious next step is to include
the name of the reviewers who made those reviews (only for accepted papers). [NIPS already gives
awards][3] for people who make the best reviews. Why not make it clear who wrote the reviews? It
seems like this would incentivize a reviewer to do a good job since their reviews might be made
public. Incidentally, those awards should be made more prestigious, perhaps by announcing them in
the &#8220;grand banquet&#8221; or wherever the entire crowd gathers?

You might ask, why not make the identity of reviewers known for *all* reviews (of accepted papers)?
I think there are several problems with this, but none seem to be too imposing, so this might not be
a bad idea. One is that the current model for computer science seems to assign people too many
papers to review, which necessarily lowers the quality of each individual review. I am not sure if
it is necessary or fair to penalize an overworked researcher for making his/her token reviews
public. Another is that it is a potential source of conflict between future researchers. I could
image someone obsessively remembering a poor public review and using that against the reviewer in
the future.

These are just my ideas, but I am not the only one thinking about the academic publishing model.
There&#8217;s been a lot of discussion on how to change the computer science conference model (see,
for instance, &#8220;[Time For Computer Science to Grow Up][4]&#8220;), but at least for the current
    model, NIPS got it mostly right by making reviews somewhat public. I argue that one additional
    step towards greater clarity would be helpful to the machine learning field.

 [1]: https://seitad.files.wordpress.com/2015/02/nips-2014-poster-thumbnail.png
 [2]: http://papers.nips.cc/
 [3]: http://nips.cc/Conferences/2013/PaperInformation/ReviewerInstructions
 [4]: http://cacm.acm.org/magazines/2009/8/34492-viewpoint-time-for-computer-science-to-grow-up/fulltext
