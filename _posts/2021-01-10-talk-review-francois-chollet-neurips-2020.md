---
layout: post
title: Talk Review - Francois Chollet's Neurips 2020 Talk
---

I've been finding Francois Chollet's line of thinking on the nature of intelligence since his 2019 paper "The Measure of Intelligence" to be very insightful. This post is my attempt to walk through the ideas from his talk at Neurips 2020 and also to synthesize for myself a better understanding of his thesis. Note that this is not intended as a tutorial on Chollet's ideas, merely my own reflections on them.

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

## III. Capabilities & limits of Deep Learning with regard to abstraction

Deep learning is good at value-centric abstraction.

*"Value-analogy is geometrically grounded... you compare instances via a distance function, and you create abstractions by merging instances that are similar into a prototype."*

*"Deep learning excels at [value-analogy] which makes sense because deep learning models are continuous, in fact, they are differentiable parametric models. So it's intuitive you would be able to produce abstractions that are grounded in geometry using deep learning. In supervised deep learning, what you're doing is [creating] an analogy between two spaces...you are learning a smooth geometric morphing between the two spaces, point by point. So it's a geomtric analogy between two spaces, and that's really what a deep learning model encodes, it's this space to space analogy."*

*"...Deep learning is about relating samples to each other via a learned distance function, which implicitly defines a manifold."*

*"Value-based abstraction relates to the manifold hypothesis in machine learning. The manifold hypothesis posits that all natural data lies on a low-dimensional manifold within the high-dimensional space where it is encoded, and as far as we know, it's accurate for pretty much any perception problem... And the manifold hypothesis also implies that within one of these manifolds it's always possible to interpolate between any two inputs... And the ability to interpolate between samples is the key to understanding generalization in deep learning. It's the reason why deep learning works... [you can] make sense of points you've never seen before by relating them to other points that lie close to them on the manifold."*

*"This is effective for perception problems but it has limitations. It's brittle. It's sensitive to small perturbations. And that's because it's a point by point mapping between two spaces and if you shift one of the spaces slightly, the mapping that was learned breaks down. That's where you start seeing that topology based abstraction is more powerful than geometry-based abstraction, because distances are not robust to small perturbations but structure is robust to small perturbations. And there's an even bigger limitation which is that for geometry-based abstraction to even be relevant, you need to be dealing with a continuous domain. So you cannot apply deep learning to discrete problems like sorting a list, for instance, or finding prime numbers...you cannot solve these problems with continuous optimization because they have a discrete structure, fundamentally... You could always try embedding that discrete structure in a continuous manifold, but you couldn't use that manifold for interpolation. So your continuous parametric model could not generalize to things it has not seen before. So in order to learn a useful embedding you would need an exhaustive sampling of the problem space."*

*"So the take away here is that in order for deep learning to be relevant for a given problem, you need two things:"*

- *"The data points fit on a manifold where interpolation is meaningful (i.e. the manifold hypothesis applies)"*

- *"There is a dense sampling of this manifold available (i.e. lots of training data)"*

So-called *good old fashioned AI* or *GOFAI* failed to solve problems like object recognition or speech recognition because programs written by hand can't handle the combinatorial explosion of possible inputs. However, it turned out that deep learning models can be trained to project images, speech, and natural language onto continuous manifolds. If any input from the distribution in question can be placed neatly onto a learned manifold, then linear layers can easily be trained to draw decision boundaries through the manifold.

## IV. Discrete program search: how to learn to reason

*"So how do you solve these problems like ARC, sorting a list, finding prime numbers, etc...? Any reasoning and planning problem. The answer is simple, it’s program synthesis. Which is to say combinatorial search over graphs of operators taken from a domain specific language (DSL). Discrete search over graphs."*

*"You can draw an analogy between ML and program synthesis. In ML, your model is a differentiable parametric function, and in program synthesis, it's a graph of ops from a DSL. In ML, your learning engine is SGD, and in program synthesis it's combinatorial search. In machine learning the key obstacle is that you need a dense sampling of your problem manifold, and in program synthesis the key challenge is combinatorial explosion."*

*"You can use program synthesis to solve problems from very few examples, unlike deep learning, but the set of possible programs that you can build grows combinatorially with problem size."*

*"Program synthesis, and in particular genetic programming, has been pretty successful on ARC..."*, although he does temper this by alluding to the fact that the best results achieved thus far are very far from optimal (the best error rate on the [2020 Kaggle competition](https://www.kaggle.com/c/abstraction-and-reasoning-challenge/leaderboard) was 79.4%.

He notes that all of the top solutions to ARC so far are based on program search over a DSL, with heuristics to make search more efficient. *"even though they're very primitive they remain infinitely more successful than deep learning on ARC problems."*

At first blush it sounds like Chollet is suggesting a return to GOFAI, but that's not what Chollet is advocating. He recognizes that to utilize program synthesis, we need to grapple with the challenge of combinatorial explosion. So how do we do this?

*"If you want to make something efficient, there's a universal recipe, which is that you introduce modularity and hierarchy...Deep learning is what you get when you add modularity and hierarchy to continuous optimization...if you hard code abstract module reuse in continuous optimization, then you get deep learning architecture patterns. For instance, convolution is a hard coded module which abstracts away spatial position. RNNs [are]... abstract with respect to the time axis..."*

*"In general, there are two tools at your disposal to make program synthesis efficient. There's abstract function reuse [i.e. program-centric abstraction]... and making smarter branching decisions... and you can actually use deep learning there."*

He continues by elaborating on the use of program-centric abstraction here:

*"The general idea is that you start with a given DSL and you run program search to solve various problems, like ARC tasks, for instance, so you generate solution programs, and you start identifying subgraph isomorphisms, both within the program and across programs, and you abstract away these subprograms into reusable functions, and you add these functions back to the DSL, and you keep searching."*

Of course this teaser paragraph above is really just the abstract for a research program, not a complete idea. Chollet provides no references and I'm not aware of any research that has made concrete steps in this direction.

> In an earlier part of the talk Chollet provides this description of program-centric abstraction:

> *"Program-centric abstraction, on the other hand, is about comparing discrete programs, which is to say graphs, and rather than computing distances you are looking for subgraph isomorphisms. And that's similar to human reasoning, planning, it's also what software engineers do..."*

> *"Program-analogy is topologically grounded. If you compare the structure of two graphs, and you create abstractions by merging instances that are isomorphic into an abstract program"*

> According to Chollet, *"...all intelligence arises from a combination of [value-centric and program-centric] abstraction."* This is not as profound a claim as it at first seems if one allows that we can divide the world into continuous domains and discrete domains, and that both domains require a distinct form of abstraction.

Returning back to the discussion on program synthesis, Chollet notes:

*"There's also a complementary and even more powerful way to improve program synthesis, and that is to merge program synthesis with deep learning, to leverage deep learning as a way to reduce the program search space and to fight combinatorial explosion."*

This is much more familiar to me as it is precisely the use of deep learning in systems like AlphaZero. It is also present in virtually all of the work on automated theorem proving with machine learning. See for instance [GPT-F](https://arxiv.org/abs/2009.03393) which utilizes a GPT-like language model to make proof search tractable.

## V. The road ahead: bridging both worlds

*"...there are two exciting research areas to combine the strengths of deep learning with the strengths of program synthesis. The first one is: discrete programs that incorporate deep learning components. And the second one is: deep learning models that inform discrete search and that improve its efficiency instead of using hard-coded heuristics. So this kinda assumes that the space of possible heuristics is an interpolative manifold on which you can do gradient descent."*

*"...[program synthesis can leverage] deep learning in two ways. You can use it as a kind of perception layer to parse a situation into discrete building blocks that you can feed to a program synthesis engine... [i.e.] you can incorporate deep learning as a building block of your DSL. And the second way is that you can use deep learning as a driver, as a guide, for program synthesis..."*

If you've been reading everything up to this point, those last 2 paragraphs aren't too surprising, but the vision it implies certainly surprised me:

*"In the future, I believe we're gonna move towards hybrid systems that will combine deep learning and program search. It will be mostly program search, but it would be deep learning driven."*

*"So this leads us to a long term vision for the future of AI and deep learning that closely resembles the workflow of software engineers today... If you want to know what the future of AI will look like, just look at software engineers today... AI will evolve along the lines of creating new programs from an existing global library of abstract primitives that is going to be shared across many different problems. So you'd have a stream of tasks [e.g. ARC tasks] and for each task you will have a program synthesis engine that is capable of assembling a task-specific solution...That will involve deep learning perception modules, so for instance, parsing objects from the input grid of an ARC task, but also algorithmic modules. And this task-specific solution program will be assembled by this program synthesis engine... This program synthesis engine will not just produce a solution program to your current task, it will also generate reusable building blocks as a by-product of the search... Some of these building blocks will be deep learning modules generated via value-centric abstraction (trained offline on lots of data), some of them will be algorithmic modules obtained via program-centric abstraction, by noticing graph isomorphisms in different functions inside [solution programs]... All these building blocks will form an ever-growing DSL."*

***"So in the future we're going to be moving towards lifelong-learning hybrid systems that combine deep learning and program search."***
