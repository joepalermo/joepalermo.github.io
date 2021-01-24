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

Deep learning has been so successful because its method of finding programs, namely gradient descent via backpropagation, is amazingly powerful and efficient. However, despite the amazing power of deep learning it's clear that as a field we're missing some things. According to Chollet, the power of deep learning arises from the capability to interpolate between data points, a capability which can only exist in a space where continuous interpolation makes sense. *"the ability to interpolate between samples is the key to understanding generalization in deep learning. It’s the reason why deep learning works… [you can] make sense of points you’ve never seen before by relating them to other points that lie close to them on the manifold.”"* That also points at another limitation of deep learning which is that to train a model that can relate never-before-seen points to points that lie close to them on a manifold, one needs a fairly dense sampling of points along the whole manifold. Otherwise, the system will have gaps in its capability to generalize, reflecting gaps in the data itself. This is why the performance of deep learning models depends heavily on the size and diversity of the datasets they are trained on.

 Furthermore he claims: *"...you cannot apply deep learning to discrete problems like sorting a list, for instance, or finding prime numbers…you cannot solve these problems with continuous optimization because they have a discrete structure, fundamentally… You could always try embedding that discrete structure in a continuous manifold, but you couldn’t use that manifold for interpolation. So your continuous parametric model could not generalize to things it has not seen before. So in order to learn a useful embedding you would need an exhaustive sampling of the problem space."*.

I share his intuition, but I can see a few objections people might have.

Is it really the case that all deep learning models rely on the ability to interpolate between samples?

Firstly, we can already make somewhat useful programming tools with deep learning. For example, one can train a language model on a mixture of code and natural language and sample from that model as an auto-completion tool. There were some impressive GPT-3 demos that [demonstrated this](https://www.technologyreview.com/2020/07/20/1005454/openai-machine-learning-language-generator-gpt-3-nlp/). However, the resulting systems are obviously highly limited.

If Chollet's thesis is correct, then the ability of model's like GPT-3 rests on the ability to interpolate
