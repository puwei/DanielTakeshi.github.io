---
title: Review of Natural Language Processing (CS 288) at Berkeley
author: Daniel Seita
layout: post
permalink: /?p=2166
geo_public:
  - 0
  - 0
categories:
  - Computer Science
tags:
  - automatic speech recognition
  - class review
  - Dan Klein
  - Michael Jordan
  - natural language processing
  - programming projects
---
[<img class="aligncenter size-large wp-image-2167" src="http://www.seitad.com/wp-content/uploads/2014/12/siri.jpg?w=460" alt="siri" width="460" height="283" />][1]This is the much-delayed review of the other class I took last semester. [I wrote a little bit about Statistical Learning Theory a few <del>weeks</del> months ago][2], and now, I&#8217;ll discuss Natural Language Processing (NLP). Part of my delay is due to the fact that the semester&#8217;s well underway now, and I have real work to do. But another reason could be because this class was so incredibly stressful, more so than *any other class* I have ever taken, and I needed some amount of time to pass before writing this.

Before I get to that, let&#8217;s discuss what the class is about. Natural Language Processing (CS 288) is about the study of natural languages as it pertains to computers. It applies knowledge from linguistics and machine learning to develop algorithms that computers can run to perform a variety of language-related applications, such as automatic speech recognition, parsing, and machine translation. My class, being in the computer science department, was focused on the *statistical* portion of NLP, where we focus on the efficiencies of algorithms and justify them probabilistically.

At Berkeley, NLP seems to be offered every other year to train future NLP researchers. Currently we only have one major NLP researcher, Dan Klein, who teaches it (Berkeley&#8217;s hiring this year so maybe that number will turn into two). There are a few other faculty that have done work in NLP, most notably Michael Jordan and his groundbreaking [Latent Dirichlet Allocation][3] algorithm (over 10,000 Google Scholar citations!), but none are &#8220;pure&#8221; NLP like Dan.

CS 288 was a typical lecture class, and the grading was based exclusively on five programming projects. They were not exactly easy. Look at the following slide that Dan put up on the first day of class:

[<img class="alignnone size-large wp-image-2264 aligncenter" src="http://www.seitad.com/wp-content/uploads/2015/01/cs288_slide.png?w=460" alt="CS288_Slide" width="460" height="345" />][4]I come into every upper-level computer science expecting to be worked to oblivion, so this slide didn&#8217;t intimidate me, but seeing that text there gave me an initial extra &#8220;edge&#8221; to make sure I was focused, doing work early, and engaging in other good habits.

Let&#8217;s talk about the fun part: the projects! There were five of them:

  1. [Language Modeling][5]. This was heavy on data structures and efficiency. We had to implement Kneser-Ney Smoothing, a fairly challenging algorithm that introduced me to the world of &#8220;where the theory breaks down.&#8221; Part of the difficulty in the project comes from how we had to meet strict performance criteria, so naive implementations would not suffice.
  2. [Automatic Speech Recognition][6]. This was my favorite project of the class. We implemented automatic speech recognition based on Hidden Markov Models (HMMs), which provided the first major breakthrough in performance. The second major breakthrough came from convolutional neural networks, but HMMs are surprisingly a good architecture on their own.
  3. [Parsing][7]. This was probably the most difficult project, where we had to implement the CYK parsing algorithm. I remember doing a *lot* of debugging and checking indices of matrices to make sure they were aligned. There&#8217;s also the problem of dealing with unary expressions, since that&#8217;s a special case that&#8217;s not commonly described in most textbook descriptions of the CKY parsing algorithm (actually, the concept of &#8220;special cases not described by textbook descriptions&#8221; could be applied to most projects we did&#8230;).
  4. [Discriminative Re-ranking][8]. This was a fairly relaxing project because a lot of the code structure was built for us and the objective is intuitively obvious. Given a candidate set of parses, the goal was to find the highest ranking one. The CYK parsing algorithm can do this, but it&#8217;s better if that algorithm gives us a *set* of (say) 100 parses, and we run more extensive algorithms on those top parses to pick the best of those, hence the name &#8220;re-ranking.&#8221;
  5. [Word Alignment][9]. This was one that I had some high-level experience with before the class. Given two sentences of different languages, but which mean the same thing, the goal is to train a computer to determine the word alignment. So for an English-French sentence pair, the first English word might be aligned to the *third* French word, the second English word might be aligned to *no *French word, etc.

I enjoyed most of my time thinking about and programming these projects. They trained me to stretch my mind and to understand when the theory would break down for an algorithm in practice. They also forced me to brush up my non-existent debugging skills.

Now, that having been said, while the programming projects were somewhat stressful (though nothing unexpected given the standards of a graduate level class), and the grading was surprisingly lax (we got As just for completing project requirements) there was another part of the class that *really* stressed me out, far beyond what I thought was even possible. Yes, it was attending the lectures themselves.

A few months ago, in the middle of the semester, I wrote a little bit about [the frustration I was having with remote CART][10], a new academic accommodation for me. Unfortunately, things didn&#8217;t get any better after I had written that post, and I think they actually *worsened*. My CART continued to be plagued by technical issues, slow typing, and the rapid pace of lecture. There was also construction going on near the lecture room. I remember at least one lecture that was *filled *with drilling sound while the professor was lecturing. (Background noise is a *killer* for me.)

I talked to Dan a few weeks into the course about the communication issues I was having in the class. He understood and thanked me for informing him, though we both agreed that slowing down the lecture rate might reduce the amount of material we could cover (for the rest of the students, of course, not for me).

Nonetheless, the remaining classes were still insanely difficult for me to learn from, and during *most* lectures, I found myself completely lost within ten minutes! What was also distressing was knowing that I would never be able to follow the question/answer discussions that students had with the professor in class. When a student asks a question, remote CART typically puts in an &#8220;inaudible&#8221; text due to lack of reception and the relatively quiet voice of the students. By my own estimate, this happened 75 percent of the time, and that doesn&#8217;t mean the remaining 25 percent produced perfect captions! CS 288 had about 40-50 students, but we were in a small room so everyone except me could understand what students were asking. By the way, I should add that while I do have hearing from hearing aids and can sometimes understand the professor unaided, that hearing ability* virtually vanishes* when other students are asking questions or engaging in a discussion.

This meant that I didn&#8217;t have much confidence in asking questions, since I probably would have embarrassed myself by repeating an earlier question. I like to participate in class, but I probably spoke up in lecture perhaps twice the entire semester. It also didn&#8217;t help that I was usually in a state of confusion, and asking questions isn&#8217;t always the ticket towards enlightenment. In retrospect, I was definitely suffering from a severe form of imposter syndrome. I would often wonder why I was showing up to lecture when I understood almost nothing while other students were able to extract great benefits from them.

Overall verdict: I was fascinated with *the material itself*, and reasonably liked the programming projects, and the course staff was great. But the fact that the class made it so hard for me to sit comfortably in lecture caused way more stress than I needed. (I considered it a victory if I learned *anything* non-trivial from a lecture.) At the start of the semester, I was hoping to leave a solid impression on Dan and the other students, but I think I failed massively at that goal, and I probably asked way too many questions on the class Piazza forum than I should have. It also adversely affected my CS 281a performance, since that lecture was right after CS 288, which meant I entered CS 281a lectures in a bad mood as a result of CS 288.

Wow, I&#8217;m happy the class is done. Oh, and I am also officially *done* with all forms of CART.

 [1]: http://www.seitad.com/wp-content/uploads/2014/12/siri.jpg
 [2]: https://seitad.wordpress.com/2014/12/30/review-of-statistical-learning-theory-cs-281a-at-berkeley/
 [3]: http://machinelearning.wustl.edu/mlpapers/paper_files/BleiNJ03.pdf
 [4]: http://www.seitad.com/wp-content/uploads/2015/01/cs288_slide.png
 [5]: http://www.cs.berkeley.edu/~klein/cs288/fa14/assignment1.pdf
 [6]: http://www.cs.berkeley.edu/~klein/cs288/fa14/assign_speech.pdf
 [7]: http://www.cs.berkeley.edu/~klein/cs288/fa14/assign_parsing.pdf
 [8]: http://www.cs.berkeley.edu/~klein/cs288/fa14/assign_rerank.pdf
 [9]: http://www.cs.berkeley.edu/~klein/cs288/fa14/assign_align.pdf
 [10]: https://seitad.wordpress.com/2014/10/05/after-a-few-weeks-of-cart-why-do-i-feel-dissatisfied/