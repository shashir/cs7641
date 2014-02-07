Lesson 4: Instance Based Learning
=================================

Instance based learning
-----------------------

Instance based learning distinguishes machine learning models which perform "lazy learning" at scoring-time directly from the training data. This is different from other machine learning models which lossily compress the training data into a simpler hypothesis function.

Some benefits

* Remembers all training data points.
* Fast for known points (lookup -- depending on properties of the data structure used to store).
* "Simple"

Some problems
* Overfits and generalizes badly
* Must handle conflicting training data

Since instance based learning often requires traversing the training data itself, it may be slow to score unknown inputs, but is easily adaptable to new data points.

