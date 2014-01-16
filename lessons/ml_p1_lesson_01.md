Lesson 1: Decision Trees
========================

Classification and regression
-----------------------------

In supervised learning, you are presented with instances (e.g. images of individuals) with labels (e.g. "BOY" or "GIRL") as training data. The task is to label new unlabeled instances (assuming the instance has the sufficient information).

* **Classification** -- labels are discrete values (often true or false).
  * Better definition (Shashir): labels (codomain of the target function) have no meaningful order.
* **Regression** -- labels are reals.
  * Better definition (Shashir): labels have a meaningful order.


Classification learning
-----------------------

* **Instances** -- inputs (vectors of features).
* **Concept** -- a function which maps instances to labels (there many concepts: |labels|^|instance space|).
* **Target concept** -- the function which maps instances to the **correct** labels.
* **Hypothesis** -- set of concepts which we are willing to search for the best approximation of the target concept.
* **Sample (training set)** -- set of inputs with correct labels.
* **Candidate** -- the "best" concept chosen from the hypothesis by the learning algorithm using the sample.
* **Testing set** -- set of instances with correct labels, similar to the training set, but used to measure how well the candidate performs on novel data.

The testing set should contain many examples not found in the training set.

Decision trees
--------------

Sequence of tests (path of nodes starting from a root node) applied to every instance in order to arrive at its label (leaf).

### Representation versus algorithm

