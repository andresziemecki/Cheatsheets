# Performance

## Decision Point

Also decision rule or threshold, is a cut-off point in which anything below the cutoff is determined to be a certain class and anything above the cut-off is the other class.

## Accuracy

The number of true positives plus the number of true negatives divided by the total number of examples.

## Unbalanced classes

When one class is far more frequently observed than another class.

## Model Training

Determining the model parameter values

## Confusion Matrix

In the binary case, is a 2x2 matrix indicating the number of:

- True Positive: We score positive and was OK
- True Negatives: We score negative and it was OK
- False Positives: We score poitives and it was wrong
- False Negatives: We score negative and it was wrong.

## Sensitivity

Also recall, it's the proportion of true positive which are correctly classified. `TP/(TP+FN)`

You can see it as the true positive rate in the left quadrant of the diagram that you know
## Specificity

The proportion of true negatives which are correctly classified. `TN/(TN+FP)`

You can see it as the true negative rate in the right quadrant of the diagram that you know

## Precision

The number of true positives divided by the true positives plus false positives.

## F1-Score

The harmonic mean of the precision and recall `2(pre*rec)/(prec+rec)` == `2(pre*sensitivity)/(prec+sensitivy)` 

## Validation

The technic of holding out some portion of examples to be tested separately from the set of examples used to train the model

## Generilize

The ability of the model to perform well on the test set as well as examples beyond the test set.

## Recivier Operator Characteristic Curve (ROC)

Also ROC curve, is a plot of how the specificity and sensitivity change as the decision threshold change. The area under the ROC curve, or AUC, is the probability that a random chosen positive example will have a higher prediction probability of being positive than a random chosen negative example.

A better explaination you can find [here](https://developers.google.com/machine-learning/crash-course/classification/roc-and-auc?hl=es-419)

It is a curve of type: `Sensitivity vs (1 - Specificity)` 

## Hyperparameter 

Any parameter associated with a model which is not learned.

## Dataset Splitting

Training/Validation - Test Set

## Croos- validation
- k fold
- Leave one out (k=N)

## In supervise Learning we do the following

1. Identify a problem
2. Make an Hypothesis (if we create some sort of rule that decrease the degree of the problem)
3. Simple Herustic
4. Measure Impact
5. More Complex Technic
6. Measure Impact
7. Tune the model
8. Model replace the existing technic