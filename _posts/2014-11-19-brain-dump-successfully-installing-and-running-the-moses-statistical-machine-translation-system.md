---
title: 'Brain Dump: Successfully Installing and Running the Moses Statistical Machine Translation System'
author: Daniel Seita
layout: post
permalink: /2014/11/19/brain-dump-successfully-installing-and-running-the-moses-statistical-machine-translation-system/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - boost
  - homebrew
  - mgiza
  - Moses
  - natural language processing
  - statistical machine translation
---
I'm using [Moses][1] again. It's an open-source statistical machine translation system. I first used
it when I was [at Bard in 2012][2], and I remember being clueless about the installation process and
being overwhelmed by all the Linux/Unix commands I had to know. I think it took me more than a
*week* before I had installed Moses and successfully completed the [suggested baseline test][3]. At
that time, I was doing nothing *but* that &#8230; so I was pretty frustrated. Even at the end of my
REU, the commands to run Moses felt like black magic.

But I&#8217;m back at it again. Armed with several more years of hacking and Linux/Unix experience,
as well as a [statistical natural language processing class][4] for background material, I managed
to install Moses and complete the baseline test on my laptop, which is a Macbook that I got last
January. It still took me almost a week (Friday night, 9-5 Saturday, 9-5 Sunday, all day Monday and
Tuesday&#8230;) to do that since I ran into some unexpected problems. To prevent me from getting
this kind of headache again, I&#8217;ll be listing the steps I conducted to install and run the
baseline, which hopefully will be applicable for anyone trying to use Moses right now. If you find
this article useful, please let me know. (Keep in mind, however, that it will probably be obsolete
in a few months.) You will need some Linux/Unix experience to follow this article.

<!--more-->

At a high level, I had problems with installing [boost][5], installing [mgiza][6], and training the
baseline system.

To start, I git cloned the moses code. The [installation instructions say][7] that I need g++ and
boost installed. Actually, I don&#8217;t think g++ is necessary because in Mavericks (i.e., OS X
10.9), Apple changed the default compiler for C++ to be clang, so we really need *that* on our
computers to run Moses, but clang should be built-in or be part of Xcode so it should definitely be
there as long as I have Xcode. Speaking of boost, I did have boost 1.56 installed; I got it via the
command ```brew install boost```, which will install boost 1.56 in ```/usr/local/Cellar/boost/```,
because that&#8217;s the default place where [homebrew][8] installs things. For example, I also have
the widely-used [numpy][9] package located in `/usr/local/Cellar/numpy`.

So, thinking that I had things taken care of, I went into my mosesdecoder directory, and followed
the instructions by running ```./bjam -j8```. Unfortunately, I ran into the dreaded &#8220;clang:
error: linker command failed with exit code 1.&#8221;

~~~
$ ./bjam -j8  
Tip: install tcmalloc for faster threading. See BUILD-INSTRUCTIONS.txt for more information.
mkdir: bin: File exists
...patience...
...patience...
...found 4469 targets...
...updating 155 targets...
darwin.link lm/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/query
ld: library not found for -lboost_thread
clang: error: linker command failed with exit code 1 (use -v to see invocation)

// Additional error messages...

...failed darwin.link mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/util_test...
...skipped <pmert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi>util_test.passed for
lack of <pmert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi>util_test...
darwin.link mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/vocabulary_test
ld: library not found for -lboost_thread
clang: error: linker command failed with exit code 1 (use -v to see invocation)

"g++" -o "mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/vocabulary_test"
"mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/VocabularyTest.o"
"mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/libmert_lib.a"
-lboost_unit_test_framework -llzma -lbz2 -ldl -lboost_system -lz -lboost_thread -lm -liconv -g
-Wl,-dead_strip -no_dead_strip_inits_and_terms
...failed darwin.link
mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/vocabulary_test... 
...skipped <pmert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi>vocabulary_test.passed
for lack of <pmert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi>vocabulary_test...
...failed updating 72 targets…
...skipped 83 targets…

The build failed. If you need support, run:
./jam-files/bjam -j8 –debug-configuration -d2 |gzip >build.log.gz
then attach build.log.gz to your e-mail.
You MUST do 3 things before sending to the mailing list:
1. Subscribe to the mailing list at http://mailman.mit.edu/mailman/listinfo/moses-support
2. Attach build.log.gz to your e-mail
3. Say what is the EXACT command you executed when you got the error
~~~

Huh. I can't even do a simple installation?!? Note: in the above terminal output, I included my
original command (after the dollar sign $), and the error message was much longer than what's
displayed; I got rid of some if it with `// Additional error messages` for the sake of clarity.

What&#8217;s the problem? Apparently, moses couldn&#8217;t find the ```lboost_thread``` library.
After some extensive research on Google and asking on the Moses mailing list, I think the issue
comes down to the layout being ```layout=tagged``` versus ```layout=system```. To give an example,
the library file that I think ```lboost_thread``` refers to is ```libboost_thread-mt.a```, which is
a *tagged* version due to having ```mt```; the untagged file version would be
```libboost_thread.a```. I *think* this was the problem I was getting, but I couldn&#8217;t figure
it out despite making moses look at the directory where boost was installed. On the instructions,
they say to do ```./bjam -with-boost=~/workspace/temp/boost_1_55_0 -j8``` where the
```workspace/temp``` folder is just where they&#8217;ve put boost in. On my system, it&#8217;s
obviously in a different location, so I ran ```./bjam -with-boost=/usr/local/Cellar/boost -j8```.

Unfortunately, that also didn&#8217;t work. Note: the tilda option indicates the path to the home
directory, so on my computer, ```~/workspace``` would be equivalent to
`/Users/danielseita/workspace`. The `/Users/danielseita` equals the ```$HOME``` path variable.

I asked on the mailing list, and their advice was to do some clean installations because it&#8217;s
obvious something was broken here, especially with boost. All right, then, the first step to do that
is to uninstall boost: `brew uninstall boost -force`.

I went through several more trials of installing boost via homebrew before I decided to avoid using
it at all; I went to the boost website directly, downloaded the .tar.gz file for version 1.57 (the
latest version at the time of this writing), and untarred it: `tar -zxvf boost_1_57_0.tar.gz`.

That pastes the boost files in the current directory, but now we have to *compile* it for Moses. At
the time of this writing, the Moses installation instructions say to execute the following two
commands in the boost directory:

~~~
./bootstrap.sh;
./b2 -j8 -prefix=$PWD -libdir=$PWD/lib64 -layout=system link=static install || echo FAILURE
~~~

Unfortunately, running those commands never helped, and I consistently got the same amount of
errors/warnings each time. After a series of uninstallations/installations, I decided to just try
following the instructions directly from the boost website, specifically from their &#8220;[Getting
Started][10]&#8221; section. I attempted the following set of commands from a clean download folder
`boost_1_57_0`:

~~~
cp -r boost_1_57_0/ /usr/local  
cd /usr/local/boost_1_57_0  
./bootstrap.sh  
./b2 install  
~~~

*And in addition to that* &#8230; I went into Apple&#8217;s Finder window, double-clicked on the
Xcode application (just to check if I had clang installed) &#8230; and upon doing so, I received a
pop-up message saying that there was some external software I needed to install! I wish I had gotten
a screenshot of that, but it showed up as soon as I double clicked on the application, and in a few
seconds it had installed what it needed. It looked like I did have clang installed, but I have no
idea about how much that initial pop-up must have helped me.

I then tried to compile moses again with a simple `./bjam -j8` command. Aaaaaand &#8230; it worked!
See some of the output (again, the dollar sign indicates lines that I typed):

~~~
$ cd ~/mosesdecoder/  
$ ./bjam -j8  
Tip: install tcmalloc for faster threading. See BUILD-INSTRUCTIONS.txt for more information.  
mkdir: bin: File exists  
...patience...
...patience...
...found 4470 targets...
...updating 63 targets...
common.copy /Users/danielseita/mosesdecoder/bin/lmplz  
darwin.link util/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/bit_packing_test  
darwin.link util/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/multi_intersection_test  
darwin.link util/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/joint_sort_test  
darwin.link util/bin/file_piece_test.test/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/file_piece_test  
darwin.link lm/bin/partial_test.test/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/partial_test  
darwin.link lm/bin/left_test.test/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/left_test  
darwin.link lm/bin/model_test.test/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/model_test  
testing.unit-test util/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/joint_sort_test.passed  
Running 4 test cases...

*** No errors detected  
testing.unit-test util/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/multi_intersection_test.passed  
Running 4 test cases...

// Additional cases not shown

***  No errors detected  
testing.unit-test mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/util_test.passed  
Running 3 test cases...

*** No errors detected  
testing.unit-test mert/bin/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/vocabulary_test.passed  
Running 2 test cases...

*** No errors detected  
testing.capture-output moses/LM/bin/BackwardTest.test/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/BackwardTest.run
**passed** moses/LM/bin/BackwardTest.test/darwin-4.2.1/release/debug-symbols-on/link-static/threading-multi/BackwardTest.test
...updated 63 targets...
SUCCESS
~~~

What's the lesson here? I guess the point is that *deleting stuff and just starting an installation
process all over again while trying out new ways of doing things is one of the most effective
techniques to tackling complicated software problems*. Yeah, it's kind of lame, but I guess
trial-and-error is the *nature* of Linux/Unix.

All right, now let&#8217;s discuss the *second* main problem I had with installing Moses, this time
related to mgiza. I initially ran into the problems that I will describe below, but the fix above
(uninstalling boost, taking it from the website, and compiling it according to the boost
website&#8217;s instructions) seemed to resolve them. But I will describe the problem I had with
mgiza just for completeness.

On the Moses website, they now recommend avoiding GIZA++ (which is a popular word-alignment
software) and instead using mgiza, which is a multi-threaded version of GIZA++. As with moses, I git
cloned it into a directory. The installation instructions are really simple, since mgiza comes with
makefiles (the cmake command will generate a Makefile). There are three commands to execute:

~~~
cmake .  
make  
make install
~~~

Notice that cmake has a period after it, which indicates that we&#8217;re assuming the installation
happens in the *current directory*.

Of course, despite the simplicity of these instructions, I still got errors. The cmake step seemed
to work fine, but not make:

~~~
1 warning generated.  
Linking CXX executable ../bin/d4norm  
Undefined symbols for architecture x86_64:  
"std::string::_Rep::_M_destroy(std::allocator<char> const&)", referenced from:  
boost::system::(anonymous namespace)::generic_error_category::message(int) const in libboost_system-mt.a(error_code.o)  
"std::string::_Rep::_S_empty_rep_storage", referenced from:  
boost::system::(anonymous namespace)::generic_error_category::message(int) const in libboost_system-mt.a(error_code.o)  
"std::string::assign(char const*, unsigned long)", referenced from:  
boost::system::(anonymous namespace)::generic_error_category::message(int) const in libboost_system-mt.a(error_code.o)  
"std::basic_string<char, std::char_traits<char>, std::allocator<char> >::basic_string(char const*, std::allocator<char> const&)", referenced from:  
boost::system::(anonymous namespace)::generic_error_category::message(int) const in libboost_system-mt.a(error_code.o)  
"std::basic_string<char, std::char_traits<char>, std::allocator<char> >::basic_string(std::string const&)", referenced from:  
boost::system::(anonymous namespace)::generic_error_category::message(int) const in libboost_system-mt.a(error_code.o)  
"std::basic_string<char, std::char_traits<char>, std::allocator<char> >::~basic_string()", referenced from:  
boost::system::(anonymous namespace)::generic_error_category::message(int) const in libboost_system-mt.a(error_code.o)  
ld: symbol(s) not found for architecture x86_64  
clang: error: linker command failed with exit code 1 (use -v to see invocation)
~~~

Yikes &#8230; another problem with boost! And this time, the "ld: symbols(s) not found for
architecture x86_64" error occurred. Again, as I mentioned earlier, the solution lies not with mgiza
itself but with boost (where it&#8217;s installed, etc.), so consider a clean installation and
compilation of boost from the official website (not homebrew). When I did that, I deleted the mgiza
directory, cloned it again from git, and the three subsequent commands worked. I got a ton of
warning messages, *but no errors,* which is the important part.

Whew! With moses and mgiza successfully compiled, I could *finally* start the baseline! Most of the
time, copying and pasting the instructions from the Moses website and modifying them according to
your directory structure should work, but there are some important things to be aware of:

(1) Installing irstlm is a little different because now it&#8217;s version 5.80.06 rather than the
5.80.03 that&#8217;s currently listed on the website. (In fact, irstlm 5.80.03 does not even compile
on my laptop.) With this new version, irstlm moved the directory structure so now the installation
won&#8217;t work if you copy the baseline. There&#8217;s a README in the `trunk` directory inside
irstlm so I followed that and didn&#8217;t seem to have many issues. Make sure you modify the rest
of the baseline&#8217;s commands accordingly, since the documentation assumes that we use
`~/irstlm/bin` as the place where the binaries are located.

(2) One thing I had trouble with was the &#8220;&#8211;text yes&#8221; option for the compile-lm. That
  created a &#8220;DEBUG: warning: too many parameters&#8221; output, [as described here][11]. The
  key is to use &#8220;&#8211;text=yes&#8221; so **put in the equals sign**. I can&#8217;t believe
  that fix took so long for me to figure out! I described this on the mailing list and the people
  maintaining the Moses website have (as of this writing) changed the instructions to conform to
  &#8220;&#8211;text=yes&#8221;.

(3) With training, the current instructions assume we&#8217;re using GIZA++, but since it&#8217;s
mgiza, we&#8217;ve got to change that. Oh, that reminds me &#8212; I also tried out these training
steps with normal GIZA++, but I could never get it work because after training went on for a few
hours, something wrong happened with the lexical reordering score, because extract.o.sorted.gz never
got generated. Here&#8217;s the error I got in the log file training.out:

~~~
libc++abi.dylib: terminating with uncaught exception of type  
util::ErrnoException: util/file.cc:68 in int util::OpenReadOrThrow(const char *)  
threw ErrnoException because '-1 == (ret = open(name, 0x0000))'.

No such file or directory while opening  
/Users/danielseita/working/train/model/extract.o.sorted.gz

ERROR: Execution of:  
/Users/danielseita/mosesdecoder/scripts/../bin/lexical-reordering-score  
/Users/danielseita/working/train/model/extract.o.sorted.gz 0.5  
/Users/danielseita/working/train/model/reordering-table.  
-model "wbe msd wbe-msd-bidirectional-fe"

died with signal 6, without coredump
~~~

The error above prevented a `moses.ini` file from even forming. To work around this issue, it&#8217;s
possible to run the training while removing the `-reordering` argument, but when I did that, tuning
fails. If you know of a fix, please let me know!

Now back to training with mgiza. The instructions are listed on the [external software page][12]. We
need to specify the `-mgiza` flag, and we also need to make sure that `-external-bin-dir` is set
correctly. This should be a directory where the mgiza *binary* files are located, *as well as* the
`merge_align.py` script (all of these must be in one directory together!). In the current version of
mgiza, they seem to be in `/mgiza/mgizapp/bin`. I decided to move everything over to a directory
called `word_align_tools`; inside the mosesdecoder directory. I also specified the number of CPUs
for mgiza to be four. The following code shows the list of commands I used to *prepare* my file
    system for training:

~~~
cd ~/mosesdecoder/  
mkdir word_align_tools  
cp ~/mgiza/mgizapp/bin/* word_align_tools/  
cp ~/mgiza/mgizapp/scripts/merge_alignment.py word_align_tools/
~~~

And this does the actual training:

~~~
/Users/danielseita/mosesdecoder/scripts/training/train-model.perl  
-root-dir /Users/danielseita/working/train  
-corpus /Users/danielseita/corpus/news-commentary-v8.fr-en.clean  
-f fr -e en -alignment grow-diag-final-and -reordering msd-bidirectional-fe  
-lm 0:3:/Users/danielseita/lm/news-commentary-v8.fr-en.blm.en  
-mgiza -mgiza-cpus 4  
-external-bin-dir /Users/danielseita/mosesdecoder/mgiza_tools/ >&training.out
~~~

I put in some backward slashes there just so the code wouldn&#8217;t require so much scrolling to
understand, but I didn&#8217;t include them when I ran it in Terminal. Also notice that I&#8217;m
using **absolute paths**, rather than relative paths. This means we want a full path like
`/Users/danielseita/mosesdecoder` instead of `~/mosesdecoder`. I saw some errors online that were
resolved with using full paths, so I decided to use full paths for *everything*, though it&#8217;s
probably worth it only for the -root-dir argument above. Finally, I&#8217;m not adding in a
&#8220;:8&#8243; to the language model argument, because I don&#8217;t know what that does (to do:
find out!).

**Update 11/29/14: **Apparently, that extra :8 argument forces the use of KenLM instead of SRILM
&#8230; so yes, include an extra :8 after the language model file name. The above command, while
still correct I believe, should not be used.

That command above took five or six hours to complete on my laptop, which is surprising because the
baseline currently claims it should be 1.5 hours, and I&#8217;ve got a pretty powerful laptop.
Perhaps the data I downloaded got updated and is larger than the baseline claims? Or maybe
it&#8217;s an mgiza issue?

Once training is done, here&#8217;s a *very* important piece of advice: **change the resulting
moses.ini file to say KENLM instead of SRILM**. This means my moses.ini file had a line that looked
like this:

~~~
KENLM name=LM0 factor=0 path=/Users/danielseita/lm/newscommentary-v8.fr-en.blm.en order=3
~~~

I&#8217;m not sure why this isn&#8217;t emphasized that much on the baseline webpage, because
it&#8217;s pretty darn important! The tuning will fail if we don&#8217;t get the language model set
correctly.

(4) I ran into many problems with tuning, but most of them were &#8220;carried over&#8221; from the
training step, such as if I made an error in the command for training. Once I finally got mgiza
working, tuning was fine, and the following command (for tuning) ran in the normal time range, which
is about four hours.

~~~
/Users/danielseita/mosesdecoder/scripts/training/mert-moses.pl  
/Users/danielseita/corpus/news-test2008.true.fr  
/Users/danielseita/corpus/news-test2008.true.en  
/Users/danielseita/mosesdecoder/bin/moses  
/Users/danielseita/working/train/model/moses.ini -decoder-flags="-threads 4"
-mertdir /Users/danielseita/mosesdecoder/bin/ >& mert.out
~~~

(5) Testing should proceed as normal. My BLEU score is 23.58, which is what they expect (they say they got 23.5).

~~~
$ ~/mosesdecoder/scripts/generic/multi-bleu.perl -lc  
~/corpus/newstest2011.true.en < newstest2011.translated.en  
BLEU = 23.58, 60.3/29.9/16.9/10.1 (BP=1.000, ratio=1.017, hyp_len=76035, ref_len=74753)
~~~

Looking back at this, while Moses is no doubt a great software system, it *does* take a lot of
effort to get it working correctly. Sometime in the next few weeks, I&#8217;ll try to post a real,
organized guide here. **UPDATE** May 16, 2015: I doubt I'll ever get a real guide up here, since
Moses isn't really an integral part of my research now. Sorry about that!

 [1]: http://www.statmt.org/moses/
 [2]: https://seitad.wordpress.com/2012/07/27/wrapping-up-my-summer-research/
 [3]: http://www.statmt.org/moses/?n=Moses.Baseline
 [4]: http://www.cs.berkeley.edu/~klein/cs288/fa14/
 [5]: http://www.boost.org/
 [6]: https://github.com/moses-smt/mgiza
 [7]: http://www.statmt.org/moses/?n=Development.GetStarted
 [8]: http://brew.sh/
 [9]: http://www.numpy.org/
 [10]: http://www.boost.org/doc/libs/1_57_0/more/getting_started/unix-variants.html
 [11]: http://comments.gmane.org/gmane.comp.nlp.moses.user/9924
 [12]: http://www.statmt.org/moses/?n=Moses.ExternalTools
