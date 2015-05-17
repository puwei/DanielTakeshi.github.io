---
title: 'CS Theory Part 2 of 8: Proving Languages are not Regular'
author: Daniel Seita
layout: post
permalink: /2012/10/13/cs-theory-part-2-proving-languages-are-not-regular/
categories:
  - Computer Science
tags:
  - automata
  - theory
---
After a little bit of a delay, I&#8217;m back to writing a little bit more about theory of
computation. (Be warned that this post will assume more prior knowledge about automata than the
previous entry.) So far, we&#8217;ve been learning a lot about languages, which are a set of strings
formed from some alphabet (e.g. 0 and 1 for binary numbers) that obey certain guidelines. Languages
can be classified as either regular or non-regular. Regular languages are those that can be
recognized by some DFA, and I made some examples of that in the first Theory post. But not all
languages are regular. And so far, I believe there&#8217;s three main ways to prove a language is
not regular.

  1. Closure properties of regular languages (unions, intersections, concatenations, &#8220;star&#8221; operation, etc.)
  2. [The Pumping Lemma][1]
  3. [The Myhill-Nerode Theorem][2] and Fooling Sets

<!--more-->

The usefulness of these three depends on the language. For some, the closure properties are the
easiest to prove non-regularity; for others, it might be the Myhill-Nerode theorem. In fact, there
are some languages that are not regular, yet are satisfied by the Pumping Lemma! That lemma is not a
sufficient condition on non-regularity, so if a language satisfies it, all bets are off as to
whether it&#8217;s regular or not. But if a language &#8220;passes&#8221; the requirements of
Myhill-Nerode, it *must* be regular. Clearly, languages require multiple strategies to prove
regularity or non-regularity.

I thought I&#8217;d present an example of  a non-regular language and see how all three methods
could be applied. First, before we begin, the canonical non-regular language (meaning, the one
language that often introduces students into the world of linguistic non-regularity) is the
following:

$$A = \{0^n1^n \mid n \ge 0\}$$

It&#8217;s the language consisting of all strings with an equal amount of zeroes and ones, with the
ones following the zeroes. Intuitively, it&#8217;s fairly simple to see that
it&#8217;s non-regular. If a DFA were to recognize this language, it would have to compute the total
amount of zeroes, followed by the ones. Consequently, since there would be an infinite amount of
states needed, we can&#8217;t make a DFA since they are meant to be finite automata. That is, they
have finitely many states. We will use this knowledge in hand, combined with the three common ways
to prove non-regularity, when we consider this similar language:

$$B = \{0^m1^n \mid m \ne n\}$$

It's similar, but we just have to make sure that there are a different amount of zeroes and
ones, and again, that the ones all come after the zeroes.

So let's consider the different ways we could prove that this language is not regular.

***Closure Properties***

First, we look at closure properties of regular languages. A theorem of regular languages is that
they are equivalent to the class of *regular expressions*. We know that $$0^*$$ and $$1^*$$ are both
regular expressions. Furthermore, a theorem states that the class of expressions is closed under
concatenation, so the following regular expression (i.e. regular *language*) $$0^*1^*$$ *is*
regular! Notice the key difference between this language and the previous two; the fact that we
don&#8217;t have restrictions on the amount of 0s and 1s makes it possible to construct a DFA for
this! Such a DFA would be fairly simple to construct &#8212; it would only require three states, one
to start and represent the initial zeroes, one to represent the ones, and another to represent the
death state, which is when, at any point, we see a 0 following a 1.

Why is knowing $$0^*1^*$$ important? The class of regular languages is closed under intersection, so
consider the language

$$\overline{B} \cap 0^*1^* = \{0^k1^k \mid k \ge 0\}$$

Where $$\overline{B}$$ represents the complement of $$B$$. Yet another theorem is that regular
languages are closed under complements. That is, if $$B$$ is regular, then $$\overline{B}$$ is
regular. But notice that if we assume $$B$$ is regular, then the intersection $$\overline{B} \cap
0^*1^*$$ must be regular by intersection closure. But we know that the intersection is equal to the
canonical non-regular language! Hence, $$B$$ must be non-regular.

***The Pumping Lemma***

That wasn&#8217;t too bad, but things will get slightly more complex when we use the pumping lemma.
We assume, by way of contradiction, that $$B$$ is regular. Then by the pumping lemma, there exists
some string length $$p$$ such that any string in this language that is at least this long can be
partitioned into components $$x, y, z$$. Consider the string $$s = 0^p1^{p! + p} \in B$$, which
clearly satisfies the minimum length requirement, so it can be pumped. We set $$x = 0^a, y = 0^b,
\mbox{ and } z = 0^{c}1^{p!+p}$$, where $$b \ge 1 \mbox{ and } a+b+c = p$$. Let us pump the $$y$$
component $$i +1 = p!/b + 1$$ times in $$s' = xy^{i+1}z$$, which must be in the language by the
pumping lemma. But pumping this string turns out to be $$s' = 0^{a+b+c+p!}1^{p!+p} =
0^{p!+p}1^{p!+p} \not \in B$$, a contradiction. Any language that fails the pumping lemma is not
regular, so $$B$$ is non-regular.

***The Myhill-Nerode Theorem***

Knowing how to use the pumping lemma after reading the solution seems simple, but the hard part is
actually coming up with the $$p! + p$$ component. We wrap up by using the often easier Myhill-Nerode
method to prove that this language is not regular. Let&#8217;s use the fooling set $$F = \{0^i \mid
i \ge 0\}$$. Then for any distinct $$x, y \in F$$, we know that the have a different amount of
zeroes in them. Let $$x = 0^j \mbox{ and } y = 0^k$$ Then take $$z = 1^j$$. We know that $$xz \not
\in B$$, but we also have $$yz \in B$$ ... so these strings are distinguishable from each other! And
since our fooling set is infinite, and any pairs of distinct strings in it are distinguishable, any
DFA would have to have an infinite amount of states, which is impossible. Hence, this language is
not regular.

(Personally, I prefer the fooling set method to solving problems &#8230; it&#8217;s often very
simple, and the same fooling sets can be used to prove non-regularity for multiple languages.)

Up next in my studies are context-free grammars. Stay tuned!

(On a side note, this is my 50th blog entry.)

 [1]: http://en.wikipedia.org/wiki/Pumping_lemma_for_regular_languages
 [2]: http://en.wikipedia.org/wiki/Myhill-Nerode_theorem
