---
layout: post
title: Talk Review - Francois Chollet's Neurips 2020 Talk
---

I've been finding Francois Chollet's line of thinking on the nature of intelligence since his 2019 paper "The Measure of Intelligence" to be very insightful. This is my attempt to both walk through the ideas from his latest talk at Neurips 2020, and also to synthesize a fuller understanding of his thesis. Note that this is not intended as a tutorial on Chollet's ideas, merely my own reflections on them.

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

In his talk Chollet briefly introduces his dataset and challenge problem for AI researchers, the *"Abstract Reasoning Corpus (ARC)"*. ARC is a task which Chollet designed to require only a subset of *"Core Knowledge"*

*"Core Knowledge is basically the set of innate cognitive priors possessed by humans, which guide our ability to learn throughout our lives [and] form the atomic building blocks of thinking..."*

*"Core Knowledge systems are innate, or at least they emerge very early which is basically the same for all intents and purposes. They're ancient. So we find them in non human primates and you also find some of them in different animals, like birds for instance."*

[*Core Knowledge*](https://www.harvardlds.org/wp-content/uploads/2017/01/SpelkeKinzler07-1.pdf) is the name of a theory developed by psychologist Elizabeth Spelke which states in essence: *"Human cognition is founded, in part, on four systems for representing objects, actions, number, and space..."*. In Chollet's talk he also references two other domains of Core Knowlege pertaining to "locations" and "social partners", but they aren't used in ARC.

## II. Abstraction is the key to generalization

*"By now you should have a pretty good ideas why we should focus on achieving broad generalizable cognitive abilities rather than task-specific skills, and this brings us to the problem of abstraction. Abstraction and generalization are closely tied because abstraction is the engine through which you produce generalization."*

*"An interesting observation about the universe, which applies to pretty much any problem domain you can think of, is that it is made of any different things that are all similar, all analogous to each other. So we are surrounded by isomorphisms, and I call this the kaleidoscope hypothesis...[a kaleidoscope] is a tube with a few bits of colored glass in it, which are repeated and amplified by a set of mirrors. And it creates a remarkable richness of complex patterns out of just a couple of kernels of original information, which are the bits of colored glass..."*

*"Generalization is the ability to mine the experience that you have to identify bits that are reusable. And you extract those bits and you call them abstractions, and they take the form of programs and representations and you reuse them to make sense of novel situations."*

*"So how do you identify reusable kernels of structure? Simply by noticing when two things similar, by noticing analogies. Because if something is repeated twice, then both instances of that thing must have a single origin, like in a kaleidoscope."*

*"So intelligence, which is to say, generalization power, is literally sensitivity to abstract analogies, and that's in fact all there is to it. Intelligence is sensitivity to analogies. So if you have a very high sensitivity to analogies, you will be able to extract powerful abstractions from little experience. And you will be able to use these abstractions to operate in a maximally large area of future experience space. You will be maximally efficient in converting past experience into the ability to handle future novelty."*

Now Chollet gets into more detail on what he means by abstraction.

*"There are two key categories of abstractions that we're interested in in this talk: value-centric abstraction and program-centric abstraction...they're pretty similar to each other: both of them are about comparing things and merging individual instances into common abstractions by eliminating certain details about these instances. But there's a key difference, which is that one of them operates over a continuous domain and the other over a discrete domain."*

*Value-centric abstraction* (or *"value-analogy"*) is the one that operates over a continuous domain and *program-centric abstraction* (*"program-analogy"*) is the one that operates over a discrete domain.

Deep learning is good at value-centric abstraction.

*"Value-analogy is geometrically grounded... you compare instances via a distance function, and you create abstractions by merging instances that are similar into a prototype."*

*"Deep learning excels at [value-analogy] which makes sense because deep learning models are continuous, in fact, they are differentiable parametric models. So it's intuitive you would be able to produce abstractions that are grounded in geometry using deep learning. In supervised deep learning, what you're doing is [creating] an analogy between two spaces...you are learning a smooth geometric morphing between the two spaces, point by point. So it's a geomtric analogy between two spaces, and that's really what a deep learning model encodes, it's this space to space analogy."*

*"...Deep learning is about relating samples to each other via a learned distance function, which implicitly defines a manifold."*

So-called *good old fashioned AI"* or *GOFAI* failed to solve problems like object recognition or speech recognition because programs written by hand can't handle the combinatorial explosion of possible inputs. However, it turned out that deep learning models can be trained to project images, speech, and natural language onto continuous manifolds. If any input from the distribution in question can be placed neatly onto a learned manifold, then linear layers can easily be trained to draw decision boundaries through the manifold.

*"Program-centric abstraction, on the other hand, is about comparing discrete programs, which is to say graphs, and rather than computing distances you are looking for subgraph isomorphisms. And that's similar to human reasoning, planning, it's also what software engineers do..."*

*"Program-analogy is topologically grounded. If you compare the structure of two graphs, and you create abstractions by merging instances that are isomorphic into an abstract program"*

According to Chollet, *"...all intelligence arises from a combination of these two forms of abstraction."* This is not as profound a claim as it at first seems if one allows that we can divide the world into continuous domains and discrete domains, and that both domains require a distinct form of abstraction.
