What makes a Bayesian?

Supervised learning is concerned with learning associative maps from data. What makes SL interesting, is that it is particularly concerned with learning associative maps that generalize outside of the training set. But how is such generalization possible?

If I observe f(0) = 1, and f(1) = 2, how confident can I be that f(2) = 3? Of course, in the general case you can't say anything about f(2) at all. The Free Lunch Theorem summarizes this by saying in effect that averaged over all possible data generating distributions, no model can generalize better than any other.

But our world is not the general case. Real environments often have an underlying simplicity that makes generalization possible. What is required for generalization is to define in advance a reasonable inductive bias for the environment one inhabits. Many such inductive biases have been used for supervised learning. They range from the assumption of linearity in linear regression to the assumption of compositional structure in neural networks.

When we talk about building models that generalize, we are necessarily talking about models which are underspecified by the data. That is, a model will make predictions which are not directly implied by the data. That is what it means to attempt to generalize. In most of supervised learning we ignore this fact. Take the state-of-the-art in training neural networks as of 2020. People generally setup some reasonable model architecture that seems to provide a good inductive bias for the problem in question*. Then gradient-based optimization of some sort is used to find parameters which maximize the likelihood of the data. In the best case scenario, what you get in the end is a decent single model of the data. However, what's often glossed over is that there were probably many potential models in parameter-space that could have given equally good but *different* predictions. In other words, the way that generalization happens to have manifested in any given model may be somewhat arbitrary.

This is why ensembles work. If you train many independent models from the same data, you can often obtain better overall predictions by averaging the predictions of the individual models. This is because the different models have generalized in different ways each of which is somewhat arbitrary. Thus by averaging, some of the randomness is removed, and the final result is less arbitrary.

There are a few ways that a model can be made less underspecified by the data. The simplest of course is to simply add more data. Of course, this is not always possible. Another way to reduce underspecification is to simplify the model (i.e. reduce model capacity), since a simpler model has less room to wiggle arbitrarily. But this is helpful only up to a point. A model can be made too simple, in which case it won't have enough capacity to represent the true data generating function.

In some sense we can think of the degree to which our models are underspecified by the data as "model uncertainty". i.e. our uncertainty about which model in parameter space is closest to being the actual generating function of our data**.

Let's think about how data constrains our models. At any given point in the training set, a trained model should generally be well specified. We already know what the correct value of the model is! However, data can be noisy, which complicates that statement and also leads to another type of uncertainty which we can think of as "data uncertainty", though it is often called "aleatoric uncertainty" (aleatoric just means "characterized by randomness").

However, outside of the training set things get more interesting. Any non-trivial model will be underspecified at such points. Nonetheless, that doesn't mean the model is free to do anything at that point. It is constrained by its inductive biases***.

What's interesting is that a model will be constrained to different degrees at different points, depending both on the data and the inductive biases. The degree to which it is constrained is again this concept of "model uncertainty". Model uncertainty can be particularly useful when we're in a situation where we get to influence what future data is obtained. This is the case in active learning and reinforcement learning, where a learner has to decide which parts of state-space to explore during training, so as to perform more optimally later. If at a particular point in state-space, model uncertainty is high that may be a good candidate for exploration because the model is underspecified at that point. More data at that particular point will aid in reducing model uncertainty. How much it will help depends on how noisy the data is (i.e. data uncertainty).

Bayesians are people who are fascinated by this notion of model uncertainty.



*Note that most of the breakthroughs deep learning research can be thought of as coming up with better inductive biases for different classes of problems (convolution for object recognition, self-attention for NLP, etc...)

**This implicitly assumes that the family of functions we are considering (i.e. our model architecture choice if we are training a neural net) is the "correct" choice.

***One very common inductive bias is the assumption of local constancy or smoothness. This means that the model will make predictions outside of the training set that are determined by the closest points within the training set. The nearest neighours algorithm is the simplest such example but tree-based models such as xgboost also make use of this assumption. As noted in the text Deep Learning by Goodfellow et al., such models have a devastating weakness. They cannot learn to generalize even so simple a pattern as a checkerboard. In a checkerboard, the correct value oscillates endlessly as one moves along any given axis. So, by simply reusing the value associated to nearest training example, one is guaranteed to be incorrect about 50% of the time.
