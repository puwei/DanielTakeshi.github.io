---
title:      Five Years of Blogging
date:       2016-08-20 12:00:00
permalink:  2016/12/30/five-years-of-blogging/
layout:     post
---

I survived. I have now been blogging for five years.

Technically, it's been five years and 20 days. Sorry. As nice as it would have been to nail down
five years *exactly*, I had some urgent work to do in the beginning of August.  But despite all the
constant work that's being thrown at me (it's my fault) I have somehow been able to keep cranking
out at least one blog post each month for five years[^general]. Given how tough it is to maintain a
long commitment to nonessential writing projects, I wonder if any of my early readers (from 2011 to
2013) thought I would last this long. 

This is a message towards *all* readers: I hope you enjoy some of what I write. I have been
pleasantly surprised by the amount of comments and emails I get about the blog. These come almost
every week, and it's especially nice when the sender is someone I know or someone who I can easily
meet in person most days.  It gives us a chance to talk, regardless of whether it's related to
what I wrote or not. I also know that the vast majority of readers won't be commenting or emailing,
so the blog audience is much larger than I think. What's interesting is that while a lot of people
seem to like *reading* blogs, they don't like *writing* one. My efforts in encouraging other people
to start their own blogs has failed catastrophically. I think my current success rate is 0 for 20.

Incidentally, I don't have to follow Rule #1 of the Internet: "don't read comments." I hope that I
--- and the readers --- will never have to follow that rule[^comments].

Since this is a special moment in the blog's history, I decided it was high time to do a few major
updates that I had been putting off for ages.

1. I updated the ["About"][1] and ["New? Start Here"][2] pages, which have been begging for a
    do-over ever since this blog [migrated from Wordpress to Jekyll][5]. The former was pretty easy
    to fix; for the latter, I decided to try and provide a few examples of my favorite posts.  With
    over 200 posts so far (the exact number, including this one, is 215) I had a wide range to
    choose from.

2. I have been rewriting some of my older political posts ([see here for one example][4]). Every now
    and then, I do these changes because I get hives when I read some of my earlier writings. I like
    to have a reasonably high standard of writing, or at least to what is generally possible within
    the constraints of a blog post and lack of any editors helping me.

    *A note regarding political posts:* I'll do my best to avoid these for the near future. Why? I'm
    getting weary of politics, first of all. Second, almost anyone can blog about poltics with
    varying degrees of quality, meaning that this blog wouldn't be as unique as I want it to be.
    Third, politics causes unnecessary conflict between people with different beliefs, and I am not
    interested in burning any bridges with the people who I work with.  Of course, given the
    near-uniformity liberalness of the Berkeley faculty and student body (and EECS is no exception
    in this regard), I can *probably* get away with writing political posts just by bashing
    conservatives. On the other hand, I think a lot of people who know me are aware of my
    self-proclaimed "centrist Democrat" leanings, so it doesn't quite seem right to do
    that.[^sanders]

    Regardless of what I believe, whether it is politics or otherwise, I am an even *firmer*
    believer in that we must keep an open mind. If I publish blog posts about particularly sensitive
    subjects, it does not mean I have exhaustively researched the area or that my opinion is fixed.
    I take pride in the amount that I read nowadays, so if there's an issue I care about, chances
    are I'm trying to read up a lot to learn more.

3. I also updated [the DeepRL post related to the class I took last year][3]. I really want to write
    more about DeepRL here, as that's an exciting field. It just takes *so darn long* to write high
    quality posts [like Andrej Karpathy's recent reinforcement learning guide][7]. I wrote a lot of
    blog posts related to my notes when I was studying for the AI prelims last summer, and those
    took a *really* long time to polish. My goal is to have several smaller posts that together
    cover a lot of DeepRL and which follow Andrej's posting style. I have my first reinforcement
    learning post in draft stage (roughly 50% done) and hope to make it public within two weeks. Or
    maybe two months, who knows?

4. I changed this blog to use https instead of http, since I want to use the more secure protocol,
    and it turns out that the MathJax (which renders LaTeX math for my posts) does not appear with
    https. I needed to do several things to get this set up properly:

    - I followed the [directions to enforce https on GitHub Pages][8]. It's literally one checkbox
      to click, very easy!

    - In the ```_config.yml``` file, I changed the site URL to
      ```https://danieltakeshi.github.io```. This is needed because my HTML code to display figures
      uses the site URL variable.

    - In two places, I had to change the MathJax script so that the link they use has https instead
      of http. The two locations to add this are in ```index.html```  and ```_layouts/post.html```.
      The former is so that MathJax is visible on the homepage, where one can scroll to see many
      posts, and the latter is for individual posts when clicking on their titles (or from the
      archives).  Here's what the script segment looks like:

      ~~~
      <script type="text/javascript" 
      src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
      </script>
      ~~~

    - Finally, I migrated all comments from http URLs to ones with the same name, but with https
      instead. This is necessary because Disqus links comments to specific URLs, so if I switched
      back and forth between http and https, I would see two different comment threads. Fortunately,
      [someone already wrote a great guide][6] on how to use the built-in Disqus URL mapping, and it
      was straightforward to follow.

    Whew! I *think* that's it.
    
5. I also modified several posts to fix them based on some of the lingering side effects of the
    [Wordpress-to-Jekyll migration][5]. For instance, I find centered text paired with left-centered
    images to look egregiously sloppy. The importer I used for the migration process automatically
    formed image tags, but it did not *center* them. For that, I have to use the following HTML
    code:

   ~~~
   <p style="text-align:center;">
       <img src="https://danieltakeshi.github.io/assets/image_name.png"> 
   </p>
   ~~~
    
    where ```image_name.png``` should be replaced with whatever image name I am using.
    
    I also observed that the importer didn't always correctly bold or italicize the text.  Sometimes
    the asterisks I need for those would be one space off, but that spacing would throw off the
    formatting entirely.  Ugh. This is always going to be a work in progress, I suppose, especially
    because I can't easily write a script to automate it.

So, what's the plan for the future? At some point I will threaten to quit blogging but not right now
as there are many things I still want to write about. With some heavy work ahead of me, I really
want to aim for more technical posts to help me learn about challenging topics. I want to write some
occasional "guides on X" where X is a concept in computer science, to help out the community.

Last thing: for years, I've been trying to get a new name change for the blog, as "Seita's Place"
has to be the lamest blog name of all time. Unfortunately, I can't come up with anything better.

That's all for now. Thanks for reading!

***

[^general]: As a general rule, if there hasn't been a blog post in a month and it's approaching the
    25th day of it, I'm scrambling behind the scenes to get something done.

[^comments]: Well, all right, if I can become a high-ranking politician then the tradeoff *might* be
    worth it, but what are the odds of me entering such a toxic field?

[^sanders]: (Sarcasm) I expect to be confronted by a bunch of angry Bernie Sanders supporters when I
    get back to Berkeley.

[1]:https://danieltakeshi.github.io/about/
[2]:https://danieltakeshi.github.io/new-start-here/
[3]:https://danieltakeshi.github.io/2015-12-17-review-of-deep-reinforcement-learning-cs-294-112-at-berkeley/
[4]:https://danieltakeshi.github.io/2015/12/08/why-dont-democrats-do-this-instead/
[5]:https://danieltakeshi.github.io/2015/05/14/moved-to-jekyll/
[6]:https://woorkup.com/migrate-disqus-comments-https/
[7]:https://karpathy.github.io/2016/05/31/rl/
[8]:https://help.github.com/articles/securing-your-github-pages-site-with-https/
