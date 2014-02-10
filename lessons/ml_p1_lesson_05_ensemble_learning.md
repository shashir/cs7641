Lesson 5: Ensemble Learning: Boosting
=====================================

Spam/whitelist rules ("from: spouse", "Nigeria", "has pr0n", etc.) apply to many emails, but not all. How do we generate rules? How do we combine rules? Similar to decision trees. If you already know the rules, the combining step may be like neural networks.

Boosting
--------

Combine simple rules into a complex rules.

* Learn over a subset of data to generate a simple rule.
* Learn over another subset of data to generate another simple rule.
* ...
* ...
* Combine all rules.

Subsetting is non-trivial.

* Uniformly randomly pick a subset of data. Apply any learning algorithm on it.


Combine is non-trivial.

* Take mean.

In the case where we pick single points and take the overall mean, the result is the same as n-NN with no weighting.

**Bagging/bootstrap aggregation** -- taking random subsets, learning, and taking mean of the individual machines.

*Instead of picking subsets randomly, take advantage of what we are learning as we go along. Especially, pick examples we are bad at. Take "hardest" subsets."*

How about using a weighted mean?

Previously we defined error in classification as the number of mismatches. Instead define **error** as Pr_D(h(x) != c(x)) where D is the distribution from which x is acquired. This allows for more probably examples to produce a greater error contribution than less likely example. We want to be good at the common points.

**Weak learner** -- does better than chance always: for all D, Pr_D(h(x) != c(x)) <= 1/2 - \epsilon.

In some problems, there may exist distributions such that there is no weak learner. This may require an expansion of the hypothesis space (relieve the restriction bias).

Boosting in code
----------------

***
Given D = {(x_i, y_i) where y_i are -1 or +1}
For t = 1 to T
    construct D_t (a distribution)
    find weak classifier h_t with small error e_t = P_D_t(h_t(x_i) != y_i) (???)
Output H_final
***

How to construct D_t?
---------------------

D_1(i) = 1/n (uniform)
D_(t+1)(i) = D_t(i)*e^(-a_t*y_i*h_t(x_i))/z_t
where a_t = 1/2 * ln ((1-e_t)/e_t)

"Generally" puts more probability on incorrect instances and less probability on correct instances. We have an issue if error is exactly half or exactly 0.

How to combine smaller classifiers into H_final?
------------------------------------------------

Take a weighted average using a_t.

H_final(x) = sgn(sum_t a_t*h_t(x))

Hypotheses/ensemble methods
---------------------------

Compare to decision trees.

Compare to locally weighted linear regression (as a modification of k-NN) where you stitch simpler models into a complex one. This characterizes all ensemble methods.

Why is boosting good?
---------------------

Every iteration of boosting only "gains" more information by better classifying badly classified examples.

Ensemble learning
-----------------

* Ensembles are good
* Bagging is good
* Combines simple into complex
* Boosting is really good -- agnostic to learner
* Weak learners
* Error based on distributions
* Cool points: boosting does not seem to overfit over arbitrary iterations in practice (or does it?)
