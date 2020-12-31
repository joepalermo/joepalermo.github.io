---
layout: post
title: Book Review - What is Thought?
---

## Introduction

In 2004, physicist Eric Baum published the book *What is Thought?* attempting to answer the question of how *“the computational events that take place within the spatial boundaries of your brain can be accounted for by computer science”*. In doing so he arrived at many insights which I believe are still not fully appreciated by AI researchers today.

In describing his work in the introduction to the book he wrote: *“As much as seems warrented, the discussion in this book follows what I perceive to be folk wisdom among computer scientists interested in cognition, but the attempt to pull ideas together and see whether a fully coherent picture emerges will lead us in directions that have been under explored.”* pg. 2

The book follows the example of a similar book published by the famous physicist Erwin Schrödinger in 1944 called *What is Life?*. *What is Life?* sought to answer the analogous question of how biology can ultimately be accounted for by physics and chemistry. In fact the answers provided in the books are also analogous because they are anchored by evolution:

*“The situation we have is in fact parallel to that facing Schrodinger: the mind is complex because it is the outcome of evolution. Evolution has built thought processes that act unlike the standard algorithms understood by computer scientists. To understand the mind we need to understand these thought processes, and the evolutionary process that produced them at a computational level.”* pg. 2

Having read Baum’s book I’ve been awakened to the notion that understanding evolution in detail can potentially be helpful to the AI researcher. Knowing what was required for evolution to discover how to build intelligent systems can potentially give us clues about the path ahead in AI. However this is not just a book about evolution, and Baum digs into results from a wide array of disciplines to shed light on the problem.

In this review I will touch upon some of the key ideas and takeaways that most excite me.

## The Core Theme

*“There is an underlying theme to almost everything this book says, which can be expressed in a single summary sentence. Here it is. Semantics is equivalent to capturing and exploiting the compact structure of the world, and thought is all about semantics.”* pg. 3

This sentence has a lot packed into it, so let’s take it apart. Firstly, what is meant by compact structure? This is a reference to Occam’s Razor, the notion that simple (i.e. compact) hypotheses ought to be preferred as explanations. The minimum description length principle, is a way of formalizing this intuition. Apparently there is a theorem (Ilya Sutskever once mentioned it in a [talk](https://www.youtube.com/watch?v=9EN_HoEk3KY&ab_channel=LexFridman) - please let me know if you happen to know the source) that the shortest program that generates a given (training) dataset provides the best possible generalization performance, i.e. performance on unseen data.

“Semantics” has always seemed to me an odd word. I believe it has its origins in philosophy and in quibbles philosophers have had about how meaning arises. There is a classic question in philosophy of how symbols come to acquire meaning. This question in the end is not as deep as it at first seems and has been beaten into the ground by many people before so we will not belabour it much here. Symbols, words, etc… acquire meaning, in other words associations with other phenomena in the world, simply due to isomorphisms between themselves and the phenomena. Meaning simply cannot be kept out. For more reading on this topic look into Douglas Hofstadter’s *Godel, Escher, Bach*.

So to say that *“semantics is equivalent to capturing and exploiting the compact structure of the world”* is to say that if a compact model is structured analogously to the world, then that model has acquired semantics with respect to the world. That is if the model begins interacting with the world, then elements of the model will come to represent corresponding elements of the world. To say that “thought is all about semantics” is simply to say that thought is the execution of such a model.

The compactness of the model is key because it is the only thing which guarantees generalization. AI researchers are always remarking on the amazing ability that humans have for generalizing from limited experience. This is possible because humans are built from the compact code of our genome. The human genome expresses all of the information needed to construct a mind and does so with at most 750MB (3 billion base pairs * 2 bits per base pair = 6B bits = 750 MB). In fact, in chapter 2 Baum estimates that the effective information content of the genome may be much less (10 MB in his estimation), but the validity of his argument doesn’t rest on whatever specific number is used. The point is simply that the genome is massively compressed compared to the process which generated it - namely evolution.

In chapter 5, Baum very roughly estimates that evolution ran through on the order of 10^35 creatures in the process that lead to humans. Of course, to simulate the outcome of the lifetime of a single creature requires many, many more orders of magnitude in computation. Clearly the amount of computation utilized by evolution dwarfs the size of the genome. Yet, the genome represents a meaningful compression of the results of that computation.

Therein lies the explanation for the amazing generalization powers of the human mind. Evolution has produced amazingly compact programs which are capable of generating creatures that can survive and thrive in our world. The compactness of the program compared to the amount of computation that was spent to produce it is what confers generality. Of course, this alone does not account for the specific quality of human intelligence as opposed to the myriad forms of animal intelligence. The unique qualities of human intelligence require further explanation which Baum expounds on in later chapters.

## Evolution

Baum starts chapter 5 by discussing the problem evolution solved in abstract terms.

*“Suppose we have some data D, a long series of 0s and 1s. We want a compact representation of it. The first step is to pick some class of hypothesis functions to explore for such a representation. Let’s begin with a Turing machine representation and look for an input for a particular universal Turing machine M such as the laptop on which I’m typing this. The input I will be some string of 1s and 0s. When we feed I into machine M as M’s input, M will compute…and hopefully print out D… now the question is, How do we find such an input I? Moreover, how do we find the smallest such input I that could be regarded as the most compact representation of the data?*

*The most straightforward approach is to try all possible input strings in order of their length…*

*This approach is straightforward but problematic. The most serious problem is that it takes too long. To have found a program that is n bits long, we will have to had to search through all programs that are n-1 bits long [of which there are 2^(n-1)]… If n is only 100, we would have to search…10^33 different programs…*

*Evolution had access to massive computation. We can very roughly estimate that evolution ran through 10^35 different creatures in the exploration that led to human beings.*

*This vast number of trials might allow an exponential search on strings of size 100 but not much longer. It would not suffice to find our DNA or almost any of our thoughts…*

*Suppose we had an algorithm that returns the best n bit program after looking at only n^4 possibilities. In chapter 2, I estimated that the program in human DNA is about 80 million bits long. Finding the best 80 million bit program using the hypothetical algorithm would require looking at about 10^32 possibilities. Evolution may have looked at this many, so this would have a chance of working.”* pg. 107-108

Of course this analogy between the search for programs that generate a particular dataset and evolution breaks down in various ways.

Firstly it is not clear if one can define in evolution the notion of a most fit organism. Which organism is more fit, humans or ants? Note that ants apparently have a worldwide population of roughly 10^16 individuals!

Secondly, the problem evolution faces is to find genes which generate organisms which in turn reproduce their genes. These genes are essentially programs which generate biochemical machines that collectively manifest evolutionarily fit behaviours. It’s not clear to me that this is analogous to a program for a universal Turing machine that simply reproduces a fixed dataset.

However, as an intuition pump I find this thought experiment very intriguing. It’s certainly the first attempt I’ve seen to estimate the computational complexity of evolution.

What sort of an algorithm for this problem could have such low computational complexity, e.g.  O(n^4)? Well if we relax the constraint that we must find the absolute best short program then it’s reasonable to suppose one could do it with some kind of hill-climbing procedure. Of course, in very rough terms this is clearly how evolution works.

## Hill Climbing

Hill climbing is the only way that simple systems can become complex systems without anything getting injected from the outside. As humans we can design complex systems from scratch, but that’s only because we are the result of a very long process of hill climbing which began from extremely simple systems.

Clearly hill climbing is more efficient than random search because it makes use of the heuristic than a good solution can be made into a better solution through incremental steps starting from the good solution. If you jump too far away from the good solution in one jump then you don’t have any guarantees about what you’ll find there and you’re back to random search.

Baum explains very nicely another reason why hill climbing is so effective:  *“[Hill climbing] essentially does credit assignment on each change of candidate solutions. That is, when the algorithm makes a change in one or a few components of a big complicated solution, say a program or a neural net, it evaluates whether the change is good in the context of the rest of its current choices of all the other parameter values in the system…In this way it assigns credit to that particular choice of component, in the context of the whole solution.”* pg. 120

## Meta-Learning Stacks

*“Biological evolution seems to have done some things that may be more powerful than ordinary hill climbing. It seems to have learned better how to learn as it went along.*

*For example, evolution discovered regulatory circuits involving Hox genes and other toolkit genes that seem to have semantic meaning, for example, the ey gene, which essentially codes “build an eye here.”…*

*Having discovered such semantic units… evolution then continued to explore how to swap these units around in meaningful ways. So, most of the evolution of different body plans since at least the origin of bilaterally symmetric animals appears to have been learning how to regulate the existing meaningful genes…*

*We can imagine that this kind of search can be extremely powerful. Instead of trying various meaningless base changes, almost all of which do nothing useful, evolution effectively searched over combinations of meaningful macros. Add long legs… Try a shell… Take the brain and scale it up…*

*There is another way evolution may have evolved to evolve better. Evolution may have discovered earlier, and at a lower level, that if introns were added into genes at appropriate locations, crossover would swap around building blocks, leading to semantically sensible searches and thus speeding up evolution.”* pg. 120-121

Baum notes that this last point is (or was) somewhat controversial at the time of his writing. But he provides a very clear argument that there is pressure for evolution to generate mechanisms of this sort:

*“…evolution does select for ability to learn to adapt better to future circumstances…The ancient genes that would have survived to the present are those in creatures able to evolve new solutions to outcompete other creatures and to survive the massive environmental insults that we believe occurred on many occasions in the history of life on earth. At any given time, evolution has selected for genomes that have solve numerous learning problems in their past, and it is a tenet of machine learning and a basis of the arguments in this book that if a compact solution solves a large class of learning problems, it can be expected to be good at solving learning problems in that class which it has not yet encountered. Thus, I expect evolution evolves mechanisms that are good for evolving solutions.”* pg. 122

Another mechanism he discusses in this vein is the existence of sex:

*“…sex speeds up evolution’s information acquisition (learning) and allows the survival of much higher mutation rates.”* pg. 122

What do all of these mechanisms have in common? They are forms of meta-learning within the evolutionary process. That is, they are mechanisms which accelerate the discovery of fit genomes. Furthermore, they are mechanisms that are themselves evolved.

Baum does not use the term ‘meta-learning stacks’, but I find it evocative in thinking about the process which produced us. Many forms of meta-learning had to be discovered from scratch and stacked on top of each other to produce human civilization in such a short time. There are several forms of meta-learning stacked on top of each other within the process of biological evolution but also likely within the learning algorithms of the human brain and within human culture (e.g. language).

Baum reflects on how the learning procedure of evolution differs from machine learning:

*“If only backpropagation is done on a network, there is inherently no way to discover sex or language. There is no way to even express changes in the learning procedure in the representation being used. But evolution, by contrast, is manipulating such a powerful representation that it has the capability of learning higher-level structure to improve its learning…*

*…evolution is benefiting from throwing truly massive computational resources at the problem. Evolution worked for billions of years before discovering structures such as Hox genes and the networks that render them meaningful.”* pg. 123

Reflecting on this has changed my view on how AGI is likely to be created. Discovery of the sort of compact structure required to build general intelligence is likely going to require massive computational search mediated by meta-learning at several levels in the process. This is reminiscent of Richard Sutton’s essay [“The Bitter Lesson”](http://www.incompleteideas.net/IncIdeas/BitterLesson.html).

## Language Learning

One implication of the evolutionary origins of intelligence is that most of the learning required to produce a human mind took place over evolutionary time, and does not occur during the life of an individual. This evolutionary learning has provided us with powerful inductive biases for learning certain things very rapidly. Perhaps the best example is language acquisition.

*"...most of what people do when they learn language is simply learn labels for complex computational modules. Constructing the computational modules themselves is much harder. But the human mind essentially starts with the computational modules, that is, detailed bias to learn them is encoded in the genes, so it need only learn the labels and the grammar that relates them."* pg. 340

I find this provides a helpful context in which to put current discussions in AI.

This year language models have been the hot topic in machine learning. It has been popular both to marvel at the amazing results they produce and also to comment on how easy it is to expose their failings. It's amazing that these models can so successfully learn the statistics of language that they can generate compelling text, and it shouldn't be surprising or even particularly notable that their failure modes are easy to find. To achieve human-level language abilities will require much more work in language grounding. That is, language has to be learned in relationship to a world that the agent interacts with. Further, the agent's other cognitive abilities need to be fully integrated with its language abilities. Easier said than done of course.

The computational modules that Baum refers to are the basis for such grounding in humans. Baum is arguing that our capability for language understanding was literally built on top of a hierarchy of pre-linguistic computational modules that facilitate reasoning. These remind me of the so-called *human innate knowledge priors* discussed by Francois Chollet in his fascinating paper *The Measure of Intelligence*. This discussion was based on the theory of [*Core Knowledge*](https://www.harvardlds.org/wp-content/uploads/2017/01/SpelkeKinzler07-1.pdf) developed by Elizabeth Spelke among others.

Chollet writes:

*"Core Knowledge identifies four broad categories of innate assumptions that form the foundations of human cognition, and which are largely shared by our non-human relatives..."*

- *"Objectness and elementary physics: humans assume that their environment should be parsed into “objects” characterized by principles of cohesion (objects move as continuous, connected, bounded wholes), persistence (objects do not suddenly cease to exist and do not suddenly materialize), and contact (objects do not act at a distance and cannot interpenetrate)."*
- *"Agentness and goal-directedness: humans assume that, while some objects in their environment are inanimate, some other objects are “agents”, possessing intentions of their own, acting so as to achieve goals (e.g. if we witness an object A following another moving object B, we may infer that A is pursuing B and that B is fleeing A), and showing efficiency in their goal-directed actions. We expect that these agents may act contingently and reciprocally."*
- *"Natural numbers and elementary arithmetic: humans possess innate, abstract number representations for small numbers, which can be applied to entities observed through any sensory modality. These number representations may be added or subtracted, and may be compared to each other, or sorted."*
- *"Elementary geometry and topology: this core knowledge system captures notions of distance, orientation, in/out relationships for objects in our environment and for ourselves. It underlies humans’ innate facility for orienting themselves with respect to their surroundings and navigating 2D and 3D environments."* -The Measure of Intelligence, pg. 26

Perhaps it is possible to learn these things simultaneously with language, but it is surely not possible to learn language without these. Learning language without learning other things about the world puts very hard limits on what language abilities can be acquired.

Later on, Baum continues articulating what is special about language:

*"To whatever extent people do have a general learning ability, there is no particular evidence that it is turned on only for a few years during childhood. To the contrary, you can take up a new sport at say 40, say, learn to ride a bicycle if you never have before. You can decide on a new career and go to medical school at 40, and if you are persistent, gain vast new knowledge. But you cannot learn a new language the way you would as a child, effortlessly and with perfect pronounciation. If groups of adults are brought together, they do no simply learn each others' languages, nor can they form a new language. But groups of children will construct a whole new language from the pigdin their parents speak. This is a special-purpose, programmed-in ability, not simple application of a general learning algorithm."* pg. 342
