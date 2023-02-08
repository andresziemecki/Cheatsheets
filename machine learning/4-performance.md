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

Also recall, it's the proportion of true positive which are correctly classified.

## Specificity

The proportion of true negatives which are correctly classified. `TN/(TN+FP)

## Precision

The number of true positives divided by the true positives plus false positives.

## F1-Score

The harmonic mean of the precision and recall `(pre*rec)/(prec+rec)`

## Validation

The technic of holding out some portion of examples to be tested separately from the set of examples used to train the model

## Generilize

The ability of the model to perform well on the test set as well as examples beyond the test set.

## Recivier Operator Characteristic Curve

Also ROC curve, is a plot of how the specificity and sensitivity change as the decision threshold change. The area under the ROC curve, or AUC, is the probability that a random chosen positive example will have a higher prediction probability of being positive than a random chosen negative example.

## Hyperparameter 

Any parameter associated with a model which is not learned.