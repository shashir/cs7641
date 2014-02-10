Lesson 3: Neural Networks
===============

Artificial neural networks
--------------------------

Based on biological neuron (cell body, axon, and synapses -- cell bodies fire signals down axons to synapses if their activation threshold is surpassed).

Perceptron
----------

The perceptron hypothesis boils down to being the sign of the dot of the weights and the input. Let's say all inputs have a zeroth component which is 1 and the zeroth component of the weight is the negative threshold.

<img src="http://s.wordpress.com/latex.php?latex=h%28%5Cmathbf%7Bw%7D%29%28%5Cmathbf%7Bx%7D%29%20%3D%20%5C%7B%5Cmathbf%7Bw%20%5Ccdot%20x%7D%20%5Cge%200%5C%7D&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="h(\mathbf{w})(\mathbf{x}) = \{\mathbf{w \cdot x} \ge 0\}" title="h(\mathbf{w})(\mathbf{x}) = \{\mathbf{w \cdot x} \ge 0\}" class="latex">

The output is 0 if the dot product is negative, 1 if positive.

How powerful is a perceptron unit
---------------------------------

Perceptrons define a discriminant line which splits the plane in half (analogy applies in higher dimensions also).

When the components of the input are boolean, then the perceptron can define boolean logic such as AND and OR, but a single perceptron can not discover XOR and others.

Given a vector <-theta, w_0, w_1> be able to visualize a half-plane and given a half-plane write the weights vector.

XOR as a perceptron network
---------------------------

A more complex discriminant "curve" can be contrived from a "network" of perceptrons.


Perceptron training
-------------------

Two ways to learn weights

* Perceptron learning rule
* Gradient descent/delta rule

The perceptron learning rule defines how to update the weights in iterative stages. Over time, it is capable of converging on the best classifier on the training set is the training set is linearly separable. However, it will not converge if the data is not linearly separable.

```
eta <- learning rate
initialize(w) // Set every component w_i of w to some random initial value
do until satisfied: 
  for each training datum (x, y) from the training set:
    y_hat <- w dot x // Compute the predicted output
    w <- w + eta * (y - y_hat) *.* x // Update the weights vector with the adjustment. *.* is Hadamard product (element-wise product).

```

This is online learning and you can stop when average error on the training set is below some threshold.

If the data is "nearly" linearly separable, perhaps reduce the learning rate over time such that the discriminant line at least appears to converge?

Perceptron learning can not be applied in the conventional sense to a multiple-layer neural network. It is only defined for a single layer.


Gradient descent
----------------

Is there a learning algorithm which is robust to non-(linear separability)?

We would like to perform gradient descent on the total error on the training set such that we can arrive at the weights which minimize the error.

Let D be the training set with ordered pairs (x,y). Let y be the target. Instead of taking the sign, we will simply take the dot product of w and x (this is essentially simple linear regression). We want to minimize:

<img src="http://s.wordpress.com/latex.php?latex=E%28%7B%5Cmathbf%20w%7D%29%20%3D%20%5Cfrac%7B1%7D%7B2%7D%5Csum_%7B%28%7B%5Cmathbf%20x%7D%2C%20y%29%20%5Cin%20D%7D%20%28y%20-%20%7B%5Cmathbf%20w%7D%20%5Ccdot%20%7B%5Cmathbf%20x%7D%29%5E2&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="E({\mathbf w}) = \frac{1}{2}\sum_{({\mathbf x}, y) \in D} (y - {\mathbf w} \cdot {\mathbf x})^2" title="E({\mathbf w}) = \frac{1}{2}\sum_{({\mathbf x}, y) \in D} (y - {\mathbf w} \cdot {\mathbf x})^2" class="latex">

The partials with respect to components of w:

<img src="http://s.wordpress.com/latex.php?latex=%5Cfrac%7B%5Cpartial%20E%7D%7B%5Cpartial%20w_i%7D%20%3D%20-%5Csum_%7B%28%7B%5Cmathbf%20x%7D%2C%20y%29%20%5Cin%20D%7D%20x_i%28y%20-%20%5Cmathbf%7Bw%7D%20%5Ccdot%20%5Cmathbf%7Bx%7D%29&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="\frac{\partial E}{\partial w_i} = -\sum_{({\mathbf x}, y) \in D} x_i(y - \mathbf{w} \cdot \mathbf{x})" title="\frac{\partial E}{\partial w_i} = -\sum_{({\mathbf x}, y) \in D} x_i(y - \mathbf{w} \cdot \mathbf{x})" class="latex">

The error decreases fastest in the direction opposite to the gradient. Walk in small steps opposite to the gradient.

Robust to linear separability and converges in the limit (eta must be small not to yo-yo in the well).

Comparison of learning rules
----------------------------

The perceptron learning rule uses the following weight update.

<img src="http://s.wordpress.com/latex.php?latex=%5CDelta%20w_i%20%3D%20%5Ceta%28y%20-%20%5C%7B%5Cmathbf%7Bw%20%5Ccdot%20x%7D%20%5Cge%200%5C%7D%29x_i&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="\Delta w_i = \eta(y - \{\mathbf{w \cdot x} \ge 0\})x_i" title="\Delta w_i = \eta(y - \{\mathbf{w \cdot x} \ge 0\})x_i" class="latex">

Learning a classifier using gradient descent on a linear regression model uses the following weight update.

<img src="http://s.wordpress.com/latex.php?latex=%5CDelta%20w_i%20%3D%20%5Ceta%28y%20-%20%5Cmathbf%7Bw%20%5Ccdot%20x%7D%29x_i&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="\Delta w_i = \eta(y - \mathbf{w \cdot x})x_i" title="\Delta w_i = \eta(y - \mathbf{w \cdot x})x_i" class="latex">

Sigmoid
-------

Why not do gradient descent on the original perceptron itself rather than remodeling it as linear regression? The step function is not differentiable. We can get around this with the sigmoid function (hyperbolic tan, arctan, logistic sigmoid).

<img src="http://s.wordpress.com/latex.php?latex=%5Csigma%28a%29%20%3D%20%5Cfrac%7B1%7D%7B1%20%2B%20e%5E%7B-a%7D%7D&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="\sigma(a) = \frac{1}{1 + e^{-a}}" title="\sigma(a) = \frac{1}{1 + e^{-a}}" class="latex">

Note that the derivative has a nice form:

<img src="http://s.wordpress.com/latex.php?latex=D%5Csigma%28a%29%20%3D%20%5Csigma%28a%29%281%20-%20%5Csigma%28a%29%29&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="D\sigma(a) = \sigma(a)(1 - \sigma(a))" title="D\sigma(a) = \sigma(a)(1 - \sigma(a))" class="latex">

Now we can use the chain rule to extend gradient descent to neurons with sigmoid activation functions.

Neural Networks
---------------

Hook up nodes which use the sigmoid of the dot product of the weights and the input. The input layer can be fed into the hidden layers and eventually into the output "layer" (a single node).

Every node can be trained based on it's respective inputs and output using the gradient descent rule on the now differentiable activation function (the sigmoid). For each input, the output can be computed. The output layer can be trained first. Then the last hidden layer can be trained. Then the next and so on. This careful bookkeeping is known as backpropagation.

With networks, there may be many local optima. We need to use clever techniques to arrive at a suitable set of weights.

Optimizing weights
------------------

How do arrive at a suitable set of weights? Optimization problem.

* Use momentum terms in the gradient (simulated annealing?)
* higher order derivatives (hamiltonians, etc.)
* randomized optimization (later on in the course)
* penalty for "complexity" (overfitting) -- too many hidden layers? too many nodes in a layer? large valued weights (interesting)


Restriction bias
----------------

Restriction bias -- the representational power and the set of hypotheses we will consider.

Perceptrons are linear models (discriminant lines splitting planes). Networks of perceptrons can approximate more complex functions. Sigmoids allow even better learning and can fit more interesting functions.

* Boolean functions -- network of threshold-like units.
* Continuous functions -- use sigmoid activation and a hidden layer.
* Arbitrary functions -- stitch together two or more functions with discontinuitives with two hidden layers.

Overfitting problem with more complex networks.

* We can bound the architecture of the network. 
* Cross validate to better bound the architecture or bound the weights.
* We should also find the number of iterations at which the network best generalizes.

Not really much of a restriction bias.


Preference bias
---------------

Preference bias -- which representation is preferred by the algorithm.

Generally we initialize the network with small random weights -- we prefer "simpler"/less complex representations. (This can hit a local minimum. We generally run the training multiple times to avoid local minimum.)

Practically, (Occam's Razor) produces simpler and generalizable representations.

Summary
-------

* Perceptron (linear and thresholded)
* Perceptron learning rule
* Gradient descent
* Sigmoid function
* Restriction bias
* Preference bias







