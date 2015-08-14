---
layout: post
title:  "Reading Russell and Norvig"
date:   2015-06-22 16:00:00
permalink: reading-russell-and-norvig
---

I had [previously
mentioned](http://danieltakeshi.github.io/2014/06/15/friendly-computer-science-textbooks/) that the
classic AI textbook by Russell and Norvig (2010) was fairly easy reading compared to most computer
science textbooks. Now that I've recently gone through the first half of the book (which is about
500 pages) in the span of two weeks, I stand by my claim. Reading all these pages, however, does
not necessarily mean that I would sufficiently *absorb* the material to the extent I wish, so in
this post, I'll give a brief overview of what's covered in the first half of the book. The first two
chapters serve as an introduction to AI, as a review of how the field came to be, and how we wish to
design AI agents that are *rational*, which means that they make decisions that "make sense"
according to some utility definition. There isn't that much to see here.

## Part II: Problem Solving

This part encompasses chapters 3 through 6 and is about problem-solving. Yes! Now we're onto
something that's interesting, and something that's also covered in every AI course. And every
*algorithms* course, because what's in chapter 3? Search algorithms on graphs!

### Chapter 3: Solving Problems by Searching

The following list outlines the most important search algorithms to know:

- Breadth-First Search (BFS), a strategy where we start from a root node, expand it to generate its
  children, and then put those children in a *queue* (i.e, FIFO) to expand then later. This means
  all nodes at some depth level $$d$$ of the tree get expanded before any node at depth level
  $$d+1$$ gets expanded. The goal test is applied when nodes are immediately detected (i.e., before
  adding it to the queue) because there's no benefit to continue checking nodes. BFS is complete and
  optimal, but it also suffers from horrible space and time complexity.
  
- Uniform Cost Search (UCS) is like BFS, except that it orders the nodes to expanded in a *priority*
  queue based on some path cost function $$g(n)$$. One would want to use UCS rather than BFS in
  cases when a step cost (i.e., the cost of traversing from one node to another) is not uniform.
  Technically, this means without a uniform step function, BFS isn't optimal, but usually we are
  smart enough to not apply BFS in those situations. UCS applies the goal test when a node is
  expanded, i.e., when it is pulled off the queue. This is *later* than when BFS would check. UCS is
  complete and optimal (so long as edge costs are nonzero, to prevent infinite loops) but can suffer
  from the same complexity issues as BFS.

- Depth First Search (DFS) expands the deepest node in the search frontier, so it stores the
  frontier as a LIFO *stack*. Unfortunately, this means that DFS can traverse one really long path
  forever, without stopping to check back at other unexpanded noes near the beginning, so it's
  clearly non-optimal. The real savings for DFS comes with space complexity, because once a node has
  been expanded, it can be removed from memory once all its descendants have been fully explored.

- Depth-Limited Search is like DFS, except that nodes at a depth limit $$\ell$$ are treated as if
  they had no children. This can avoid DFS spiraling off in wild directions, but it also means that
  we will never reach the goal if the shallowest goal is beyond the depth limit.

- Iterative Deepening Search (IDS) is another version of depth-first search, and here we run
  depth-limited search multiple times, increasing the depth limit by one each time so as to
  gradually get close to the goal. It's not as slow as one might think, because we would be
  repeating most of the initial node expansions, which have a lower branching factor.

- Bidirectional Search means that we run two searches, one from the starting state and another from
  the ending state. The real challenge is how to combine the two search paths in the middle, and how
  to backtrack if necessary. In the $$n$$-queens problem, it's not clear how to backtrack.

- Greedy Best-First Search uses a heuristic function (explained later) to choose which node to
  expand. This means that nodes are stored in a priority queue according to $$h(n)$$. This may seem
  a lot like UCS (and it is), but here, $$h(n)$$ is the estimated cost of reaching the goal from
  node $$n$$, *not* the overall path cost we have seen so far.

- A-Star Search fixes problems with greedy best-first search by supplementing $$h(n)$$ with the path
  cost seen so far, $$g(n)$$. So here, the nodes would be stored in a priority queue based on
  $$g(n)+h(n)$$, where the first term indicates a *known* cost so far, and the second indicates our
  *estimate* of the future cost. A-Star Search is probably the most widely used form of best-first
  search.

For problems that use heuristic functions (i.e., $$h(n)$$ in the above notation), one would like
heuristics that are **admissible** and **consistent**, because then that would make A-Star search
complete and optimal. Admissible means that the function *never overestimates* the cost of reaching
to the goal, and consistent means that the function obeys the triangle inequality[^another]. Every
consistent heuristic is also admissible, but the reverse is not true. Probably the canonical example
of a consistent heuristic in traveling salesman-like problems is when we use the straight-line
distance from one city to another (well, assuming that our travel speed would be uniform across all
possible routes).

If one has multiple admissible heuristics $$h_1,\ldots,h_m$$ for a problem, and none dominates the
other, then we should take the max of those for each node, $$h(n) = \max\{h_1(n), \ldots,
h_m(n)\}$$. Do not take the sum if we want an admissible heuristic!

### Chapter 4: Beyond Classical Search

Amusingly enough, this chapter is about trying to extend the previous one to bring it closer to the
"real world." Though admittedly, yes it is more like what most people would use. The first part of
this chapter gives a very brief introduction to the field of **optimization**. Hill-climbing search is
a search algorithm that attempts to move in the direction of increasing utility value, and is a more
general version of the commonly-used **gradient-descent** algorithm, which is only applicable in
continuous domains. The main problem with these local algorithms is that they can get stuck in local
minima (or maxima, depending on whichever is most convenient for the problem description), so one
should run the algorithm multiple times with random starting positions. Alternatively (or in
addition), one can use *simulated annealing*. The way to think about how that works is to imagine a
local minima problem where we have a small ping-pong ball on a curvy, bumpy surface and are trying
to get it to rest in the deepest crevice. The ball would obviously get stuck in a local minima
easily due to gravity, so simulated annealing is like "shaking" the surface enough to shoot the ball
out of a small valley, but *not* out of the actual global minima, which would be like a deep, giant
pit. I find this analogy a lot easier to understand than most descriptions of simulated annealing,
by the way.

The fact that we bring up gradient descent is interesting, because the search problems in Chapter 3
cannot handle continuous domains due to the infinite branching factor. Said another way, a human has
an infinite number of ways to walk in a specific direction along the 360 degree circle; how would we
design DFS to help a robot do that? One way to find optimal solutions in continuous spaces is to
**discretize** the problem, so going back to my "human walking" example, we might limit the search
directions to be anywhere from 0 up to 30 degrees, any where from 30 up to 60 degrees, etc. Another,
of course, is to use the gradient and update the current state according to $$X \leftarrow X +
\alpha \nabla f(X)$$. We could also have **constrained optimization** problems, of which the best
known and easily solvable problems are of the **linear programming** variety.

Remember that in Chapter 3, the environment is assumed to be fully deterministic and observable. It
is also interesting to see how we would design an agent to search in spaces that have
*non-deterministic actions* and if the agent can only have *partial* or even no (!) observations
about the world. The key idea here is that we have to make use of an agent's **percepts** that will
help inform it what state it is in, so that we can say things like "if X happens, do Y, else do Z."
We can still design search trees and traverse them to reach the goal, but the trees have different
flavors. In the nondeterministic environment case, we would need to have edges between a parent node
and all its possible children nodes that could result. In the partial observation case, we would
have the tree's nodes be **belief states**, so each node is actually a set that contains the
possible states the agent could be in. Gradually moving around in the search space might narrow down
the set of possible belief states. The book's vacuum cleaner example helps to explain how even an
agent with no observations can still tell which state it is in given that it executes a specific
sequence of actions and knows the consequences. In fact, having a sensor-less agent can be
*advantageous* in situations when it would be expensive to pin down an exact state, which is why
doctors tend to prescribe a broad spectrum antibiotic rather than perform detailed analysis of a
patient to decide on an incredibly specific drug.

As an interesting side note, I was reading sections 4.3 and 4.4 and noticed the similarities between
the graphs provided here and the finite automata I learned from my undergraduate theoretical
computer science course. We have notions of a *state*, a *transition function*, *actions*, and
*final* (i.e., goal) states. Section 4.5, discussing online search, also uses these graphs. The nice
thing about the book's organization is that the search algorithms from Chapter 3 can be applied to
the graphs on Chapter 4, along with additional problem-specific restrictions.

### Chapter 5: Adversarial Search

We spent a lot of time in my undergraduate AI course on adversarial search. This is like what we
consider in Chapters 3 and 4, except that the agent is no longer alone, and its actions are in
conflict with other agents. The simplest abstraction of adversarial search is a two-player game
involving one overall game score. The players are named MAX and MIN because they wish to maximize
and minimize, respectively, the overall game score. In normal search algorithms, a player named MAX
(who by convention tends to start these games) would just search for and form a sequence of moves
that would reach a terminal state. Unfortunate, MIN can stop this in some cases. So the best
algorithm for MAX to pursue is the *minimax* algorithm, because it minimizes the worst-case
scenario[^ofcourse]. The easiest way to view this algorithm is to draw a graph of the game tree with
various scores. Levels would alternate between a MAX player and a MIN player, so the MAX player
should trace through the entire game tree and recursively backtrack to check and see the best score
it can get on each node assuming that MIN plays optimally.

The problem with minimiax search is that nontrivial games have too many possible states; it's
actually exponential in the depth of the tree. By using **alpha-beta pruning** to prune away
branches that cannot possibly affect the final decision, we can cut the exponent in about half and
still return the same solution used by minimiax. For any given state at any time in the search
algorithm, alpha is the value of the best choice found along the path for MAX, and beta is the value
of the best choice found along the path for MIN. Alpha starts as negative infinity and tries to go
*up*, whereas beta starts as positive infinity and tries to go *down*. It's easiest to see how this
works by tracing through some game trees. 

I remember these algorithms well because my undergraduate AI courses used the Berkeley Pacman
assignments[^berkeleyai], which involved heavy use of minimiax search and alpha-beta pruning. I
remember that our problem involved four agents: Pacman (us) and three ghosts who wanted to eat him.
With more than two players, we can associate a *vector* of values, and I think that's what we did in
the assignment, since [the description says](http://ai.berkeley.edu/multiagent.html): 

>Now you will write an adversarial search agent in the provided MinimaxAgent class stub in
>multiAgents.py. Your minimax agent should work with any number of ghosts, so you'll have to write an
>algorithm that is slightly more general than what you've previously seen in lecture. In particular,
>your minimax tree will have multiple min layers (one for each ghost) for every max layer.

If you've checked the AI project description, you'll also see that we only run minimax algorithms to
a limited depth, sometimes as small as just two layers. This is necessary due to the exponential
explosion in the number of states in the Pacman maze. Another way to speed up the searching (but
again, at the cost of optimality) is to treat nonterminal nodes at a given level as terminal nodes,
and create a heuristic evaluation function for their values. (Yes, this is very similar to Chapter 3
material!) After all, this is what humans do when they play games. I can't remember 20 moves ahead
in a chess game, but I can reason that moving my queen to capture an opponent's queen, while not
threatening any of my pieces in the process, will have a higher utility for me.

One can also use minimax algorithms with games involving chance, which means that game nodes have
**chance nodes** in addition to the normal MAX and MIN nodes. To make correct decisions here, we
have to change our analysis to consider **expected values**.

### Chapter 6: Constraint Satisfaction Problems

Now we'll switch gears and focus on problems that have more sophisticated notions of a "state." The
reason for doing this is that algorithms like DFS, BFS, etc., assume that states are just black
boxes. There is no domain-specific part of those search algorithm to those problems[^evals]. With
constraint satisfaction problems (CSPs), we represent each state as a set of variables
$$(X_1,\ldots,X_m)^{(i)}$$, and a problem is solved when each variable has a value that satisfies
all the constraints imposed from the states and problem formulation. The example used in the book is
about coloring the seven regions of Australia so that no two bordering regions have the same color.
To formulate it as a CSP, we

- define seven variables to be the seven regions
- define the domain for each variable, which consists of three colors for us
- define the constraints, which means listing all the color inequalities from bordering regions

Just to be clear, *why* do we want to use CSPs? Here are a few reasons:

- It is nice to have a single solver for a CSP. We can then solve a problem by converting it to a
  CSP, and then running our CSP solver. This is what a lot of theorists do when they reduce problems
  to known ones.
- There is no need to develop a detailed, problem-specific heuristic.
- CSPs can eliminate large portions of the search space all at once by quickly identifying variable
  assignments that violate constraints.

It's worth discussing that last point in more detail. In the search problem of previous chapters,
our search algorithm can search. With a CSP, we can perform inference called **constraint
propagation**, which uses the constraints to reduce the number of legal values for variables. As
the book delightfully points out, Sudoku is a problem that has "introduced millions of people to
constraint satisfaction problems." Constraint propagation is obvious here: if I see a column of
variables that has all values other than 3 and 7 filled in (i.e., two empty squares), I can identify
one of those spots that I want to fill in and constrain the number of possible variables from nine
to two. If I then see that the square coincides with a row that already has 3 in it (but not 7,
unless something went wacky), then that further constraints the choice of my variable to be 7 ...
and I will obviously put 7 there.

But while Sudoku problems can be solved by inference over constraints, sometimes we just have to
search for a solution, and here is where **backtracking search** comes into play. This is a
depth-first search algorithm that goes down the tree assigning values to variables, and if it
reaches a point where a variable has no legal values left to assign, then there is clearly no
solution, so it backtracks to previous variables to try and perform different assignments.  The
order that we assign the variables does not matter, which helps to cut down on the branching factor.

To make backtracking search more efficient *without* using problem-specific knowledge, we should
decide on solid heuristics for the following:

- What is the order in which we should choose to assign variables, and in what order should the
  possible assignments be done?
- What inferences should be performed at each step in the search?
- When the search arrives at an assignment that violates a constraint, how can we avoid repeating
  this failure?

For choosing the variable ordering, one way is the **minimum-remaining-values** (MRV) heuristic, or
choosing the variable that has the fewest legal values, because then we can detect failure quicker.
When we *do* choose a variable, but have to assign it from the list of possible values, it actually
makes sense to follow **least-constraining-value** heuristic, or choose the variable that rules out
the fewest choices for the neighboring variables in the constraint graph (this is a graphical
representation of the CSP) because it allows the possibility of more solutions down the road
(ideally). So, most constrained when *choosing* a variable, and least constrained when *assigning*
that chosen variable.

To perform inference, we can do **forward checking** after we assign a variable. This establishes
arc consistency among adjacent variables in the constraint graph by iteratively updating constraints
on those variables. However, this will fail in simple cases such as after we have assigned a
variable a color in a problem where we have to two-color the $$\mathcal{K}_3$$ graph, because
forward checking can't reason about arcs that don't directly include the currently assigned
variable.

When we violate a constraint, we can backtrack one step up in the DFS tree like normal DFS, 
but that tends to work poorly because if we have an inconsistency, then we may have made a mistake
much earlier in our sequence of variable assignments, so we want to backtrack far up in the tree
beyond the most recent decision point. We can design a backjumping method by maintaining **conflict
sets** for each variable, or in other words, a set of assignments that are in conflict with a
variable assignment. Then the backtracking process would go back to the most recent variable
assignment in the conflict set. However, forward checking *already* supplies the conflict set (check
this yourself!), and so "simple" backjumping as previously described is redundant in a forward
checking search or a search that utilizes arc consistency measures.

Instead, we can use the more sophisticated **conflict-directed backjumping**. Instead of backjumping
once we detect a failure based on conflict sets, we should backtrack all the way before that to the
point where the branch "gets doomed." Clearly, this is a more challenging task, and we do this by
redefining what it means to be a conflict set: for a variable, its conflict set is the set of
preceding variables that caused this one, together with any *subsequent* variables, to have no
consistent solution. These conflict sets are computed by an ingenious method of "absorbing" other
nodes' conflict sets.

Once we have our constraint graph, we can also apply some local search techniques from Chapter 4
(e.g., simulated annealing) to CSPs. 

The previous stuff is very general, but honestly, if you look at the problem and can figure out
something from it that is "obviously" going to make the problem easier, do it! In the Australian
color mapping, Tasmania was not connected to the mainland, so it's obvious that it shouldn't have
been part of the original coloring problem at all! Thus, splitting the graph into connected
components would have been a smart tactic. Another way to make a problem easier is to *reduce 
their constraint graphs to trees*, because any tree-structured CSP can be solved in time linear in
the number of variables. We can assign values to variables so that the remaining ones form a tree,
or we can do a more sophisticated **tree-decomposition**, where nodes are now a set of variables,
and variables can be part of multiple nodes. Each node represents its own subproblem.

## Part III: Knowledge, Reasoning, and Planning

This part of the book is a little dry, and is about how one can design "languages" or various
formalisms for agents to help them reason and plan about the world by extracting from a knowledge
base. In my undergraduate AI course, we barely covered this part at all, and it was only towards the
last week of class, when attendance was half the normal level because we didn't have a final exam.
I'm not sure how important this part is to AI research nowadays, since AI tends to be synonymous
with machine learning these days. But maybe in some parts of robot motion planning?

Nevertheless, I still decided to read the entirety of it as there might be some important stuff here.

### Chapter 7: Logical Agents

> In which we design agents that can form representations of a complex world, use a process of
> inference to derive new representations about the world, and use these new representations to
> deduce what to do.

This somewhat boring chapter[^wumpus] introduces the class of logic known as **propositional
logic**, which lets agents represent the world through a series of statements and provides inference
techniques to make conclusions. This is an upgrade over the agents in previous chapters. Why?  When
we tell Pacman to perform DFS to determine where it should move in the game, Pacman doesn't *really
know* anything about the game. A human can deduce a number of facts from the world, such as that
Pacman should avoid going towards dead ends if a ghost is behind it and there is no power-up
available there, but to the point of view of the DFS search agent, that knowledge is irrelevant. To
say it another way, search agents only know the world in a very narrow, inflexible sense, and they
can't **make real conclusions**. They **cannot reason**. Constraint Satisfaction Problems alleviate
this knowledge block by changing the representation of states from atomic to a set of variables,
which allows for more efficient inference techniques (arc consistency, etc.), so there is a little
bit of reasoning going on. Here, in Chapter 7, we take another step by representing the world not
through a set of states and variables, but through *logic*. Remember that throughout this chapter
(and the subsequent chapters), the overall theme is *representation*.

A few terms are in order to review:

- A **knowledge base** (KB) is the central component of our agents and will contain all the set of
  sentences (each represented with a specific syntax) that are known to the agent. A knowledge base
  is **monotonic** if the set of *entailed* sentences only increases as new information is added.
  Otherwise, it would be like the model is changing its mind.
- But wait, what is **entailment**? It is the idea that a sentence follows logically from another
  sentence.  By writing $$\alpha \models \beta$$, we state that $$\alpha$$ entails $$\beta$$, so
  that in every model in which $$\alpha$$ is true, $$\beta$$ is also true. The relation implies that
  $$\alpha$$ is a stronger assertion than $$\beta$$ (check this yourself).
- An **inference algorithm** is one that uses existing logical sentences and derives logically valid
  conclusions from them. If we have in our knowledge base that $$x=0$$ and $$y=1$$ then we should be
  able to make the conclusion somehow that $$x+y=1$$. Algorithms that are **sound** derive only
  entailed sentences (this is a good thing), and algorithms that are **complete** can derive any
  sentence that is entailed from the KB, so complete algorithms are also sound. The slowest complete
  inference algorithm (assuming finite spaces) is **model-checking** because it enumerates all
  models to check for entailment. This is not a scalable solution.

Propositional logic includes the following:

- *atomic sentences*, which consist of one symbol
- *not* connectives ($$\neg$$) to negate an expression
- *and* connectives ($$\wedge$$) to join two expressions together (producing a **conjunction**)
- *or* connectives ($$\vee$$) to join two expressions together (producing a **disjunction**)
- *implies* relationships: $$\alpha \Rightarrow \beta$$
- *if and only if* relationships: $$\alpha \iff \beta$$

The semantics of these relationships are what one would expect, i.e., directly based on your
discrete math or math logic class.

How do we use these facts to perform *inference*, and to do it efficiently[^conp]? In other words,
the ultimate question is that we want to decide if $$KB \models \alpha$$ (logically equivalent to
$$KB \Rightarrow \alpha$$) for some sentence $$\alpha$$.  For this, we do some **theorem-proving**.
An important rule is **Modus Ponens**, which states that whenever $$\alpha \Rightarrow \beta$$ is
true, *and* if $$\alpha$$ is true, then $$\beta$$ has to be true. (This makes sense because $$\alpha
\Rightarrow \beta$$ is only false if $$\alpha$$ were true but $$\beta$$ false.) There are a few
others, such as **and-elimination**, which reduces $$\alpha \wedge \beta$$ to (without loss of
generality) $$\alpha$$, but I generally apply these rules by directly appealing to what I remember
about logic, rather than trying to remember rule names and their exact syntax. This must be why I
hate resolving logic by hand.

A rule like Modus Ponens is sound, but incomplete. For a complete rule, we want to use
**resolution**[^requiressearch], which simplifies our problem by eliminating clauses that resolve
with each other and don't contribute to the resulting truth values. If we have $$(P_1 \vee P_2)
\wedge (\neg P_1 \vee P_3)$$, then we can simplify the sentence to be $$P_2 \vee P_3$$ because $$P_1
\vee \neg P_1$$ are complimentary, so they cannot both force their respective clauses to be true.
This is resolution. It applies to pairs of arbitrarily long clauses ANDed together. The key fact is
that a resolution-based theorem prover can, for any sentences $$\alpha$$ and $$\beta$$ in
propositional logic, decide whether $$\alpha \models \beta$$.  Why?

- *Every sentence of propositional logic is logically equivalent to a conjunction of clauses*, or
  said another way, every sentence can be converted into **CNF form**. This is important for
  resolution because it relies on there being a disjunction of literals. (Again, a sentence is in
  CNF form if it is an AND of ORs, and a *clause* is a *disjunction* of symbols.)
- Resolution-based theorem provers work by using contradiction. To show that $$KB \models \alpha$$,
  we show $$(KB \wedge \neg \alpha)$$ is unsatisfiable. Starting with a sentence in CNF form, we
  apply the resolution rule to pairs of clauses to produce (potentially) new clauses. We continue
  with this until there are no new clauses that can be added ($$KB$$ does not entail $$\alpha$$) or
  if *any* two clauses resolve to yield the empty clause ($$KB \models \alpha$$).
- Termination of the above algorithm follows due to the finite amount of symbols in the knowledge
  base, so long as useless literals such as $$A \vee \neg A$$ are removed throughout the clause
  formation process. The proof of completeness for resolution is the **ground resolution theorem**.

While resolution is complete, sometimes we do not need its full power, or it is too slow.  A **Horn
clause** is a disjunction of literals of which at most one is positive, and if our clauses are of
this form, we can perform more efficient inference using **forward-chaining** and
**backward-chaining** algorithms. Forward-chaining means we start with the known facts and try to
draw conclusions (e.g., using Modus Ponens) and propagate inference through the AND-OR graph.
Backward-chaining does this in reverse. These algorithms decide entailment in linear time. And they
are easy to describe to humans. Yay. Of course, we *need* Horn clauses for these to apply.

Moving away from resolution and back to model checking (remember how inefficient that is?), we can
devise several heuristics to improve model checking, such as backtracking search and hill-climbing
search.  Backtracking search is a depth-first enumeration of possible models with early termination,
pure symbol heuristics, and unit clause heuristics. Hill-climbing search is a seemingly crazy way of
doing inference. It randomly picks an unsatisfied clause and flips a symbol in it.  Obviously, this
may go on forever if we get unlucky in our draws, but if we *do* get a solution, then we know for
sure that a solution actually exists!

### Chapter 8: First-Order Logic

To design an agent based on propositional logic, as in the Wumpus world, one has to perform
cumbersome steps to take care of variables representing the same world object, but at different
times. The next upgrade of logic into what is known as *first-order logic* will alleviate us of this
nuisance because of existential ($$\exists$$) and universal ($$\forall$$) quantifiers. The following
rule:

$$\forall x\quad King(x) \Rightarrow Person(x)$$

means that "For all $$x$$, if $$x$$ is a king, then $$x$$ is a person." More formally, first-order
logic assumes that the world now consists of *facts*, *objects*, *relations*, and *functions*, while
propositional logic only assumes the world consists of facts (or propositions). The syntax terms are
that **constant symbols** represent objects, **predicate symbols** represent relations, and
**function symbols** stand for functions. Functions are a special type of relation where there is
only one value for an input (which is the standard way we think of functions). In the above rule,
$$x$$ is a **variable**; terms with no variables are called **ground terms**.

A model in first order logic consists of not only objects, but also various *interpretations* of
each predicate and function. If our world consists of three terms $$A, B,$$ and $$C$$, and two
objects, there are multiple ways we could map those terms: all of them could mean the first object,
or $$A$$ could mean the first and $$B$$ and $$C$$ could both mean the second, and so on. Due to the
amount of ways one could assign symbols to various objects or change the definition of a relation,
model-checking for entailment (which must apply to all possible models) in first-order logic is much
slower than it is for propositional logic.

Going back to universal quantification, we say that $$\forall x\: P$$ is true in a given model if
$$P$$ is true in all possible **extended interpretations** constructed from the interpretation given
in the model. This is a fancy way of saying that if our model has three objects (e.g., Richard the
Lionheart, King John, and Richard's Left Leg), then we better be able to plug in all three of those
objects in as the variable $$x$$ in the rule $$P$$ and have those statements be true. For
existential quantifiers, we just need at least one statement true in the extended interpretation for
$$\exists x\: P$$ to be true.

First-order logic also includes equality. This is convenient when we need two variables to be
unequal. Consider the following rule:

$$\exists x, y\quad Brother(x,Richard) \wedge Brother(y, Richard) \wedge \neg(x = y)$$

This is stating that Richard has at least two brothers. If we removed the $$\neg(x = y)$$ part, then
we could assign $$x$$ and $$y$$ to be the same person. But even if $$x$$ and $$y$$ referred to two
different names (e.g., Daniel and Darius) then they could *still* refer to the same symbol/object.
Thus, to make things easier for our brains, we will follow the **unique-name assumption**. We can
also invoke the **closed-world assumption** in which atomic sentences not known to be true are
false.

### Chapter 9: Inference in First-Order Logic

One way to perform inference for first-order logic is to convert a first-order knowledge base to a
propositional one, and then apply the propositional inference algorithms from Chapter 7. (Yes, I
know you can tell that this will be crazily inefficient, but it might be useful to see *how* that
works.) There are two techniques that help:

- **Universal instantiation** means we can substitute a ground term for a variable in a universally
  quantified rule. The rule is that if $$\forall v\: \alpha$$ is true, then so is $$Subst(\{v/g\},
  \alpha)$$, where $$g$$ is the ground term[^subs].
- **Existential instantiation** means that in an existentially quantified rule, we can create a
  single *new* constant symbol that does not appear in the knowledge base. If $$\exists v\: \alpha$$
  is true, then so is $$Subst(\{v/k\},\alpha)$$, where $$k$$ is that new symbol. This new symbol is
  a **Skolem constant** and is part of a general process called **skolemization**.

These two methods help us to discard universal and existential quantifiers, respectively. (The
former would require us to make *many* new rules, the latter requires only one new rule.) There's
more to this technique of **propositionalization**, but the point is that we can transform
first-order inference queries into propositional form while preserving entailment. Unfortunately,
the question of entailment is **semidecidable**. We will be able to prove entailment for every
entailed sentence, but we cannot *refute* entailment (in layman's terms, "say no") to every
non-entailed sentence. The reason for this is that functions can construct infinitely-many
ground-term substitutions, and we found out earlier that propositional inference algorithms (i.e.,
resolution) terminate *precisely because* we are guaranteed to have finitely many terms.

Despite this somewhat sorrowing news, there is better news to be had with regards to how efficiently
we can "propositionalize." For this, there are two techniques we can draw from: Generalized Modus
Ponens and Unification.

- **Generalized Modus Ponens** is an inference rule which states that for atomic sentences $$p_i,
  p_i'$$ and $$q$$, if there is a substitution $$\theta$$ such that $$Subst(\theta,p_i') =
  Subst(\theta,p_i)$$, then if the following are true:

  $$p_1', \ldots, p_n'$$

  $$(p_1 \wedge \cdots \wedge p_n) \Rightarrow q$$

  then the conclusion is that $$Subst(\theta,q)$$ is true. So what does this mean in English? The
  conclusion is the sentence $$q$$ after we have applied the substitution $$\theta$$ that created
  equivalence between $$p_i$$ and $$p_i'$$. This is helpful in cases when the $$p_i$$s are variable
  rules (e.g., $$King(x)$$) and the $$p_i'$$s are knowledge-base sentences (e.g., $$King(John)$$).
  By applying Generalized Modus Ponens with appropriate substitutions (like $$\{x/John\}$$), we can
  avoid the unnecessary extended interpretations of $$(p_1 \wedge \cdots \wedge p_n) \Rightarrow
  q$$.

  Before moving on, it's worth connecting this rule to *Modus Ponens* from Chapter 7. It's obvious
  that there are *some* similarities: we make the conclusion $$q$$, which is the result of an
  implication $$\alpha \Rightarrow q$$. But why is this called the **generalized** version? It's
  because we "generalize" this rule from propositional logic to first-order logic by introducing
  variables and substitutions, which we know are not present in propositional logic. The book uses
  the term **lifted** for this, but it seems a bit arbitrary to me.
  
- Our next rule relates to the previous one. Remember that we have to make sure that
  $$Subst(\theta,p_i') = Subst(\theta,p_i)$$, but this will require a lot of comparisons.
  **Unification** is the hugely-important process of making different logical expressions have
  identical meanings. For two sentences $$p$$ and $$q$$, unification returns $$\theta$$, a set of
  substitutions for their variables to make them identical, *if* one exists.
  
  Unification may require **standardizing apart** variables to avoid name clashes. Also, more than
  one unifications may be possible for a set of statements, so it is logical to pick the one that
  places fewest restrictions on the variables.

  A naive (but sound) algorithm for unification recursively explores the expressions and builds up a
  unifier along the way, but has complexity quadratic in the size of the expressions being unified.
  More complicated unification algorithms can run in linear time.

Let us now briefly discuss three families of first-order inference algorithms: forward chaining,
backward chaining, and resolution. These should be familiar from propositional logic, since all we
are doing here is extending them to fit in the framework of a first-order logic system, but it is
important to understand *where exactly* the extensions occur. We will clearly have to use rules like
Generalized Modus Ponens and Unification here.

**Forward chaining** in first-order logic applies Generalized Modus Ponens repeatedly to add more
atomic sentences to the knowledge base until no further inferences are possible. This is similar to
propositional logic, where forward chaining would repeatedly apply *Modus Ponens*. But remember how
propositional forward chaining required *Horn clauses* (a generalized version of propositional
definite clauses)? In first-order logic, forward chaining requires *first-order definite clauses*,
which are disjunctions of literals of which exactly one is positive. Many (but all not all)
knowledge bases can be converted into a set of definite clauses, which acts as a preprocessing step.
Then, as stated earlier, we apply Generalized Modus Ponens, ideally until we've solved our query or
reached a fixed point. Again, it's similar to the propositional logic version, except here we
include universally quantified atomic sentences. It is sound and complete, but entailment with
definite clauses is semidecidable.

There are three sources of inefficiency in the naive forward chaining algorithm: (1) that
unification involves searching through too many sets of facts on the knowledge base, (2) that the
algorithm rechecks each rule on every iteration to see whether its premises are satisfied, and (3)
that the algorithm generates facts that may be irrelevant to the goal.

**Backward chaining** in first-order logic means we work backward from the goal, searching for
substitutions and unifications to satisfy $$lhs \Rightarrow rhs$$ where the $$rhs$$ expression is
already known. To find suitable substitutions for $$lhs$$, which is a list of conjuncts which must
all be positive, we may have to perform additional backtracking. The naive backward chaining
algorithm is depth-first search, so it suffers from some standard problems with DFS (e.g, lack of
completeness) that forward chaining avoids.

Backward chaining is used in **logic programming**, a technology where systems are constructed and
make conclusions using processes similar to what happens in first-order logic. **Prolog** is an
example of a logic programming language, but it is incomplete as a theorem prover for definite
clauses. To avoid redundant computations, backward chaining should memoize solutions to
sub-problems.

We can extend **resolution** from propositional logic to create a complete inference procedure for
first-order logic. As before, the first step is to convert first-order sentences into inferentially
equivalent CNF sentences, which is always possible, and forms the basis for future
proofs-by-contradiction resolution procedures. This conversion process isn't too difficult, though
we need to eliminate existential quantifiers via **Skolemization** (briefly mentioned earlier). The
process might involve creating *Skolem functions* to clarify variable dependencies.

The resolution *inference* rule is a generalization of the propositional reference rule to handle
variables. Two clauses standardized apart (i.e., no shared variables) can be resolved (and therefore
removed from proof as they don't affect the outcome) if they contain complementary literals. In
first order logic, complimentary literals are those in which one *unifies* with the *negation*  of
the other; remember that in propositional logic, we just had to worry about straightforward
negations.

Resolution is *refutation*-complete in the following sense: if $$S$$ is an unsatisfiable set of
clauses, then the application of a finite number of resolution steps to $$S$$ will yield a
contradiction. Resolution cannot generate all logical consequences of a set of sentences.

### Chapter 10: Classical Planning

This chapter introduces a representation for planning problems in single-agent, deterministic,
observable environments, which scales far better than the earlier search agents of Chapter 3 and the
logical agents of Chapter 7. As a starting step to analyze and standardize language, AI researchers
have introduced the **PDDL** language, the Planning Domain Definition Language. It can describe the
things we need to define a search problem:

- the initial state, or states in general, which are conjunctions of ground (i.e., no variables or
  functions) atoms called *fluents*.
- the actions, which have variables, preconditions, and effects. They are only applicable in a state
  if the state satisfies the preconditions.
- the list of actions at each state, and the result of applying each action.
- the goal test, which is again a conjunction of literals, though these may contain variables. The
  goal is to find a sequence of actions that lead to a goal state.

There are several straightforward examples of PDDL in the book. They are intuitive descriptions of
various problems written in a structured framework, though there is some trickery involved (e.g.,
with inequalities).

PDDL maps planning problems to search problems, and we can solve these with forward searching or
(you must know what's coming...) backward searching through states. Forward searching needs
heuristics, because as stated earlier, the branching factor is too large to apply one of the Chapter
3 or 4 search algorithms directly. Backward searching avoids many irrelevant states, and PDDL makes
it easy to represent the backtracking process, but requires *sets* of states and does not lend
itself to easy heuristics.

To get an admissible heuristic, we can relax the problem to make it easier and apply the resulting
solution to the original one. The corresponding search graph has nodes as states and actions as
edges. Some ideas for heuristics:

- Ignore preconditions, so every action becomes applicable in every state.
- Ignore delete lists, applicable if all goals and preconditions are positive literals. This removes
  all negative literals from all actions, and the problem is easier now because no action will undo
  progress made by another action.
- To reduce the number of states, ignore some of the fluents.
- Assume subgoal independence, so if the goal is $$G_1 \wedge \cdots \wedge G_n$$, take as the
  estimate the maximum cost over all $$n$$, or sum up the estimated costs for each state (note: this
  is inadmissible).

A special data structure called a **planning graph** can provide better admissible heuristics than
the ones previously suggested; we build the graph, and then search over it (this is called
"GraphPlan" in the book). The planning graph is a directed graph of states, and is a
polynomial-sized approximation to the exponential-sized tree that consists of all the possible
paths taken from the starting state, with the goal of finding a path to the goal state. It consists
of alternating *state levels* $$S_i$$ and *action levels* $$A_i$$. The state levels contain the
literals that might be true (since it's an approximation) at a given state[^planning], and the
action levels contain the actions whose preconditions are satisfied by those literals in the
previous state level.  Literals that show up later in the tree (i.e., farther away from the starting
state) are "harder" to achieve, so the true states that *contain* those literals are "harder" to
reach.

A key property of state and action layers is that they contain **mutual exclusion** or **mutex**
links between literals and actions, respectively. A mutex relation holds between two *actions* if
they have inconsistent effects, interference, or competing needs. A mutex relation holds between two
*literals* if one is the negation of the other, or if the pairs of actions that could *lead* to
those literals are mutex.

Now that we've constructed a planning graph, how do we *use* it? As stated earlier, we can estimate
the cost of achieving any goal literal $$g_i$$ as the *level* in which it first appears in the
planning graph, i.e., the **level cost**. If the goal state is a conjunction of literals, which is
the normal case anyway, then some ideas are:

- Take the maximum level cost over all literals. This is admissible.
- Take the sum over all literals. This is *not* admissible, though it might work if the individual
  literals are reasonably independent of each other.
- Take the level cost of the level in which all literals are in the planning graph, *without* there
  being any mutex relations between the two. This is admissible and also clearly dominates the
  maximum level cost heuristic because the level we return will have all the literals.

As an alternative, we can run the GraphPlan algorithm to search *directly* on the planning graph.
The algorithm repeatedly adds levels to the planning graph, and finishes once all the goals show up
as non-mutex in some possible state for a state layer. If the action and state levels do not
increase, then the algorithm returns failure.

The downside of planning graphs is that they only work for propositional planning problems, though
if we wanted, we could obviously convert a first-order logic encoding of a plan into propositional
logic. They also fail to detect unsolvable problems with three-way mutex relations but no two-way
mutex relations.

There are a few other classical planning paradigms:

- We can treat this as a theorem-proving problem by transforming the PDDL description into a form
  that can be processed by a SAT solver. This step involves propositionalizing the actions and the
  goal, as well as adding in more axioms to handle successor states and mutual exclusions.
- We can use first-order logical deduction rather than PDDL. Rather than tie time directly to
  fluents, we can use *situation calculus* and create new rules to apply to our states. The downside
  of this approach is that it's hard to get good heuristics.
- We can transform the problem of finding a plan of length $$k$$ as a constraint satisfaction
  problem (from Chapter 6), similar to the encoding for a SAT problem.
- We can also create **partially ordered plans**, which is useful with independent subproblems.
  We can create such plans by searching through the space of plans, rather than the state space.
  Unfortunately, it doesn't represent states easily, and these fell out of favor (after the 1990s)
  in place of plans that search through states with strong heuristics.

### Chapter 11: Planning and Acting in the Real World

This rather amusingly-titled chapter now brings us into the "real world" by requiring that our agent
representation must handle not only planning, but also handle a *changing environment*. Here are
some of the new assumptions we make in our world:

- We may have to deal with time and resource constraints.
- We may have to organize plans in a hierarchical fashion.
- We may have to handle nondeterminism and uncertainty in our environment.
- We may have to deal with multiple, competing agents.

Let's briefly discuss how we design an agent to handle these four cases.

To deal with time and resource constraints, we augment the language of the problem formulation to
include *amounts* for certain resources (e.g., $$Inspectors(9)$$ means there are nine inspectors
available in a car inspection problem), as well as *Consume* and *Use* keywords to indicate whether
the resource is gone or available again after usage (e.g., inspectors would usually be available
again after their usage). We can represent the problem with a directed graph that obeys the
time/resource constraints, and then find the *critical path* through the graph, which is the path
with the longest duration and thus is the "limiting factor" in the schedule. A heuristic to find the
minimum cost path: for each iteration, choose the action with all predecessors satisfied, and which
has the least amount of slack.

In order for AI systems to think like humans do, AI systems will need to make plans at a higher
level of abstraction by forming hierarchies. The classic example is when we organize a plane trip to
Hawaii. The high-level abstraction is: take the BART to the airport, search for the gate, etc.
Humans do not think: first, open the door carefully, then take seven paces to the right, then walk
down this way for 500 steps, then put the ticket inside the BART gate, etc. That kind of detail
would lead to too much combinatorial explosion in AI systems. So AI agents must use **high-level
actions** (HLA) that can possibly be refined later. One way to solve such hierarchy problems is to
start with one or multiple HLAs that solve the problem, and then refine it (e.g., in a BFS fashion)
until we get a sequence of *primitive* actions that accomplishes the goal. This can be substantially
faster than normal BFS over the space of primitives. To get an even greater --- potentially
*exponential* --- speedup in search, what we would like to do is only search through the space of
HLAs, and once we find a sequence of HLAs that work, *then* we can refine that one plan into
primitives, since we *know* it works. To do this, we set up preconditions and effects for each HLA,
and the state space will be a set of fluents (as it was before in many areas of Chapter 10). We can
define a search problem known as **angelic search** that utilizes **reachable sets** of HLAs.
Pessimistic and optimistic reachable sets can prune away refinements that have no chance of reaching
the goal.

Our agents will have to deal with nondeterminism and uncertainty in the environment. With no
observations, we can perform sensorless planning. With partial observations, we can perform
contingency planning, and for unknown environments, we can do online learning. Some material is
similar to what was presented in Chapter 4, and the main difference here is that we have a far
richer state representation (fluents rather than atomic) and thus we can represent belief states
easily using $$O(n)$$-length conjunctions (well, assuming that our belief states are 1-CNF). It can
be tricky to update belief states after an action.  An example problem with fluents might be that we
have to paint two chairs to be the same color, and a sensorless agent could solve the problem by
just dumping a can of paint on both chairs, without knowing the color of the paint at all. A
contingent agent can also solve the problem, and often does so more efficiently.

Finally, we can consider the *multiagent* case, either when one "super" agent controls multiple
smaller agents, or when there are multiple, separate agents who only control themselves (and whose
goals may be in competition with one another). If the agents are loosely coupled, it makes sense to
decompose the transition model into independent subproblems to avoid an exponential *branching*
factor.

### Chapter 12: Knowledge Representation

> In which we show how to use first-order logic to represent the most important aspects of the real
> world, such as action, space, time, thoughts, and shopping.

Wait, *shopping*? All right all right, let's see what's in store here in the final chapter of the
*Knowledge, Reasoning, and Planning* aspect of AI. The previous chapters have come up with the
*technology* (e.g., first-order logic and its various inference methods) for knowledge-based agents,
but now, we have to figure out the *content* to put in an agent's knowledge base.

I don't think there is much material in this chapter that I need to know, and a lot of it is common
sense. But here are the highlights regardless:

- **Ontological engineering** is the process of representing abstract concepts of events, time,
  physical objects, and beliefs in various domains. We clearly have to do something like this to
  design an agent! One way is to describe an *upper ontology* of the world by listing some general
  things first, and then moving to more specific items down the tree (this is what we do in object
  oriented programming).
- We need to represent the following: categories, objects, and events. We can represent categories
  by using straightforward predicates (e.g., the category of basketballs could be $$Basketball(b)$$)
  or by **reification**[^reify], a.k.a. *thingification*, which means representing it as an object
  $$Basketballs$$. To *reason* about categories, we can use the graphically appealing **semantic
  network** framework, or appeal to formalism with **description logic**[^exceptions]. Objects
  should be arranged in a hierarchy of categories with subclassing and inheritance, kind of like
  (again) how we do it in object-oriented programming. For events, rather than the *situational
  calculus* we saw earlier, we should use **event calculus** to deal with continuity.  Event
  calculus reifies fluents and events.
- Sometimes, we may wish to represent mental beliefs by **model logic** rather than first-order
  logic, because the former lets us take *sentences* as arguments, and allows us to represent a set
  of *possible worlds* of beliefs. The notation $$K_AP$$ means that agent $$A$$ knows $$P$$.
- At the end of the chapter, there is a shopping mall example, which I find to be amusing but not
  that educational.

Whew! Reading the above ten chapters, as well as Chapters 1 and 2 in the book, and Chapter 13 (which
is about basic probability, nothing to see here!) brings me to the 500-page mark out of 1000 pages.
Now I only have 500 pages to go!

***

[^another]: Said another way, it never overestimates the cost of reaching a given state.

[^ofcourse]: It is also possible that the MIN player is dumb and doesn't play optimally, but the MAX
    player following the minimax strategy would perform even better if that were the case. 

[^berkeleyai]: These assignments are a great way to see more complicated applications of algorithms
    from the textbook.

[^evals]: Various *evaluation functions* (e.g., heuristics) are of course domain-specific, but the
    point is that the *search algorithms* are not domain-specific. It's worth thinking about this
    often.

[^wumpus]: There's also a nice Wumpus example in this chapter that makes it twice as much fun to read. 
    *That* part is not dry.

[^conp]: The book states that propositional entailment is co-NP-complete, so every known inference
    algorithm for propositional logic has a **worst-case** complexity exponential in the size of the
    input. Still, this is "only" worst case complexity.

[^requiressearch]: Technically, resoultion is complete if it is coupled with a complete search algorithm.

[^higherorder]: If you're curious, **higher-order logic** takes logic another step up by treating
    everything from first-order logic as objects (including relations) that are subject to
    *additional* relations.

[^subs]: The notation $$Subst(\theta, \alpha)$$ denotes the result of applying the substitution
    $$\theta$$ to sentence $$\alpha$$. The substitution rule should be of the form $$\{x/y\}$$ where
    $$x$$ is a variable and $$y$$ is a real term that we want to plug in.

[^planning]: A literal cannot appear *too late* in a state level, because that would be like
    over-estimating the cost of that literal and the states it belongs to, resulting in inadmissible
    heuristics.

[^reify]: One of the advantages of reification is that by doing so, we represent what we want in
    terms of *objects*; then we can add an arbitrary amount of information about them. For instance,
    refiying events means we can add in as many descriptions about the event as we want by adding in
    more conjuncts.

[^exceptions]: Representing categories these ways also helps us to establish *default values* for
    categories. Unlike in previous forms of knowledge representation, semantic networks and
    description logics make it easy for us to have *exceptions* for objects. For example, most
    tomatoes are red, but some can be purple. Thus, the category of tomatoes should have a *default*
    color attribute of red, with individual objects potentially overriding those values. The
    connections between this and programming languages is once again obvious. Also, note that if we
    allow overriding, then this violates **monotonicity** of the logic. Monotonicity means that if
    $$KB \models \alpha$$, then for any $$\beta$$, $$KB \wedge \beta \models \alpha$$.




