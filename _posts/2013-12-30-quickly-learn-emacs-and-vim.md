---
title: Quickly Learn emacs and vim
author: Daniel Seita
layout: post
permalink: /2013/12/30/quickly-learn-emacs-and-vim/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - Eclipse
  - emacs
  - text editor
  - vim
---
[<img class="aligncenter size-large wp-image-1493" alt="emacs_tutorial" src="http://seitad.files.wordpress.com/2013/12/emacs_tutorial.png?w=460" width="460" height="383" />][1]

Programming as part of a large project, such as building a new C++ compiler from scratch, is vastly different compared to a smaller task, like writing a script to answer a random [Project Euler][2] question. Large projects typically involve too many files interacting with each other to work on a single program in isolation (for instance, it can be confusing to know what methods to refer to from another program in a file), so using an advanced [integrated development environment][3] (IDE) like [Eclipse][4] is probably the norm. For smaller tasks, two of the most commonly used text editors by programmers are [emacs][5] and [vim][6].

One of the biggest problems that people new to these editors face is having to memorize a bunch of obscure commands. Emacs commands often involve holding the control or escape/meta key while pressing some other letter on the keyboard. With vim, users have to press escape repeatedly to go into &#8220;insert&#8221; (i.e., one can type things in) versus &#8220;normal&#8221; (i.e., one can move the cursor around, perform fancy deletions, etc.) mode.

<!--more-->

Once one becomes used to the commands, though, emacs and vim allow *very* fast typesetting. If you watch an emacs or vim master type in their preferred text editor, you will be *amazed* at how quickly he or she can perform fancy alignment of text, advanced finding/replacing involving regular expressions, and other tasks that would otherwise have taken excruciatingly long using &#8220;traditional methods.&#8221; (Unfortunately, these people are hard to find&#8230;.)

So what&#8217;s the quickest way to get started with these editors to the point where someone can write a small program? In my opinion, the best way is to go through their tutorials. Open up your command line interface (e.g., the Terminal on Macs) or your method of opening these editors.

  1. For emacs, type in &#8220;emacs&#8221; and then perform control-h (hold the control key while pressing &#8220;h&#8221;) and press &#8220;t.&#8221; In emacs terminology, C-h t.
  2. For vim, type in &#8220;vimtutor&#8221; from the command line.

This method of learning is excellent since you get a copy of the tutorial and can go through steps and exercises to test out the commands while navigating or modifying the file. I think the vim tutorial is better because it&#8217;s more structured but again, both of them do the job. They emphasize, for instance, that once a programmer gets used to the commands to move the cursors, using them will be faster than resorting to the arrow keys since one doesn&#8217;t have to move hands off of the keyboard:

  1. From emacs: There are several ways you can do this. You can use the arrow keys, but it&#8217;s more efficient to keep your hands in the standard position and use the commands C-p, C-b, C-f, and C-n.
  2. From vim: The cursor keys should also work. But using hjkl you will be able to move around much faster, once you get used to it. Really!

I have to confess that I didn&#8217;t learn emacs by using their tutorial. I just went by a list of common commands given to me by my professor and picked things up by experience and intense Googling. As a result, I experienced a lot of pain early on in my computer science career that could have been avoided by just reading the tutorial. (The control-g command to quit something was a HUGE help to me once I read about it in the emacs tutorial.) And judging by the emacs questions that other Williams College computer science students have asked me, I can tell that not everyone reads the tutorial.

So read the tutorials before seriously using these text editors.

Of course, one should decide at an early step of his or her programming career: emacs or vim? This is certainly a non-trivial task. They both do basically the same thing, and with the variety of extensions and customizations possible, I&#8217;m not sure there&#8217;s anything they *can&#8217;t* do that any other text editor can do, to be honest. If I had to give a general rule, I&#8217;d just go with choosing the one that felt best to you in the tutorials, or the one that&#8217;s most common among your colleagues, professors, or other peers.

And besides, it&#8217;s difficult to say which one of these editors is better than the other. [It][7] [really][8] [depends][9] [on][10] [who][11] [you][12] [ask][13]. I don&#8217;t have a good answer to this so I&#8217;ll opt-out and provide a lame one: **the one that&#8217;s better is the one that you can use best**.

Personally, I started my programming career using the emacs text editor because that was the preference of my Computer Organization professor, so I didn&#8217;t see the need to deviate. Within the past year, I substantially increased my emacs usage to the point where I was using it almost everyday for most typing tasks, including LaTeX, and my pinky finger didn&#8217;t like the constant reliance of the control key. So I&#8217;m giving vim a shot.

It&#8217;s still useful to know the emacs commands, because they often work in other places. For instance, when I type in blog entries here, I can use a subset of emacs commands while typing in my entry in the built-in editor for WordPress, which was surprising to me when I first found out. Instead of deleting a line by using the mouse or Mac trackpad, I can use the ctrl-k emacs command to do that. And many IDEs will have support for emacs or vim commands, so one can get the best of both worlds. I know that Eclipse has this, but I was personally disappointed that certain emacs commands didn&#8217;t work.

To wrap up this post, I suggest that knowing one of emacs or vim well is important for (computer science) graduate school since programming is a huge part of research today, so the faster things get done, the better. Moreover, university professors tend to take on more of a &#8220;leader&#8221; role rather than someone who &#8220;gets things done&#8221; (I&#8217;m not trying to disparage professors here). In other words, they tell the graduate students what to do in research projects and the students will write the necessary programs.

 [1]: http://seitad.files.wordpress.com/2013/12/emacs_tutorial.png
 [2]: http://projecteuler.net/
 [3]: http://en.wikipedia.org/wiki/Integrated_development_environment
 [4]: http://www.eclipse.org/
 [5]: http://www.gnu.org/software/emacs/
 [6]: http://www.vim.org/
 [7]: http://stackoverflow.com/questions/1430164/differences-between-emacs-and-vim
 [8]: http://www.terminally-incoherent.com/blog/2012/03/21/why-vim/
 [9]: http://stackoverflow.com/questions/592125/should-i-switch-from-vim-to-emacs-and-if-so-any-suggestions?rq=1
 [10]: https://www.udemy.com/blog/vim-vs-emacs/
 [11]: http://unix.stackexchange.com/questions/986/vim-vs-emacs-and-no-this-is-not-a-flame-war
 [12]: http://www.diffen.com/difference/Emacs_vs_Vim
 [13]: http://batsov.com/articles/2011/11/19/why-emacs/