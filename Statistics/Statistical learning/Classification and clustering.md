
Classification is the task of identifying, with a probable certainty, which of a given set of categories, $C_1,\dots,C_N$, (sub-populations) a observation, $x$, drawn from an underlying distribution belongs to. With the decision being often based on previously gathered data about elements of each class. Classification (methods) decisions are made by [[Classifiers]], which are concrete implementations of rules for classification; often in the form of an algorithmic procedure or function.

Clustering, on the other hand, is the task of _grouping_ a given set of objects $x_1,\dots,x_N$ in such a way that objects in the same group (called a cluster) are more similar (in some sense) to each other than to those in other groups. 

The differences between the topics of classification and clustering are based on the context of the method being used; classification methods partition the sample space completely (or nearly so) while clustering methods are only concerned with the given set of elements. In the context of machine learning, classification is often seen as a [[Overview of machine learning#Supervised learning|supervised learning]] problem with clustering considered a [[Overview of machine learning#Unsupervised learning|unsupervised learning]] problem.


# Classification
**Problem: (Classification)** In a classification problem we are given $K$ possible classes $C_1,\dots,C_K$, often called labels, with the goal of mapping any particular input $\vec{x}$ drawn from an underlying sample space $\mathcal{X}$ to its respective class with some degree of certainty.  We wish to construct a method, a rule, for the assignment of $\vec{x}$ that maximizes some optimality criteria. Such a rule will divide the sample space into regions, $R_1,\dots,R_K$, called _decision regions_, associated with each class, such that all points within $R_i$ are assigned to $C_i$; these regions might not be contiguous, but could be interrupted by other regions. The boundaries between the regions are called _decision boundaries_ or _decision surfaces (in higher dimensions)_. 

When the number of classes equals two, this is called _binary classification_. Likewise, if the number of classes is greater than two, the classification problem is known as _multiclass classification_. If the class labels are not mutually exclusive (an object can belong to multiple classes) the problem is called _multi-label classification_, and is best viewed as predicting multiple related binary classes for each object. See [[@Murphy_2012]], [[@Mortier_2021]].


## Subvariants of classification
There are various subtypes of classification problems, each with various methods of treatment and computational efficiency.

### Multi-label classification
[[Multi-label classification]]


### Set-valued (multi-set) classification

^700a8d

Set-valued classification is an extension of regular (or also called _precise_) classification where objects can be assigned collections (sets) of classes opposed to just a singular class. This form of classification is useful in situations where the penalty for misclassification is high but it is still preferable to receive an output opposed to rejecting to classify in the face of too much uncertainty (or when there are problem relating to outlier detection in data which cannot be classified).

This form of classification can be seen as method of modeling uncertainty in multi-class classification, making predictions in the face of aleatoric uncertainty which originates from noise in the sample data predictions are based (trained) on.

**Problem: (Set-valued classification)** Suppose we are given $K$ possible classes $C_1,\dots,C_K$, which comprise all categories a input $\vec{x}$ drawn from an underlying sample space $\mathcal{X}$ might belong. It is the problem of set-valued classification to construct a method, a rule, for the assignment of $\vec{x}$ to a collection of sets (possibly a hierarchy of subsets) that maximizes some optimality criteria; that is, we wish to construct a rule of the from $f:\mathcal{X}\to\mathcal{P}\{C_1,\dots,C_K\}$. The size of the collection assigned to a given element expressed, in some way, the uncertainty or confidence in the assignment to individual elements. See [[@Ha_1997]], [[@Tong_2021]], [[@Mortier_2021]].


## Classification methods
Suppose we have a training set $X=\{x_1,x_2,\dots,x_N\}$ and we are trying to learn the rule associated with classes $C_1,\dots,C_m$. We want to build a [[Classifiers|classifier]] (ML) that is based on our training data and can classify new values accurately. 

### MAP estimate
For a selected model (architecture) trained on the data from $X$, the most probable class label estimate for a new input $x$ is $$\hat{Y} = \hat{f}(x) = \arg\max_{C_1,\dots,C_m}P(Y=C|x,X),$$where $P(Y|x,X)$ is the probably distribution given $x$ and $X$ which is implicitly conditioned on the model $A$ as the true probabilities are typically not known. 


### Nearest-neighbours methods
![[Nearest-neighbour methods]]


# Clustering 
**Problem: (Clustering)** In clustering we are given a set of unlabeled data $X=\{x_1,\dots,x_N\}$ with the goal of grouping (labeling or moving) data into $K$ different groups (the true value of $K$ is not known) such that the difference between data points within any group is less than that for data points between clusters.

Thus, the primary goal in clustering is to estimate the distribution (of the number of clusters comprising the data) $P(K|X)$ over the number of clusters, this is known as the model selection problem. The labels (characteristics) of a cluster are _hidden_ (or [[Random variables#^b42b34|latent]]) variables as they are only inferred from the data. The second goal is then to assign data points to individual clusters. 

## Clustering methods 
### MAP estimate
For simplicity the distribution $P(K|X)$ is often estimated using its mode, $$K^* = \arg\max_K P(K|X),$$with clusters assigned to data points using the same MAP rule as for [[Classification and clustering#Classification|classification]] $$\hat{Y} = \arg\max_{C_1,\dots,C_K} P(Y=C|x,X).$$

### k-means clustering 
![[k-means clustering]]


