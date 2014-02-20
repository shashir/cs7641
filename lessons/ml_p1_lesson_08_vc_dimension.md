Lesson 8: VC Dimensions
=======================

Infinite hypothesis spaces
--------------------------

Haussler theorem breaks with infinite hypothesis spaces.

Consider example:

X: {1, 2, ..., 10}
H: h(x) = {x >= t where t is real}

Though there are infinite hypotheses, there are find semantically relevant hypotheses (11).

Power of a hypothesis space
---------------------------

What is the largest set of inputs that the hypothesis class can label in all possible ways?

In the above hypothesis, there is no way for a pair of data points to be labeled in all possible ways. It can however label **one** point is all possible ways (two ways).

What VC stands for
------------------

**Shattering** -- labeling in all possible ways.

Vapnik-Chervonenkis dimension -- the largest set of inputs shattered by a class of learners.

Quiz: interval training
-----------------------

X = Reals
H = {h(x) = {x in [a, b] -- a real interval}}

Has VC dimension of 2.

Note on logic
-------------

To prove yes: There exists points for all labelings there exists hypothesis
To prove no: not(there exists points for all labelings there exists hypothesis) = for all points, not(for all labelings there exists hypothesis) = for all points, there exists labelings not(there exists hypothesis)

Quiz: linear separators
-----------------------

X = R^2
H = {h(x) = w^T x >= \theta}

Has VC dimension of 3.

The rings
---------

The d-dimensional hyperplane as VC dim d + 1

Quiz: polygons (convex)
-----------------------

X: R^2
H: points inside some convex polygon

VC dimension is infinite. (Use a circle for vertices and put points on edge).

Sample complexity and VC dimension
----------------------------------

Update Haussler's theorem with VC dimension:

m >= 1/\epsilon (8* VC(H)*lg(13/\epsilon) + 4*lg(2/\delta))  (infinite case)
m >= 1/\epsilon (ln |H| + ln (1/\delta)) (finite case)

VC dimension of finite H
------------------------

Upper bound: d = VC(H) implies there exist 2^d distinct concepts (each gets a different h)
2^d <= |H|    and d <= lg |H|

**Fundamental Theorem of Machine Learning** 
H is PAC-learnable if and only if VC dimension is finite.

Summary
-------
* VC dimension. Shattering
* VC relates to hypothesis space parameters ("true" number of parameters)
* VC relates to finite hypothesis space size.
* Sample complexity related to VC dimension.
* VC dimension captures PAC-learnability
