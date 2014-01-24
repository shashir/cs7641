Neural Networks
===============

Artificial neural networks
--------------------------

Based on biological neuron (cell body, axon, and synapses -- cell bodies fire signals down axons to synapses if their activation threshold is surpassed).

Perceptron
----------

The perceptron hypothesis boils down to being the sign of the dot of the weights and the input. Let's say all inputs have a zeroth component which is 1 and the zeroth component of the weight is the negative threshold.

<img src="http://s.wordpress.com/latex.php?latex=h%28%5Cmathbf%7Bw%7D%29%28%5Cmathbf%7Bx%7D%29%3D%7B%5Ctextrm%7Bsgn%7D%7D%28%5Cmathbf%7Bw%7D%20%5Ccdot%20%5Cmathbf%7Bx%7D%29&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="h(\mathbf{w})(\mathbf{x})={\textrm{sgn}}(\mathbf{w} \cdot \mathbf{x})" title="h(\mathbf{w})(\mathbf{x})={\textrm{sgn}}(\mathbf{w} \cdot \mathbf{x})" class="latex">

Here we are defining sign as a boolean function (0 if negative, 1 if positive).

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


