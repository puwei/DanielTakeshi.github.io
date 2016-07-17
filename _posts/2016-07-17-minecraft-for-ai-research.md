---
layout: post
author: Daniel Seita
title:  "Minecraft for AI Research?"
date:   2016-07-17 10:00:00
permalink: 2016-07-17-minecraft-for-ai-research/
---

More games are jumping on the AI bandwagon.

We saw [IBM's Deep Blue][8], which beat chess Grandmaster Gary Kasparov in 1997. Then in 2013, we
saw DeepMind's AI agents[^nowgoogle] achieve [human-level performance on many classic Atari 2600
games][7]. Then earlier this year, we saw DeepMind's next product, AlphaGo, beat Lee Sodol in a
widely publicized Go match. You can view the details on [DeepMind's AlphaGo website][6], which also
has the corresponding *Nature* paper. I have not read it yet (it's on my TODO-list), but I read and
considerably enjoyed their other *Nature* paper (from 2015) about Atari 2600 games.

Yet it looks like we are not done with AI and games. The news is out that [Microsoft Research has
made Project Malamo open source][2]! It allows people to use the popular sandbox game *Minecraft*
for AI research. Microsoft has been using it for a few months, as evident by [this earlier
article][3], but I only found out about Project Malamo after it became open source. Ironically, I
didn't find this by browsing Microsoft's website --- I found it on [the Minecraft forum website][1]. 

Their overall goal is stated as follows:

> [...] five computer scientists are spending their days trying to get a Minecraft character to
> climb a hill.
> 
> That may seem like a pretty simple job for some of the brightest minds in the field, until you
> consider this: The team is trying to train an artificial intelligence agent to learn how to do
> things like climb to the highest point in the virtual world, using the same types of resources a
> human has when she learns a new task.
> 
> That means that the agent starts out knowing nothing at all about its environment or even what it is
> supposed to accomplish. It needs to understand its surroundings and figure out what’s important –
> going uphill – and what isn’t, such as whether it’s light or dark. It needs to endure a lot of trial
> and error, including regularly falling into rivers and lava pits. And it needs to understand – via
> incremental rewards – when it has achieved all or part of its goal.

Stated succinctly, they want to train the player to get to higher ground in Minecraft, *without*
having to explicitly code that concept. One can formulate this as a reinforcement learning problem
using some form of a Markov Decision Process (you can view [my earlier article on MDPs here][9]).
As in the case for DeepMind's work, the researchers of Project Malamo want to accomplish this while
*only* relying on information that a human can see. That is, they want the agent to learn like a
human would. This is definitely going to be a challenging problem. Minecraft is one of the most
open-ended games ever, and even humans are often unsure of what their objectives are when playing.
I've had people tell me, "what's the point of Minecraft?"

The researchers are constraining their focus to "moving uphill", which helps to narrow down the
problem. That still results in a very broad game, and is unlike previous work using Chess, Go, and
Atari 2600 games, which have clearer goals for the player. I will be particularly interested in
seeing how researchers will compare their results. How do we evaluate the quality of agents? I am
also curious about what role deep learning will play in this research.

On a final note, if they want an AI enthusiast who is also a Minecraft enthusiast to serve as a
contributor ... my contact information [is on the "About" page of this website][4]. Unfortunately, I
have not played Minecraft in months (maybe a year?!?) and my guess is that a disproportionate share
of computer scientists are also Minecraft players.

***

[^nowgoogle]: After they demonstrated their results, Google bought the company, so we commonly call
    them *Google DeepMind*.

[1]:http://www.minecraftforum.net/
[2]:https://blogs.microsoft.com/next/2016/07/07/project-malmo-lets-researchers-use-minecraft-ai-research-makes-public-debut/#sm.0000w00y4ts8ze02rks2bwp04gf12
[3]:http://blogs.microsoft.com/next/2016/03/13/project-malmo-using-minecraft-build-intelligent-technology/#sm.0000tzemfiq02dj9zge197fnn2m46
[4]:http://danieltakeshi.github.io/about/
[5]:https://www.youtube.com/watch?v=MmB9b5njVbA
[6]:https://deepmind.com/alpha-go
[7]:https://deepmind.com/dqn
[8]:https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer)
[9]:http://danieltakeshi.github.io/2015-08-02-markov-decision-processes-and-reinforcement-learning/
