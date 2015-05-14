---
layout: post
title:  "Welcome to Jekyll!"
date:   2015-05-12 15:16:49
categories: jekyll update
---

# A New Era

This post marks the beginning of a new era for my blog. For almost four years, it was hosted by
Wordpress.com. Over the past few months, I've realized that Wordpress.com isn't quite what I want
for the long run. It took me four years and over 150 posts (to be precise, this is post number 152)
for me to make the switch to Jekyll.
    
Many others have discussed why this might be the case, but here are a few for me:

- I wanted to feel like I had more control over my site, rather than just writing some stuff up and
  then handing it over to a database to do all the work.
- I was tired of various advertisements clogging my view beneath the posts
- I wanted to get more experience with using git and GitHub, which will be useful for me as I
  continue to work in computer science.
- I wanted to use my own personal text editor (vim is my current favorite and default choice)
  rather than Wordpress's WYSIWYG.
-  etc.

In fact, I even just now realized the difference between Wordpress.com and Wordpress.org. I had
Wordpress.com, arguably the worse of the two, and only useful for those who want to get a quick
start on blogging. As one of the older guides say, Oh well.

I am slowly, but surely, becoming a real computer scientist. I was not someone who took a crazy
amount of computer science or did a lot of programming before college, so I often feel like I am
handicapped. Hopefully having more control over this blog, and having an easier time with math and
code, will help me in this process.

Jekyll was created by a guy who created GitHub. By the way, in the computer science community, that
is known as credibility, the equivalent of a Yale Law School degree.

# How Did I Migrate?

Oh, wow. The migration process did not go as planned. I was hoping to get that done in about two
hours, but it took me about ten, spanning across two days. Fortunately, since the semester is over
for me and it's summer, there is no better time for me to work on this stuff.
    
So here's how I did it.

- Used Bluehost to create a Wordpress.org site (this is costing me 71 dollars, and I hate Bluehost
  because they seem to spam me with money messages, so I'm going to use their 30 day off to get out
  of their service.)
- Migrate from Wordpress.com to Wordpress.com
- Then use the wordpress to jekyll by Ben (on the Github staff) to create another .xml file.
- Use jekyll to create a directory, unzip, etc.
- Copy disqus comment code
- Also explain github integration (oh, my entire blog is backed up by github! Nice!)

But what *really* took a long time to migrate correctly were the old comments I had. I don't get
very many comments on this blog, but for the most part, they've been nice to see and I didn't want
them to just disappear. The fix was to use Disqus, but reading a bunch of guides alone did not help,
so I had to figure out a lot of thigns on my own.

- Apparently, we also have to do a SECOND import. Yeah...

The following blog posts were useful for me as an aid to learning:

- Girlie Mac
- Hari Hari

The Jekyll docs themselves, by the way, were not much help. I worry when we need to rely on blog
posts for help, but whatever... Amusingly enough, the Jekyll docs actually linked certain blog
posts. Blog posts do go out of date soon, right?

# Quick Impressions

Well, I am impressed with the simplified look so far.

- Simplified code
- Footnotes are really easy! Just click on them, and then click a link to get back to where we were
- etc.

# Next Steps

I have a couple of plans for this summer. First, the ones related to Jekyll are:

- Well, I'm not finished with this process. I'm still getting the images, links, and other stuff
  working. If you see any dead links or anything like that, please contact me. I also need to get a
  reasonable design up and running.
- Learn more Markdown, and also figure out a nice text editor for Markdown. The use of vim for me is
  already great, but one issue is that I'm not sure how easy it is to put Markdown-style hyperlinks,
  for instance. But there has to be some vim tool out there, so I will search for that first. For
  Markdown, what I'd really like to do is get some nice math up here. (The code, I showed in an
  earlier segment.)
- As far as the old wordpress.com site, I guess I'll make a site redirect, since I'd rather all site
  traffic go here now, not there.

And what about this summer?

- I'm going to *try* and actually post some real computer science-related stuff here, so that I can
  look it up here in a pinch. Perhaps some prelim review material would also be good to have, and
  I'll definitely need to study over the summer. I can't wait until the semester begins, after all!

# Older Stuff

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see
your changes. You can rebuild the site in many different ways, but the most common way is to run
`jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention
`YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for
this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all
bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them
on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
