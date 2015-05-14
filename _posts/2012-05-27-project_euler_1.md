---
title: Project Euler 1 in Several Languages
author: Daniel Seita
layout: post
permalink: /2012/05/27/a-revised-solution-to-support-the-womens-crusade/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - Project Euler
  - Scala
---

**UPDATE** May 13, 2015: Wow, look at the Jekyll code support!

Here&#8217;s some code to answer Project Euler 1 in a few languages.

By the way, you do not need code to solve this problem&#8230;

(1) Java:

{% highlight java %}
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
{% endhighlight %}

(2) Python:

{% highlight python %}
total = 0  
for i in range(1000):  
  if i % 3 == 0 or i % 5 == 0:  
  total += i  
print(total)  
{% endhighlight %}

(Alternatively, the one-liner below is probably &#8220;better&#8221;.)

{% highlight python %}
print(sum(x for x in range(1000) if x % 3 == 0 or x % 5 == 0))  
{% endhighlight %}

(3) C++:

{% highlight cpp %}
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
{% endhighlight %}

(4) Scala:

{% highlight scala %}
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
{% endhighlight %}

Note to self for Scala: **to*** *means it includes the last value, **until*** *means it does not.
