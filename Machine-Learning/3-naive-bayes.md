# Naive Bayes

In the machine-learning world, naive bayes are probabilistic **classification** algorithms based on Baye's theorem (describes the probability of an event, based on prior knowledge of conditions that might be related to the event).

`P(A/B) = P(A^B)/P(B) = P(B/A)*P(A)/P(B)`

## Model

An approximation of a relationship between an input and an output.

## Huristic

An approach to finding a solution which is typically faster but less accurate than some optimal solution.

## Bernoulli Distribution

A distribution which evaluates a particular outcome as binary. In the Bernulli Naive Bayes classifier case, a word was either in a message or not in a message, which is binary representation.

In probability theory and statistics, the Bernoulli distribution, is the discrete probability distribution of a random variable which takes the value 1 with probability *p* and the value 0 with probability *q=1-p*. Less formally, it can be thought of as a model for the set of possible outcomes of any single experiment that asks a yes–no question. Such questions lead to outcomes that are boolean-valued: a single bit whose value is success/yes/true/one with probability *p* and failure/no/false/zero with probability *q*. It can be used to represent a (possibly biased) coin toss where 1 and 0 would represent "heads" and "tails", respectively, and p would be the probability of the coin landing on heads (or vice versa where 1 would represent tails and p would be the probability of tails). In particular, unfair coins would have a distinct p of 0.5.

The Bernoulli distribution is a special case of the binomial distribution where a single trial is conducted (so *n* would be 1 for such a binomial distribution). It is also a special case of the two-point distribution, for which the possible outcomes need not be 0 and 1.

Bernulli Distribution in [Wikipedia](https://en.wikipedia.org/wiki/Bernoulli_distribution)

Which is a special case of the binomial distribution, also [here in wikipedia](https://en.wikipedia.org/wiki/Binomial_distribution)

## Binomial Distribution

In probability theory and statistics, the binomial distribution with parameters *n* and *p* is the discrete probability distribution of the number of successes in a sequence of *n* independent experiments, each asking a yes–no question, and each with its own Boolean-valued outcome: success (with probability p) or failure (with probability *q=1-p*). A single success/failure experiment is also called a Bernoulli trial or Bernoulli experiment, and a sequence of outcomes is called a Bernoulli process; for a single trial, i.e., n = 1, the binomial distribution is a Bernoulli distribution. The binomial distribution is the basis for the popular binomial test of statistical significance.

The binomial distribution is frequently used to model the number of successes in a sample of size n drawn with replacement from a population of size N. If the sampling is carried out without replacement, the draws are not independent and so the resulting distribution is a hypergeometric distribution, not a binomial one. However, for N much larger than n, the binomial distribution remains a good approximation, and is widely used.

The probability of getting exactly *k* successes in *n* independent Bernoulli trials is given by the probability mass function:

`(n k)*p^k*(1-p)^(n-k)`

where `(n k)` is the binomial coefficient `n!/(k!(n-k)!)`

the k successes can occur anywhere among the n trials, and there are `n!/(k!(n-k)!)` different ways of distributing k successes in a sequence of n trials.

The expected value `E[x]` is `n*p` and `Var(X)` is `n*p*(1-p)`

This similarly follows from the fact that the variance of a sum of independent random variables is the sum of the variances.

## Prior

Indicates the probability of a particular class regardless of the features of some examples. For example, the probability of Spam is 

`total spam / total messages`

Doesn-t care about the words inside of the mssage.

## Likelihood

THe probability of some features given a particular class. What's the probability of having these words given the message being spam? and What's the probability of having these words given the message being not-spam?

## Evidance

The denominator of the Naive Bayes classifier

## Posterior

The probability of a class given some features. For example, the resolution of the entire model in Naive Bayes will be the posterior.

## Vocabulary

THe list of words that the Naive Bayes classifier recognize.

## Laplace Smoothing

A type of additive smoothing which mitigates the chance of encountering zero probabilities within the Naive Bayes classifier. It is applied to all probabilities and not only to those that are zero. So if we have a word that have never been in a spam message. The probability of a new message being spam given that word, it's 0 but with laplace smoothing will be 1/2 since we add 1 in the numerator and 2 in the denominator. 

## Tokenization

The splitting of some raw textual input into individual words of elements. Like splitting a sentnces betwee words.

## Featurization

The process of transforming raw inputs into something a model can perform training and predictions on.

## Vectorizer

Used in a step of featurizing. It transform some inputs into something else. One example is a binary vectorizer which transform tokenized messages into a binary vector indicating which items in the vocabulary apperas in the message. `['a', 'hey'] =>[1,0,0,1]`

## Stop Word

A word, typically discarded, which doesn't add much predictive value.

## Stemming

Removing the ending modifiers of a word, leaving the stem of a word.

## Lemmatization

A more calculated form of stemming which ensure the proper lemma results from removing the words modifiers.
For example, Studying and studies with Stemming will be Study and Studi, with Lemmatization will remains the same "Study" for both.

## Lowercasing

Put all words in lowercase has some disavantaje because we can loose Names.


# Decision Trees

A tree-base model which traverse examples down to leaf nodes by properties of the examples features.

## Sample Size

The number of examples taken from a complete population