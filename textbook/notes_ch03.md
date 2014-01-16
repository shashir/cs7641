Chapter 3: Decision tree learning
=================================


3.1-3.2 Decision tree representation
------------------------------------

The usage of decision trees as classifiers is obvious. Given an
instance, the machine starts at the root node. At each node of the tree,
the machine tests the value of some attribute of the instance and
accordingly directs the machine to the next node until the machine
arrives at a leaf node. The value of the leaf node is emitted as the
final classification.

*Each path from the tree root to a leaf corresponds to a conjunction of
attribute tests, and the tree itself to a disjunction of these
conjunctions.* Since the conjunctions are mutually exclusive, this
disjunction can actually be an exclusive disjunction (XOR).

3.3 Appropriate problems for decision tree learning
---------------------------------------------------

-   *Instances are represented by attribute-value pairs.*

-   *The target function has discrete output values.*

-   *Disjunctive descriptions may be required.* This makes decision
    trees highly interpretable.

-   *The training data may contain errors.*

-   *The training data may contain missing attribute values.*

The basic decision tree learning algorithm
------------------------------------------

ID3 (or *this* variation) is a recursive algorithm that passes through
all the instances and their attributes to find the attribute which best
classifies the data by itself. Then at each descendent node, the process
is repeated sans the previously considered attributed. Eventually, all
attributes will be considered and the algorithm is guaranteed to halt.

The *best* attribute at each iteration is the one that maximizes
*information gain*. Information gain depends on *entropy*. Let’s define
entropy of a set $S$ contains values $i$ with frequency $p_i$ (idealized
probabilities).

$$Entropy(S) = - \sum p_i \log p_i = -\log \prod_i p_i^{p_i}$$

Entropy can be interpreted as the expected number of bits required to
optimally encode stream of values $i$. (Confirm.)

The following is an adaptation of the ID3 algorithm.

$ID3(EXAMPLES, TARGET, ATTRIBUTES)$ //

-   Add $ROOT$ node to $TREE$.

-   If all elements are positive, label $ROOT$ node $+$ and return
    $TREE$.

-   Else if all elements are negative, label $ROOT$ node $-$ and return
    $TREE$.

-   Else if $ATTRIBUTES$ is empty, label $ROOT$ node as the most common
    $TARGET$ attribute values and return $TREE$.

-   Else

    -   A \<– the attribute from $ATTRIBUTES$ that best classifies
        $EXAMPLES$.

    -   The decision attribute for Root \<– A


