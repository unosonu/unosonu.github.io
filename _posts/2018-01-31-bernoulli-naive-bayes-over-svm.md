---
layout: post
title: Bernoulli naive bayes over svm for text classification
---

Why use bernoulli naive bayes over svm for text classification. Answer - they may give slightly better recall per class for small text. How small? Small like one sentence or few sentences. 

Let's list their advantages and disadvantages to know them better.

First about support vector machines. They are effective in high dimensional spaces. You know why! They are still effective in cases where number of dimensions is greater than the number of samples. They use a subset of training points in the decision function (called support vectors), so it is also memory efficient. They are versatile: different Kernel functions can be specified for the decision function. It is possible to write custom kernel. Another good post will be about how to identify if data points are linearly separable or not.

One of the problems with them is if the number of features is much greater than the number of samples, over-fitting in choosing Kernel functions should be avoided and regularization term becomes crucial.

Also SVMs do not directly provide probability estimates, these are calculated using an expensive five-fold cross-validation. Are they reliable? I don't know.

When it comes to multi-class classification, SVC and NuSVC implement the “one-against-one” approach (Knerr et al., 1990). On the other hand, LinearSVC implements “one-vs-the-rest” multi-class strategy. Note that the LinearSVC also implements an alternative multi-class strategy, the so-called multi-class SVM formulated by Crammer and Singer. This method is consistent, which is not true for one-vs-rest classification. 

In practice, one-vs-rest classification is usually preferred, since the results are mostly similar, but the runtime is significantly less.

Now about Naive bayes methods which apply bayes’ theorem with the “naive” assumption of independence between every pair of features.

The different naive Bayes classifiers differ mainly by the assumptions they make regarding the distribution of P(x_i \mid y).
They require a small amount of training data to estimate the necessary parameters.
Naive Bayes learners and classifiers can be extremely fast compared to more sophisticated methods. The decoupling of the class conditional feature distributions means that each distribution can be independently estimated as a one dimensional distribution. This in turn helps to alleviate problems stemming from the curse of dimensionality.

Till here we see that both svm and naive bayes are quite comparable.

Naive bayes is known to be a bad estimator, so the probability outputs are not to be taken too seriously. For this algorithm we know this for sure whereas it's possible for svm as well.

GaussianNB implements the Gaussian Naive Bayes algorithm for classification. The likelihood of the features is assumed to be Gaussian.

MultinomialNB implements the naive Bayes algorithm for multinomially distributed data, and is one of the two classic naive Bayes variants used in text classification (where the data are typically represented as word vector counts, although tf-idf vectors are also known to work well in practice). 

The smoothing priors alpha accounts for features not present in the learning samples and prevents zero probabilities in further computations. Setting alpha = 1 is called Laplace smoothing, while alpha < 1 is called Lidstone smoothing.

BernoulliNB implements the naive Bayes training and classification algorithms for data that is distributed according to multivariate Bernoulli distributions; i.e., there may be multiple features but each one is assumed to be a binary-valued (Bernoulli, boolean) variable. Therefore, this class requires samples to be represented as binary-valued feature vectors; if handed any other kind of data, a BernoulliNB instance may binarize its input (depending on the binarize parameter).

The decision rule for Bernoulli naive Bayes differs from multinomial NB’s rule in that it explicitly penalizes the non-occurrence of a feature i that is an indicator for class y, where the multinomial variant would simply ignore a non-occurring feature.

In the case of text classification, word occurrence vectors (rather than word count vectors) may be used to train and use this classifier. BernoulliNB might perform better on some datasets, especially those with shorter documents which is why this post.

Now just a short example of how to implement grid search in sklearn pipeline.


from sklearn.model_selection import GridSearchCV
parameters_svm = {'clf-svm__loss': ('hinge', 'log', 'modified_huber', 'squared_hinge', 'perceptron', 'squared_loss', 'huber', 				                  'epsilon_insensitive','squared_epsilon_insensitive'),
                  'clf-svm__alpha': (1e-2, 1e-3), 
                  'clf-svm__penalty':('l2', 'l1', 'elasticnet'),
                  'clf-svm__n_iter':[50] }

gs_clf_svm = GridSearchCV(text_clf_svm, parameters_svm, n_jobs=-1)
gs_clf_svm = gs_clf_svm.fit(xtrain, ytrain)

print gs_clf_svm.best_score_
gs_clf_svm.best_params_



__References__

http://scikit-learn.org/stable/modules/svm.html#svm-classification
http://scikit-learn.org/stable/modules/naive_bayes.html#bernoulli-naive-bayes



