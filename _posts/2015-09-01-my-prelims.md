---
layout: post
title:  "My Prelims"
date:   2015-09-01 23:00:00
permalink: 2015-09-01-my-prelims/
---

*Note: I wrote the following "transcript" of my exam from memory, so it should not be taken as
verbatim.*

## Before the Exam

Of the twelve AI students taking the prelims this fall, I was up last to go; my times were 4:10 to
4:40 with Pieter Abbeel and Dan Klein, and 5:10 to 5:40 with Ruzena Bajcsy and Trevor Darrell.
Obviously, I had spent the entire day of August 24 before 4:10 doing some last-minute preparation. I
arrived in the seventh floor of Sutardja Dai Hall and met my sign language interpreter there, who
was relieved that she hadn't gotten lost or sent to the wrong location.

Actually, I should backtrack to rant a little. My prelims was yet another example of how having 
multiple channels of communication in setting up a sign language interpreting appointment can mess
things up. A week before the prelims, I carefully prepared a three-page document of preparatory
material for my interpreter to review. Most of the document was a list of advanced terminology that
she might expect to hear on the prelims. My goal was for her to look at the words, remember the
spelling, check the pronunciations online (if necessary) so that she could finger-spell them
quickly[^fingerspell] during the prelims. I also listed where and when we should meet before the
prelims. Finally, and this is important, I gave the document to Berkeley's DSP, who then forwarded
it over to the agency that officially appoints the interpreters.

Yet when I arrived in the location where I requested to meet (the third floor of Sutardja Dai Hall),
I never saw her, and when it was 4:05pm, I had no choice but to go up to the seventh floor. It was
only when I finally got near Pieter's office that I saw her. She then said that she had never gotten
that document I created. This is the problem: I *specifically asked* to send my prep documents to
the interpreter *directly* -- *not* through multiple parties -- but got declined[^dsp].  We lost a
bit of early discussion time: she went right to the location of the exam at 3:50pm, while I was
anxiously pacing around in the lobby waiting for no one.

In the end, this might be me going overboard, since the prelims are not a case where having
interpreters is *strictly necessary* for me. I can understand most people when they talk clearly
*and* directly to me, but there are many other situations when having informed interpreters would
be vital.

Sorry for the rant. A few minutes after I arrived near his office, Pieter came out and immediately
told me to come in. It was time.

## Part One

"So ... hello," Pieter and Dan said simultaneously. 

"Hi," I replied. I had never seen Dan and Pieter look like this before, though admittedly I do not
know either of them that well. I think they were either super-tired after having eleven other
students before me, or they were trying super-hard to make me feel less nervous.

"The prelims are going to be a little different this time," Dan said, "but everyone is doing the
same thing, so don't worry. It's a written exam. You have thirty minutes to answer these questions.
You can say things out loud if you already know the answer, and you don't have to show excessive
work. While you do that, I will take notes on my laptop, so ... try not to worry about me."

Fat chance, I thought as he smiled awkwardly. Dan pressed the timer on his phone, starting the exam.

I opened the exam and flipped through all the nine questions to get a feel for them. Then I went
back to the fifth question, about logic, since I knew the answer already.

"Well, the term $$\alpha \models \beta$$ just means alpha entails beta, which is the same thing as
saying that $$\alpha$$ implies $$\beta$$," I said, writing down briefly. "And an algorithm for doing
that is resolution. Or if we're assuming Horn or definite clauses, we can use forward chaining and
backward chaining."

Both of them nodded. Since that was the extent of the question[^logic], I went back to the start of
the exam, in an attempt to do the rest of the questions in order. The first question was about
different search algorithms and heuristics. The graph was structured as a directed tree with two
goal states, with (different) edge costs listed for each arc.

"For depth first search, we just go to the left," I said, outlining the path. "For uniform cost
search, we expand this goal state. For a heuristic, we just need to not overestimate to the goal.
And for the last part, when we talk about ranges that would make the heuristic admissible, it seems
like we just need to make sure we have that be at most four ... wait, we are doing A-star search,
right?"

"Yes," Pieter said. "Think about the value 4.5."

I nodded and wrote my answer formally on the sheet. Then I moved on to the next question, about
constraint satisfaction problems. What happens if we enforce arc consistency, and (1) we have one
element in each domain, (2) we have a variable with no values left, (3) we have multiple values in
each domain? "The first one should have an immediate solution," I said. "For the second case, we're
guaranteed *not* to have a solution. For the third, we are *not* guaranteed to have a solution."

Dan and Pieter did not noticeably react, so I went on to the third question. It presented me with a
tree and asked me to write down a set of leaf node values so that the expectimax versus minimax
paths are different. That was easy for me, as I wrote down "1," "1," "10," and "0" for the two sets
of two leaf nodes (so four leaf nodes in all). Both of them nodded in approval.

The fourth one was about Markov Decision Processes, and involved substantially more text than the
previous questions. I looked at it and decided to move on to the sixth question.

"Oh yeah, a lot of people skipped that one," Pieter said.  I did not ask if that meant they skipped
and solved it later, or (gulp) if they skipped it entirely.

The sixth question (remember, the fifth was about logic) presented me with two Bayesian Networks.
The first part, asked me to write down the joint (that's easy -- just multiply $$P(X_i \mid {\rm
Parents}_{X_i})$$ values together). The second was slightly more challenging, which asked me to
outline a good variable elimination ordering and a bad variable elimination ordering. The graph was
shaped with a root node $$X$$ connected to $$Y_1$$ through $$Y_n$$ and there were also "$$Z$$" nodes
downstream of the $$Y$$ nodes.

"Obviously, a bad elimination ordering starts with $$X$$ because if you eliminate it, all the
$$P(Y_n\mid X)$$ terms get put into one factor that depends on all the $$Y_n$$s, so you get a giant
table," I said. "Now, for a *good* variable elimination ordering, eliminate $$X$$ last. Then I guess
the only question is whether we should eliminate $$Y_1$$, $$Y_2$$, and so on, or the other way
around. To do that ..."

"You don't need to do that," Dan interrupted.

"Oh, I guess the ordering of the $$Y$$s doesn't matter," I said. I probably would have figured this
out eventually, but I'm glad they were helping me to speed up.

The seventh question presented me with a familiar decision network diagram. "The oil can be in one
of three locations," I muttered out loud, reading the question. "One hundred utility for getting the
oil, zero for not getting it. So the *MEU* with no information is just one hundred divided by three,
since one third of the time, we get 100 utility and otherwise we get nothing."

The second part asked about the VPI of knowing with certainty the state of oil in one of the three
locations (i.e., it was either "there" or "not there" with certainty).  "For that, we need to find
the maximum expected utility with this information, minus the MEU I found from the first part," I
said. "So one third of the time, we know the oil for certainty, and two thirds of the time, we can
narrow down our options to the other two. So subtracting that off ... it's fifty over three."

The eighth part was about maximum likelihood. Given that we have heads, heads, tails, and heads, I had
to show that the MLE of $$P(H) = 3/4$$.

"The standard way of doing this is to write the product of the Bernoullis and form the Lagrangian
..." I began, but Dan correctly pointed out that it wasn't going to be that complicated.

"Oh yeah, we can literally write out $$h^3(1-h)^1$$," I said, writing it out. Unfortunately, I ended
up getting $$P(H) = 1/4$$. I stared at my algebra for an embarrassingly long time before Dan pointed
out my stupid error: failing to distribute a "3" appropriately.

"Yeah, that's right," I said, relieved. "Moving on..."

The last question (well, second last for me) showed me three different two-dimensional Gaussian
distributions, with different $$\sigma$$ "curves" printed. I never saw these diagrams before but it
was pretty intuitive what it meant; if the curve stretched "long" in the $$x$$ direction but "short"
in the $$y$$ direction, then the covariance matrix would have $$\Sigma_{1,1} > \Sigma_{2,2}$$. Two
of them had diagonal covariance matrices, and the third one, which stretched out long in the second
and fourth quadrants, I put down as having $$Cov(X,Y) = -1.5$$.

"Why did you pick that?" Pieter asked.

"Well ... " I said, not entirely sure if that was correct. (I later realized after the exam that
I *was* right, and knowing that with certainty required remembering the formula for correlation.) I
wrote out the definition of the covariance: $$\Sigma_{1,2} = Cov(X,Y) = \mathbb{E}[XY] -
\mathbb{E}[X]\mathbb{E}[X]$$.

"And the expected values of both are zero," Pieter pointed out.

I wasn't sure if he said that in agreement with my answer, but time was running out so I came back
to that MDP question I skipped earlier (and left my answer to the ninth question unchanged). There
was a grid of squares arranged in a "circular" fashion where we could move to any of two adjacent
squares, except for two "slide" locations that forced us to move right.

"This is asking me about the value of states after three, ten, and infinity iterations of Value
Iteration, with discounts of $$\gamma=1$$ or $$\gamma=0.1$$" I said. "Well, the value of the state
by the slide is going to be two plus two-tenths after three iterations with discounting. Without,
it's four."

I proceeded, figuring out the different values of states they asked me to write. I tried to sprinkle
in a few jokes here and there to amuse them, and was moderately successful. Unfortunately, time ran
out before I could fill in the last two blanks, so I put in a "2" in one of the boxes at random.

"Are you sure about your answer to that one?" Pieter asked.

"No, I only put a random value down to get something down in the time limit," I said.

"Well, why don't you try and solve it?"

I looked at it, and within a few seconds, saw that the answer was infinity. "Um, yeah, infinity I
guess, for both" I said, knowing that I should have gotten that earlier.

"All right, I guess we're done. You're the last one so you can now talk to any of the other students
about this part of the exam," Pieter said.

"Do you have a rough idea of how well I did?" I asked.

Dan smiled awkwardly. "We ... can't really do that now."

Fine, I acknowledged, and left the office feeling reasonably happy with my performance. I read my AI
book for a few more minutes before showing up at Ruzena's office.

## Part Two

"Well, hello. Why don't you introduce yourself?" Trevor asked. Again, I'm assuming they were doing
this to help the students feel less nervous, though in my case I did not expect these two to know
anything about me so this really did qualify as an introduction. I mentioned my undergraduate
institution and my advisor, but I also wish I had remembered to say that I was deaf since birth.

Then they proceeded to ask questions. 

"Explain logistic regression," Trevor said.

"This is a classification algorithm," I replied. "Let's suppose we're in the binary classification
case. Then logistic regression means that we are assuming -- at least in the discriminative case --
that our data should be assigned probabilistically to classes of 0 or 1 based on the logistic
function, $$P(y = 0\mid x, \theta) = (1+e^{-\theta^Tx})^{-1}$$." I wrote the formula on Ruzena's
white board.

"And what are the parameters?" Trevor asked. I pointed to $$\theta$$ and mentioned that we could
update these with a stochastic gradient method based on the gradient of the data log likelihood.

"Next up: how do you do linear regression on a V-shaped data?" Trevor asked.

"This is a mixture model," I said. "Just have different linear regressions for the two sets of
data." I drew some hypothetical data on the board.

"But how do you know that you will have two components?" Trevor asked, shrugging. "Why not just
one regression line?"

"Well, this is basically ordinary least squares, right? So with an extra regression, we would be
able to better minimize the sum of squared errors..."

"Perhaps I should rephrase this," Trevor said. "We have to decide the number of components, and in
the general case, we can't just eyeball the data and say that we will have two components. We need
to try out different models and evaluate them somehow."

"Oh, just try out different numbers of distributions in the mixture model and perform cross
validation--"

"Yes, good," Trevor interrupted. "Next up, how would you classify data if you did not know the
labels?"

"One way to do that is with an algorithm like K-means," I replied. I drew out some unlabeled data
and tried to signal how the algorithm would work by mentioning how the center of each cluster gets
updated.

"Is this parametric or non-parametric?"

"Uh ... it's parametric in the sense that we can fix $$K$$ and we only have a finite number of
parameters."

"That's correct," Trevor said, "but what is an example of a non-parametric technique?"

"Nearest neighbors."

It was Ruzena's turn to ask. "Can you write down Bayes' rule for classification?"

I wrote down Bayes' rule on the white board, for $$P(y=0\mid x,\theta)$$. I wasn't sure if I really
understood the question, because it's just Bayes' rule!

"Often times we care about learning the parameters," Ruzena said.

"Yes, in which case we would have something like Bayes' rule applied to $$P(\theta \mid x)$$," I
said, still unsure if I was supposed to answer something in more detail.

"Can you write down or explain what the Bayes' risk means?" Ruzena asked.

This wasn't on the syllabus, I thought, but remembering the formulas from CS 281A, I wrote down
$$\mathbb{E}[\ell(y,\hat{y})]$$. "Basically, the expected loss between what we predict $$\hat{y}$$
and the true $$y$$."

Surprisingly, they seemed satisfied with that brief answer, so Trevor changed the subject to the
next part -- neural networks[^nn].

"First, describe a neural network."

"This is a classifier that can also be viewed as an architecture," I said, drawing out some nodes on
the board. "We have an input layer that takes in our data, such as pixels in an image. Then we have
the option of having hidden layers, and I'll write down one. Then an output layer, where we have
outputs. The key with these architectures is that the hidden layers allow for extra complexity, so
to speak, but we also need to make sure we add in *activation functions* for the nodes to introduce
nonlinearity. So we can use the sigmoid."

I explained a few more basic properties in detail, and also went over backpropagation, until Trevor
seemed satisfied.

"Now we're going to talk about convolutional neural networks," Trevor said. I kind of expected this
to happen since Trevor was on the committee, but since CNNs were not on the syllabus, I would have
to rely on my memory of CS 280 material (thank goodness I took the class).

"I have a network architecture listed here," Trevor said, showing me his iPad. "Please draw it."

I drew it out. It was a standard LeNet-like architecture, with a $$13\times 13$$ input layer, a
convolutional layer, a max-pooling layer, and a fully connected layer, resulting in four outputs.

"How many pixels are there in each resulting image in the convolutional layer, given the kernel size
listed?"

"They are ten by ten," I replied, since the filters were $$4\times 4$$ and the stride was one.

"Good. Now what about the size of the max-pooling layers?"

"Five by five."

"And how many weights are there in the fully connected part?"

I wrote down $$(3\times 25) \times 4$$ on the board.

"So, three hundred," Trevor approved. "Now can you tell me the difference in run time or space time
between convolutional and fully connected layers?"

"Yes, the space time is higher for fully connected layers because convolutional ones have weight
sharing," I replied, with Trevor nodding. "As far as runtime, wouldn't the same apply for the
convolutional one ..."

"Well, think about the total amount of weights," Trevor corrected.

I mutter something about the total number of (not necessarily unique) weights, and tried to make a
high-level argument that the runtime would be higher in the convolutional layer, assuming that
training or testing time would be proportional to the number of weights. Trevor seemed happy, and
continued with asking neural network questions.

"Can you talk about the vanishing gradient problem?"

This was another topic that I only remember from CS 280. Fortunately, I *did* remember, and I wrote
out the curve of the sigmoind function. "With the sigmoid, the gradient will go to zero as $$x$$
goes to plus or minus infinity. After a certain point, the difference in gradients is irrelevant and
will not contribute to the update. This is why we like ReLU layers, because those are $$f(x) =
\max\{0,x\}$$ and the gradient will increase linearly."

I fumbled around with my initially sloppy explanation until I felt Trevor seemed satisfied with a
less sloppy version.

"The last question for today is about transfer learning," Trevor said. "What is it?"

Yet another question from CS 280! Wow, I am really glad I took the class. "That's when we use
weights learned from one task to apply to another task, hence *transferring* the knowledge from
training one thing to another. So, in a computer vision object recognition challenge, imagine that
we have one large data and one small, specialized data. We train on the specialized data to get some
weights. Then we..."

"Other way around," Trevor smiled, motioning with his hands.

"Oh, right, sorry! Yeah, I remember that. So we would train on the large, broad data to get some
weights. Then, for another neural network on a more specific task, we use those as the initial
weights.  Say, for instance, we are trying to classify objects as being *Trevor* or *Darrell* ..."

"*I'm* Trevor Darrell!" Trevor replied.

"Yeah, I meant that those are two similar output classes, so we would need specific weights for
those," I said. I worried a bit that my joke backfired, but Trevor seemed to be in a good mood, so
maybe not. I provided a half-baked concluding overview of transfer learning and neural networks in
general.

"And we're all out of time!" Trevor said, feeling satisfied.

"When do you think you can provide the results?" I asked.

"Probably tomorrow!" Trevor grinned.

I left Ruzena's office, feeling pleased that I had remembered how convolutional neural networks
worked from CS 280, but wishing that it had been explicitly listed on the syllabus. I knew I would
be constantly refreshing my email tomorrow.

As it turned out, it wasn't until another week when I got an email from Pieter saying I completely
and comfortably passed the AI prelim. Now I feel a little better.

***

[^fingerspell]: I may not have the most *fluid* ASL due to lack of practice, but I can fingerspell
    *blazingly fast* and can *understand* blazingly fast fingerspelling. If you're interested, we
    can talk about that.

[^logic]: Despite Stuart Russell *not* being on the prelim committee this time, we *did* get a logic
    question, but it was by far the easiest (assuming you studied it!) and shortest question on the
    exam.

[^nn]: Yeah, I should have known that two prominent computer vision researchers would have asked me
    about neural networks.

[^dsp]: DSP later told me that it was because the agency that provides interpreters only gives them
    prep materials at the *moment* of assignment, which was set about a week before I sent them the
    document.



