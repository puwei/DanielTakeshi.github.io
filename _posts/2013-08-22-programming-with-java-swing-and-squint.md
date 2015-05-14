---
title: Programming with Java, Swing, and Squint
author: Daniel Seita
layout: post
permalink: /2013/08/22/programming-with-java-swing-and-squint/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - Java
  - Squint
  - Swing
---
Since I&#8217;m going to build a complete compiler for a subset of the Java programming language
this fall in my Compiler Design course[^footnote], I thought it would be prudent to at least look through an
introductory Java book over the summer. I want to make sure I didn&#8217;t forget much in the
one-year period from last summer to this one, where I didn&#8217;t touch Java at all. Upon some
thinking and exploration, I decided to do a speed read of the 337-page book *Programming with Java,
Swing, and Squint*. (You can find the [entire book online][1], in the link that lists all the
chapters.) Having just finished the book, I can offer some of my comments.

This book was written by a Williams College computer science professor and is intended to be
supplementary reading material for our introductory programming class. Since I never took the first
(or second!) courses in the typical sequence for the CS major, this might help me fill in some holes
in my knowledge as compared to other Williams College students. According to what I&#8217;ve read
and heard, our first CS class is a straightforward intro-to-Java course, with a special emphasis on
the understanding of networks and digital communication.

*Programming with Java, Swing and Squint* therefore *does not assume any prior Java knowledge* and
is relatively easy to read. For those who are wondering, [Swing][2] is a widely-used application
programming interface that one can import into Java code (put the line ```import javax.swing.*;```
at the top of your code) to provide graphical user interfaces (GUIs) for user programs,
and [Squint][3] is a library specifically designed for the Williams intro CS course.

The book doesn&#8217;t waste any time in introducing the reader to small programs that construct
simple GUI interfaces. At first, the author makes the necessary claim that one has to accept certain
incantations of Java as &#8220;magic words&#8221; that must be included in code in order for it to
run, e.g. the &#8220;public class XXX&#8221; text, but he explains this stuff in the appropriate
(and humorly-named) subsequent chapters. Even the other examples in the book &#8212; email
interfaces, building a calculator, etc. &#8212; are simple enough yet comprehensively presented and
introduce the programmer to a variety of concepts, including (but not limited to) primitives,
objects, classes, methods, control structures, loops, recursion, and arrays. While there is at least
one substantial program for each chapter, the book doesn&#8217;t include any programming exercises
or exercises/solutions. Thus, readers may find that they need to search elsewhere for additional
programming tasks.

My final opinion: this *can* be useful as a first book for someone who has no programming experience
but is interested in writing Java scripts immediately. Even a more advanced programmer can probably
use this book for the purpose of figuring out *how to explain a programming concept to a complete
newbie*. There were many facts about programming and Java that I subconsciously knew but
couldn&#8217;t explain clearly to a layman before today. Thus, I&#8217;m happy to have read this
book even though I already knew almost all of the material.

[^footnote]: Side note: I only have three classes this semester: Compiler Design, Artificial Intelligence, and Complex Analysis. My fourth &#8220;class&#8221; is actually my senior thesis, and my fifth &#8220;extra class&#8221; consists of the graduate school applications.

 [1]: http://dept.cs.williams.edu/~tom/weavingCS/
 [2]: http://docs.oracle.com/javase/tutorial/uiswing/components/
 [3]: http://dept.cs.williams.edu/~tom/weavingCS/s07/squint.html
