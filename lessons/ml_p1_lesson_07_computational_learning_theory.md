Computational Learning Theory
=============================

* Defining learning problems.
* Showing specific algorithms work.
* Show these problems are fundamentally hard.

Resources in machine learning
-----------------------------

* Time
* Space
* Training samples

Defining inductive learning
---------------------------

* Probability of successful training. 1 - \delta
* Number of training examples. m
* Complexity of hypothesis class. 
* Accuracy to which target concept is approximated. \epsilon
* Manner in which training examples presented. (especially matters in online training as opposed to batch)
* Manner in which training examples selected.

Selecting training examples
---------------------------

1. Learner asks questions from teacher.
2. Teacher gives examples to help learner.
3. Some natural fixed distribution.
4. Evil distribution.

Teaching via 20 questions
-------------------------

H -- set of possible people (ask the correct question)
X -- set of questions

* Teacher chooses only one question (he knows the right answer).
* Learner chooses log |H| questions.

Teacher with constrained queries
--------------------------------

H: Conjunction of literals or negation -- but not negation of conjunction? (find the right conjunction)
X: x1x2x3...xk k-bit input

To solve:
* Show what is irrelevant... two positive examples which are unperturbed by a changing feature.
* Show what is relevant... k negative examples which validate that perturbing a relevant feature matters.

Even though there are 3^k (positive, absent, negated) hypotheses, the smart teacher can ask k + 2 questions.

Learner with constrained queries
--------------------------------

H: Conjunction of literals or negation -- but not negation of conjunction? (find the right conjunction)
X: x1x2x3...xk k-bit input

Does not know the actual answer like the teacher does so does not know what the right training examples are.

Start enumerating every data point from 0,...,0 to 1,...,1 which is 2^k possibilities.

The first positive result helps us significantly.

Learner with mistake bounds
---------------------------

H: Conjunction of literals or negation -- but not negation of conjunction? (find the right conjunction)
X: x1x2x3...xk k-bit input

+ Input arrives
+ Learner guesses answer
+ Wrong answer **charged**
+ Go to 1.

1. Assume each feature positive and negated.
2. Given input, compute output.
3. If wrong, set all positive features that were 0 to absent, negative features that were 1 to abset. Go to (2).

Never make more than k + 1 mistakes.

Definitions
-----------

* Learner chooses examples
* Teacher chooses examples
* Nature chooses examples
* Mean teacher chooses examples

**Computational complexity** -- how much computational effort is needed for learner to "converge"
**Sample complexity* -- batch; how many training examples are needed for a learner to create a successful hypothesis
**Mistake bounds** -- online; how many misclassifications can a learner make over an infinite run?

Version spaces
--------------

True/target hypothesis: c in H
Candidate hypothesis: h in H
Training set: S subset of X
**Consistent learner** : produces h such that c(x) = h(x) for x in S (always produces a hypothesis that is consistent with data)
**Version space**: VS(S) = {h in H s.t. h is consistent with S} -- hypotheses consistent with examples

PAC learning -- error of h
--------------------------

Training error -- fraction of traning examples misclassified by h.
True error -- fraction of examples that would be misclassified on sample drawn from distribution D.

error_D(h) = Pr_{x from D}[c(x) != h(x)]

PAC learning
------------

* c -- concept class
* L -- learner
* H -- hypothesis space
* n -- |H|, size of hypothesis space
* D -- distribution over inputs
* 0  <= \epsilon <= 1/2    (our error goal)
* 0 <= \delta <= 1/2   (failure-probability -- certainty goal -- with probability 1 - \delta, must produce true error less than \epsilon)


PAC -- probably (1 - \delta) approximately (\epsilon) correct (error_D(h) = 0)!

"C is PAC-learnable by L using H iff learner L will with probability 1 - \delta, output a hypothesis h in H such that error_D(h) <= \epsilon in time and samples polynomial in 1/\epsilon, 1/\delta, and n.

Quiz: PAC-learnable
-------------------

C = H = {h_i(x) = x_i}  (k-bit inputs)

There are k hypotheses. So n = |H| = k.

Pick a hypothesis uniformly from VS(S, H).

\epsilon-exhausted version space
--------------------------------

VS(S) is \epsilon-exhausted iff for all h in VS(S), error_D(h) <= \epsilon

Every element in the version space has error less than epsilon.

Haussler Theorem -- bound true error
------------------------------------

Let error_D(h1,...,hk in H) > \epsilon   -- this is high true error.

How much data do we need to knock out these hypotheses?

Pr_{x from D}(h_i(x) = c(x)) <= 1 - \epsilon
Pr(h_i consistent with c on m examples) <= (1 - \epsilon)^m
Pr(at least one of h1,...,hk consistent with c on m examples) <= k(1 - \epsilon)^m <= |H|(1 - \epsilon)^m

Note that (1 - \epsilon)^m <= exp(\epsilon*m) (this comes from -\epsilon >= ln(1 - \epsilon))

So we have Pr(at least one of hypothesis is consistent with c on m examples) <= H*exp(-\epsilon*m) <= \delta

This is the upperbound that version space is **not** \epsilon-exhausted after m samples. We want \delta to be a bound on this.

ln |H| - \epsilon * m <= ln \delta
m >= 1/\epsilon (ln |H| + ln (1/\delta)) (i.e. polynomial)

Satisfying this will satisfy PAC-learnability.

Quiz: PAC-learnable example
---------------------------

H = {h_i(x) = x_i} (where x is 10-bits)
\epsilon = 0.1
\delta = 0.2
D: uniform

1/0.1 * (ln 10 + ln (1/0.2)) = 10*(ln 10 + ln 5) = 10*ln 50 = 39

This bound is agnostic to distribution of nature's data.

What we learned
---------------

* Teachers versus learners and interaction
  - What is learnable? Like complexity theory for ML.
* Sample complexity - data
* types of interactions:
  - learner picks questions
  - teacher picks questions
  - nature picks questions
  - evil teacher picks questions
* mistake bounds (as opposed to how many samples you need)
* PAC learning: version spaces, training/test/true error, distribution.
* m >= 1/\epsilon (ln |H| + ln (1/\delta)) (i.e. polynomial)
  - this assumed target in hypothesis
  - otherwise **agnostic** and the bound is slightly different, but still polynomial.
  - infinite hypothesis space can be a problem
