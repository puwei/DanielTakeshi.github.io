---
title: On Data Wrangling
author: Daniel Seita
layout: post
permalink: /2014/09/25/on-data-wrangling/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - Big Data
  - data science
  - data wrangling
  - machine learning
---

<img src="{{site.url}}/assets/data_science.jpg" alt="data_science">

Last month, the New York Times [published an interesting article][2] that connected with my
experience working as a computer scientist. The idea is that there&#8217;s so much data out there
&#8212; in case you&#8217;ve been living under a rock, it&#8217;s the age of Big Data &#8212; but
it&#8217;s becoming increasingly harder for us to make sense of it so that we can actually *use* the
data well. Here's a relevant passage:

> But if the value comes from combining different data sets, so does the headache. Data from
> sensors, documents, the web and conventional databases all come in different formats. Before a
> software algorithm can go looking for answers, the data must be cleaned up and converted into a
> unified form that the algorithm can understand.

So why does this article connect to me? *Every major computer science project* I've worked on has
involved a nontrivial amount of data &#8220;wrangling&#8221; (for lack of a better word), such as
the one I worked on at the [Bard REU][3]. I also had a brief internship last summer where my job was
to implement [Latent Dirichlet Allocation][4], and it took me a substantial amount of time to
convert a variety of documents (plain text, .doc, .docx, .pdf, and others) into a format that the
algorithm could easily use.

Fortunately, many researchers are trying to help us out, such as professors [Jeff Heer][5] at the
University of Washington and [Joe Hellerstein][6] at the University of California, Berkeley. I met
Jeff when I was [visiting the school a few months ago][7], and he gave me an update on the amazing
work he and his group have done.

Meanwhile, as I finished reading the article, I was also thinking about how our computer science
classes should prepare us for the inevitable amount of data wrangling we&#8217;ll be doing in our
jobs. The standard machine learning computer science project, for instance, will tell us to
implement an algorithm and run it on some data. That data, though, is often formatted and
&#8220;pre-packaged,&#8221; which makes it easier for students but typically doesn&#8217;t provide
the experience of having to deal with a haphazard collection of data.

So I would suggest that in a data-heavy computer science class, at least one of the projects should
involve *some* data wrangling. These might be open-ended projects, where the student is given little
to no starter code and must implement an algorithm while at the same time figuring out how to deal
with the data.

On a related note, I should also add that students should appreciate it when their data comes nicely
formatted. *Someone* had to assemble the data, after all. In addition, for many computer science
projects, such as the [Berkeley Pacman][8] assignments, much of the complicated, external code has
already been written and tested, making our jobs much easier. So to anyone who is complaining about
how hard their latest programming project is, just remember, someone probably had to work twice as
hard as you did to *prepare* the project and its data in the first place.

 [1]: https://seitad.files.wordpress.com/2014/09/data_science.png
 [2]: http://www.nytimes.com/2014/08/18/technology/for-big-data-scientists-hurdle-to-insights-is-janitor-work.html
 [3]: http://danieltakeshi.github.io/2012/07/27/wrapping-up-my-summer-research/
 [4]: http://machinelearning.wustl.edu/mlpapers/paper_files/BleiNJ03.pdf
 [5]: http://homes.cs.washington.edu/~jheer/
 [6]: http://db.cs.berkeley.edu/jmh/
 [7]: http://danieltakeshi.github.io/2014/03/29/graduate-school-visit-4-the-university-of-washington/
 [8]: http://inst.eecs.berkeley.edu/~cs188/pacman/project_overview.html
