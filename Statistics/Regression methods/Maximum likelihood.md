Maximum  [[Data reduction#The likelihood principle|Likelihood]]  is one of the most commonly used method for deriving estimates for parameters (e.g., [[Density estimation]]). (p315)[[@Casella_2001]]


# Overview 
**Definition: (Likelihood function)** Let $X_1,\dots,X_N$ be a iid sample from a population with pdf (or pmf) $f(x|\theta)$, the likelihood function is defined by $$\mathcal{L}(\vec{\theta}|\vec{x}) = \mathcal{L}(\theta_1,\dots,\theta_k|x_1,\dots,x_k) = \prod_{i=1}^N f(x_i|\theta_1,\dots,\theta_k)$$and gives the probability of the observed data as a function of the model parameter. See [[@Neal_1996]].

**Definition: (Maximum likelihood estimator)** For each sample point $\vec{x}$, let $\theta^*$ be a parameter value at which $\mathcal{L}(\theta|\vec{x})$ attains its maximum as a function of $\theta$, with $\vec{x}$ held fixed. A _maximum likelihood estimator_ of the parameter $\theta$ based on the sample $\vec{X}=\vec{x}$ is $$\theta^*=\arg\max_{\theta}\mathcal{L}(\theta|x).$$ ^accd74

By construction the range of the MLE coincides with the range of the parameter being estimated. Unfortunately, MLE suffer from being difficult to compute as a global maximum must be found and depending on the estimate this calculation might suffer from numerical sensitivity. This last point is especially important in practice, as measured data contains error (small changes in value - like those that cause issues in unstable numerical methods) so it is important to know how small changes in the data effects the MLE being considered. 


# Methods of optimization
There are various analytical (and numerical) methods of optimizing for a maximum value of a function, e.g., the likelihood function, that can be employed to find the MLE of $\theta$ given some sample data.

If the likelihood function is differentiable in $\theta_i$, _possible candidates_ for the MLE are the values of $(\theta_1,\dots,\theta_k)$ that solve the system of partial derivates $$\frac{\partial}{\partial\theta_i}L(\vec{\theta}|\vec{x}) = 0,\quad \text{for $i=1,\dots,k$.}$$It is often easier in cases where differentiation can be used to work with the natural logarithm of $L(\vec{\theta}|\vec{x})$, known as the _log likelihood_, than to work with the differential of $L(\vec{\theta}|\vec{x})$ directly. This is possible, meaning it yields the same solution, because $\ln(\cdot)$ (or more generally $\log(\cdot)$) is strictly monotone increasing on $(0,\infty)$, which is the domain of interest for maximizing the likelihood function. 


A useful property of maximum likelihood estimators is that known as the _invariance property of maximum likelihood estimators_ (not to be confused with statistical invariance).

**Theorem: (Invariance property of MLE)** Suppose that a distribution $p(x|\theta)$ is indexed by parameter $\theta$, and we are interested in finding an estimator for some function of $\theta$, say $T(\theta)$. If $\theta^*$ is the MLE of $\theta$ with respect to $p(x|\theta)$, then $T(\theta^*)$ is the MLE of $T(\theta)$.


## Maximum likelihood and least squares
The error function of least squares, that is the sum-of-squared error, can be motivated as the maximum likelihood solution provided we assume the given sample points come from a certain (known) distribution. [[@Bishop_2006]]

Particularly, suppose the sets $X=\{x_1,x_2,\dots,x_N\}$ and $Y=\{y_1,y_2,\dots,y_N\}$ are given matched pair observation data; that is $x_i$ is associated with the value $y_i$ for each $i=1,2,\dots,N$ by some unknown underlying function that we are seeking to determine (or rather approximate). Denote by $y(x,\vec{w})$ this underlying function, and assume $Y$ is generated according to the rule $y_i = y(x_i,\vec{w})+\epsilon$, where $\epsilon$ represents noise in measurement which is assumed to be a standard normal distribution random variable with precision (inverse variance) $\kappa = 1/\sigma^2$.  Under these assumptions, it can be seen that for any values of $x$ and $y$, $$P(y|x,\vec{w},\kappa) = \mathcal{N}(y|y(x,\vec{w}),\kappa^{-1}).$$This follows from the fact that, for a square loss (error) function the optimal [[Fundamentals of prediction|prediction]] for a new value is given by the conditional mean of the target variable. Which is given in this case by $E[y|x] = \int yp(y|x)dy = y(x,\vec{w})$ for any $x\in X$ and $y\in Y$. 

As is commonly done for compactness, define the vectors $\vec{x}=(x_1,\dots,x_N)$ and $\vec{y} = (y_1,\dots,y_N)$ composed of the individual data points from $X$ and $Y$ respectively. Assuming the paired observations to be iid, the likelihood function is $$\mathcal{L}(\vec{y}|\vec{x},\vec{w},\kappa) = \prod_{i=1}^N\mathcal{N}(y_i|\vec{w}^\intercal \phi(x_i),\kappa^{-1}),$$where $\phi(x)$ is a vector of basis functions with $\vec{w}^\intercal\phi(x_i)=y(x_i,\vec{w})$; in the case of [[Curve fitting#Polynomial curve fitting|polynomial curve fitting]] $\phi(x)=x$. 

The log-likelihood function is  $$\begin{align} \ln \mathcal{L}(\vec{y}|\vec{x},\vec{w},\kappa) &=\sum_{i=1}^N\ln\mathcal{N}(y_i|\vec{w}^\intercal \phi(x_i),\kappa^{-1})\\ &=\frac{N}{2}\ln\kappa - \frac{N}{2}\ln(2\pi) - \frac{\kappa}{2} err(\vec{w}),\end{align}$$where $err(\vec{w})$ is the sum-of-squares error function, which takes the general form of $err(\vec{w}) = \sum_{i=1}^N(y_i-\vec{w}^\intercal \phi(x_i))^2$.  ^79a115


### Analytical solution to sum of squares maximum likelihood
We can now maximize this likelihood function with respect to $\vec{w}$ by minimizing the sum-of-squared error function $err(\vec{w})$ to find values for $\vec{w}$. Taking the gradient of the likelihood function with respect to $\vec{w}$ gives$$\nabla \ln \mathcal{L}(\vec{y}|\vec{w},\kappa) = \sum_{i=1}^N(y_i-\vec{w}^\intercal \phi(x_i))\phi(x_i)^\intercal.$$ Setting this to zero and expanding the right hand side yields $$0 = \sum_{i=1}^N y_i\phi(x_i)^\intercal - \vec{w}^\intercal \left(\sum_{i=1}^N \phi(x_i)\phi(x_i)^\intercal \right) \Rightarrow \vec{w} = (\Phi^\intercal \Phi)^{-1}\Phi^\intercal\vec{y}$$which are called as the _normal equations_ for the least squares problem. Where $\Phi$ is an $N\times d$ matrix, called the _design matrix_, consisting of elements given by $\Phi_{ij} = \phi_j(x_i)$; i.e., $$\Phi = \begin{bmatrix}\phi_0(x_1) & \phi_1(x_1) & \cdots & \phi_d(x_1)\\ \phi_0(x_2) & \phi_1(x_2) & \cdots & \phi_d(x_2)\\ \vdots & \vdots & \ddots & \vdots\\ \phi_0(x_N) & \phi_1(x_N) & \cdots & \phi_d(x_N)\end{bmatrix}.$$The quantity $\Phi^{+}=(\Phi^\intercal\Phi)^{-1}\Phi^\intercal$, is called the [[Matrix inverses#^73409a|Moore-Penrose pseudo-inverse]]. 

In practice, direct numerical solutions to the normal equations can lead to computational difficulties (loss of precision and a high computational cost for naïve matrix operations) when $\Phi^\intercal\Phi$ is nearly a [[Singular matrix]]. 