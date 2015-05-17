---
title: Recap of the 2013 Algorithmic Combinatorics on Words REU
author: Daniel Seita
layout: post
permalink: /2013/07/28/recap-of-the-2013-algorithmic-combinatorics-on-words-reu/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - algorithms
  - combinatorics
  - Greensboro
  - research
  - REU
  - summer
---
<img src="{{site.url}}/assets/Hike_UNCG.png" alt="uncg">

Yesterday, I arrived back home after spending the previous eight weeks at the 2013 [Algorithmic
Combinatorics on Words][2] REU. It was a great experience overall, so I thought I’d share a bit
about what happened.

<!--more-->

**The Experience**

I arrived in Greensboro, NC, on June 2, and was greeted by one of the research assistants (RAs) and
a few other student participants who had arrived at roughly the same time. The RAs had generously
offered to drop us off at our apartments, and they also assisted us in getting settled during the
first day by providing keys, taking us out to dinner, etc. The following morning, we met our REU
coordinator, Professor Francine Blanchet-Sadri and went through a typical orientation process. (She
gave me permission to address her on a first-name basis, so hopefully it&#8217;s okay if I use
&#8220;Francine&#8221; in the rest of this post.)

One of the unique things about this REU is that there&#8217;s only one faculty advisor here
(Francine) who advises all the student research groups. From what I know, most REUs are structured
such that several faculty members offer their own projects, and students have to apply to the REU
while ranking them according to preference. The faculty members also typically advise only one team
of students. At UNCG, all students and the RAs (who conduct their own research here as well)
essentially work in the field of algorithmic combinatorics on words in teams of two, though some
individuals paired together may agree to split and work by themselves.

We spent the first few days going over background material in [Algorithmic Combinatorics on
Words][3] and listening to Francine (or the RAs) give seven talks about different subfields in which
we could perform research. After we were through with the background material, the fourteen of us
&#8212; eleven student participants and three research assistants &#8212; ranked the seven projects
and attempted to match up the groups as fairly as possible. After some <del>unlawful coercion</del>
gentle negotiation, we eventually settled on an alignment of two students to each of the seven
possible topics. Note that Francine demanded that all seven topics be used, so we had to make sure
that there were people working on the less popular topics. I was assigned to work with another
student on the topic entitled *Abelian and Subword Complexity*.

As it turned out, we only seriously investigated abelian complexity. I won&#8217;t get into too much
depth here, but I figure it can&#8217;t hurt to at least give an extremely basic introduction. If we
define a word $$w$$ to be a sequence of characters over some alphabet, then the *abelian complexity*
of that word with respect to $$n$$, denoted $$\rho_{w}^{ab} (n)$$, is simply the number of abelian
equivalence classes of subwords of length $$n$$ in $$w$$. Two words are abelian equivalent (and thus
in the same equivalence class) if and only if each letter in a given alphabet shows up the same
amount of times in the two words; for instance, words $$x_1 = 010$$ and $$x_2 = 100$$ are abelian
equivalent since both have two 0s and one 1, but $$ y_1 = 011$$ and $$y_2 = 001$$ are not abelian
equivalent. With this in mind, suppose we have the word $$w_0 = 010110$$ over the binary alphabet
$$A_k = \{0,1\}$$. We have $$ \rho_{w_0}^{ab} (4) = 2$$ because we can form a length-4 subword of
$$w_0$$ with using two 0s and two 1s (e.g. 0101) or one 0 and three 1s (e.g. 1011). To make things
more interesting, I investigated *infinite* words, but that&#8217;s a topic for another day.

The first few weeks were primarily devoted to background reading provided with the set of notes
Francine compiled for our particular research topic. Even though we mostly read papers with the
dreaded &#8220;in progress&#8221; label (in other words, they&#8217;re littered with typos and
confusing English), the reading wasn&#8217;t too bad, and I began brainstorming a bunch of ideas and
possible avenues for research.

There was a major open conjecture posed in one of the longer papers I read, and during the third
week, I felt like I began seeing ways to prove it. Thus, I spent days putting my ideas into writing
and verifying them with a variety of my own Python scripts.

The problem, of course, was that there was always at least one case/example that wouldn&#8217;t
work.

I suspect I&#8217;m not the only one who got roadblocked this way. I came up with idea after idea,
but my programs came up with counterexample after counterexample, and eventually, I had to choose
between (a) splitting my already numerous cases into smaller cases with little hope that I could
cover all of them, or (b) abandon the conjecture for now and move on to a different topic.

Fortunately, my research partner actually knew what he was doing, and during the time I had spent
trying to solve the open question, he had found some interesting patterns regarding abelian
complexity in a certain class of words. For instance, with the help of Mathematica, he showed me
graphs of abelian complexities for infinite words that resembled fractal patterns. We soon made his
findings our primary research focus and dedicated ourselves to explaining why these graphs showed up
the way they did, and if there was an efficient algorithm to actually compute abelian complexities.

Over the next few weeks, we would prove a variety of lemmas, come up with additional conjectures,
create almost a hundred Python scripts, and write up our results in what would eventually become a
25-ish page paper that we gave to Francine just before the conclusion of the program. Thus, what
started out as a bunch of pictures eventually turned into algorithms and mathematically rigorous
theorems. I never did prove the conjecture I first worked on, and after contacting the person who
actually formed the conjecture (he was in the REU last year), it seemed like he had tried a similar
version of a proof &#8212; albeit on a smaller scale &#8212; that I had done but failed as well.

Overall, I believe this REU really gives students a sense of research beyond the stereotypical
advisor-student relationship. Previously, my research &#8212; even at another REU &#8212; mostly
consisted of the following cycle:

Faculty Advisor: &#8220;Do task X&#8221;  
Me: &#8220;Yes, sir/ma&#8217;am&#8221;

Instead, it was more like we really got to look at what we wanted to explore. Heck, one student
somehow made heavy use of [complex analysis][4] in his research. I still haven&#8217;t been able to
figure out the connection.

My learning obviously wasn&#8217;t just limited to algorithmic combinatorics on words. For instance,
I found out that I&#8217;m as clear a [type one personality][5] as it gets (though I was close to
testing as a [type six][6]), that my diet is incredibly strange, that machine learning is more
important to the national government than theory or algebraic geometry, and a whole host of other
things. (Actually, I suspected these were true prior to coming, but my experience there all but
confirmed them. Also, I don&#8217;t know anything about algebraic geometry.) I do hope, though, that
I was able to teach the other students as much as they taught me.

**Other Thoughts**

One of the defining features of this REU is that it&#8217;s heavily structured. The work day is six
days a week from nine to five daily, with Sundays off. (Note to future/prospective REU students: If
you plan on setting aside a full weekend for your own non-research related activities in the summer,
then this program isn&#8217;t for you.) Students are expected to be in our designated classroom by
9:00 AM each morning. At that time, Francine comes into the room and briefly meets with each group
to discuss their progress and to provide feedback.

The classroom itself is where many students do research, which reminds me of Google-style facilities
where there are no individual offices or labs. There are [tradeoffs][7] to this kind of &#8220;open
plan&#8221; work environment; it allows for greater interaction among groups and quick feedback, but
it can get distracting at times. Fortunately, there&#8217;s a computer science lab nearby where
students can work if they want a more serene environment. I sometimes worked there even though I
could have simply turned off my hearing aids in the classroom and not get distracted. (Turning off
my hearing aids presents a whole host of problems.) Even if one wants complete isolation, there are
so many accessible classrooms in the science building that this objective is not difficult to
accomplish.

Saturdays are unique work days, with REU-sponsored pizza for lunch and typically some sort of event,
such as a presentation on LaTeX. During the end of the fourth and eighth weeks of the REU, we all
convened together to present our research. This consisted of about seven fifty-minute talks, so it
does consume the full work day. There is a coffee machine in the classroom, so unless you&#8217;re
like me and hate coffee, you should get enough caffeine to stay focused.

Surprisingly, this REU isn&#8217;t all about work. At least from my experience, the RAs and students
formed social activities such as hiking (see the image at the top of this post), card games, movie
nights, and dinners. We had a Facebook group to help in this regard, which was especially useful
since the fourteen of us were divided among five different houses, which were not next to each
other. Incidentally, housing quality will obviously depend on whichever house you&#8217;re assigned
to live in. I was probably assigned to the worst one, but I still had a decent-sized bedroom and a
functioning bathroom/kitchen, so I survived.

The campus and nearby area is decent enough. There are plenty of restaurants and eating places near
the working area, which means it&#8217;s possible to go out for lunch at Subway, Jimmy Johns, Thai
food, etc. There are also a variety of fields, basketball courts, and a gym where people can
participate in sports and other activities outside of work. The weight room &#8212; located in the
student recreation center &#8212; isn&#8217;t *that* bad, since it actually has a [power rack][8].
Yes, it has its share of bozos who spend their entire gym sessions doing curls and who can&#8217;t
[squat correctly][9], but I did meet two other guys there who actually knew a thing about barbell
training. And I was even able to convince another REU student to join me in the gym. (Here, a one
out of thirteen ratio is impressive.)

I&#8217;m probably forgetting a whole host of other things I wanted to write about, but I think the
above summarizes some of the interesting things about the REU.

Good luck to everyone who went and I wish you all the best.

 [2]: http://www.uncg.edu/cmp/reu/
 [3]: http://www.amazon.com/Algorithmic-Combinatorics-Discrete-Mathematics-Applications/dp/1420060929
 [4]: http://en.wikipedia.org/wiki/Complex_analysis
 [5]: http://www.eclecticenergies.com/enneagram/type1.php
 [6]: http://www.eclecticenergies.com/enneagram/type6.php
 [7]: http://www.pgbovine.net/open-vs-closed-offices.htm
 [8]: http://en.wikipedia.org/wiki/Power_cage
 [9]: http://stronglifts.com/how-to-squat-with-proper-technique-fix-common-problems/
