---
layout: post
title: On the State of Artificial Intelligence
---

## What AI can do today

Today AI is practically synonomous with deep learning. All of the landmark AI accomplishments of the last 10 years were accomplished with deep learning. Here is a sample of the landmark achievements of deep learning:

- AlexNet
- Practical self-driving cars (e.g. Tesla Autopilot, Waymo, etc...)
- AlphaGo
- AlphaFold
- GPT-3
- DALL-E

Before deep learning a list of notable AI accomplishments might look something like this:

- DeepBlue
- Watson (the Jeopardy playing system)

It's a short list because most of what came before deep learning was closer to the core of computer science. It was about algorithms for efficiently searching data structures, logic-based representations of knowledge, etc... It involved coming up with lots of tricks and heuristics, and its methods were less powerful and general. A history of the early days in AI reveals many systems like SHRDLU (1972). SHRDLU was a reasoning engine in a virtual "blocks world" environment. It was implemented in Lisp and had separate hardcoded modules for parsing language and logical inference [1]. Given a representation of a "blocks world" it could respond to things such as: "Find a block which is taller than the one you are holding and put it in the box". It was very impressive at the time, but it wasn't generally understood until later that such systems scaled very poorly to larger problem instances.

In their textbook, Norvig and Russell list the following accomplishments as state-of-the-art (2010):

- Robotic vehicles
- Speech recognition
- Autonomous planning and scheduling
- Game playing
- Spam fighting
- Logistics planning
- Robotics
- Machine translation

Nearly all of these are dominated by deep learning today! Even in the domain of planning and scheduling (which is not a focus area of deep learning research), such problems can potentially be converted into reinforcement learning environments and solved with deep reinforcement learning.

Deep learning has brought about a unification of many previously disparate disciplines of AI: computer vision, natural language processing, audio processing, and reinforcement learning are now all unified by the use of backpropagation as the core learning algorithm.

Now let's dig a bit deeper into this capability deep learning has unlocked.

## Deconstructing deep learning

Current systems are very good at **extracting functions underlying robust correlations, particularly in domains with large amounts of continuous data**. Thanks to the deep learning revolution, this is the case even if the patterns underlying the correlations are complex and hierarchical. By hierarchical I mean that the patterns exist at several levels in a hierarchy. For example, protein structure is influenced by multiple levels in a hierarchy (individual amino acids have interactions that influence structure but so do larger groups and sub-structures). Before deep learning it was generally the case that only non-hierarchical patterns could be easily learned.

Let's deconstruct this:

- **functions**: We're always learning a mapping from one space to another space (although sometimes the function maps back to the same space, as in an autoencoder)
- **robust**: The correlations need to be consistent over time. If they are rapidly changing then there is no durable function to learn, for example take the correlations between stock prices.
- **correlations**: To learn a function you need inputs and outputs. These have to be correlated with each other, otherwise there is nothing to learn.
- **large amounts [of data]**: Distributed representations and hierarchical structure provide impressive generalization power, but these models still require a fairly dense sampling of the input space.
- **continuous data**: In order for deep learning to work, you have to be able to interpolate between samples.

For more on this conception of the nature of deep learning please see [Francois Chollet's 2020 Neurips talk](https://slideslive.com/38935790/abstraction-reasoning-in-ai-systems-modern-perspectives) or [my writeup on it](https://joepalermo.github.io/2021/01/10/talk-review-francois-chollet-neurips-2020.html).

## Some things AI can't yet do

### Truly interact with us via natural language

We can't yet have truly meaningful conversations with AIs because they don't have sufficiently powerful world models. When we converse with each other we're leveraging our common sense understanding of the world and our capability to simulate it. GPT-3 is famously bad at this [2]:

Q: How many eyes does a giraffe have?
A: A giraffe has two eyes.

Q: How many eyes does my foot have?
A: Your foot has two eyes.

Q: How many eyes does a spider have?
A: A spider has eight eyes.

Q: How many eyes does the sun have?
A: The sun has one eye.

GPT-3 is unable to distinguish the questions that make sense from those that don't - in fact, I think it's fair to say that it's not really trying to. Language models are great for creating surrealist generative fiction (try out AI Dungeon if you're curious - it's pretty amazing). But it's not really fair to ask them these sorts of questions. For one thing, they're way outside the training distribution. The training dataset to create GPT-3 was constructed by pulling lots of text from the internet - text which mostly consists of humans communicating with each other, not testing each other's common sense with weird questions. However, there is a deeper reason why language modelling alone is probably incapable of solving common sense.

I think sense-making requires simulation of some sort. If you were to pose the question "How many eyes does my foot have?", an image of a foot may flit subliminally in your mind. You know what an eye is and what a foot is because they are both a part of the world you inhabit. In order to answer the question, your mind might be executing an algorithm such as the following:

1 - Generate a visuo-spatial representation of a foot

2 - Look for eyes in that representation and then count them

I'm not literally saying this is the algorithm, but I have a hunch that this is the right direction. I'm also not saying this is how you answer every question. For example when answering "How many eyes does a spider have?", I'm pretty sure the answer is arrived at in most people by rote memory lookup rather than generating a mental image of a spider and counting its eyes.

### Reasoning from limited data

AI is already better than us at reasoning in sufficiently constrained, simulatable domains. For example, we've seen this in game-playing systems such as AlphaGo (subsequently superseded by AlphaZero and MuZero). However, these systems are much less efficient at learning to play than humans are. A human can reach expert level in perhaps thousands or tens of thousands of games. Reinforcement learning systems require millions of games.

The best definition of intelligence I've ever encountered is Francois Chollet's:

*"The intelligence of a system is a measure of skill-acquisition efficiency over a scope of tasks, with respect to priors, experience, and generalization difficulty."*

I wrote about this at length in my aforementioned writeup of Chollet's 2020 Neurips talk, but the original resource on this definition is his excellent paper [*"On the Measure of Intelligence"*](https://arxiv.org/abs/1911.01547).

By this definition, surpassing humans at any specific highly constrained task cannot demonstrate intelligence. This is because it is always possible to achieve better performance by hardcoding better priors or acquiring more experience at the task (which machines are very efficient at acquiring).

In Chollet's paper he introduced a reasoning task that he believes gets at the core of the problem - The Abstract Reasoning Corpus (ARC). ARC tasks are visual puzzles that require generalizing from very few examples. The small size of the dataset is an important feature of the dataset because it means that one cannot hope to simply fit the dataset with a high capacity model and get good generalization results. With ARC, Chollet is trying to stimulate research in the development of new stronger priors that can enable generalization from smaller amounts of data.

Another task I think could be interesting for this purpose is the general problem of theorem proving. There is a very limited body of existing formalized mathematics for neural theorem provers to learn from. Of course, mathematics is inherently computational and so in principle can be explored without limit by machines. However, the question of how to do open-ended exploration and learning in the mathematical domain is a very hard open problem, as the size of the state and action spaces is practically infinite.

### Generalization in reinforcement learning


### OOD Generalization

## References

[1] - Terry Winograd's PhD dissertation: http://hci.stanford.edu/~winograd/shrdlu/AITR-235.pdf

[2] - https://lacker.io/ai/2020/07/06/giving-gpt-3-a-turing-test.html
