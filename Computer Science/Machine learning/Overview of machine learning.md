Much of (modern 2000's) machine learning can be referred to, if only slightly backhandedly, as the algorithmic rediscovery of statistics with a focus on prediction opposed to inference. 


# Introduction
A machine learning algorithm having been run on a set _training data_ results in a function (or collection of functions) that, should, approximate the underlying relation between training data. The precise form the of the function is determined by this training phase, also known as the learning phase, and is depended on the input training data. The ability for the trained model to respond in a fashion appropriate to the chosen input and task given new input effectively is known as _generalization_. Due to practical limitations generalization is one of the central goals of machine learning methods. [[@Bishop_2006]]

There are two primary categories of machine learning problems (1) [[Classification and clustering|classification]] which deals with categorical data (labels), and (2) [[Supervised learning#Regression methods|regression]] which is the problem of trying to predict (or interpolate) continuous output (target) variables given a input variable .

In general data in machine learning is represented in the from $(x,f(x))$ where $x$ is some input value and $f$ a function that maps $x$ to the correct (exact) answer to the question being posed. When the output of $f$ is known but not its exact form (e.g., how to identify a car in a photo), it is the role of [[Supervised learning]] methods to derived an approximation of $f$. If very little is known of $f$ then [[Unsupervised learning]] methods may be used to attempt to extract the approximate underlying rules (approximate $f$) from the given data.


## Dimensionality and classification
[[Curve fitting]] and [[Regression methods]] are core to much of machine learning; in practical applications the data spaces dealt with are of high dimensionally comprising many (possibly independent) input variables. This poses some serious challenges in terms of the feasibility of training certain models, and thus, considerations must be made during the initial design of pattern recognition and [[Classification and clustering|classification]] ([[Classifiers]]) methods.


## Decision theory 
Suppose we are given an input vector $\vec{x}$ together with a corresponding vector $\vec{y}$ of target variables, and our goal is to predict a matched value $\vec{y'}$ to newly given input vector $\vec{x'}$. For [[Regression methods|regression]] problems, $y$ will comprise continuous variables, whereas for [[Classification and clustering]] problems $y$ will represent class labels. The [[Distribution functions of random variables#^fa2cbe|joint probability distribution]] $P(\vec{x},\vec{y})$ (i.e., $P(X=\vec{x}\cap Y=\vec{y})$) provides a complete summary of the uncertainty associated with these variables. We will see ideas of decision theory for a variety of problems.


## Feature extraction (pre-processing)
Input data is typically preprocessed into a vector composed of individual [[Knowledge representation and features|features]] (or attributes), that hopefully, simplifies the problem. This stage is sometimes called _feature extraction_, as it's goal is to make those features the algorithm will be operating on more "evident", or to speed up computation.

The methods for constructing such features can be programed by hand or done automatically (to an extent) via certain machine learning methods; e.g., [[Neural autoencoders]].


# Supervised learning 
In (predictive) [[Supervised learning]] the training data consist of a set of input vectors $x_0,\dots,x_N$ along with matched target values $f(x_i)$ called labels, that is, the training data takes the form of input-output pairs $(x_0,y_0),(x_1,y_1),\dots,(x_N,y_N)$, from which the goal is to learn a approximation of the function $f$, commonly denoted $h$ and called the _hypothesis_, between input and label outputs. [[@Murphy_2012]].


# Unsupervised learning
In [[Unsupervised learning]] (or descriptive learning) the training data is a set of input vectors $x_0,\dots,x_N$ without any matched target values, with the goal being to discover groups of similar examples within the data, a process called [[Classification and clustering|clustering]], or to determine the distribution of data within the given space, known as [[Density estimation]]; among other tasks. Unsupervised learning, per the name, ideally requires less _tailored_ data than supervised learning. [[@Murphy_2012]].


# Reinforcement learning
[[Reinforcement learning]] is concerned with finding actions to take in a presented situation that will maximize a given reward function. Here the learning algorithm is not given examples of optimal outputs, in contrast to supervised learning, but must instead discover them through an iterative or "evolutionary" process of rewarded behaviours or results. Reinforcement learning can be thought of as a hybrid approach between supervised and unsupervised learning.