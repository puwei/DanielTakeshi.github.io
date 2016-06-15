---
layout: post
title:  "The Master Algorithm: How the Quest for the Ultimate Learning Machine Will Remake Our World"
date:   2016-05-31 17:00:00
permalink: 2016-05-31-the-master-algorithm-how-the-quest-for-the-ultimate-learning-machine-will-remake-our-world/
---

I recently finished *The Master Algorithm: How the Quest for the Ultimate Learning Machine Will
Remake Our World*, by acclaimed computer science professor [Pedro Domingos][1] of the University of
Washington. *The Master Algorithm* is aimed at a broad but well-educated audience and attempts to
serve as an intermediate between dense, technical textbooks and simple, overly-hyped 800-word "AI IS
GOING TO DESTROY PEOPLE" newspaper articles. The main hypothesis is that there exists a universal
algorithm for solving general machine learning problems: *the master algorithm*.  Or, as Domingos
humorously puts it, *one algorithm to rule them all*. For background information, Domingos provides
a historical overview of five "tribes" of machine learning that we must unify and understand to have
a chance at unlocking the master algorithm. In general, I think his master algorithm idea has merit,
and his explanation of the five areas of machine learning are the most important and valuable parts
of the book.  Nonetheless, as there are fundamental limitations on learning a technical subject like
machine learning in a book with just 300 (non-mathematical) pages, this book is bound to disappoint
a few readers.  The explanation of the hypothetical master algorithm is also limited since it relies
almost entirely on Domingos' decade-old research. In addition, some of the implications on society
seem far fetched.

I was familiar with most of the material in this book beforehand, but as stated earlier, I still
found Domingos' organization of machine learning into five tribes to be immensely useful for
understanding the field. His five tribes are: symbolists, connectionists, evolutionaries, Bayesians,
and analogizers. I would never have thought about organizing machine learning this way, because I
have limited experience with evolutionaries (i.e., people who use genetic programming) and because
whenever I try to study logic and reasoning (i.e., what the symbolists do) I struggle to avoid
falling asleep. I have been able to study logic, though, as [shown in this long blog post][4].

I am most familiar with the other three areas Domingos lists. The connectionists are dominating
machine learning nowadays because they use neural networks. (Ever heard of "deep learning," anyone?)
The Bayesians used to dominate; these are the people who use graphical models. The analogizers use
the nearest neighbor and support vector machine algorithms. For all three of these tribes, I have
covered corresponding topics in previous blog entries (e.g., [see this post for a discussion on
SVMs][3]).

Given the constraints of 30 pages per tribe, Domingos explains each of them remarkably well. Having
studied these in mathematical detail, I find it enjoyable to just relax, avoid the math, and
understand the history: who invented which algorithm, what were competing trends, and similar
stories.  In addition to the five tribes, Domingos goes over other important concepts in machine
learning and artificial intelligence, including Expectation-Maximization and reinforcement learning.
Domingos then describes his thoughts on a universal algorithm, invoking his own research (Markov
logic networks) in the progress.  Finally, he discusses the implications of improved machine
learning on our lives.

For the sake of a general audience, Domingos avoids mathematical details and relies on examples and
analogies. This is fine, and both Domingos and I agree that it is possible to understand some
machine learning without math. I probably do not agree with that statement as much as Domingos does,
though; I really need to go over all the math details for me to understand an algorithm, and other
readers with my mindset can get disappointed.

I also think his attempts at explaining the master algorithm at the end fall prey to excessive
storytelling. After his long, adventure-related metaphor, I was (and still am) confused about how to
effectively build upon his Markov logic network work to get a *real* master algorithm.  Regarding
the implications of the master algorithm on human life, that chapter felt more fantasty than reality
to me, and I can't see the kind of stuff Domingos says happening in the near future.  For instance,
Domingos says that since AI might take over human labor, we will need to use a "universal basic
income," but [that would not necessarily be the best thing to do][2] and I can't see how this will
be politically viable (it's possible, though, but I'm probably thinking on a longer time horizon
than Domingos).

I don't mean for the last two paragraphs to sound overly critical. I think *The Master Algorithm* is
interesting and I would recommend it to those who would like to learn more about computer science.
I would not, however, say it is among my top-tier favorite books. It's a decent, solid, but not
once-in-a-generation, and I think that's a fair characterization.

[1]:http://homes.cs.washington.edu/~pedrod/
[2]:http://www.nytimes.com/2016/06/01/business/economy/universal-basic-income-poverty.html
[3]:http://danieltakeshi.github.io/2015-08-08-perceptrons-svms-and-kernel-methods.md/
[4]:http://danieltakeshi.github.io/2015-06-22-reading-russell-and-norvig/
