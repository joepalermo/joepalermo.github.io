---
layout: post
title: What Makes a Bayesian?
---

## Supervised Learning and Generalization

Supervised learning is concerned with learning associative maps from data. What makes SL interesting, is that it is particularly concerned with learning associative maps that generalize outside of the training set. But how is such generalization possible?

If I observe f(0) = 1, and f(1) = 2, how confident can I be that f(2) = 3? Of course, in the general case you can't say anything about f(2) at all. The Free Lunch Theorem summarizes this by saying in effect that averaged over all possible data distributions, no model can generalize better than any other.

But our world is not the general case. Real environments often have an underlying simplicity that makes generalization possible. What is required for generalization is to define in advance a reasonable inductive bias for the environment one inhabits. Many such inductive biases have been used for supervised learning. They range from the assumption of linearity in linear regression to the assumption of compositional structure in neural networks.

When we talk about building models that generalize, we are necessarily talking about models which are underspecified by the data. That is, a model will make predictions which are not directly implied by the data. That is what it means to attempt to generalize. In most of supervised learning we pay little attention to this fact. Take the state-of-the-art in training neural networks as of 2020. People generally setup some reasonable model architecture that seems to provide a good inductive bias for the problem in question (convolution for computer vision, self-attention for NLP, etc...). Then gradient-based optimization of some sort is used to find parameters which maximize the likelihood of the data. In the best case scenario, what you get in the end is a decent single model of the data. However, what's often glossed over is that there were probably many potential models in parameter-space that could have given equally good but *different* predictions. In other words, the way that generalization happens to have manifested in any given model may be somewhat arbitrary.

This is why ensembles work. If you train many independent models from the same data, you can often obtain better overall predictions by averaging the predictions of the individual models. This is because the different models have generalized in different ways each of which is somewhat arbitrary. Thus by averaging, some of the randomness is removed, and the final result is less arbitrary.

There are a few ways that a model can be made less underspecified by the data. The simplest of course is to add more data. But this is not always possible. Another way to reduce underspecification is to simplify the model (i.e. reduce model capacity), since a simpler model has less room to wiggle arbitrarily. But this is helpful only up to a point. A model can be made too simple, in which case it won't have enough capacity to represent the true data generating function.

## Model Uncertainty

In some sense we can think of the degree to which our models are underspecified by the data as "model uncertainty". i.e. our uncertainty about which model in parameter space is closest to being the actual generating function of our data [1].

Let's think about how data constrains our models. At any given point in the training set, a trained model should generally be well specified. We already know what the correct value of the model is! However, data can be noisy, which complicates that statement and also leads to another type of uncertainty which we can think of as "data uncertainty", though it is often called "aleatoric uncertainty" (aleatoric just means "characterized by randomness").

However, outside of the training set things get more interesting. Any non-trivial model will be underspecified to a degree at such points. Nonetheless, that doesn't mean the model is free to do anything at that point. It is constrained by its inductive biases [2].

What's interesting is that a model will be constrained to different degrees at different points, depending both on the data and the inductive biases. The degree to which it is constrained is again this concept of "model uncertainty". Model uncertainty can be particularly useful when we're in a situation where we get to influence what future data is obtained. This is the case in active learning and reinforcement learning, where a learner has to decide which parts of state-space to explore during training, so as to perform more optimally later. If at a particular point in state-space, model uncertainty is high that may be a good candidate for exploration because the model is underspecified at that point. More data at that particular point will aid in reducing model uncertainty. How much it will help depends on how noisy the data is (i.e. data uncertainty).

We can measure model uncertainty with the posterior of the model parameters given the data:

`P(\theta|D)`

where \theta are the model parameters and D is the dataset. Probability is the language of uncertainty. It is a way of formalizing degrees of uncertainty. That is why we can think of `P(\theta|D)` as providing us with a measure of uncertainty about the parameters of our model, i.e. model uncertainty. We can arrive at this expression by applying Bayes rule:

`P(\theta|D) = \frac{P(D|\theta)P(\theta)}{P(D)} \propto P(D|\theta)P(\theta)`

`P(D|\theta)P(\theta)` should be familiar to supervised learners. The term `P(D|\theta)` is known as the likelihood of data. This term literally is a loss function. The `P(\theta)` is a known as a prior, and it corresponds to the use of weight regularization (such as `L_1` or `L_2`), also a standard component of loss functions.

`P(\theta|D)` is a probability density over the parameters of the model conditioned on the data. Having the probability density over the parameters means that for any given point in parameter space, we can assess how likely it is to be the parameter set that produces the generating function of our data. Furthermore, we can in principle at least, find the point of maximum probability, known as the "maximum a posterior" or MAP estimate. There may in fact be many such points in parameter space, especially if we consider points that are nearly equal in probability. A collection of many such high probability parameter sets can be used to construct an ensemble. If the constituent parameter sets all have high posterior probability, then they are all "good" models of the data, and if they also produce different predictions, then an ensemble of them is likely to produce predictions that are better still. To single out any one of those individual models and call "the model" of our data would be arbitrary, but this is exactly what people do all the time in supervised learning. In practice this is understandable due to the computational constraints of Bayesian approaches and ensembling more generally. But we should at least be aware that we are doing this and should be mindful of opportunities to do better.

## The Suprising Power of Ensembles

One hope for Bayesian ML is that it will enable us to more efficiently build the most effective ensembles. But is Bayesian machine learning just a fancy way of building ensembles? In a sense it is, but ensembles are more powerful and interesting than they first appear. They are not just a means of achieving better predictions by averaging. Just as we can average over the predictions from an ensemble to get better predictions, we can also take the variance or the entropy to measure uncertainty. Suppose, we're working on a binary classification problem and we have an ensemble of 2 models \theta_1 and \theta_2. Furthermore, suppose that at a fixed point in our test set, \theta_1 and \theta_2 produce the following predictions:

class1, class2

\theta_1: 0.2, 0.8

\theta_2: 0.5, 0.5

The variance or entropy within a column tells us about model uncertainty at this point in the test set. To the degree to which we reduce our model uncertainty, then we obtain more clarity about data uncertainty. For instance, if every model we sample from the posterior provides consistent predictions, then we can measure data uncertainty by taking the variance or entropy across the rows. If the models we sample from the posterior provide inconsistent predictions then there is little if anything we can say about data uncertainty.

## Bayesians

You may sometimes hear people jokingly (or seriously) refer to themselves as Bayesians. Some people even describe the moment they self-identified as Bayesians as a moment of ["enlightenment"](https://www.lesswrong.com/posts/Ti3Z7eZtud32LhGZT/my-bayesian-enlightenment). In a machine learning context, I believe this identity has a special significance which ought to be more widely appreciated. *Fundamentally, Bayesians are simply people who are fascinated by model uncertainty.* That is, Bayesians are bothered and fascinated by the fact that any given model trained simply to maximize likelihood will generalize in a way that is at least somewhat arbitrary, and can potentially be improved by accounting for this. For me this was recently a big "aha" moment, and is what inspired me to write this post.


Additional Notes:

[1] This implicitly assumes that the family of functions we are considering (i.e. our model architecture choice if we are training a neural net) is the "correct" choice.

[2] One very common inductive bias is the assumption of local constancy or smoothness. This means that the model will make predictions outside of the training set that are determined by the closest points within the training set. The nearest neighours algorithm is the simplest such example but tree-based models such as xgboost also make use of this assumption. As noted in the text Deep Learning by Goodfellow et al., such models have a devastating weakness. They cannot learn to generalize even so simple a pattern as a checkerboard. In a checkerboard, the correct value oscillates endlessly as one moves along any given axis. So, by simply reusing the value associated to nearest training example, one is guaranteed to be incorrect about 50% of the time.
