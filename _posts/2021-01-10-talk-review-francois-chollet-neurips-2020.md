---
layout: post
title: Talk Review - Francois Chollet's Neurips 2020 Talk
---

I've been finding Francois Chollet's line of thinking on the nature of intelligence since his 2019 paper "The Measure of Intelligence" to be very insightful. This is my attempt to both walk through the ideas from his latest talk at Neurips 2020, and also to synthesize a fuller understanding of his thesis and where I agree and/or disagree. Note that this is not intended as a tutorial on Chollet's ideas, merely my own reflections on them.

The title of this talk is *"Why abstraction is the key to intelligence, and what we're still missing"*.

*"...my talk is specifically about the intersection between reasoning and deep learning."*

The presentation outline was as follows:

I. To make progress towards AI, we need to measure & maximize generalization
II. Abstraction is the key to generalization
III. Capabilities & limits of Deep Learning with regard to abstraction
IV. Discrete program search: how to learn to reason
V. The road ahead: bridging both worlds

## I. To make progress towards AI, we need to measure & maximize generalization

Chollet begins by defining generalization and his definition won't surprise you. He defines it as *"the ability to handle situations (or tasks) that differ from previously encountered situations"*. He then proceeds to introduce a simple hierarchy of the forms of generalization (from no generalization at all to *"extreme"* generalization) that he introduced originally in his paper *"The Measure of Intelligence"*.

In that paper he defined intelligence as: *"The intelligence of a system is a measure of its skill-acquisition efficiency over a scope of tasks, with respect to priors, experience, and generalization difficulty."*

In other words, one can say very roughly that intelligence is the ability to acquire new skills with as little in the way of priors or experience as possible. However, there are several axes to consider here:

1 - *What tasks* are in scope?
2 - *How useful* are the learned skills at solving those tasks? i.e. how well can they 'solve' the tasks.
3 - *How much* prior knowledge and experience was used to acquire those skills?
4 - *How hard* is it to generalize from the priors and experience to the learned skills?

Chollet also refers to intelligence as a "conversion ratio" between priors & experience into skills. *"The Measure of Intelligence"* also includes a lengthy section that formalizes this with algorithmic information theory.

It's interesting to consider this definition in the historical context of AI.

The early days of AI looked very much like the field we simply call "algorithms" today. It was about identifying structure in problems and defining data structures and algorithms to exploit that structure to rapidly solve instances of a given problem type. Many students of AI have no doubt been surprised and disappointed (as I was) to open up the standard textbook on the field (Norvig & Russell's *Artificial Intelligence: A Modern Approach*) and find that the first several sections, tracing the early history of the field, is nearly indistinguishable from a textbook on algorithms. A\* search, alpha-beta pruning, constraint satisfaction algorithms, etc... The connection to Chollet's ideas is that the early history of AI tended to focus on defining *priors* in the form of data structures and algorithms, and tended to leave out experience and learning.

The field of AI post the deep-learning revolution seems to have the opposite obsession. In the last few years there is much emphasis about learning as much as possible from scratch, and for good reason. Computer vision researchers laboured for years refining complicated algorithms by hand, only to be blown away by AlexNet which utilized only a few simple inductive biases (distributed representations, equivariance to translation, etc...) plus lots of training data. DeepMind's progression from AlphaGo to AlphaZero to MuZero has been about removing assumptions about the structure of the problem, thus increasing the generality of the resulting learning algorithms. Note however that these systems seem to require a massive amount of experience to reach human-level performance on the tasks they train on. Using massive models on massive datasets is all the rage, with OpenAI's GPT-3 and DALL-E being perhaps the most impressive systems in this line of development. Again, the connection to Chollet's ideas is that the deep learning era seems to be focused on maximally exploiting *experience* in the form of training data. Of course, deep learning still relies on *priors* encoded by the architecture and optimization procedures. In machine learning, these are also known as inductive biases. What makes them priors is that they are specified by-hand. Despite much effort to automate designer effort, architecture and hyperparameter search only goes so far, especially when you're already investing so much compute into training a single model from scratch.

In Chollet's view, task-specific skills can't tell you anything about an agent's intelligence, because it is possible to *"buy arbitrary performance"* by simply defining better priors or utilizing more experience. *"[Defining better priors or training from more experience] reduces uncertainty and novelty and thus reduces the need for generalization."*

One thing that used to confuse me about this is that that priors, i.e. inductive biases, are the only thing that makes generalization possible. Generalization ability actually comes from priors. Chollet as it turns out also agrees with this as he notes in *TMOI*, *"...priors are not a limitation to our generalization capabilities; to the contrary, they are their source, the reason why humans are capable of acquiring certain categories of skills with remarkable efficiency."* So what does it mean to say that we need to measure and adjust for priors? The answer is that we only need to account for domain-specific priors, also known as *"knowledge priors"*.

There is in fact a spectrum of possible priors. We tend to think of priors as domain-specific heuristics, for example the use of endgame tables in chess playing, or even merely encoding the rules of a game into an agent. However, there are also more general and abstract priors. For example, Chollet makes ample reference to *"human cognitive priors"*.

*"Human cognitive priors come in multiple forms, in particular:"*

- *"Low-level priors about the structure of our own sensorimotor space, e.g. reflexes such as the vestibulo-ocular reflex, the palmar grasp reflex, etc. These priors enable infants (including prior to birth) to quickly take control of their senses and bodies, and may even generate simple behaviors in a limited range of situations."*

- *"Meta-learning priors governing our learning strategies and capabilities for knowledge acquisition. This may include, for instance, the assumption that information in the universe follows a modular-hierarchical structure, as well as assumptions regarding causality and spatio-temporal continuity."*

- *"High-level knowledge priors regarding objects and phenomena in our external environment. This may include prior knowledge of visual objectness (what defines an object), priors about orientation and navigation in 2D and 3D Euclidean spaces, goal- directedness (expectation that our environment includes agents that behave according to goals), innate notions about natural numbers, innate social intuition (e.g. theory of mind), etc."*

*"When it comes to creating artificial human-like intelligence, low-level sensorimotor priors are too specific to be of interest (unless one seeks to build an artificial human body). While human meta-learning priors should be of the utmost interest (understanding the strategies that the brain follows to turn experience into knowledge and skills is effectively our end goal), these priors are not relevant to evaluating intelligence: they are intelligence, rather than a third-party modulating factor to be controlled for. They are part of the black box that we seek to characterize."*

*"It is knowledge priors that should be accounted for when measuring a human-like form of intelligence. A system that does not possess human innate knowledge priors would be at a critical disadvantage compared to humans when it comes to efficiently turning a given experience curriculum into skill at a given human task. Inversely, a system that has access to more extensive hard-coded knowledge about the task at hand could not be fairly compared to human intelligence*"

Note that priors *determine* generalization ability, and therefore determine how much experience will be needed to acquire a given skill. If we interpret priors as simply everything required to specify the initial state of a system, then this is surely true. Thought about this way, the problem of AI is thus to define (and/or meta-learn) the right priors such that relatively small amounts of experience are sufficient to acquire *any* conceivable skill. Note that we can think of skills as programs.

The field of AI has been focused on the outputs of intelligence, producing the programs that implement specific skills. In Chollet's view, if our goal is to produce intelligence, then this is an error because there are always shortcuts to produce such programs that don't correspond to progress towards building intelligent systems. For example, the shortcut of building-in domain specific priors, i.e. human defined abstractions that simplify a problem, or the shortcut of using massive amounts of experience.

---

After the failures of the so-called *good old fashioned AI"* or *GOFAI*, it's been amazing to see how rapidly AI has progressed in the last decade. *GOFAI* failed to solve problems like object recognition or speech recognition because programs written by hand can't handle the combinatorial explosion of possible inputs. However, it turned out that deep learning models could be trained to project images, speech, and natural language onto continuous manifolds. If any input from the distribution in question can be placed neatly onto a learned manifold, then linear layers can easily be trained to draw decision boundaries through the manifold.



## II. Abstraction is the key to generalization





TODO REMOVE:
He also distinguishes *system-centric generalization* (the ability of a system to generalize from its past experience) from *developer-aware generalization* (the ability of a system to generalize beyond what its developer anticipated).
less powerful generalization => more powerful generalization
system-centric generalization => developer-aware generalization
