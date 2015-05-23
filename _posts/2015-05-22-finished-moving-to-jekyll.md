---
layout: post
title:  "Finished the Wordpress-to-Jekyll Migration"
date:   2015-05-22 17:20:00
permalink: 2015/05/22/finished-moving-to-jekyll.html
---

In my [last post][1], I talked about the process of migrating my Wordpress.com blog into this Jekyll
blog. I finally finished this process --- at least, to the extent where nothing is left but
touch-ups --- so in this post, I'd like to explain the final migration steps.

## The Manual Stuff

Let's start with the stuff that I put off as long as possible: checking *every single post* to fix
*every single blog-to-blog post link* and *every single image*.  With 150 posts, this was not the
most fun activity in the world.

Due to the transition to Jekyll, the old blog-to-blog links[^clarify] that I had in my blog posts
were no longer valid. To fix those up, I went through every single blog post, checked if it
referenced any other blog posts as links, and changed the link by replacing `seitad.wordpress.com`
with `danieltakeshi.github.io`. Remember, this is only valid because I changed the Wordpress.org way
of permalinks to match Jekyll's style.  If I had not done that, then this process would have
involved more editing of the links.

I also fixed the images for each post. For each post that uses images, I had to copy the
corresponding file location in my old folder that contained my Wordpress.com images, and paste them
into the `assets` folder here. Then, I fixed the image HTML in the Markdown file so that they looked
like this:

~~~
<img src="{{site.url}}/assets/image_name" alt="some_alt_text">
~~~

By keeping all images in the same directory, they have a common "skeleton" which makes life easier,
and `image_name` is the file name, including any `.png`, `.jpg`, etc. stuff. The `some_alt_text` is
in case the image does not load, so an alternative text will appear in place of the image.

## The Interesting Stuff

Incorporating LaTeX into my posts turned out to be easier than expected. Unlike in Wordpress, where
I had to do a clumsy `$latex ... $` to get math, in Jekyll + MathJax (which is the tool to
get LaTeX to appear in browsers) I can do `$$ ... $$`. For example: `$$\int_0^1 x^2dx$$` results in
$$\int_0^1 x^2dx$$. It does require two extra dollar signs than usual, but nothing is perfect.

Note: to get MathJax, I pasted the following code at the end of my `index.html` file:

~~~
<script type="text/javascript" 
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
~~~

There were a few other things I wanted to do after incorporating math, and they also required
modifying `index.html`:

- To have all the post content appear on the front page rather than only the titles.  The latter
  case forces the user to click on the title to see any of the content.
- To add pages on the home page so that the first page (the default one) would display the 20 most
  recent posts, then the next page would list the next 20, etc.

To get the post content to appear, in `index.html` where it loops through the posts in the site,
there is a place where one can post the content by using the `post.content` variable[^excerpt]. To
get the pages, see [this blog post][2] which explains that one needs to add the `paginage: X` line
in the `_config.yml` file, where `X` is clearly the amount of posts per page. Then, one can loop
through the `paginator.posts` variable to loop through the posts. To get a page counter at the
bottom that lets you jump from page to page, you need to use the `paginator.previous_page`,
`paginator.page`, and `paginator.next_page` variables. Again, see the linked blog post, which
explains it clearly.

## The Future

There are certainly a bevy of things I could do to further customize this blog. I'll probably add
some Google Analytics stuff later to track my blog statistics, but I don't view that as a high
priority.  Instead, I would like to start writing about more computer science topics.

***

[1]: http://danieltakeshi.github.io/2015/05/14/moved-to-jekyll.html
[2]: http://learn.andrewmunsell.com/learn/jekyll-by-example/tutorial

[^clarify]: Just to be clear: these are when blog posts link to another blog posts in the text, such
    as by saying "click HERE to see my earlier statement", where "HERE" is replaced with the link.

[^excerpt]: It's also possible to use `post.excerpt` which will only display part of a post on
    the home page, but I found that it messed up the links within the post.

