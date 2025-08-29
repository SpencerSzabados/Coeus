# Features and representation 
Fundamentally, what makes prediction without enumeration of all possible values from a observed sample possible is having some alternative form of _knowledge_ about the underlying population being drawn from. This is the role of [[Families of distributions|probability distributions]], a model of the population being considered that is believed to describe the primary features. This is a fundamental idea of statistics, [[Fundamentals of probability theory|probability theory]], in general. Within the domain of machine learning representation of observational characteristics, and therefore the [[Knowledge representation and features|representation of knowledge]], plays an important role in the algorithmic implementation and optimization of methods.

**Definition: (Feature)** In machine learning each component of an input (data point) vector $\vec{x}=(x_1,\dots,x_d)$ is called a _feature_.

Often feature vectors, $\vec{x}$, are considered to be given; however, their form and construction is important to consider, not only does their dimensionality have repercussions in terms of complexity (e.g,. size of search space) but it is often based on models that have underlying assumptions. Feature representations must first, at a population level, admit decision boundaries with low error rates; second, optimization of [[Supervised learning#^f14fbf|empirical risk]], in sample risk, should be efficient for the given form; and third, the choice of features also influence the generalization ability of the resulting model (i.e., how well the model performs on data outside the initial training data). 

Per [[@Hardt_2022]], there are few standard processes that measurements, and resulting features, are run though to meet the above considerations. First, the captured data (measurements) are turned into vectors thought a process called _data quantization and embedding_. Second, to highlight the most distinctive (principle) directions, the vectors are sorted relative to their similarity to a set of likely patterns (or one another), a process called _template matching_. Third, in an attempt to make the representation more robust and to standardize the dimension of the data, feature vectors are compressed into a low fixed dimension space via _histograms and counts_. Finally, in the case of working with linear predictors, _nonlinear liftings_ are used to enable linear predictors to approximate nonlinear decision boundaries.

The resulting feature vectors can be represented using a series, of features which result from application of each method in turn, of the form$$\vec{x}_{l+1} = \Phi(A_l\vec{x}_l+\vec{b}_l),$$with $l$ indexing the layer of the model. A representation that is similar to that of classical [[Artificial neural networks]], which shouldn't be surprising.

# Measurement
It is helpful to frame feature creation as measurement. Practitioners of machine learning should consult with experts on measurement within specific domains before creating ad-hoc measurement procedure; however, this does not appear to happen. This last point is especially important when measuring humans, e.g., [[Ethics of machine learning and statistics]].


# Quantization and embedding
The (ideal) goal of quantization is to discretize a continuous (or discrete) measurement into a form that can be efficiently stored within the bounds of the current environment, where it is later possible to reconstruct the original measurement perfectly. 

Embedding refers to converting high dimensional data into a lower dimensional representation. This is typically a lossy process. 


# Template matching
Discriminative tasks benefit from representations which express higher level patterns which might not be apparent in the original representation of the data. 

A popular way to extract these patterns is template matching, where a feature vector, $\vec{x}$, correlation to with a known pattern, $\vec{v}$, called a _template_, is measured. A new feature $\vec{x}'$ vector is created by combining this new correlation information with the original vector $\vec{x}$.

Some common types of templates used in pattern classification are Fourier transforms, Wavelet transforms, Convolutions, Downsampling and Pooling, Summarization methods, etc.


## Fourier transforms
One of the foundational patterns matched to spatial or temporal data is sinusoids, such as computing the magnitude of the [[Statistics/Signal Processing/Fourier transformation|Fourier transformation]] of a feature vector.

In particular, for a vector $\vec{x}\in\mathbb{R}^d$, consider the transformation with $k$-th component $$x'_k = |v_k^\intercal \vec{x}|.$$Where the $l$-th component of $v_k$ is given by $v_{kl} = e^{\frac{2\pi i\cdot kl}{d}}$. This transform measures the amount of oscillation in the vector at different modal frequencies.


## Convolution methods
Two spatial or temporal data points are often considered similar if we can translate one to align with the other. [[Convolution|Convolutions]] can be thought of as translating a template over a feature to measure the amount of similarity between feature and known pattern. The output of a convolution has component values indicating the amount of correlation with the template at each location in the vector. Multiple convolutions can be composed together to add to the discriminative power of the result.


## Summarization and histograms 
[[Histogram methods|historgrams]] summarize data by counting similar observations. 


## Downsampling or pooling
Downsampling is a method of summarizing and reducing dimensionality of data (or rather the amount of data) by locally average results together.


# Nonlinear predictors
One common method for constructing nonlinear predictors is to perform a nonlinear transform to the data, embedding it into a different higher dimensional space, where the construction of a nonlinear decision boundary in the original space reduces to a search for a linear decision boundary in the new space. Thereby allowing the use of results derived for linear predictors in the construction of nonlinear decision rules.


## Transformation (lift) methods

^6582bd

Linear decision rules are well understood and their methods of construction are equally developed; however, such simple decision rules are not always immediately applicable (have low accuracy) in situations where data separators might be more complex in form, e.g., polynomials etc. Thus, there exists various established techniques that can be used to embed (via nonlinear transformations called lifts) data (feature vectors) into spaces where linear separation, and therefore prediction, performs well. 


### How many features are required
Given an expressive enough function, we can always construct a lift function (transformation into a higher dimensional space) such that a particular dataset can be mapped into a desired set of labels. How high does the dimensionality of this lifted space need to be to obtain good results?

Suppose we are give the dataset $S=\{\vec{x_1},\dots,\vec{x_N}\}$ with each $\vec{x_i}\in\mathbb{R}^d$. Construct the $N$-by-$d$ matrix $X=[\vec{x_1}|\vec{x_2}|\dots|\vec{x_N}]$ of concatenated column feature vectors. The prediction results across the entire dataset can now be expressed as $\hat{\vec{y}}=X\vec{w}$. If all columns, $\vec{x_i}$, are linearly independent and $d\geq N$ (matrix isn't overdetermined), then any vector of predictions can be made by finding a corresponding vector $\vec{w}$; i.e., the system allows for arbitrary solutions.

Thus, in feature design, it is important to find lift functions that ensure $X$ has linearly independent columns. Moreover, models with more parameters than data points are often preferred in machine learning, so called _overparameterized systems_, as they admit solutions after fixing parameters; in addition to being likely to perform well using [[Gradient decent#Stochastic gradient descent|stochastic gradient descent]] optimization methods as mentioned in [[Empirical risk]].


### Limitations
Transformation based methods can suffer from the increase in dimensionality of the data that results from lifting the data into a higher dimensional space, since the number of mixing coefficients (weights) can grow exponentially, e.g., a polynomial decision boundary of degree $p$ in a $d$ dimensional space ($d>p$) has $\binom{d+p}{p}$ coefficients that need to be fitted. 


### Polynomial transforms
Polynomials are one of the most commonly used nonlinear predictors, see [[Curve fitting#Polynomial curve fitting]].

Fitting a quadratic polynomial to data can be viewed as fitting a linear function to the feature vector in a space with a basis of quadratic monomials $$\Phi_2^{poly}(\vec{x}) = (1,x_1,x_2,x_1^2,x_1x_2,x_2^2)^\intercal.$$
(Note here $\vec{x}$ is implicitly assumed to be a two component vector, otherwise, this would not be a valid lifting function.)

As quadratic function can be written as $\vec{w}^\intercal\Phi_2^{poly}(\vec{x})$ for some weight vector $\vec{w}$, the connection to optimization methods is clear. 

The map $\Phi_2^{poly}$ is known as a _lifting function_ that transforms a set of features into a more _expressive_ set of features (higher dimensional in this case). ^5f94d2

The features resulting from the quadratic polynomial lifting function can be expressed as the crossproducts of existing features. 

The associated (resulting) prediction function is a linear combination of pairwise products of features. 


### General basis function transforms
In general, we can write prediction functions are linear combinations of functions that form a basis, $\mathcal{B}=\{b_k\}$, of suitable dimension $D$, i.e., $$f(\vec{x}) = \sum_{k=1}^D \vec{w}_kb_k(\vec{x}).$$
In this case, the lifting function $\Phi_\mathcal{B}(\vec{x})$ maps into $D$ dimensions with the $k$-th component equal to $b_k(\vec{x})$ and the predictor is $f(\vec{x})=w^\intercal\Phi_\mathcal{B}(\vec{x})$.  


#### Random basis functions and features
A powerful means of choosing [[Knowledge representation and features#General basis function tranforms|basis functions]] for the use in nonlinear prediction and feature transformation (lifting) is by random selection.

Suppose we have a parametric family of basis functions $b(\vec{x},\theta)$, where $\theta$ is the parameter. A random [[Knowledge representation and features#^5f94d2|feature map]] $\Phi_{rf}$ is constructed by choosing random values $\Theta_1,\dots,\Theta_D$ from some distribution on $\Theta$ and setting $$\Phi_{rf}(\vec{x}) = \begin{bmatrix}b(\vec{x},\Theta_1)\\ b(\vec{x},\Theta_2)\\ \vdots\\ b(\vec{x},\Theta_D)\end{bmatrix}.$$The prediction function is then taken to be $$f(\vec{x}) = \sum_{i=1}^D w_ib(\vec{x},\theta_i) = w^\intercal \Phi_{rf}(\vec{x}).$$
This method allows for the approximation of complex functional behaviour due to the high probability of the random basis functions being linearly independent, so provided sufficiently many draws are taken it is possible to fit any set of desired labels.

The resulting prediction function resembles the classical formulation of a [[Artificial neural networks#^8b5b5d|neural network]] but here the parameters are chosen randomly and aren't the result of fitting to training data; that is, prediction functions built with random features can be considered as randomly wired neural networks. (A lot of recent, per [[@Hardt_2022]], theory around neural networks is based on connections between random maps and randomized initial conditions used for neural network training.)


##### Connection to kernel methods (machines)
Recall, any random feature map $\Phi_{rf}$ generates an empirical kernel, $\Phi_{rf}^\intercal\Phi_{rf}$, see [[Knowledge representation and features#^38edf1|feature kernel map]]. The expected value of this kernel can be associated with a [[Reproducing Kernel Hilbert Space]], $$\begin{align} E\left[\frac{1}{D}\Phi_{rf}(\vec{x})^\intercal\Phi_{rf}(\vec{z})\right] &= E\left[\frac{1}{D}\sum_{i=1}^D b(\vec{x},\Theta_i)b(\vec{z},\Theta_i)\right]\\ &= E\left[b(\vec{x},\Theta_1)b(\vec{z},\Theta_1) \right]\\ &=\int p(\Theta)b(\vec{x},\Theta)b(z,\Theta)\, d\Theta,\end{align}$$
where $p$ is the cdf associated with $\Theta$. The final integral is a kernel representation, and through choice of the integrands can result in various well studied distributions, .e.g., Gaussian.

This connection makes THE generalization properties of random features more approachable for analyse.


### Kernel methods
One method that attempts to avoid high dimensionality is to constrain the space of prediction function to lie in a low dimensional subspace, namely the span of the training data. This is the approach of [[Kernel machines|kernel machines (or kernel methods)]]. 
