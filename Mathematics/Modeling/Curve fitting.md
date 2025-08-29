# Overview
This note contains information on summary curve fitting (modeling) methods.

For the remainder, suppose we are given a data set of $N$ observations of $X=\{x_1,x_2,\dots,x_N\}$ together with a set of corresponding values $Y=\{y_1,y_2,\dots,y_N\}$; that is, $x_i$ results in $y_i$ by some unknown process (e.g., a function, probability distribution, etc.) for $i=1,2\dots,N$. Let $y(x)$ denote this desired underlying function, and assume $Y$ is generated according to the rule $y_i = y(x_i)+\epsilon$, where $\epsilon$ represents noise in measurement which is, typically, assumed to follow a standard normal distribution with precision (inverse variance) $\kappa = 1/\sigma^2$.


# Polynomial curve fitting 
Polynomial curve fitting seeks to find a approximator of $y(x)$ in the form of a polynomial, $$y(x,\vec{w}) = \sum_{i=0}^dw_ix^i$$with fixed coefficients of $\vec{w} = (w_0,w_1,\dots,w_d)$ called weights. Polynomials models, as outlined, can be treated as a [[Linear regression#Linear basis function models|Linear basis function model]].

The particular coefficients of $\vec{w}$ chosen are typically determined by attempting to optimize some measure of the error, $err(\cdot)$, between matched pairs of $Y=\{y_1,\dots,y_N\}$ and $\{y(x_1,\vec{w}),y(x_2,\vec{w}),\dots, y(x_N,\vec{w})\}$, a process called _fitting_ the curve. The exact measure of the error used varies depending on the problem considered, and the desired properties.

The selection of $d$ is an important factor in the efficacy of the model, a concept called _model comparison_ or _model selection_. Low $d$ values may not be cable of adequately capturing "high frequency" information within the data leading to large error after fitting, called _underfitting_, with poor inferencing and prediction capabilities. Likewise, high values of $d$ might accurately fit all the given data points, but oscillate wildly between points; thereby, producing interpolated results that are inconsistent with expectations, a result called _overfitting_, where the model begins to capture noise within the data. Thus a good balance must be struck between the two extremes, based on the expected behaviour of the process from which the data is pulled (e.g., do you expect to see a linear relationship for the selected data, etc.). A number of quality of fit tests exist in an attempt to quantify the quality of fit between a model with parameters $d$ and $\vec{w}$ and the sample data, so that the modeler can aim to improve their results, see [[Regression methods#Goodness-of-fit tests]].  ^024b32


## Multidimensional polynomial curve fitting 
Fitting higher dimensional polynomials of multiple independent variables is done as follows. 

If we have $D$ input variables (D-dimensional space) and desire a degree $d$ multivariant polynomial (sum of degrees), a standard option is the multivariate polynomial that is of degree one in each input variable, $$y(\vec{x},W) = w_0 + \sum_{i=1}^Dw_ix_i + \sum_{i_1=1}^D\sum_{i_2=1}^Dw_{i_1i_2}x_{i_1}x_{i_2} + \cdots + \sum_{i_1=1}^D\cdots\sum_{i_d=1}^Dw_{i_1\cdots i_d}x_{i_1}\cdots x_{i_d}$$ where $W$ is a $D^d$ matrix of coefficients.


## Model (degree) selection
In any realistic situation the supply of data for training (fitting) and validation is limited, thus to build good models, as much of the data should be used as possible during fitment; as we cannot afford to reserve a subset of the data for later validation (generalization performance) testing as it would be better used during fitment.

### Cross validation
The method of cross validation uses multiple stages and a proportion of the data for training, while managing to use the entire data set to access performance afterwards. 


# Error functions
Some of the most common error functions (or in machine learning [[Point estimation#^45314f|loss functions]] as used in [[Empirical risk#Empirical risk minimization|empirical risk minimization]]) are the following:

**Definition: (Least squares error)** The _least squares error_ is equal to $$err(\vec{w}) = \frac{1}{N}\sum_{i=1}^N(y(x_i,\vec{w})-y_i)^2,$$and is also called the _sum-of-squares error_ or minimum [[Point estimation#^c8b7fb|mean squared error]]. As the sum-of-squares error is continuously differentiable and quadratic in terms of elements from $\vec{w}$ it is guaranteed to have a unique minimizer. 


# Fitting coefficients 
## Regularization
One common method used in attempting to avoid overfitting is called _regularization_, which incorporates a penalty term to the error function in order to bias the coefficients $\vec{w}$ towards smaller values; putting this another way, regularization allows complex models to be trained with _limited_ data sets without severe over-fitting, by essentially limiting the expression of model complexity by the supporting data.

Such techniques are called _shrinkage methods_ in statistics, see [[Regression methods]], or _weight decay_ in the context of [[Artificial neural networks]] and [[Overview of machine learning]], because in sequential learning algorithms it encourages weights to decay towards zero unless supported by data observation (biased to optimization functions within the span of the data).  

**Definition: (Regularized least squares error)** A simple regularized least squares error is, $$err_R(\vec{w}) =  \frac{1}{N}\sum_{i=1}^N(y(x_i,\vec{w})-y_i)^2 + \lambda\|\vec{w}\|^2 ,$$where the coefficient $\lambda$ governs the relative importance of the regularization term compared to the sum-of-squares error. The coefficient $w_0$ is often omitted from $\vec{w}$ in the calculation of $\|\vec{w}\|^2$, as its inclusion causes the result to depend on the location of the origin, an effect called _bias_. In the more general setting the norm $\|\vec{w}\|$ is not necessarily a standard norm, but can be tailored to the training data considered.

Due to the resulting error function remaining quadratic in terms of $\vec{w}$, an exact minimizer for $err_R$ can be found to be $\vec{w} = (\lambda I+\Phi^\intercal\Phi)^{-1}\Phi^\intercal \vec{y}$, which results from a extension of the standard least squares solution. 

More generally regularization rules can be stated in terms of any (convex) [[Point estimation#^45314f|loss function]] $L$, $$err(\vec{w}) = \frac{1}{N}\sum_{i=1}^N L(y(\vec{w}, x_i),y_i)+\lambda\|\vec{w}\|^2.$$It can be derived that for $\lambda=0$, there are infinitely many values of $\vec{w}$ that minimize this quantity. However, for $\lambda>0$, there is a unique minimizer (provided the loss function is convex). ^c0eeb7


## Optimal coefficients for least squares 
## Maximal likelihood
[[Maximum likelihood]] can be applied to find parameters, $\vec{w}$, of best fit for a degree $d$ polynomial or more general curve. 


## Bayesian fitting
Under the Bayesian methodology, we introduce a prior distribution over the polynomial coefficients $\vec{w}$. Assume, for simplicity, it takes the form of a normal distribution $$P(\vec{w}|\kappa_p) = \mathcal{N}(\vec{w}|\vec{0},\kappa_p^{-1}I) = \left(\frac{\kappa_p}{2\pi}\right)^{d/2}\exp(-\frac{\kappa_p}{2}\vec{w}^\intercal\vec{w})$$where $\kappa_p$ is the precision of the distribution and $d$ is the total number of elements in the vector $\vec{w}$ for a degree $d$ polynomial. 

Then via Bayes theorem the posterior distribution of $\vec{w}$ satisfies the proportional relation $P(\vec{w}|\vec{x},\vec{y},\kappa_p,\kappa)\propto P(\vec{y}|\vec{x},\vec{w},\kappa)P(\vec{w}|\kappa)$, and so values of $\vec{w}$ can be found by [[Maximum posterior|maximizing posterior]] probability.

More exactly, in a Bayesian treatment of the problem of curve fitting we must integrate over all possible values of $\vec{w}$, with $$P(y|x,\vec{x},\vec{y}) = \int P(y|x,\vec{w},\kappa)P(\vec{w}|\vec{x},\vec{y},\kappa_p)\,d\vec{w}.$$ 


## Gradient (steepest) descent
The technique of [[Gradient decent]] can be used to iteratively optimize the coefficients $\vec{w}$ by seeking a (local) minimum of the error function, provided the error function is differentiable; global minimization of the error cannot be guaranteed unless a more sophisticated methodology than what is now shown is employed. 

Begin by initializing $\vec{w}$ with random components, ideally such that $\vec{w}$ is near the global minimum; the position of which is typically unknown, but a general region can typically be determined (TODO - how). Then repeatedly update $\vec{w}$ based on the weighted addition of the error function's gradient with respect to $\vec{w}$, namely $$\vec{w} \gets \vec{w} - \eta\frac{\partial{e(\vec{w})}}{\partial\vec{w}},$$
where $\eta\in \mathbb{R}$ is biasing weight applied to the difference, called the _learning rate_. As the error approaches zero, the updates get continually more gradual. ^c983b3

# Confidence in fitment
We can express our uncertainty over any particular value of the target variable (fitted curves value at a point) using a probability distribution. 

Assume that given a value $x$ the corresponding value $y$ has a Gaussian normal distribution with mean equal to $y(x,\vec{w})$ of the fitted curve; i.e., $y(x,\vec{w})=y+\epsilon$ where $\epsilon$ has normal distribution with zero mean, see [[Location and scale families of distributions]]. Thus, $$P(y|x,\vec{w},\kappa) = \mathcal{N}(y|y(x,\vec{w}),\kappa^{-1})$$where $\kappa = \frac{1}{\sigma^2}$ is the precision. See the following image:
![[Bishop_ProbCurve.PNG]]

Then for the initial matched observations sets $X$ and $Y$, assume we have determined the parameter values $\vec{w}^*$ and $\kappa^*$ that [[Maximum likelihood#Maximum likelihood and least squares|maximize the least squares error]]. We can then make predictions for other argument values of $x$, in terms of a _predictive distribution_ that gives the probability distribution over $Y$, by substituting the maximal likelihood parameters into the probability function from above to get $$P(y|x,\vec{w}^*,\kappa^*) = \mathcal{N}(y|y(x,\vec{w}^*),\kappa^*).$$This allowing us to express, that given any (possibly new) value of $x$ its exact corresponding value $y$ will be close to $y(x,\vec{w})$ with probability $P(y|x,\vec{w^*},\kappa^*)$.






