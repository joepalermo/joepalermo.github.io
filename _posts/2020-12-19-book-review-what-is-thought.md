In 2004, physicist Eric Baum published the book What is Thought attempting to answer the question of how “the computational events that take place within the spatial boundaries of your brain can be accounted for by computer science”. In doing so he arrived at many insights which I believe are still not fully appreciated by AI researchers today.

In describing his work in the introduction he wrote “As much as seems warrented, the discussion in this book follows what I perceive to be folk wisdom among computer scientists interested in cognition, but the attempt to pull ideas together and see whether a fully coherent picture emerges will lead us in directions that have been under explored.”

***

The book follows the example of a book published by the famous physicist Erwin Schrodinger in 1944 called What is Life. The book sought to answer the analogous question of how biology can ultimately be accounted for by physics and chemistry. In fact the answers produced by both books are also analogous because they are anchored by evolution:

“The situation we have is in fact parallel to that facing Schrodinger: the mind is complex because it is the outcome of evolution. Evolution has build thought processes that act unlike the standard algorithms understood by computer scientists. To understand the mind we need to understand these thought processes, and the evolutionary process that produced them at a computational level.”

Having read Baum’s book I can no longer discount the importance of understanding evolution to the AI researcher.

***

“There is an underlying theme to almost everything this book says, which can be expressed in a single summary sentence. Here it is. Semantics is equivalent to capturing and exploiting the compact structure of the world, and thought is all about semantics.”

This sentence has a lot packed into it, so let’s take it apart. Firstly, what is meant by compact structure? This is a reference to Occam’s Razor, the notion that simple (i.e. compact) hypotheses ought to be preferred as explanations. There is in fact a theorem (TODO: find source) that the shortest program that generates a given (training) dataset provides the best possible generalization performance, i.e. performance on unseen data. This deep but simple result is in some sense all we need to understand to see how intelligent minds like ours can exist. We will come back to it many times.

“Semantics” has always seemed to me an odd word. I believe it has its origins in philosophy and in quibbles philosophers have had about how meaning arises. There is a classic question in philosophy of how symbols come to acquire meaning. This question in the end is not as deep as it at first seems and has been beaten into the ground by many people before so we will not belabour it much here. Symbols, words, etc… acquire meaning, in other words associations with other phenomena in the world, simply due to isomorphisms between themselves and the phenomena. Meaning simply cannot be kept out. For more reading on this topic look into Douglas Hofstadter’s Godel, Escher, Bach.

So to say that “semantics is equivalent to capturing and exploiting the compact structure of the world” is to say that if a compact model is structured analogously to the world, then that model has acquired semantics with respect to the world. That is if the model begins interacting with the world, then elements of the model have come to represent corresponding elements of the world. To say that “thought is all about semantics” is simply to say that thought is the execution of this model.

The compactness of the model is key because it is the only thing which guarantees generalization. AI researchers are always remarking on the amazing ability that humans have for generalizing from limited experience. This is possible because humans are built from the compact code of our genome. The genome expresses all of the information needed to construct a mind and it
