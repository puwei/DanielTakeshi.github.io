---
title: Project Euler 179
author: takeshidanny@gmail.com
layout: post
permalink: /?p=143
geo_public:
  - 0
  - 0
dsq_thread_id:
  - 3755961542
categories:
  - Computer Science
tags:
  - Java
  - optimization
  - Project Euler
---
[Project Euler][1] is an interesting website that offers about 400 different mathematics and computer programming questions. They range from easy (finding the sum of some set of big numbers) to impossible (navigating through Rudin-Shapiro sequences). Just recently, I solved the 179th question with the help of some Java code. While my program gave me the correct answer, the execution time on my Macbook Pro laptop was 80 seconds &#8212; and there is an informal &#8220;60 seconds&#8221; rule that implies that code should be able to solve a problem in less than 60 seconds. So I wanted to determine in what ways I could optimize my code.

Here was the question: Find the number of integers 1 < n < 10^7, for which n and n + 1 have the same number of positive divisors. For example, 14 has the positive divisors 1, 2, 7, 14 while 15 has 1, 3, 5, 15.

This wasn&#8217;t too bad for me. I already had a method that could compute the sum of the divisors of a number based on problem 23, so I revised it to add up the *number* of divisors, rather than the sum. Then I just iterated through each number from 1 to 10 million. Here was the first version of my code:

[sourcecode language=&#8221;java&#8221;]  
public class ProjectEuler179 {  
public static void main(String[] args) {  
long startTime = System.currentTimeMillis();  
int result = 0;  
int prevDivisors = 2;  
for (int i = 3; i <= 10000000; i++) {  
int currentDivisors = numberOfDivisors(i);  
if (currentDivisors == prevDivisors) {  
result++;  
}  
prevDivisors = currentDivisors;  
}  
System.out.println("The number of integers is: " + result + ".");  
long endTime = System.currentTimeMillis();  
System.out.println("Execution time: " + (endTime &#8211; startTime) + " ms.");  
}

public static int numberOfDivisors(int x) {  
int numOfDivisors = 2;  
for (int k = 2; k <= Math.sqrt(x); k++) {  
if (x % k == 0) {  
if (k != Math.sqrt(x)) {  
numOfDivisors += 2;  
} else {  
numOfDivisors += 1;  
}  
}  
}  
return numOfDivisors;  
}  
}  
[/sourcecode]

I&#8217;m not going to say what the answer was, but as mentioned before, the execution time (endTime &#8211; startTime) was about 80 seconds. Looking at the code, the limiting factor is the 10 million calls I make to the method numOfDivisors(). So how can I improve this? In other words, how can I avoid making all those calls to my static method here?

To start, I initialized an array of 10,000,001 elements, called divs, where divs[x] refers to the number of divisors of x. Then, I used two nested for loops to make sure that each entry of divs[x] *did* hold the number of divisors of x. The outer for loop went from int i = 1 to 10,000,000, and the inner for loop went as far from int j = 1 to as large a number such that i*j <= x. This implies that all divisors for a number are counted! For instance, if we had the number 2, which has the divisors of 1 and 2, then the entry divs[2] should be incremented twice &#8212; which it is, because of i=1 and j=2 first, then i=2, j=1 second.

Here, I avoid all the testing of &#8220;is a number is a factor of another number?&#8221;, as I do in my old code, because if I consider i*j = n, then I know that n has at least those two factors!

The updated code is as follows:

[sourcecode language=&#8221;java&#8221;]  
public class ProjectEuler179 {  
public static void main(String[] args) {  
long startTime = System.currentTimeMillis();  
int result = 0;  
int[] divs = divisors(10000000);  
for (int i = 2; i < 10000000; i++) {  
if (divs[i] == divs[i+1]) {  
result++;  
}  
}  
System.out.println(result);  
long endTime = System.currentTimeMillis();  
System.out.println("Execution time: " + (endTime &#8211; startTime) + " ms.");  
}

public static int[] divisors(int x) {  
int[] divs = new int[x + 1];  
for (int i = 1; i <= x; i++) {  
for (int j = 1; i * j <= x; j++) {  
divs[i*j]++;  
}  
}  
return divs;  
}  
}  
[/sourcecode]

It gave me the right answer. And the runtime was an amazingly quick 1.9 seconds &#8212; much, much better! I don&#8217;t claim full credit for this second code, as I read the discussion forum for that problem after I solved it the first time, but it&#8217;s still nice to know how to optimize a program.

 [1]: http://projecteuler.net "Project Euler"