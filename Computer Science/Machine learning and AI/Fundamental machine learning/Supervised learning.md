---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - machine_learning
  - supervised_learning
  - summary
references:
  - "[[@Hardt_2022]]"
---
---

The general task of supervised learning is to learn good method of prediction (or inference) to questions by way of provided examples.

Theoretically optimal predictors (see [[Fundamentals of prediction]]) require exact knowledge of the probability distributions for the classes being predicted, information that is likely not known in practicality, thus we must make assumptions on the data considered (e.g., is this temperature data etc); this is referred to as "no-free-lunch". [[Supervised learning]] theory (or more generally [[PAC-learning]]) attempts to algorithmically use known sample data consisting of labeled entries to build _good_ predictors. 

More specifically, in the problem setting, the only knowledge of the underlying population distribution at our disposal is likely to be previously observed data consisting of (finite) $N$ labeled instances $(x_1,y_1),\dots,(x_N,y_N)$ of correctly matched pairs, which are, typically, assumed to have been independently drawn from the same underlying distribution of $(X,Y)\sim f_{X,Y}$. The notion of supervision in the construction of predictors refers to the availability of previously correctly identified labels. Supervised learning is therefor the task of construct a good predictor by considering an optimization problem, the most common approach being [[Empirical risk#Empirical risk minimization|empirical risk minimization]], involving said data points.

Considerations of assumptions on sampling are difficult in practice, and can strongly affect the performance and application of statistical estimators and the validity of what can be confidently learned from data. These issues are often ignored for the most part in learning theory, instead focus is placed on the solving secondary problems.


# Classification and prediction
The simplest form of prediction is binary prediction (i.e., binary [[Classification and clustering|classification]]) which involves only two classes, a topic discussed throughout [[@Hardt_2022]]. If the number of classes is greater than two, this is called _multiclass classification_

There are two primary stages in classification problems 1) the inference stage in which training data is used learn (fit) a model $P(C_i|\vec{x})$, and 2) the subsequent decision stage in which the posterior probabilities are used to make optimal class assignments. 


## Optimization criteria
### Minimizing misclassification rate
Given a classification problem of assigning one of the classes $C_1,\dots,C_N$ to any particular input $\vec{x}$; or vise versa. We wish to construct a method, a rule, for the assignment of $\vec{x}$ that produces a minimal amount of misclassifications when considering multiple inputs; where misclassification is determined using some know external information about the classes which any particular element truly belongs to. Such a rule will divide the sample space into regions, $R_1,\dots,R_N$, called _decision regions_, associated to certain classes, such that all points within $R_i$ are assigned to $C_i$; these regions might not be contiguous, but could be interrupted by other regions. The boundaries between the regions are called _decision boundaries_ or _decision surfaces (in higher dimensions)_. 

Particularly, we which to minimize the quantity $$\begin{align} P(mistake) &= \sum_{i=1}^N\sum_{j\neq i}^N P(\vec{x}\in R_i,C_j)\\ &=\sum_{i=1}^N\int_{R_i}\sum_{j\neq i}^N P(\vec{x},C_j)\,d\vec{x}.\end{align}$$We should arrange $R_1,\dots,R_N$ such that each $\vec{x}$ is assigned to whichever class $C_i$ has the highest joint probability $P(\vec{x},C_i)$ value. To put it another way, since $P(\vec{x},C_i) = P(C_i|\vec{x})P(\vec{x})$ we can make our selection of $C_i$ for any given $\vec{x}$ based on whichever maximizes $P(C_i|\vec{x})$. Alternatively, to show the equivalence, it is often more feasible to maximize the probability of being correct, which is given as $$P(correct) = \sum_{i=1}^N \int_{R_i}P(\vec{x},C_i)\,d\vec{x}.$$
#### The reject option
In some applications it will be appropriate to avoid making decisions when there is sufficient uncertainty between the different joint probabilities for the possible classes $P(\vec{x},C_i)$. This can be achieved by introducing a threshold $\theta$, and rejecting classifications of $\vec{x}$ values which the largest of the posterior probabilities $P(C_i|\vec{x})$ is less than or equal to $\theta$. The rejection region can be tuned to minimize the expected loss, when a loss matrix is given, taking account of the loss incurred when a reject decision is made. 


### Minimizing expected loss (risk)
For many applications the objective is more complicated than minimizing the number of [[Supervised learning#Minimizing misclassification rate|misclassifications]]. Depending on the problem certain outcomes may be more desirable than others, taking a higher weight, e.g., in diagnosing someone with a particular illness the consequences of misreporting the person is heathy has greater risk than biasing results to report they are sick and to order more testing for confirmation. This idea, is formalized using what is called a [[Point estimation#^45314f|loss function]] (or _negatory a utility function_) which we seek to minimize for any particular problem and solution method. 

Again for a given classification problem of assigning one of the classes $C_1,\dots,C_N$ to any given input $\vec{x}$. We can define a loss matrix $L$ whose elements $L_{ij}$ correspond to some incurred loss from incorrectly matching element $\vec{x}$ belonging to class $C_i$ to class $C_j$ instead. The optimal assignment rule being that which minimizes the loss function. However, as the true classes of inputs $\vec{x}$ outside the initial data set are not known, we instead attempt to minimize the average loss, the expected loss, by using the joint probability distribution $P(\vec{x},C_i)$; particularly, we seek to minimize $$E[L] = \sum_{i=1}^N\sum_{j}\int_{R_j}L_{ij}P(\vec{x},C_i)\,d\vec{x},$$by choosing regions $R_1,\dots,R_N$ appropriately or rather by constructing the underlying decision rule accordingly. To this effect, we want to minimize $\sum_{i=1}^N L_{ij}P(\vec{x},C_i)$ or equivalently by the product rule $\sum_{i=1}^N L_{ij}P(C_i|\vec{x})$; that is, the decision rule that minimizes $E[L]$ is the one that assigns each new $\vec{x}$ to $C_j$ such that $\sum_{i=1}^N L_{ij}P(C_i|\vec{x})$ is minimized.


#### Minimizing empirical risk
Under binary prediction the problem of minimizing [[Point estimation#^1832d6|risk]], which is the expected value of a [[Point estimation#^45314f|loss function]], reduces to specifying a cost to each of the four possible pairs of labels corresponding to true positives, false positives, true negatives, and false negatives.


#### Representations and optimization 
In order to attempt to solve the optimization problem of [[Empirical risk#Empirical risk minimization|empirical risk minimization]], with the additional constringent of obtaining a good [[Empirical risk#^0b48ca|generalization gap]], we must settle on the class (representation) of functions being considered, as well as the choice of a loss function, see [[Knowledge representation and features]].


## Regression methods 
The problem of trying to predict (or interpolate) continuous output (target) variables given a input variable is called regression, see [[Regression methods]], and is considered a problem in supervised learning. 

Given a _training set_ of $N$ input _features_ (observations) $x_1,\dots,x_N$ for which the corresponding outputs $y_1,\dots,y_N$ are known, we wish to construct a _model_, a function $y:X\to Y$, that represents the relationship between the given $x_i$ and $y_i$. We utilize a _loss_ (also called a _cost_ or _objective_) function to indicate how well (accurate) our model approximates the supplied training examples.

The three most important questions for performing regression analysis on a given problem set are:
  1. What is a effective parameterization of the model?
  2. What loss (objective) function should be used?
  3. What type of optimization should be used to fit the unseen function? This is known as _generalization_. 
Simple models typically do not fit the sample data exactly, as they might not be able to account for all data targets. You may also need to consider the effects of noise in the collected data (e.g., Imprecision in the collected data, Errors in data targets and labels, etc...) when it comes to accessing the quality of a models fit. 
