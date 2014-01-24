Lesson 2: Regression & Classification
=====================================

What is regression?
-------------------

The term regression became overloaded over time. Initially it described how children of very tall people and children of very short people tended both to be a bit closer average height than their parents.

The "function" child_height(parent_height) looks like a line and has slope less than 1.


Linear regression
-----------------

It's possible to fit affine hyperplanes to data. If we transform the input vectors with squared or cubed terms, etc. we can also fit any higher dimensional polynomial with the same technique.

We would like for the best fit "curve" (surface) such that it minimizes an error. However, there are certain inductive biases we can make. What degree polynomial should we fit? The higher the degree, the better we can fit a set of points, but the more "overfit" the curve will be.

When we have an overfit candidate function, though it produces no error on the training set, it will not generalize.


Performing linear regression
----------------------------

Let our instance be elements of R^n. Suppose we have a training set {(x_1, y_1), (x_2, y_2), ..., (x_m, y_m)} where x_i are in R^n and y_i are in R. We would like to find w such that x dot w approximates y.

Let w be a column vector and x_i be row vectors. Define matrix X = [x_1 x_2 x_3 ... x_m] and Y = [y_1 ... y_m]. We want to find w such that wX = Y (approximately).

We find that if we multiply by X^T on both sides, we will very likely have an invertible matrix XX^T. So we arrive at:

w = Y(X^T)(XX^T)^-1

For details: http://en.wikipedia.org/wiki/Linear_regression

This formula minimizes the squared error (prove by differentiating L(w) = ||Y - wX||^2).


Errors
------

All data has noise/errors arising from sensor error, malicious agents, transcription error, unmodeled influences, etc.

We should not overfit to training data in order not to model the errors.

We want to train until we minimuze the mean squared error (MSE) on the training data.

<img src="http://s.wordpress.com/latex.php?latex=MSE%20%3D%20%5Cfrac%7B1%7D%7Bn%7D%20%5Csum_i%20%28w%20%5Ccdot%20x_i%20-%20y_i%29%5E2&amp;bg=ffffff&amp;fg=000000&amp;s=0" alt="MSE = \frac{1}{n} \sum_i (w \cdot x_i - y_i)^2" title="MSE = \frac{1}{n} \sum_i (w \cdot x_i - y_i)^2" class="latex">

Next we want to compute the error on various testing sets to make sure that the model is not so complicated that it overfits and doesn't generalize.

Cross validation
----------------

To check that data generalizes well, hold aside a subset of the training data as "testing data", training on the remaining set and test against the "testing data." Choose our inductive bias (picking model or model complexity) such that when the model is trained on the training set it's error on the testing set is still minimal.


Other input spaces
------------------

Our instance elements need not all be reals (though the regression would be better under certain special circumstances). Ideally the values of each feature should have a natural order. Boolean vectors are a good choice often.
