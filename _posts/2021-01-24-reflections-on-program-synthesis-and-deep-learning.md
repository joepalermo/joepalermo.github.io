---
layout: post
title: Reflections on Program Synthesis and Deep Learning
---

## Program Synthesis

I've come to view program synthesis as a powerful framework for advancing AI. Program synthesis is the endeavour to build systems that construct programs that solve specific problems on demand, just as a human programmer does.

The problem of AI is how to build intelligent computational systems, which of course raises the question of what exactly we mean by intelligence. Let us suppose that the intelligence of a system is as Francois Chollet [claims](https://joepalermo.github.io/2021/01/10/talk-review-francois-chollet-neurips-2020.html): *"a measure of skill-acquisition efficiency over a scope of tasks, with respect to priors, experience, and generalization difficulty."* What exactly are these "skills" that our systems are supposed to acquire? Well they're software programs of course!

Framed this way, it's obvious that if we construe program synthesis broadly, then artificial intelligence and program synthesis are the same problem.

Traditionally people have referred to program synthesis as the more narrowly defined task of constructing programs via search methods to solve highly constrained problems. But over time I suspect our view of this subfield will broaden.

We can view machine learning as a type of program synthesis. In machine learning we define a search space of functions, then we use various optimization methods to find a function in that space that optimizes a cost function expressed in terms of a dataset. That learned function is simply a program that computes outputs given inputs.

## When and Why does Deep Learning Work?

Deep learning has been so successful because its method of finding programs, namely gradient descent via backpropagation, is amazingly powerful and efficient. However, despite the amazing power of deep learning it's clear that as a field we're missing some things. According to Chollet, the power of deep learning arises from the capability to interpolate between data points, a capability which can only exist in a space where continuous interpolation makes sense. *"the ability to interpolate between samples is the key to understanding generalization in deep learning. It’s the reason why deep learning works… [you can] make sense of points you’ve never seen before by relating them to other points that lie close to them on the manifold."* That also points at another limitation of deep learning which is that to train a model that can relate never-before-seen points to points that lie close to them on a manifold, one needs a fairly dense sampling of points along the whole manifold. Otherwise, the system will have gaps in its capability to generalize, reflecting gaps in the data itself. This is why the performance of deep learning models depends heavily on the size, diversity, and stationarity of the datasets they're trained on.

 Chollet also claims: *"...you cannot apply deep learning to discrete problems like sorting a list, for instance, or finding prime numbers…you cannot solve these problems with continuous optimization because they have a discrete structure, fundamentally… You could always try embedding that discrete structure in a continuous manifold, but you couldn’t use that manifold for interpolation. So your continuous parametric model could not generalize to things it has not seen before. So in order to learn a useful embedding you would need an exhaustive sampling of the problem space."*.

I share the general thrust of his intuition here, but I want to address some of my own confusion around these concepts.

Let's take apart this claim that *"the ability to interpolate between samples is the key to understanding generalization in deep learning. It’s the reason why deep learning works…"*

Deep learning models are not explicitly optimized to interpolate between samples, and not all deep learning models provide a natural way of interpolating between samples.

It's a well known fact that deep learning models can facilitate interpolation between samples in various domains. For example, take generative models of images. With generative models it is possible to [interpolate between images](https://www.youtube.com/watch?v=djsEKYuiRFE&ab_channel=NolanStrait). How does this work? Suppose that an autoencoder has been trained on a set of images. One can produce embeddings of images using the encoder and reproduce the original images from the embeddings using the decoder. To produce an interpolation between any 2 images, embed each of them into the latent space using the encoder model. One can then linearly interpolate between these two encoded points, thereby generating a sequence of encoded points. By decoding all these points one can thus generate an interpolation between the two images in the original space.

How does this relate to a more canonical deep learning task, for instance a classification task such as object recognition? Notice that if all the points of a given class cluster in the same part of the embedding space, and all the points of some other class cluster in a different part of the embedding space, then one can easily train a binary classifier in the embedding space via a linear method such as logistic regression. So the ability to train classifiers depends on the ability to cluster data points of the same class, such that they remain *close* to other points of the same class, and *far* from points in different classes, in the embedding space.

Recall that Chollet says: *"the ability to interpolate between samples... [is] the reason why deep learning works"*. I think it's possible to be more precise than this. For instance, I think it's equally accurate to say that the ability to cluster samples of the same class close together in an embedding space is the reason deep learning works. In other words, there must be a deeper principle at work here than the ability to interpolate.

When is it possible to use a deep learning to effectively cluster samples? Perhaps it is only possible when it is *also possible* to interpolate between samples? Both of these are related by their reliance on the data having a certain kind of geometry. In fact, Chollet argues that deep learning is all about geometry: *"...it’s intuitive you would be able to produce abstractions that are grounded in geometry using deep learning. In supervised deep learning, what you’re doing is [creating] an analogy between two spaces…you are learning a smooth geometric morphing between the two spaces, point by point. So it’s a geometric analogy between two spaces, and that’s really what a deep learning model encodes, it’s this space to space analogy.”"*

In some problems it will be fairly easy to construct such a geometric analogy. In others it will be harder. In fact, I think there is at least in principle a continuum here between problem-spaces where geometric analogy is easy and others where it is hard.

### Successes of Deep Learning

The areas that deep learning has been particularly successful in tend to have clear geometric interpretations. Consider this list:

- Sensory perception: Object recognition/segmentation, speech recognition, etc...
- Sensory synthesis: Generative models of images and video, speech synthesis, etc...
- Game play: MuZero
- Protein folding: AlphaFold

In visual perception and synthesis a geometric interpretation is quite intuitive. After all visual perception and synthesis are explicitly about processing information derived from 2 and 3 dimensional spaces.

Auditory perception and synthesis is also intuitive to see as a geometric domain if you reflect on the structure of a time or frequency domain audio waveform - images of which can be projected into 2 dimensional space.

Considering games such as Go or Chess, a geometric interpretation is very natural in that pieces on a board have a simple and well-defined geometric relationship to each other. The same is generally true of video games.

Protein folding is perhaps the clearest example of all. Proteins fold into 3-dimensional shapes from a sequence amino acids. In retrospect it seems obvious that this would be a natural application of deep learning.

One could add some of the recent accomplishments with large pre-trained language models to this list, however, as impressive as these systems are, they still seem very far from solving the domain of NLP. Many people have noted that in order to build systems that are capable of powerful generalization in the domain of natural language one needs to train models on more than just text. In other words, language grounding will be required to solve NLP. How to do this is an open problem.

DALL-E was a recent and amazing step in this direction. I was as many people have been [shocked](https://twitter.com/karpathy/status/1346558827643080705) at how effective it is at [generalizing](https://twitter.com/sama/status/1346543962652246017).

In any case, though models like BERT and GPT-3 are interesting and powerful if used only in ways that don't expose their many limitations. A purely geometric approach to language seems to be lacking something.

### A Notable Gap

One of my favourite examples of a problem where geometric approaches (i.e. deep learning) don't work very well is the [DeepMind Mathematics Dataset](https://github.com/deepmind/mathematics_dataset).

DeepMind and OpenAI have [both](https://arxiv.org/abs/1904.01557) [trained](https://arxiv.org/abs/2010.14701) fairly large transformer models on it, treating it as a sequence-to-sequence problem where the input is the question statement and the output is the answer. It's a testament to the power of deep learning that this works at all. If you restrict concern to the arithmetic problems it's like trying to implement a pocket calculator within the weights of a neural network. Yes, amazing that it kinda works, but I'm quite confident that the first systems that satisfactory solve this dataset won't look like that.

I believe that the right way to solve this problem is via program synthesis.

Notably that's also how humans do it. When you look at problems like these you'll first figure out what the problem is asking for, then you'll compose a sequence of symbolic computations which produce the answer. In other words you'll construct an algorithm to compute the answer. In fact, you might get the algorithm right and yet make mistake in the calculation (since you're not a computer).

For computers, the calculation part is trivial. It's the construction of algorithm for each problem which is the interesting challenge.

Once you define a set of operators that can be composed to construct a program in the form of a compute graph, the problem reduces to a form of search. Here deep learning can become useful again. As Chollet notes: *"...there are two exciting research areas to combine the strengths of deep learning with the strengths of program synthesis. The first one is: discrete programs that incorporate deep learning components. And the second one is: deep learning models that inform discrete search and that improve its efficiency instead of using hard-coded heuristics."*
