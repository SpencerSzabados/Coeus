# Overview

# Linear regression
One of the simplest models (or methods) for performing [[Regression methods|regression analysis]] is to consider (assume) the target function to be a linear combination of input variables $$y(\vec{x},\vec{w}) = w_0 + w_1x_1 + \dots + w_dx_d+err,$$where $\vec{x} = (x_1,\dots,x_d)$ is an input vector and $\vec{w} = (w_0,w_1,\dots,w_d)$ at vector of coefficients (weights), and $err$ is the residual error which typically isn't written unless it is being analysed. The parameter $w_0$, called the _bias_, is a fixed offset in the data.

Given a data set of $N$ observations of $X=\{\vec{x}_1,\vec{x}_2,\dots,\vec{x}_N\}$ together with a set of corresponding observation values $Y=\{y_1,y_2,\dots,y_N\}$; that is, $\vec{x}_i$ results in $y_i$ by some unknown process (e.g., a function, probability distribution, etc.) for $i=1,2\dots,N$. Let $y(\vec{x})$ denote this desired underlying function with generated $Y$, in fact, suppose the addition of noise to the values of $Y$ so that $y_i = y(x_i)+\epsilon$, where $\epsilon$ represents noise in measurement which is typically assumed to be a standard normal distribution random variable; this assumption is made on large data sets due to the central limit theorem.

The object is then to determine optimal values for $\vec{w}$, values the best match the given data, with respect to some measure of error (a loss function) called $L$ whereby we obtain a function $y(\vec{x},\vec{w})\approx y(\vec{x})$; this last is typically chosen as the Euclidean distance. That is, we desire $$w^* = \arg\max_{\vec{w}}\sum_{i=1}^NL(y(\vec{x_i},\vec{w}),y_i).$$


## Linear basis function models 
Standard linear regression is quite limited, but it can be easily extended by considering a linear combination of fixed _basis functions_ (see [[Basis transformations]]) opposed to the direct input, namely $$y(\vec{x},\vec{w}) = w_0 + \sum_{i=1}^d w_i\phi_i(\vec{x}),$$where $\{\phi_1,\dots,\phi_d\}$ is a collection of know functions which are not necessarily linear. Inclusion of the _dummy basis function_ $\phi_0 = 1$ allows the above expression to be written more compactly as $$y(\vec{x},\vec{w}) = \vec{w}^\intercal \phi(\vec{x}),$$with $\phi = (\phi_0,\dots,\phi_d)$. ^6b2538

In the case of linear basis functions, the bias $w_0$ is used to compensate for the difference between the averages (over the training set) of target values and the weighted sum of the averages of the basis function values. See [[@Bishop_2006]].


### Bias-Variance (decomposition) tradeoff
The Bias-Variance tradeoff is a property that the variance of a estimated model parameter can be reduced by increasing the bias in the estimated parameters. This decision is in conflict with trying to simultaneously minimize sources of error resulting from variance and bias in the data.

Flexible models can be characterized by having low bias with high variance, whereas rigid models have high bias and low variance. The model with optimal predicative capability is often that is the most balanced between bias and variance.

The Bias-Variance decomposition is a way of analyzing a learning algorithms expected generalization error.

While this decomposition provides some interesting insights into the model complexity (from the standard frequentist perspective) it is of limited practical value as it is based on averages of different ensembles of data sets, where typically in practice only a single observed data set is given, with multiple independent data sets often being combined to reduce overfitting in the model in question rather than used independently.


### Polynomial models 
One of the more common choices for basis functions are the standard basis $\{1,x,x^2,\dots,x^d\}$ polynomials for a $d$-dimensional (univariant) polynomial; see [[Curve fitting#Polynomial curve fitting|polynomial curve fitting]].

A limitation of the standard polynomial basis functions is that they are global functions of the input variable, so changes in one region of the input space affects all other regions. This can be addressed by dividing the input space into separate regions and fitting different polynomial splines (that are joined) in each region.


### Higher-dimensional models
I some applications, we may want to predict $D>1$ target variables. This could be done by introducing different sets of basis functions for each component of $\vec{y}$ we are trying to model, giving multiple independent regression problems. However, a "more interesting", or at least more common in [[Overview of machine learning]] approach is to use the same set of basis functions to model all the components of the target vector, so that $$y(\vec{x},\vec{w}) = W^\intercal\phi(\vec{x})$$where $\vec{y}$ is a $D-dimensional column vector, $W$ is an $d\times D$ matrix of parameters, and $\phi(\vec{x})$ is an $d$-dimensional vector of elements $\phi_i(\vec{x})$, with $\phi_0(\vec{x})=1$. (p166)[[@Bishop_2006]]
## Connection to gaussian distribution 
We can connected linear regression models to the gaussian distribution by assuming the residual $err\sim \mathcal{N}(\mu,\sigma^2)$, and expressing the model as $$P(y|\vec{x},\theta) = \mathcal{N}(y|\mu(\vec{x}),\sigma^2(\vec{x})),$$where $\theta$ are the parameters of the model, this makes it clear the model is a conditional probability distribution. In the linear case, we have $\mu(\vec{x}) = \vec{w}^\intercal \vec{x}$ and the noise $\sigma^2$ is fixed; in which case, $\theta = (\vec{w},\sigma^2)$.


# Bayesian linear regression
In trying to avoid [[Curve fitting#^024b32|overfitting]] a model, as commonly occurs when using [[Maximum likelihood]] estimates, without setting aside a portion of our limited data set for verification/testing after modeling, we turn to [[Bayesian probability theory]].


## Parameter distribution 
Investigating the prior probability distribution over model parameters $\vec{w}$, with known precision $\kappa$ constant and [[Families of distributions#Gaussian Normal distribution|gaussian]] likelihood function. 

The conjugate prior is given by $$P(\vec{w}) = \mathcal{N}(\vec{w}|\mu,\Sigma)$$having mean $\mu$ and [[Expected values#^d4d0c3|covariance]] $\Sigma$. It then follows that that the posterior distribution is of the from $$P(\vec{w}|\vec{y}) 
= \mathcal{N}(\vec{w}|\mu^*,\Sigma^*)$$where $\mu^* = \Sigma^*(\Sigma^{-1}\mu+\kappa\Phi^\intercal \vec{y})$ and $(\Sigma^*)^{-1} = \Sigma^{-1}+\kappa\Phi^\intercal\Phi$. 

Due to the posterior being normal the maximum posterior weight vector is given directly as $\vec{w}^* = \mu^*$. Moreover, if we consider a infinitely broad prior $\Sigma = \alpha^{-1}I$ with $\alpha \to 0$, the mean $\mu^*$ of the posterior distribution reduces to the maximum likelihood value, $\vec{w}^* = (\Phi^\intercal\Phi)^{-1}\phi^\intercal\vec{y}$, given by the normal equations for least squares.

