Density estimation is the unsupervised task of learning an estimator for a (joint) probability distribution (an unconditional distribution opposed to [[Supervised learning]]) over a set of random variables from a set of samples. Many [[Overview of machine learning|machine learning]] problems can be reframed as different kinds of probabilistic inference questions dependent on learned density estimates, [[@Vergari_2019]].


# Introduction
Given a random variable $X$ and a finite sample set $x_1,x_2,\dots,x_N$ of realised values, that are assumed to be identically distributed, the problem of _density estimation_ is to find a probability distribution $P(X)$ that fits the given data. This problem is fundamentally ill-posed as there are infinitely many probability distributions that could give rise to the observed data; e.g., any distribution that is nonzero at each of the data points is a potential candidate. And since, most observations are discrete there is no restriction on the continuity or discontinuity of said distributions; however, assumptions are often made to limit those considered.


# Parametric methods
Parametric density estimation methods revolve around the assumption that the given observations originate from a specific family of densities. After assuming the from the underlying density parameters of best fit are estimate from the sample data.

## Binomial distribution
### Parameter estimation 
#### Maximum likelihood optimization
#### Bayesian posterior maximization
In [[Bayesian probability theory|Bayesian inference]] the [[Families of distributions#Beta distribution|Beta distribution]] is the [[Bayesian probability theory]] probability distribution for the  [[Families of distributions#Bernoulli distribution|Bernoulli]] and [[Families of distributions#Binomial distribution|Binomial]] distributions; that is, the beta distribution gives a prior probability $P(p)$ on the probability parameter value $p$ of the Binomial distribution. 

In particular observe, for the notion of conjugate priors, the beta distribution resembles that of the Bernoulli probability function, $p^x(1-p)^{1-x}$, with additional parameters for the number of observed successes and failures, along with a normalization (and shape) constant $B(\alpha,\beta)$; that is, we can interpret the parameters $\alpha$ and $\beta$ in the prior distribution (or posterior distribution after including attritional observation data), $P(p) = Beta(p|\alpha,\beta)$, as the _effective number of observations_ of $x=1$ and $x=0$ events respectively. Alteration of these parameters in tern changes how probably any particular value of $p$ is for any set of observed values.

(Because of this, the parameters $\alpha$ and $\beta$ of the beta distribution are often called _hyperparameters_ as they control the distribution of the parameter $p$.)

The posterior distribution of $p$ is then obtained by multiplying the Beta (prior) distribution by the binomial likelihood function (Bernoulli probability) and normalizing, to give $$P(p|m,l,\alpha,\beta) =\frac{\Gamma(m+\alpha+l+\beta)}{\Gamma(m+\alpha)\Gamma(l+\beta)}p^{m+\alpha-1}(1-p)^{l+\beta-1}$$where $l=N-m$, and therefore corresponds to the number of losses ($x=0$ events) in the sample. 

Then for a given collection of previous observed values $\vec{x} = (x_1,x_2,\dots,x_N)$, the best value of $p$ is predicted as $$\begin{align} p^* = P(X=1|\vec{x}) &= \int_0^1 P(X=1|\mu)P(\mu|\vec{x})\,d\mu\\ &=\int_0^1 \mu P(\mu|\vec{x})\, d\mu\\ &=E[\mu|\vec{x}]. \end{align}$$Using $P(\mu|\vec{x})=P(p|m,l,\alpha,beta)$ in conjunction with the above equation for the posterior probability with values for $m$ and $l$ derived from $\vec{x}$, and mean $\mu=\alpha/(\alpha+\beta)$ of the prior beta distribution we get $$p^* = E[\mu|\vec{x}] = \frac{m+\alpha}{m+\alpha+l+\beta}.$$
For a finite set of observations, the predicted value of $p$ always lies between the prior mean and maximum likelihood estimate, the sample mean, of $\sum_{i=1}^N x_i/N$. Moreover, as we observe more data the uncertainty, the variance of the posterior distribution, steadily decreases.


## Normal distribution 
### Parameter estimation
Suppose we are given a set of observations $x_1,x_2,\dots,x_N$, which are often encoded into a vector $\vec{x} = (x_1,x_2,\dots,x_N)$ within computational domains such as [[Overview of machine learning]], of a scalar random variable. Assume these observations are drawn independently from a normal distribution with unknown mean $\mu$ and variance $\sigma^2$. 

### Maximum likelihood optimization 
As the observations are drawn independently we have $$P(\vec{x}|\mu,\sigma^2) = \prod_{i=1}^N\mathcal{N}(x_i|\mu,\sigma^2).$$Viewing this as a function of $\mu$ and $\sigma^2$, this is the likelihood function for the normal distribution for the given observations.

We may find parameters of best fit by maximizing this likelihood function, or equivalently, for practical purposes, the log of the likelihood function; $$\ln P(\vec{x}|\mu,\sigma^2) = -\frac{1}{2\sigma^2}\sum_{i=1}^N(x_i-\mu)^2-\frac{N}{2}\ln\sigma^2-\frac{N}{2}\ln(2\pi).$$For any fixed $\sigma^2$, we obtain a [[maximum likelihood]] solution by picking $\mu$ equal to the _sample mean_ $\bar x = \frac{1}{N}\sum_{i=1}^N x_i$. Likewise, for any fixed $\mu$, we maximize the above by taking $\sigma^2$ to the _sample variance_  $s^2 = \frac{1}{N}\sum_{i=1}^N (x_i - \bar x)^2$. 

Unfortunately, this method of estimation systematically underestimates the variance of the distribution, due to the above being a biased estimator of the variance, see [[Random samples#^88238b]]. Instead, we take $s^2 = \frac{1}{N-1}\sum_{i=1}^N (x_I-\bar{x})^2$, in order to obtain an unbiased estimator of the population variance. 


## Beta distribution 
### Parameter estimation 
### Method of moments
For two unknowns $\alpha$ and $\beta$, the sample mean $\bar{x}$ and variance  $s^2$ can be used to estimate the beta parameters by $$\begin{align} \alpha &\approx \bar{x}\left(\frac{\bar{x}(1-\bar{x})}{s^2}-1\right),\\ \beta &\approx (1-\bar{x})\left(\frac{\bar{x}(1-\bar{x})}{s^2}-1\right),\quad \text{if $s^2<\bar{x}(1-\bar{x})$}.\end{align}$$
### Maximum likelihood


# Nonparametric methods 
Unlike in parametric density estimation where the underlying distributions is assumed to have a specific form (belong to a select class of family) non-parametric methods make no such assumptions, instead attempt to make direct estimate based on the structure of the data alone. 


## Histogram methods
One of the simplest nonparametric methods of modeling a distribution are [[Histogram methods]], where a histogram is constructed using the observations.


## Kernel method 
[[Parzen-Kernel density estimators]] can be thought of as a more sophisticated version of histogram estimation methods.


## Projection pursuit method 
[[Projection pursuit density estimation]]