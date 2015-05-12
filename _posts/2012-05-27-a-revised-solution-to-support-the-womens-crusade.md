---
title: Project Euler 1 in Several Languages
author: Daniel Seita
layout: post
permalink: /?p=140
geo_public:
  - 0
  - 0
categories:
  - Computer Science
tags:
  - Project Euler
  - Scala
---
Here&#8217;s some code to answer Project Euler 1 in a few languages.

By the way, you do not need code to solve this problem&#8230;

<span style="line-height:1.5;">(1) Java:</span>

[code language=&#8221;java&#8221;]  
public class pe1 {  
public static void main(String[] args) {  
int total = 0;  
for (int i = 3; i < 1000; i++) {  
if (i % 3 == 0 || i % 5 == 0) {  
total += i;  
}  
}  
System.out.println(total);  
}  
}  
[/code]

<span style="line-height:1.5;">(2) Python:</span>

[code language=&#8221;python&#8221;]  
total = 0  
for i in range(1000):  
if i % 3 == 0 or i % 5 == 0:  
total += i  
print(total)  
[/code]

(Alternatively, the one-liner below is probably &#8220;better&#8221;.)

[code language=&#8221;python&#8221;]  
print(sum(x for x in range(1000) if x % 3 == 0 or x % 5 == 0))  
[/code]

(3) C++:

[code language=&#8221;cpp&#8221;]  
#include <iostream>

int main() {  
int total = 0;  
for (int i = 3; i < 1000; i++) {  
if (i % 3 == 0 || i % 5 == 0) {  
total += i;  
}  
}  
std::cout << total << std::endl;  
return 0;  
}  
[/code]

(4) Scala:

[code language=&#8221;scala&#8221;]  
object HelloWorld {  
def main(args: Array[String]): Unit = {  
var result : Int = 0  
for (a <- 1 until 1000) {  
if (a % 3 == 0 || a % 5 == 0) {  
result += a;  
}  
}  
println(a)  
}  
}  
[/code]

Note to self for Scala: **to*** *means it includes the last value, **until*** *means it does not.