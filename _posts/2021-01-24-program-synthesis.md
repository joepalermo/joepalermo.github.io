---
layout: post
title: Reflections on Program Synthesis and Deep Learning
---

## Program Synthesis

I've come to view program synthesis as a powerful framework for advancing AI. Program synthesis is the endeavour to build systems that construct programs that solve specific problems on demand, just as a human programmer does.

Ultimately the problem of AI is how to build intelligent computational systems. The question of what exactly we mean by intelligence is crucial. Let us suppose that the intelligence of a system is as Chollet claims: *"a measure of skill-acquisition efficiency over a scope of tasks, with respect to priors, experience, and generalization difficulty."*. What exactly are these "skills" that our systems are supposed to acquire? Well they're software programs of course!

Framed this way, it's obvious that if we construe program synthesis broadly, then artificial intelligence and program synthesis are the same problem.

Traditionally people have referred to program synthesis as the more narrowly defined task of constructing programs via search methods to solve highly constrained problems. But over time I suspect our view of this subfield will broaden.

We can view machine learning as a type of program synthesis. In machine learning we define a search space of functions, then we use various optimization methods to find a function in that space that optimizes a cost function expressed in terms of a dataset. That learned function is simply a program that computes outputs given inputs.

## Deep Learning

Deep learning has been so successful because its method of finding programs, namely gradient descent via backpropagation, is amazingly powerful and efficient. However, despite the amazing power of deep learning it's clear that as a field we're missing some things. According to Chollet, the power of deep learning arises from the capability to interpolate between data points, a capability which can only exist in a space where continuous interpolation makes sense. *"the ability to interpolate between samples is the key to understanding generalization in deep learning. It’s the reason why deep learning works… [you can] make sense of points you’ve never seen before by relating them to other points that lie close to them on the manifold.”"* That also points at another limitation of deep learning which is that to train a model that can relate never-before-seen points to points that lie close to them on a manifold, one needs a fairly dense sampling of points along the whole manifold. Otherwise, the system will have gaps in its capability to generalize, reflecting gaps in the data itself. This is why the performance of deep learning models depends heavily on the size, diversity, and stationarity of the datasets they are trained on.

 Furthermore he claims: *"...you cannot apply deep learning to discrete problems like sorting a list, for instance, or finding prime numbers…you cannot solve these problems with continuous optimization because they have a discrete structure, fundamentally… You could always try embedding that discrete structure in a continuous manifold, but you couldn’t use that manifold for interpolation. So your continuous parametric model could not generalize to things it has not seen before. So in order to learn a useful embedding you would need an exhaustive sampling of the problem space."*.

---

I share the general thrust of his intuition here, but I want to address some of my own confusion around these concepts.

Let's take apart this claim that *"the ability to interpolate between samples is the key to understanding generalization in deep learning. It’s the reason why deep learning works…"*

Deep learning models are not explicitly optimized to interpolate between samples, and not all deep learning models provide a natural way of interpolating between samples.

It's a well known fact that deep learning models can facilitate interpolation between samples in various domains. For example, take generative models of images. With GANs it is possible to [interpolate between images](https://www.youtube.com/watch?v=djsEKYuiRFE&ab_channel=NolanStrait). How does this work? Suppose that a GAN has been trained on the images. Further suppose that the generator model has an encoder-decoder architecture, such that one can produce embeddings of images using the encoder and reproduce the original images using the decoder. To produce an interpolation between any 2 images, embed each of them into a latent space using the encoder model. The embeddings for those 2 images are points on a manifold. One can linearly interpolate between these two encoded points, thereby generating a sequence of encoded points. By decoding all these points one can thus generate an interpolation between the two images in the original space.

Notice that if all the points of a given class cluster in the same part of the embedding space, and the same is true of some other class, then one can easily create a binary classifier in the embedding space via a linear method such as logistic regression. So the ability to train classifiers depends on the ability to cluster data points of the same class, such that they remain *close* to other points of the same class in the embedding space.

Recall that Chollet says: *"the ability to interpolate between samples... [is] the reason why deep learning works"*. I think it's possible to be more precise than this. For instance, I think it's equally accurate to say that the ability to cluster samples of the same class close together in an embedding space is the reason deep learning works. There is a deeper principle at work here than the ability to interpolate.

When is it possible to use a deep learning to effectively cluster samples? Perhaps it is only possible when it is *also possible* to interpolate between samples? Both of these are related by their reliance on the data having a certain kind of geometry. In fact, Chollet argues that deep learning is all about geometry: *"...it’s intuitive you would be able to produce abstractions that are grounded in geometry using deep learning. In supervised deep learning, what you’re doing is [creating] an analogy between two spaces…you are learning a smooth geometric morphing between the two spaces, point by point. So it’s a geometric analogy between two spaces, and that’s really what a deep learning model encodes, it’s this space to space analogy.”"*

In some problems it will be fairly easy to construct such a geometric analogy. In others it will be harder. In fact, I think there is at least in principle a continuum here between problem-spaces where geometric analogy is easy and others where it is hard.
