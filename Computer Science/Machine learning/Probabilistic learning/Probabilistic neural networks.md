A probabilistic [[Artificial neural networks]] (PNN) is a [[Artificial neural networks#Classical feedforwards neural networks|feedforwards network]], commonly used in classification and pattern recognition problems, where a parent probability distribution (pdf) of each supposed class (in the classification setting) is approximated using a [[Parzen-Kernel density estimators|kernel]] which is then used in conjunction with Bayes rule to classify new values. See [Wiki](https://en.wikipedia.org/wiki/Probabilistic_neural_network#cite_note-7), [Vijaysinh Lendave](https://analyticsindiamag.com/introduction-to-probabilistic-neural-networks-for-beginners/), [[@Specht_1990]], .


# Structure of PNNs
Much of the following is taken from [[@Samui_2020]] and [[@Specht_1990]] with the Skelton from the above sources.

Operations in a PNNs are organized into a multilayer network with the following breakdown: [Input]->[Pattern layer]->[Summation layer]->[Output]

## Input layer
The input layer consists of a set of neurons, each representing (associated with) a singular predictor variable (class) of the input vector, which is assumed to be a categorical random vector. Input data (fed into the neurons) is _standardized_ (according to the sample distribution) by subtracting the median and dividing the result by the interquartile range (see [[Random samples#^52c883|quantiles]]). 

## Pattern layer
Each class being modeled (from the training data) is associated with a neuron in the patter layer. The nodes in this layer store (calculate) their corresponding classes predictors variables in addition to the target values. In addition, each node is paired with a hidden node that calculate the distance (Euclidean) between the input value and the associated nodes distribution center, the standard deviation of this value is then used to apply the radial basis kernel function (see [Wiki](https://en.wikipedia.org/wiki/Radial_basis_function)) to (?).

## Summation layer
This layer consists of a collection of nodes representing the individual classes. Each nodes combines the values of the two paired nodes modeling a particular class from the pattern layer.

## Decision layer
The output layer compares the calculated scores (probabilities of class membership) from the summation nodes of each class to predict the target class.


# Algorithms 


# Applications


# Advantages and Limitations
PNNS have a few advantages over multilayer [[Perceptrons]] networks (i.e., classical feedforwards networks): PNNs are more robust to outliers in data, can generate predicted target probabilities (explainable), approach Bayes optimal classification results, and are very quick to train and perform reasonably even with very limited training data sets.

Unfortunately, PNNs suffer some performance limitations, namely requiring more memory space to store the model compared to the former while also taking more time to evaluate new input data (slow generalization performance as - unless I find otherwise - the training data must be held in storage as each new data point must be run through a series of computations involving the training data).