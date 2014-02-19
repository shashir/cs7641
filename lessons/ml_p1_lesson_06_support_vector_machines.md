Lesson 6: Support Vector Machines
=================================

The best line
-------------

The discriminant line that generalizes best is the farthest from the two classes ("commits least to the training data").

Support vector machine (massive handwaving)
-------------------------------------------

We are interested in maximizing the size of the margin.

The general linear classifier formula is: y = w^T x + b (here y is the classification)

The equation for the discriminant line is 0 = w^T x + b

Translate this line up or down to get 1 = w^T x + b or -1 = w^T x + b

We want w such that the distance between these two lines in maximal (and the choice of 1 is really arbitrary -- we just want w "up to" scaling).

Take the difference: w^T (x_1 - x_2) = 2 (where x_1 and x_2 are support vectors.

Divide ||w||. Then w^T/||w|| (x_1 - x_2) = 2/||w||

Now we have the difference of x_1 and x_2 projected onto the normalized w vector... Since w is parallel to the vector from x_1 to x_2. Some handwaving magic. The left handside is the margin m.

m = 2/||w||

So handwavily, the "distance" between the -1 line and 1 is 2/||w|| and we can maximize this by minimizing w's magnitude. What about direction?

Support vector machines
-----------------------

Maximize 2/||w|| while classifying everything correctly.

The problem is: y_i(w^T x_i + b) >= 1 for all i.

Alternatively minimize 1/2 ||w||^2 

This is a quadratic programming problem (which is a load of bullshit from shoddy under-formalized areas of math) which can be solved by jumping off a cliff.

Some properties of the solution.

* w = sum_i a_i y_i x_i and b = easy
* a_i mostly 0 (which means only some of the x_i matter).
* The data points are being dotted. Similar direction means greater weight... how "similar" are they to each other?


Like k-NN except we learn which points are important (as opposed to considering all neighbors).

SVMs: linearly married
----------------------

What if some points can not be classified correctly? Have a cost for misclassification.

What if lines are a bad hypothesis? Transform the data points and throw them into a higher-dimensional space where a line might be a better hypothesis.

Phi(q) = <q1^2, q2^2, sqrt(s)*q1*q2>

Phi(q) . Phi(p) = (q . p)^2 (which makes the classifier into a circle instead of a line).

Instead of computing Phi, just square the dot product -- **the kernel trick**.

Kernels
-------

We can replace the dot product with a kernel.

Implicitly throws data points into higher dimensional space and get similarity.

Kernel choice requires domain knowledge.

Polynomial kernel: K(x, y) = (x^T y + c)^p

RBF kernel: exp(-(||x - y||^2)/(2*sigma^2))

Kernels must satisfy Mercer condition -- must act like an inner product.

SVMs -- review
--------------

* margins ~ generalization and overfitting
* big is better
* optimization problem for finding max margins: quadratic programming and dual problem
* support vectors
* kernel trick which extends the inner product
* Mercer condition

Back to boosting
----------------

Boosting doesn't seem to conventionally overfit (testing error keeps going down).

**Confidence** -- how confident is a classification? (Number of neighbors agreeing in k-NN or local variation in linear regression).

Explain the difference between confidence and error.

We can examine each iteration of boosted classifiers by normalizing the argument of the sign. This is the confidence. Hard examples fall near the center (toward 0). As we boost further, the hard points also start having higher confidence. The margin keeps increasing and does not overfit.

Boosting will overfit if the individual learners always overfit.

**Pink noise** -- uniform noise. Boosting overfits.

**White noise** -- Gaussian noise.

Summary
-------

* Margins -- important to SVM and margins
* big is better
* optimization problem for finding max margins: quadratic programming and dual problem
* support vectors
* kernel trick which extends the inner product
* Mercer condition






