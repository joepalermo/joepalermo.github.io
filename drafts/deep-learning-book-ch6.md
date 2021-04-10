Below you will find thoughts developed while working through parts in the book that I found confusing or interesting.

Notation:

Let $latex \zeta(x) = log(1 + e^{x})$, i.e. the softplus function.

Let $latex \sigma(x) = \frac{1}{1 + e^{-x}}$, i.e. the logistic sigmoid function.

The following identities will be useful:

$latex p=\sigma(z)$

$latex 1-\sigma(x) = \sigma(-x)$

$latex log(\sigma(x)) = -\zeta(-x)$

On Section 6.2.2.2

They write that the maximum-likelihood cost function for learning a Bernoulli output variable is given by:

$latex \zeta((1-2y)z) $

We will see that this expression is simply a different way of expressing the familiar binary cross-entropy loss function.

$latex -ylog(p) + (y-1)log(1-p)$

$latex -ylog(\sigma(z)) + (y-1)log(1-\sigma(z))$

$latex -ylog(\sigma(z)) + (y-1)log(\sigma(-z))$

$latex y\zeta(-z) + (1-y)\zeta(z)$

This expression is a restatement of the binary cross-entropy loss function, written in terms of the logits instead of the probabilities.

Then note that if y = 1, we have:

$latex \zeta((1-2y)z) = \zeta(-z)$, and $latex y\zeta(-z) + (1-y)\zeta(z) = \zeta(-z)$

Likewise if y = 0, we have:

$latex \zeta((1-2y)z) = \zeta(z)$, and $latex y\zeta(-z) + (1-y)\zeta(z) = \zeta(z)$

So $latex \zeta((1-2y)z) $ is an alternative way of expressing the binary cross-entropy loss function.

Note that these alternative expressions involving the softplus function have the advantage of being more numerically stable since they don't ever require taking the log of values close to 0.
