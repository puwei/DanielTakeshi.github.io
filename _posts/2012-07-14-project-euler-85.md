---
title: Project Euler 85
author: Daniel Seita
layout: post
permalink: /2012/07/14/project-euler-85/
categories:
  - Computer Science
tags:
  - Project Euler
  - Python
---
A few weeks ago, I remember solving a Project Euler question that particularly intrigued me. I saw problems similar to this when I was in middle school, but never recalled myself successfully solving something them. For reference, the problem was [Project Euler 85][1], counting the number of rectangles in a rectangular grid.

But when I attempted this particular problem? It took me fewer than thirty minutes to think of a solution and code it. So what changed?

> I believe it&#8217;s been my new algorithmic approach to solving problems.

I fully admit that I&#8217;m a brute-force, &#8220;try-them-all&#8221; kind of person. Whenever I see a problem of the form &#8220;*How many X satisfy the property Y*,&#8221; my first instinct is to go through all possible candidates of X and store a count of how many satisfy Y. I first approached this problem by remembering what I did years ago &#8212; count rectangles by hand. The questions I experienced back then were much easier in that it was feasible, though time consuming, to actually count all the possible rectangles. Of course, it&#8217;s so easy to miss or double-count a few rectangles here and there that I was bound to be off in my final answer.

So I realized I needed a formulaic, or algorithmic, approach to this problem. There had to be some formula out there that could take as input just the dimensions of the largest rectangle, and use that information to compute the total amount of rectangles contained within it.

There was. I started by counting rectangles by hand for rectangles of a small scope (e.g. a 2&#215;3 one), and then testing my conclusions on other small rectangles. This was my algorithm:

> total = 0  
> for i: 1 to n, inclusive  
> for j: 1 to m, inclusive  
> total += (n-i+1)*(m-j+1)  
> return total. 

Basically, I consider all the possible dimensions of a smaller rectangle within a larger, n-by-m rectangle. (For instance, I could consider all 1&#215;1 rectangles.) Then I use the (n-i+1)*(m-j+1) formula I derived which computed all the possible rectangles! It was very pleasing for me to solve this problem, and I know that I would be able to solve questions relating to counting rectangles within rectangles with an algorithms-based approach.

For reference, here was my actual code. It&#8217;s written in Python. (I used Java to solve the first 50 or so problems, but since then, it&#8217;s been Python all the way.) The code gave me the correct answer in fewer than five seconds.

[sourcecode language=&#8221;python&#8221;]  
import math

def computeRectangles(row, col):  
total = 0  
for r in range(1, row + 1):  
for c in range(1, col + 1):  
total += (row &#8211; r + 1) * (col &#8211; c + 1)  
return total

smallestDiff = 2000000  
area = -1  
finalRow = -1  
finalCol = -1  
for row in range(1,101):  
for col in range(1,101):  
rectangles = computeRectangles(row, col)  
diff = math.fabs(rectangles &#8211; 2000000)  
if (diff < smallestDiff):  
area = row * col  
smallestDiff = diff  
finalRow = row  
finalCol = col  
print &#8216;Result: [%s]x[%s] with area of %s.&#8217; %(finalRow, finalCol, area)  
[/sourcecode]

I have to thank Project Euler for not just giving me a medium through which to practice programming, but also for lending me a new perspective on problem solving approaches. I&#8217;m just two solutions away from level 3 at this time&#8230;.

*This post is part of a series of posts related with my solutions to selected Project Euler questions.*

 [1]: http://projecteuler.net/problem=85