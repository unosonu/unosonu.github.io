---
layout: post
title: Uncertainty and variance
---
This post explains my understanding of these concepts and why we are interested in these.

![double slit to the world]({{ site.baseurl }}/assets/img/double-window.jpg)

photo credit: [Double Slit](http://www.flickr.com/photos/39488690@N04/23314278599) via photopin [(license)](https://creativecommons.org/licenses/by-nc-nd/2.0/)

Certainty is of no use to us other than being boring. It's uncertainty we are interested in.
Is uncertainty similar to variance or is it opposite in meaning to that of variance. Is it in anyway related to variance?

To understand uncertainty to our use we need to understand how to measure it. An indirect measure is a quantity called entropy. This is a concept from information theory.

Entropy is defined as
Entropy(S) = Sigma(-p log p)


Think of the case of a biased dice. I have 6 possible outcomes(1,2,3,4,5,6) with respective probabilities of 1/8, 1/6, 1/8, 1/4, 1/4, 1/12. You can tell by looking at the probabilities to know which are the outcomes which are most uncertain to happen. Don't make a mistake that, what often can't happen(by looking at the probability) or when it comes to your personal interest if they happened once, they will not happen again and again in the next rolls (confirmation bias). To make uncertainty part more clear let me ask you what are the chances that 7 will appear in a dice roll. The answer is zero. Hence you can say again that "it is totally certain that 7 will not come in any dice roll". Similarly you can ask further question like how certain/uncertain is 2 in a dice roll. So probability can play a useful role in your life if you face too many occurrences of an event (this brings experience). At least so many that you can create an unbiased distribution out of it.

So how does the data in machine learning fits to the analogy of a dice. In a dataset again you can draw a distribution of occurrences. Now it becomes useful for you. For example you can know by looking at the distribution of features how probable they are for the outcome of our interest. How certain or uncertain they are. This forms the basic of decision trees rules. The more the feature is uncertain, it goes to more on the top of the decision trees and then while coming down to the leaves we also move towards more certain features.

The difference between the parent node’s entropy and the weighted sum of children nodes entropy is called information gain. It measures the expected reduction in entropy.

Intuitively, by gaining more information, we have reduced the uncertainty.

Now why is variance important for us and in what ways? We are interested in variance capture of results or the outcome based on inputs. We want to know how much an output varies based on one input or a combination of inputs in any way. This helps us know in concrete manner to know how the outcome varies after we have identified the variance of an input.

Variance tells us how important ( don't confuse this with variableImportance of random forests ) a
feature is for the outcome of our interest. Hence how much variance it covers. How much our outcome is dependent(varies) according to that feature.
This is measured in terms of percentage because we want to know it relative to the other features in the dataset.

Variance that we are interested in can be defined as:

Var(X) = E[(X-mean)^2]

or if thought of as covariance of a random variable with itself:

Var(X) = Cov(X,X)

So it is a measure of how much it varies from the mean significantly or nor-significantly. It doesn't mean the more a variable varies more it captures the variance of the outcome. For this purpose we see the covariance or correlation ( covariance in normalized manner ) .

In general
Cov(X,Y) = E[ (X-E[X]) (Y-E[Y]) ]

E is the expected value ( probability weighted average ) in the above formulas.

This helps in identifying the features or creating new features which have the highest variance and to see how much variance they capture alone. This way we can decide and identiry the minimum number of inputs for effective prediction. Also it helps to study further in what interesting ways these vary the outcome.
