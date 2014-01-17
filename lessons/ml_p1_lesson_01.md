Lesson 1: Decision Trees
========================

Classification and regression
-----------------------------

In supervised learning, you are presented with instances (e.g. images of individuals) with labels (e.g. "BOY" or "GIRL") as training data. The task is to label new unlabeled instances (assuming the instance has the sufficient information).

* **Classification** -- labels are discrete values (often true or false).
  * Better definition [Shashir]: labels (codomain of the target function) have no meaningful order.
* **Regression** -- labels are reals.
  * Better definition [Shashir]: labels have a meaningful order.


Classification learning
-----------------------

* **Instances** -- inputs (vectors of features).
* **Concept** -- a function which maps instances to labels (there many concepts: |labels|^|instance space|).
  * [Shashir] Concepts are the set of functions mapping from the instance space to the labels space.
* **Target concept** -- the function which maps instances to the **correct** labels.
  * [Shashir] The target concept is a specific concept which we wish to model.
* **Hypothesis** -- set of concepts which we are willing to search for the best approximation of the target concept.
  * [Shashir] Subset of the concepts set. Easier space to search through, but introduces *inductive bias*.
* **Sample (training set)** -- set of inputs with correct labels.
* **Candidate** -- the "best" concept chosen from the hypothesis by the learning algorithm using the sample.
  * [Shashir] Element of hypothesis which best approximates the target concept according to our learning algorithm.
* **Testing set** -- set of instances with correct labels, similar to the training set, but used to measure how well the candidate performs on novel data.

The testing set should contain many examples not found in the training set.

Decision trees
--------------

Sequence of tests (path of nodes starting from a root node) applied to every instance in order to arrive at its label (leaf).

Decision trees: learning
------------------------

1. Pick the best attribute to split the data.
2. Asked test every possible value of the attribute.
3. Follow the correct answer path.
4. Go to 1 until the possibilities has been narrowed to one answer.

How can this intuition be used to build a "tree" for all possible instances of the problem?

Decision trees: expressiveness
------------------------------

Consider the inclusive disjunction: **OR(a1, a2, ..., an)** (any). Note that the tree is "linear" and has a height of n.
```
--->a1--T-->a2--T-->...--T-->an--T-->TRUE
        |       |                |
        F       F                F
        |       |                |
        v       v                v
      FALSE   FALSE            FALSE
```

Next, consider the exclusive disjunction: **XOR(a1, a2, ..., an)** (odd parity). Note that the tree is balanced and has height O(2^n).

```
--->a1--T-->a2--T-->a3--T-->TRUE
     |       |       |
     |       |       F----->FALSE
     |       |
     |       F----->a3--T-->FALSE
     |               |
     |               F----->TRUE
     |   
     F----->a2--T-->a3--T-->FALSE
             |       |
             |        F---->TRUE
             |
             F----->a3--T-->FALSE
                     |
                     F----->TRUE
```
It's better just to add in integers mod 2.

Decision trees: expressiveness (search space)
---------------------------------------------

Given n binary attributes, how many possible decision trees are there? 2^(2^n)

Intuition:
* There are 2^n possible configurations of the attributes.
* Each "unique" decision tree maps these 2^n configurations into a 2^n-sized bit vector.
* There are 2^(2^n) possible bit vectors of size 2^n.
* Therefore, there must are 2^(2^n) possible trees to search.

ID3 Algorithm
-------------

'''
Node {
  Node parent;
  Set<Node> children;
  Set<Instance> instances;
}

Instance {
  Map<Key=Attribute, Value=Attribute.domain> attributes;
}

Tree decisionTree = null;

'''

















