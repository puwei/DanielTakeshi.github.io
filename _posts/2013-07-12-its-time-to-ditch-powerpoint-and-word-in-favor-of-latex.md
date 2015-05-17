---
title: 'It&#8217;s Time to Ditch PowerPoint and Word in Favor of LaTeX'
author: Daniel Seita
layout: post
permalink: /2013/07/12/its-time-to-ditch-powerpoint-and-word-in-favor-of-latex/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - Beamer
  - LaTeX
  - Microsoft Word
  - PDF
  - PowerPoint
---
<img src="{{site.url}}/assets/LaTeX_image.png" alt="latex">

**The Big Idea**

I&#8217;m surprised I didn&#8217;t do this earlier, but since I was planning to do so anyway, now
seems like a good time. To put it simply &#8230;

> *I will not voluntarily use Microsoft PowerPoint, Microsoft Word, or any other word processing or
> slideshow software (e.g. Google Docs)*.

Instead, as the title of this blog post indicates, I will be using [LaTeX][2] to fulfill all of my
needs.

<!--more-->

**A Brief History**

[Don Knuth][3], Professor Emeritus of Computer Science at Stanford, created TeX (which would later
influence the creation of LaTeX) in the late 1970s in order to easily create publication-quality
mathematics papers. LaTeX is basically the same thing as TeX, except it&#8217;s easier to use (e.g.
fewer esoteric commands required, etc.). The way LaTeX works is that we take a *text editor* of our
choice, write down a bunch of stuff in LaTeX syntax, and then *compile* the text to form a PDF
document as output. My primary LaTeX text editor is [TexShop][4], which you can see in the top image
of this post, but I&#8217;ve also been using [emacs][5] lately.

It&#8217;s not &#8220;what you see is what you get&#8221; (WYSIWYG), which for some people is
understandably a major drawback. Nonetheless, LaTeX has become so popular and is standard knowledge
among serious mathematicians and scientists, so in hindsight, Knuth&#8217;s creation was an enormous
success. In fact, WordPress even allows LaTeX directly into its posts, such as the following
(random) integral: $$\int_0^\infty (x^5 - 3x) dx$$, which was generated with the following
text: ```\int_0^\infty (x^5 - 3x) dx```, surrounded by appropriate *tags*, which are usually dollar
signs.

**Rationale**

If you&#8217;ve never heard of LaTeX before this post, my proclamation might seem like a pretty big
deal. Why avoid using two popular and crucial software in favor of something that seems complicated
and only oriented for mathematicians? In my opinion, there are several strong reasons, and
I&#8217;ll focus first on the use of LaTeX versus Word (or similar word processing software).

The first and most important reason is that in terms of formatting math, LaTeX is far superior to
what Word can offer. Sure, one can try to be a master at using Word&#8217;s equation editor to
circumvent this drawback. (I had a statistics professor who claimed that LaTeX was worthless to him
because he could live by using equation editors.) But there are many problems with that stance, and
I&#8217;ll list some of them.

  1. LaTeX &#8212; when written *correctly* &#8212; still produces cleaner and crisper math than the
  equation editor.

  2. LaTeX can be formatted in many ways depending on the kind of document (e.g. class notes versus
  a conference publication).

  3. Using an equation editor or other tools often require clicking on a bunch of buttons and pages
  to search for fraction layouts, Greek symbols, and other non-standard document elements. In LaTeX,
  we can do all this from our keyboard in an easy and intuitive way. Suppose we want to insert the
  greek symbol *alpha* in the document. In Word, I have to look up either the keyboard shortcuts or
  a large database of symbols. In LaTeX, I simply type in ```$\alpha$``` to get $latex alpha$.
  (Special names in LaTeX have the reverse backslash ```\``` preceding them.)

In a sense, what I&#8217;m really trying to say is that a LaTeX *expert* can use his or her
experience, knowledge, and online documentation to produce quality mathematical expressions quickly.

A second reason to favor LaTeX over Word is that (I believe) LaTeX performs faster. Just today, I
opened up a six-page Microsoft Word document and was amazed at how long it took from the moment I
pressed the blue &#8220;W&#8221; on my screen to when I could actually modify the document. There is
also a delay between when the document&#8217;s contents become visible and when you can actually
modify the text without lag. In that same time, I can open up a 50-page LaTeX document and edit it
seamlessly, since it&#8217;s just plain text. If I want to *compile *it to view the PDF output, it
can take a while during the first compilation (but it&#8217;s definitely not unreasonable) and after
that, compiling tends to be faster. In addition, a competent LaTeX user shouldn&#8217;t be compiling
his or her document every ten seconds.

A third reason is that LaTeX can format the endings and beginnings of pages better than the standard
&#8220;widow and orphan control&#8221; of Microsoft Word. If I&#8217;m writing a document in Word
and I start a new paragraph at the very last line of the page, Word will automatically put that line
on the following page once I&#8217;ve written enough of that new paragraph. Sometimes I want this,
and sometimes this is annoying because I know that I&#8217;m wasting space and that the text on
different pages might look weird if one page ends on an earlier line than another. LaTeX solves this
problem automatically by cleverly &#8220;squishing&#8221; the text together or forcing it to be on a
new page, whichever looks better.

This even works when there are figures involved (e.g. graphs, pictures), which is a huge plus. If
there&#8217;s not enough space for a figure to appear at the bottom of some page, or if
there&#8217;s too many to fit on one page, LaTeX will reassign them to some pages accordingly (in
the final PDF output) and fill up the remaining spots on the page with text. It&#8217;s also
possible to &#8220;assign&#8221; a figure so that it will always be at the top (or bottom) of
whatever page it ends up on in the PDF output, a handy feature. Users have the option to resize and
center figures, assign captions, and assign labels for referencing in text (e.g. &#8220;Figure 3
shows that &#8230;&#8221;). In fact, we can label anything we want by using the label{} tags. Then,
elsewhere in the document, we can use ref{label_name} to refer to something we&#8217;ve labeled. The
reason why labels are useful is that LaTeX keeps the number consistent no matter how many other
figures we add or modify. For instance, if we add in an earlier figure at the start of the document,
the &#8220;Figure 3 shows that &#8230;&#8221; text will automatically convert to &#8220;Figure 4
shows that &#8230;&#8221; &#8212; reflecting the added image. Needless to say, labels are
**extremely** useful when writing academic papers filled with theorems, lemmas, propositions, etc.

There are other advantages, too, such as that the default settings for LaTeX are superior to those
of Microsoft Word (e.g. justified versus non-justified and page numbers on versus off,
respectively). Others have discussed these advantages, too; see [this][6] post for a start. Also,
*LaTeX is free. *It&#8217;s open source, relatively bug-free (after all, it&#8217;s been around for
decades), and definitely not going away anytime soon.

*But what if I need to make slides to give a presentation?*

Don&#8217;t worry, LaTeX has that covered as well! The key is to use the [Beamer][7] class. The
following image shows the &#8220;cover slide&#8221; of a presentation I gave using LaTeX Beamer in
my machine learning class last semester, based on this ICML 2012 [paper][8]. And yes, that paper,
like virtually all computer science papers, was formatted using LaTeX.

<img src="{{site.url}}/assets/LaTeX_Beamer.png" alt="beamer">

With Beamer, we use ```\begin{frame}``` and ```\end{frame}``` and put text between those two
commands to get what we want on one &#8220;slide.&#8221; The advantage of using Beamer is that
it&#8217;s a LaTeX class, so we can seamlessly incorporate LaTeX code into our slides. Beamer will
also output documents in PDF and can have a nice and clickable &#8220;table of contents&#8221;
settings on the top of each slide, depending on the *theme* one uses. The PDF output is important,
since while PowerPoint is used on many computers throughout the world, PDF viewers are virtually
standard in modern computers.  There are many more computers with PDF viewers but without PowerPoint
than there are computers with PowerPoint but without PDF.

**Exceptions**

Now, I understand that I will be unable to completely avoid Word and PowerPoint, so I won&#8217;t
uninstall them from my laptop. Why might I need to use them?

  1. The biggest reason is probably if I&#8217;m collaborating with a group of non-LaTeX users. No
  one is going to want to learn LaTeX in one night just to please me, especially if there&#8217;s no
  math involved, so I&#8217;ll have to suck it up and go with what they&#8217;re using.

  2. I also want to keep Word and PowerPoint just in case there are some important documents I need
  to open from someone (or from a webpage). I don&#8217;t want to ask people to send me PDFs as an
  alternative, and if I&#8217;m trying to open up stuff written by someone on his website years ago,
  I likely won&#8217;t even be able to ask in the first place.

**Bottom Line**

I&#8217;m looking forward to life largely bereft of PowerPoint and Word. Admittedly, the benefit of
LaTeX decreases when one moves from writing technical documents to writing generic documents, but
there are still times when LaTeX&#8217;s beauty can make it clearly the superior choice of
typesetting software. For instance, LaTeX is great for writing resumes and curriculum vitaes.
Needless to say, my current resume/CV was formed using LaTeX, and I recently won second place in a
competitive resume contest.

 [2]: http://www.latex-project.org/
 [3]: http://www-cs-faculty.stanford.edu/~uno/
 [4]: http://pages.uoregon.edu/koch/texshop/
 [5]: http://www.gnu.org/software/emacs/
 [6]: http://oestrem.com/thingstwice/2007/05/latex-vs-word-vs-writer/
 [7]: http://en.wikipedia.org/wiki/Beamer_(LaTeX)
 [8]: http://icml.cc/2012/papers/592.pdf
