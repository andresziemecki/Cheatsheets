
# Support Vector Machines

The logistic regression gives you the probability of an example belonging to a particular class. But if we don-t care the probability and we want to correct classify it, here is where the support vector machines comes to play. 

Support vector machines try to create a decision boundary that classify the most two difficult examples. These two most difficult examples two classify are called "Support Vectors". 

In contrast the logistic regression minmize the log loss of the training example. SVM on the other hand only focus on these support vectors and try to maximuze the distances between the decision boundary and the support vectors.

The decision boundary of the SVM is made by an hyperplane `0=w*x-b`

The distance between the most closes example of each category to the decision boundary is called **margin**.

SVM are super sensitive to outliers training data, 
```
oooooo  |  xxxxxx -> decision boundary without outlier 
oooooo   o|xxxxxx -> decision boundary with outlier (low bias to the training data but high variance on new data)
```

If we want to avoid this sensitiveness we need to allow **missclassifications**. Number of missclassification is the balance of the trade off that we choose on variance/bias classification. 

When we allow missclassification, the distance between the observation and the threshold os called **Soft Margin**. We have as many soft margin as examples. TO determine the number of missclassifcation that we want to configure, we use cross-validation. When we choose one the threshold becomes the **Soft Margin Classificer**.

What happen if we have something like this: The correct amount of dosis we have to add to a patinet to cure it:

```
xx x x oooooo x xx x
```

SVC doesn't perform well on this type of data. There is when the SVM comes to play. 

So we can create a *y* axes with the square of the *x* axis and find a support vector classifier that could separate our data.

Why we use x^2 and not another function? Support vector machines has something called **kernel functions** that try to find relations in a higher dimension. So the process is to compute each par relation in different **d** dimensions and then compute the best kernel for our support vector classifier. (I'm not sure how use this relation pair of each example to compute to choose the kernel). To choose the correct d, we use cross-validation. 

So, you could imagine how bad this become when the data comes bigger and bigger. 

There are other complex things to study like the Radial Kernel, the Kernel Trick and so on. ( see the polynomial kernel and radial kernel of statquest video).

In summary, Support Vector Machines work by moving the data into a high dimensional space and find a relatvely support vector classifier that can effectively classify the observations.

## Support Vectors

The most difficult to separate points in regard to a decision boundary. They influence the location and orientation of the hyperplane.

## Margin

The space between the hyperplane and the support vectors. In the case of soft margin Support Vector Machines, this margin includes slack.

## Hyperplane

A decision boundary in any dimension. The SVM uses an hyperplane of dimension n-1 where n is the dimension of the dataset. 0-Dimension is a point, 1-Dimension is a line, 2-Dimension is a plane, 3+Dimension is a hyperplane.

## Norm

Here, the L2 Norm, is the square root of the sum of squares of each element in a vector

## Outlier 

A feature or group of features which vary significantly from other features

## Slack

The relaxing of the constrain that all examples must lie outside of the margin. This creates a soft-margin SVM.

## Hinge Loss

A loss function which is used by a soft-margin SVM

## Sub-gradient

The gradient of a non-differentiable function

## Non-Differentiable

A function which has kinks in which derivate is not defined.

## Convex function

Function with one optima

## Kernel Trick

THe process of finding the dot product of a high dimensional representation of feature without computing the high dimensional representation itself. A common kernel is the Radias Basis Function kernel.

