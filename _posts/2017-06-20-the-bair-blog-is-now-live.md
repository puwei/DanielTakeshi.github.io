---
layout:     post
title:      "The BAIR Blog is Now Live"
date:       2017-06-20 9:00:00
permalink:  2017/06/20/the-bair-blog-is-now-live/
---

<p style="text-align:center;"> 
<img src="{{site.url}}/assets/BAIR_Logo_BlueType_Tag.png" width="600"> 
</p><br>

The word should now be out that BAIR --- short for Berkeley Artificial
Intelligence Research --- now has a blog. The official [BAIR website is here][1]
and the [blog is located here][2].

I was part of the team which created and set up the blog. The blog was written
using Jekyll so for the most part I was able to utilize my prior Jekyll
knowledge from working on "Seita's Place" (that name really sounds awful,
sorry).

One neat thing that I learned throughout this process was how to design a Jekyll
blog but then have it appear as a *sub-directory* inside an *existing* website
like the BAIR website with the correct URLs. The key is to understand two
things:

- The `_site` folder generated when you build and preview Jekyll locally
  contains all you need to build the website using normal HTML. Just copy over
  the contents of this folder into wherever the server is located.

- In order to get *links* set up correctly, it is first necessary to understand
  how "baseurl"s work for project pages, among other things. [This blog post][3]
  and [this other blog post][4] can clarify these concepts. Assuming you have
  correct `site.url` and `site.baseurl` variables, to build the website, you
  need to run 

  `
  JEKYLL_ENV=production bundle exec jekyll serve
  `

  The production mode aspect will automatically configure the contents of
  `_site` to contain the correct links. This is extremely handy --- otherwise,
  there would be a bunch of annoying `http://localhost:4000` strings and we'd
  have to run cumbersome find-and-replace commands. The contents of this folder
  can then be copied over to where the server is located.

Anyway, enough about that. Please check out our inaugural blog post, about an
exciting concept called *Neural Module Networks*.


[1]:http://bair.berkeley.edu/
[2]:http://bair.berkeley.edu/blog/
[3]:https://byparker.com/blog/2014/clearing-up-confusion-around-baseurl/
[4]:http://downtothewire.io/2015/08/15/configuring-jekyll-for-user-and-project-github-pages/
