---
title: Foundations of Computers
author: Daniel Seita
layout: post
permalink: /2011/11/26/foundations-of-computers/
categories:
  - Computer Science
tags:
  - computers
  - digital logic
  - hardware
---
In my computer organization class, we’ve discussed three major topics: Assembly Language, C
Programming, and Digital Logic. We’re now moving on to our final topic, microcode, but I thought I
would just share some feelings about the third item I listed.

<p style="text-align:center;"> <img src="{{site.url}}/assets/237.gif" alt="237_image"> </p>

Digital logic is incredible. That’s the first thing you should know about it. Logic gates, such as
AND, OR, NOR, and NAND, are the basic building blocks for any computer. They combine to form latches
and flip-flops that, when packaged in large quantities, form memory.

The circuits that I’ve seen so far made me think about efficiency. *How can I better optimize a
digital circuit?* By optimize, I mean use the fewest amount of gates possible. My paradigm right now
is to create what I call a “maximally inefficient” system that works according to whatever objective
I have, but incorporates a ridiculous amount of logic gates. From there, I optimize, such as
sourcing all inverters into one wire, which eliminates multiple NOT gates. That often brings me to
pleasantly few gates, but I’m never sure if it’s completely optimized. I wonder if there are methods
to find out the most efficient circuit for a certain task. (One that I know of now is by using
Karnaugh Maps.)

It’s been an interesting class so far. Our exact progress is 13/18 (this was the answer to an exam
question!) and we’ll be moving on to our notorious and infamous microcode project that’s bound to
keep me working longer hours than investment bankers. They generally work 80-100 hours per week, and
someone &#8212; a student at Williams &#8212; just told me about a record 130-hour week that he
worked as an intern. It’s a good thing my professor has promised to buy us pizza.

