Lesson 9: Bayesian Learning
===========================

Bayesian learning
-----------------

* Learn the **best** hypothesis given data and some domain knowledge.
* Learn the **most probable** H given data and domain knowledge. (**best** == **most probable**)

argmax_{h in H} Pr(h | D)

Bayes rule
----------

P(h|D) = P(D|h)P(h)/P(D)

P(D) -- prior on the data
P(h) -- prior on h (this encapsulate our domain domain knowledge)
P(D|h) -- data given the hypothesis (in a world where the hypothesis is true... likelihood of seeing this data)

Quiz: Bayes' rule
-----------------

98% true positive. 2% false positive.
97% true negative. 3% false negative.

Only 0.008 percent of population has it.

P(T|P) = P(P|T)*P(T)/P(P) = .98*.008/.0376 ~ 0.209

P(not T|P) = P(P | not T)*P(not T)/P(P) = .03*.992/.0376 ~ 0.791

If 0.008 were higher, the test would be more useful.


Bayesian learning
-----------------

For each h in H,

h_MAP = argmax_h P(h|D) = argmax_h P(D|h)P(h) (maximum a posteriori)
h_ML = argmax_h P(D|h) (maximum likelihood -- assume prior P(h) is uniform)

Direct computation not practical for large hypothesis spaces.

Bayesian learning in action
---------------------------
Assume:
* We have labeled training data {<x_i, d_i>} as noise-free examples of c.
* c is in H
* Uninformed prior over hypothesis space.

P(h|D) = P(D|h)P(h)/P(D)

P(h) = 1/|H|
P(D|h) = {1 if d_i = h(x_i) for all i; 0 otherwise} = {1 if h is in VS(D)}
P(D) = sum_i P(D|h_i)P(h_i) (total probability)
     = sum_{h in VS_H(D)} 1 * 1/|H| = |VS|/|H|

P(h|D) = (1 * 1/|H|)/(|VS|/|H|) = 1/|VS| 
This means, given a bunch of data, the probability of a particular hypothesis being correct is uniform over elements of the version space.

Any element of the version space is good.

Bayesian learning with noise
----------------------------

Assume
* We have labeled training data {<x_i, d_i>}
* d_i = f(x_i) + e_i (where e_i is error)
* e_i ~ N(0, s^2) (i.i.d.)

h_ML = f = argmax_h P(D|h) = argmax product_i P(d_i | h)

This probability can be approximated with gaussian: stuff*exp(-1/2(d_i - h(x_i))^2)/s^2)... we can log it for the purpose of argmax.

h_ML = argmax sum_i -(d_i - h(x_i))^2 = argmin sum_i (d_i - h(x_i))^2

This is the sum of squared error.... derived from the gaussian noise model and the maximum likelihood assumption.

Bayesian learning
-----------------

h_MAP = argmax P(D|h)P(h) = argmax [lg(P(D|h)) + lg(P(h))] =  argmax [ -lg(P(D|h)) - lg(P(h))]

Event w has probability p, i.e. has length -lg p

"Minimizing length(D|h) + lenght(h)"

If the hypothesis fits the data well, the data is superfluous information. Otherwise, we need a lot of data. So the first term correlates to misclassifications/errors

The second term tries to simplify the second term.

**Minimum description length**

Bayesian classification
-----------------------

The consensus of non-MAP or non-ML hypotheses may differ from the MAP or ML hypotheses. Vote?

In some sense we are throwing out the hypotheses for "boosted" superhypotheses.

value_MAP = argmax_v sum_h P(v|h)P(h|D) (weighted vote of h in H) **Bayes Optimal Classifier**

Summary
-------

* Bayes rule (swap "causes and effect")
  + P(h|D) ~ P(D|h)P(h)
* priors matter
* h_MAP, h_ML
* derived least square from Gaussian h_ML.
* best classification is consensus of all classifiers: **Bayes Optimal Classifier** (the best classifier you can possibly do)

