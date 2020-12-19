
Introduction

In 2004, physicist Eric Baum published the book What is Thought attempting to answer the question of how “the computational events that take place within the spatial boundaries of your brain can be accounted for by computer science”. In doing so he arrived at many insights which I believe are still not fully appreciated by AI researchers today.

In describing his work in the introduction to the book he wrote “As much as seems warrented, the discussion in this book follows what I perceive to be folk wisdom among computer scientists interested in cognition, but the attempt to pull ideas together and see whether a fully coherent picture emerges will lead us in directions that have been under explored.”

The book follows the example of a book published by the famous physicist Erwin Schrodinger in 1944 called What is Life. The book sought to answer the analogous question of how biology can ultimately be accounted for by physics and chemistry. In fact the answers produced by both books are also analogous because they are anchored by evolution:

“The situation we have is in fact parallel to that facing Schrodinger: the mind is complex because it is the outcome of evolution. Evolution has build thought processes that act unlike the standard algorithms understood by computer scientists. To understand the mind we need to understand these thought processes, and the evolutionary process that produced them at a computational level.”

Having read Baum’s book I can no longer discount the importance to an AI researcher of understanding evolution.

***
The Core Theme

“There is an underlying theme to almost everything this book says, which can be expressed in a single summary sentence. Here it is. Semantics is equivalent to capturing and exploiting the compact structure of the world, and thought is all about semantics.”

This sentence has a lot packed into it, so let’s take it apart. Firstly, what is meant by compact structure? This is a reference to Occam’s Razor, the notion that simple (i.e. compact) hypotheses ought to be preferred as explanations. There is in fact a theorem (TODO: find source) that the shortest program that generates a given (training) dataset provides the best possible generalization performance, i.e. performance on unseen data. This deep but simple result is in some sense all we need to understand to see how intelligent minds like ours can exist. We will come back to it many times.

“Semantics” has always seemed to me an odd word. I believe it has its origins in philosophy and in quibbles philosophers have had about how meaning arises. There is a classic question in philosophy of how symbols come to acquire meaning. This question in the end is not as deep as it at first seems and has been beaten into the ground by many people before so we will not belabour it much here. Symbols, words, etc… acquire meaning, in other words associations with other phenomena in the world, simply due to isomorphisms between themselves and the phenomena. Meaning simply cannot be kept out. For more reading on this topic look into Douglas Hofstadter’s Godel, Escher, Bach.

So to say that “semantics is equivalent to capturing and exploiting the compact structure of the world” is to say that if a compact model is structured analogously to the world, then that model has acquired semantics with respect to the world. That is if the model begins interacting with the world, then elements of the model have come to represent corresponding elements of the world. To say that “thought is all about semantics” is simply to say that thought is the execution of this model.

The compactness of the model is key because it is the only thing which guarantees generalization. AI researchers are always remarking on the amazing ability that humans have for generalizing from limited experience. This is possible because humans are built from the compact code of our genome. The human genome expresses all of the information needed to construct a mind and does so with at most 750MB (3 billion base pairs * 2 bits per base pair = 6B bits = 750 MB). In fact, in chapter 2 Baum estimates that the effective information content of the genome may be much less (10 MB in his estimation), but the validity of his argument doesn’t rest on whatever specific number is used. The point is simply that the genome is massively compressed compared to the process which generated it - namely evolution.

In chapter 5, Baum very roughly estimates that evolution ran through on the order of 10^35 creatures in the process that lead to humans. To simulate the outcome of the lifetime of a single creature then requires many, many more orders of magnitude in computation. Clearly the amount of computation utilized by evolution dwarfs the size of the genome. Yet, the genome  represents a meaningful compression of the results of that computation.

Therein lies the explanation for the amazing generalization powers of the human mind. Evolution has produced amazingly compact programs which are capable of generating creatures that can survive and thrive in our world. The compactness of the program is what guarantees generality in a wide variety of circumstances. Of course, this alone does not account for the specific quality of human intelligence as opposed to the myriad forms of animal intelligence. The unique qualities of human intelligence require further explanation which Baum expounds on in later chapters.

***

Evolution and Meta-Learning Stacks

…

***

Interesting Ideas

Ch 1

-The way that mind reasons is different than standard CS algorithms because it manipulates semantic chunks
-> these semantic chunks are themselves grounded in the functionality of a hierarchy of computational models shared in the cognitive architecture of many organisms
-Mind must be modular because that’s the only way it could have hill-climbed in evolutionary fitness

Ch 4

-Compactness of a model => generalization
-> Understanding is a result of a compact isomorphism, and it too implies knowledge which is sufficiently factorized that it can be generalized to solve problems very different from any seen before

Ch 5

-> Hill-climbing is the the only way to create complex adaptive systems from simpler more primitive systems

-Evolution deployed massive computation to create us, very roughly on the order of 10^35 creatures plus the compute needed to run each of them!
-Random search through n-bit programs requires exponential runtime and is still much too slow to have produced genomes
-Hill climbing enables efficient search for “good” solutions to hard problems, e.g. TSP
-Hill climbing works because it drags the whole system along the path to better performance
-Biological evolution is more powerful than the “ordinary” hill climbing we see in ML for example, and this is because evolution leverages lots of meta-learning
-> In fact, we can think of this as a meta-learning stack, meta-meta-meta-….-learning

Other chapters

-Mind is capable of reasoning in meta-problem space: Reasoning about algorithms instead of reasoning about individual problems (e.g. in blocks world)
