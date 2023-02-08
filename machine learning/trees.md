
# Classification and Regression Tree

Also CART, is an algorithm for constructing an approximate optimal decision tree for given examples.

## Missing Data

When some features within an example are missing. In a Binary tree, when a feature is missing, the node that evaluate that feature will evaluate the next best feature computed during the training according to the gini impurity and will use this other feature to split on.

## Split point

A pair of feature and feature value which is assigned to a node in a decision tree. This split point will determine which examples will go left and which examples will go right based on the features and the features values.

## Gini impurity

Used as a way to determine the best split point for a given point in a classification tree. It's based on the probability of incorrectly classifying an item based on all of the items in the node.

## Surogate Split

A suboptimal split point reserved for examples which are missing the optimal split point feature.

## Mean Squared Error

The average squared difference between the prediction and the true label across all examples.

## Boosting

An ensamble technic which trains many weak learners sequentially, which each subsequent weak learner being trained on the previous weak learner's error. 

The final score is the sum of all tree scores.

## Bagging

Also bootstrap aggregation, a sampling technique which selects subsets of examples and/or features to train an ensamble of models. This generally reduce the variance error. 

The final score is the average of all tree scores.

## Weak Learner

SHallow decision trees in our case. However, it generally can be any underfitting model.

## Ensemble

Using more than one model to produce a single prediction

## Random Forest

AN ensemble technic which trains many independent weak learners. This generally reduce the variance error.
The subsample where each tree is trained, could be with relacement. Not all subset of the example space will be different for every tree.

## XGBoost

An open-source library which provide a gradient boosted framework. Short for extreme gradient boosting.

## LightGBM

An open source library created by Microsft which provides a distributed gradient boosted framework. Short for light gradient Boosted Models.

## Multi Class

In DTC we do the same thing but we now have three classes so the GIni impurity formula has one more term `(1-(p1^2-p2^2-p3^2))`.
ANd then the final decision node will take the decision depending on the majority or mode of elements of one particular class.

## Regression in DTC

Instead of the ginni impurity it uses the mean squared error of the split. And the average of examples tht have ended up in one node, it will be the value predicted for new examples.

## Categorical values in DTC

It create all subset of size 2 in the set (2^n subset) and split the node for each pair of subset. Caulcates the Gini IMpurity of each pair and select the best group pair of split.

## CART Downside

- Overfit easily: We can solve by limit the depth and then Boosting: `Tree1(Label(xi)) + Tree2(error(tree1)) + Tree3(error(tree2))`
