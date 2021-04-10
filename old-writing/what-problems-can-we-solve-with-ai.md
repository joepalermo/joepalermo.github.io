Recently, I was asked:

At what point do you think algorithms will make humans irrelevant in investing? Do you think that will be achieved before human-level artificial intelligence?

Before answering directly, I want to outline some principles that seem useful for thinking about this kind of thing.

A more general question is: For humans trying to solve problems, which problems are more amenable to machine solution, as opposed to the direct application of human intelligence. Ultimately, I think this is a false dichotomy (i.e. humans intelligence + machine intelligence, in combination, will solve some problems better than either alone), but more on that later.

The question of which problems will succumb to algorithms first has to do with the type of structure inherent to different classes of problems.

What really surprised early AI researchers was how much easier it is to solve problems in formally defined and closed problem-spaces as opposed to messy, open-ended real-world problems. Take for instance the work that has been done in chess playing algorithms. At first, it seemed as if an algorithmic solution to chess would signal that we weren’t far off from creating a general purpose algorithm that could solve any intellectual problem. After all, chess is a highly intellectually challenging for humans. When a person is world-class at chess, we generally consider them to be extremely intelligent. Now, in hindsight, it’s clear that chess playing represents this tiny class of problems that can be solved just by searching a relatively simple game tree. Furthermore, applying the same approach to solving real-world problems is hopeless. Each juncture in the ‘game tree’ would include infinitely many options.

Solving a non-trivial problem with an algorithm always requires exploitation of the underlying structure of the problem-space. Let’s unpack that statement by looking at how it applies to the problem of playing chess.

For an algorithm to beat humans at chess it needs to be able to more accurately assess the value of the available positions. One way to do this is to have a more effective evaluation function. An evaluation function is a function that takes as input a board position and returns as output an estimate of the value of that position. If one evaluates each of the boards resulting from each available move at a given position, in principle, that should be sufficient for choosing the optimal next move.

Human masters play chess as well as they do because they have developed very effective evaluation functions, i.e. intuition. Thus, beating a human by training an evaluation function is akin to beating them at their own game. But machines have another avenue available to them to that humans don’t.

The reason that machines are so vastly better than humans at chess today is that they can search game trees with extreme efficacy. As it turns out, it’s generally easier to assess the value of a position that is more developed and has fewer pieces. Thus machines can use their incredible speed to search more deeply into the game tree, improving the quality of their evaluations.

There are two ways you can improve your search depth. You can do it either by simply checking more positions, or you can exploit the structure of the game to prune away large parts of the search through possible moves. This is analogous to making either a hardware improvement, or a software improvement.

It’s interesting to note that when humans play chess they explicitly consider only a tiny fraction of the positions that a chess computer does. The reason why chess masters are still somewhat competitive with some of these systems is that they can exploit the structure of chess. Their mind never even considers most of the options available to them, because they have trained their mind to sniff out only promising paths through the space of possibilities available to them. In other words, they instinctively prune away most of the game tree with pattern recognition. They think about the game with higher level concepts – they talk about the ‘flow’ of the game, or attacking and defending configurations, etc…And not quite so much as a search through deep branches of move sequences.

So when we represent the problem of playing chess as the problem of searching through the game tree of all possible move sequences, that says more about our ignorance of chess than it does about intelligent chess play. This is because chess has a compact underlying structure. By that, I mean that with knowledge of chess you can search a smaller space of possible moves. The ‘true’ structure of the search space is more compact than the trivial one of enumerating all possible moves – but you have to know about chess concepts before you can search that smaller space.

Ultimately, every interesting problem-space has a compact underlying structure. Even the world itself must have a compact underlying structure. If it didn’t then general intelligence would be impossible, and the human mind would be impossible. We humans don’t enumerate all possible actions of what to do next. We just instinctively think of (mostly) coherent courses of action.

Now, in light of these principles, let’s revisit the original question:

At what point do you think algorithms will make humans irrelevant in investing? Do you think that will be achieved before human-level artificial intelligence?

This depends on the structure of the problem-space. Because the space of all possible things that can affect the value of a stock is so huge and varied, it seems clear that human intelligence will have a role to play at least until there are significant developments in artificial general intelligence. When that will occur is impossible to predict.

The thing that AI can’t do at all yet, and that humans do really well, is build compact models of an open-ended world. Each of us has represented in our minds, partly explicitly and partly implicitly, a model of how the world works. Furthermore, we’re constantly updating this model with new information, and inventing entirely new concepts to try to simplify our model. It seems to me that this is the kind of thing you would have to do to entirely replace a human investor.

However, that leaves open the question of how well algorithms will be able to aid human investors in the interim before AGI takes over. You can imagine scenarios in which humans may have worked out a model of how things work, but are enable to reason out what parameters to plug into their system without running algorithms to tune it.

In this vein we can ask ourselves, which algorithms might we apply to databases about the world, whose output we could then back feed into our own models of the world.  There can be a symbiosis between human intelligence and machine intelligence. For those parts of the problem-space where structure is well understood, we can unleash the machine’s raw power and come away with new insights. Where structure is less well understood, which occurs in more open-ended problem-spaces, machines will for the time being be rather useless.
