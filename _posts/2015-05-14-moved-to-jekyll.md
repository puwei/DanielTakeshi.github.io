---
layout: post
title:  "Seita's Place has Migrated from Wordpress to Jekyll!"
date:   2015-05-14 15:16:49
categories: jekyll update
---

# A New Era

This post marks the beginning of a new era for my blog. For almost four years (!), which saw 151
posts published (this post is #152), Seita's Place was hosted by Wordpress.com. Over the past few
months, though, I've realized that this isn't quite what I want for the long run. I have now made
the decision to switch the hosting platform to Jekyll.

Many people others (e.g., [Vito
Botta](http://vitobotta.com/migrating-from-wordpress-to-jekyll-part-one-why-i-gave-up-on-wordpress/)
and [Tomomi Imura](http://www.girliemac.com/blog/2013/12/27/wordpress-to-jekyll/)) have provided
reasons why they migrated from Wordpress to Jekyll, so you can read their posts to get additional
perspectives.

In my case, I:

- wanted to feel like I had more control over my site, rather than writing some stuff and then
  handing it over to a black-box database to do all the work
- wanted to write more in Markdown and use git/GitHub more often, which will be useful for me as I
  continue to work in computer science
- wanted to more easily be able to write code and math in my posts
- wanted to use my own personal text editor (vim is my current favorite) rather than Wordpress's
  WYSIWYG editor
- was tired of various advertisements underneath my posts
- wanted to be more of a hacker and less like the "ignorant masses," no offense intended folks ... =)

Jekyll, which was created by GitHub founder [Tom
Preston-Werner](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)[^tom], offers
a splendid blogging platform with minimalism and simplicity in mind. It allows users like me to
write posts in plain text files using Markdown syntax.  These are all stored in a `_posts` file in
the overall blog directory. To actually get the site to appear online, I can host it on my GitHub
account; [here is the GitHub repository](https://github.com/DanielTakeshi/DanielTakeshi.github.io)
for this site[^git]. By default, such sites are set to have a URL at `username.github.io`, which for me
would be `danieltakeshi.github.io`. That I can use GitHub to back up my blog was a huge factor in my
decision to switch over to Jekyll for my blog.

There's definitely a learning curve to using Jekyll (and Markdown), so I wouldn't recommend it for
those who don't have much experience with command-line shenanigans. But for me, I think it will be
just right, and I'm happy that I switched.

# How Did I Migrate?

*Oh boy*. The migration process *did not* go as planned. I was hoping to get that done in about
three hours, but it took me much longer than that, and the process spanned about four days (and it's
still not done, for reasons I will explain later). Fortunately, since the spring semester is over,
there is no better time for me to work on this stuff.

Here's a high-level overview of the steps:

- Migrate from Wordpress.com to Wordpress.org.
- Migrate from Wordpress.org to Jekyll
- Migrate comments using Disqus
- Proofread and check existing posts

The first step to do is one that took a surprisingly long time for me: I had to migrate from
Wordpress.com to Wordpress.org. It took me a while to realize that there even *was* a distinction:
Wordpress.com is hosted by Wordpress and they handle everything (including the price of hosting, so
it's free for us), but we don't have as much control over the site, and the extensions they offer
are absurdly overpriced. Wordpress.org, on the other hand, means we have more control over the site
and can choose a domain name to get rid of that ugly "wordpress" text in the URL.

In my case, I had been using Wordpress.com for `seitad.wordpress.com`, so what I had to do was go to
[Bluehost](http://www.bluehost.com/wordpress), pay to create a Wordpress.org site, which I named
`seitad.com`, and *then* I could migrate. The migration process itself is pretty easy once you've
got a Wordpress.org site up, so I won't go into detail on that. The reason why I used Bluehost is
because it's a recommended Wordpress provider, and on their website there's actually a menu option
where you can click to create a Wordpress.org site. Unfortunately, that's about it for my praise,
because I otherwise really hate Bluehost. Did anyone else feel like Bluehost does almost nothing but
shove various "upgrade feature XXX for $YZ" messages down our throats? I was even misled by their
pricing situation and instead of paying $5 to "host" `seitad.com` for a month, I accidentally paid
$71 to host that site for a *year*. I did notice that they had a 30-day money back guarantee, so
hopefully I can hastily finish up this migration and request my money back so so I won't have to
deal with Bluehost again[^gitfree].

To clarify, the only reason why I am migrating to Wordpress.org is because the next step, using a
Wordpress-to-Jekyll exporter plugin, only works on Wordpress.org sites, because Wordpress.com sites
don't allow external plugins to be installed. (Remember what I said earlier about how we don't have
much control over Wordpress.com sites? Case in point!) But before we do that, there's a critical
step we'll want to do: change the permalinks for Wordpress to conform to Jekyll's default style.

TODO describe, include image?

This plugin, founded by GitHub staff member Ben Balter, can be found (you guessed it) [on
GitHub](https://github.com/benbalter/wordpress-to-jekyll-exporter). What you need to do is go to the
"Releases" tab to download a .zip file of the code. Then unzip it, and follow the instructions that
I've taken from the current README file:

1. Place plugin in `/wp-content/plugins/` folder
2. Activate plugin in WordPress dashboard
3. Select Export to Jekyll from the Tools menu

Steps (2) and (3) shouldn't need much explanation, but step (1) is the trickiest. The easiest way to
do this is to establish what's known as an FTP connection to the Wordpress.org server. What I did
was download [FileZilla](https://filezilla-project.org/), a free FTP provider, and used its
graphical user interface to connect to my Wordpress.org site.

TODO screenshot of ftp

Note that to connect to the site, one does *not* generally use his or her Wordpress.org's login, but
instead, one needs to use the login information from Bluehost[^bluehost]! Once I got over that
confusion, I was able to "drag and drop" the wordpress-to-jekyll exporter plugin to the Wordpress
site. Then executing steps (2) and (3) should result in a `jekyll-export.zip` file that contains the
converted HTML-to-Markdown information about blog entries, as well as other metadata such as the
categories, tags, etc.

All right, now that we have our zip file, it's time to create a Jekyll directory with the `jekyll new
danieltakeshi.github.io` command, where `danieltakeshi` should be replaced with whatever GitHub
username you have. Then take that `jekyll-export.zip` file and unzip it in this directory. This
should mean that all your old Wordpress posts are now in the `_posts` directory, *and* that they
are converted to Markdown, *and* that they contain some metadata.

The official Jekyll documentation [contains a
tool](http://import.jekyllrb.com/docs/wordpressdotcom/) that you can use to convert from Wordpress
(or Wordpress.com) to Jekyll. The problem with the Wordpress.com tool is that the original
Wordpress.com posts are *not* converted to Markdown, but instead to plain HTML. Jekyll *can* handle
HTML files, but to really get it to look good, you need to use Markdown. I tried using the
Wordpress.org (not Wordpress.com) tool on the Jekyll docs, but I couldn't get it to work due to
missing some Ruby libraries that later caused a series of dependency headaches. Ugh. I think the
simplicity and how the posts actually get converted to Markdown automatically are the two reasons
why Ben's external jekyll plugin is so popular among migrators.

At this point, it makes sense to try and commit everything to github. The way that the
`username.github.io` site works is that it gets automatically refreshed each time you push to the
master branch. Thus, in your blog directory, assuming you've already initialized a git repository
there, just do something like

~~~
$ git add .
$ git commit -m "First commit, praying this works..."
$ git push origin master
~~~

These commands[^commands] will update the github repository, which automatically updates
`username.github.io`, so you can check the website to see your blog.

One thing you'll notice, however, is that *comments by default are not enabled*. Moreover, *old
comments made on Wordpress.org are **not** present* even with the use of Ben's wordpress-to-jekyll
tool. Why this occurs can be summarized as follows: Jekyll generates static pages, but comments are
*dynamic*. So it is necessary to use an external system, which is where Disqus comes into play.

Unfortunately, this step was what took me a *really* long time to figure out. I'll summarize the
steps as follows:

- In the Admin panel for Disqus, create a new website and give it a "shortname" that we will need
  later. (For this one, I used the shortname `seitasplace`.)
- In the Wordpress.org site, install the Disqus comment plugin[^plugin] and make sure your comments
  are "registered" with Disqus. What this means is that you should be able to view all comments in
  your blog from the Disqus Admin panel.
- Now comes the part that I originally missed, which took me hours to figure out: I had to import
  the comments with Disqus! It seems a little confusing to me, but I guess we have to do it. On
  Disqus, there is a "Discussions" panel, and then there's a sub-menu option for "Import". There, we
  need . The following image should clarify what I mean:

<IMG SRC="{{site.url}}/assets/disqus.png" ALT="disqus_image" WIDTH=256 HEIGHT=256>

- You will also likely need to do some URL mapping.

After several restarts due to some random issues with Disqus/Wordpress having problems with deleted
material, I was *finally* able to get comments imported correctly, and they had the same names
assigned to the commentators! Excellent! The *traceback* comments, which are created by Wordpress
when one blog post links to another blog post, did not get copied over here, but I guess that's OK
with me. I mostly wanted the *human* comments, for obvious reasons.

Whew! <del>So we are done, right</del>? Oh, never mind -- we have to proofread each post!

DRAFT BELOW


# Next Steps

```bash
$ jekyll build
$ jekyll serve
```

These commands will generate a local copy of the 

The Jekyll docs themselves, by the way, were not much help. I worry when we need to rely on
arbitrary blog posts for help[^jekyll].

Well, I am impressed with the simplified look so far.

- Simplified code
- Footnotes are really easy! Just click on them, and then click a link to get back to where we were
- etc.

How to add new posts:

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see
your changes. You can rebuild the site in many different ways, but the most common way is to run
`jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention
`YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for
this post to get an idea about how it works.

Whew! The best part about the migration is that you only have to do it once.

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

***

[^tom]: By the way, saying something like "GitHub co-founder Tom ..." is the computer programming
    equivalent of the law school saying "Yale Law School graduate Bob ...". The fact that he founded
    GitHub immediately hightens my opinion of him. Oh, by the way, do you like how Jekyll does
    footnotes? Just click the little arrow here and you'll be back up to where you were in the
    article!

[^git]: If you have experience using GitHub, then you can even fork my repository on GitHub to serve
    as a launching point for your own site or to test out Jekyll.

[^gitfree]: Just to be clear, if you host a site on a public GitHub repository, then it's free.
    That's yet another reason to use Jekyll/GitHub!

[^bluehost]: This username information should be included in the first email (or one of the first,
    I think) you got from Bluehost. The password should be the password you use to log into
    Bluehost to get to your user control panel.

[^jekyll]: Interestingly enough, [the Jekyll docs for migrating from Wordpress.com to
    Jekyll](http://import.jekyllrb.com/docs/wordpressdotcom/) currently link to an external blog
    post from March 2011. I found that blog post to be reasonably helpful, but it didn't really do
    what I needed, which tends to be a problem when following such guides.

[^commands]: If you're wondering how I was able to get a code block highlighted like that, I wrap
    the commands with three tildas (`~~~`) before and after the text. This is with the `kramdown`
    Markdown scheme.

[^plugin]: Fortunately, you can find this plugin by searching in Wordpress directly; there's no need
    to do some fancy FTP stuff.

