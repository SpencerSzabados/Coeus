Here we are concerned with generating a [[Random samples|random sample]] $X_1,\dots,X_N$ from a given distribution $f(x|\theta)$.


## Direct method 
To generate directly a random vector $Y$ with a desired distribution, we require there to exist a closed from function $g(u)$ such that the transformed variable, $U$, has the desired distribution, $Y=g(U)$, when $U\sim Uniform(0,1)$. 

For continuous random variables the [[Statistical transformations#^a89d65|probability integral transform]] is one such method; specifically, were we sample a uniform distribution and and apply the inverse of the probability integral transforms with respect to the desired distribution, this leads to [[Inverse transform sampling]].


## Indirect method 


## Delta method 
The delta method(s) deals with wanting to sample/estimate parameters of the distribution of a function of a random variable, rather than the random variable itself. For this series approximation is useful.

The first order [[Taylor series]] approximation of a random variable is given as follows. If, $T_1,T_2,\dots,T_k$ are random variables (sample) with means $\mu_1,\mu_2,\dots,\mu_k$, and we define$\vec{T} = (T_1,\dots,T_k)$ and $\vec{\mu} = (\mu_1,\dots,\mu_k)$. Suppose there is a differentiable function $g(\vec{T})$ (and estimator of some parameter of interest) for which we want to approximate an estimate of variance. Define $$g'_i(\vec{\mu})=\frac{\partial}{\partial t_i}g(\vec{t})|_{t_1=\mu_1,\dots,t_k=\mu_k}.$$The first-order Taylor series expansion of $g$ about $\mu$ is then$$g(\vec{t}) = g(\vec{\mu})+\sum_{i=1}^k g'_i(\vec{\mu})(t_i-\mu_i)+R$$where $R$ denotes the remainder terms.

This approximation has a very convent [[Expected values|expectation]], namely$$E_{\vec{\mu}}[g(\vec{T})]\approx g(\vec{\mu})+\sum_{i=1}^kg_i'(\vec{\mu})E_{\vec{\mu}}[T_i-\mu_i] = g(\vec{\mu}).$$ Thus, the [[Expected values#^e635ea|variance]] of $g(\vec{T})$ can be approximated by $$Var_{\vec{\mu}}[g(\vec{T})]\approx E_{\vec{\mu}}\left[(g(\vec{T})-g(\vec{\mu}))^2\right]\approx \sum_{i=1}^k g_i'(\vec{\mu})^2Var_{\vec{\mu}}[T_i]+2\sum_{i>j}g_i'(\vec{\mu})^2Cov_{\vec{\mu}}[T_i,T_j],$$where the last equality comes from expanding the square. All this yields an approximation formula for the variance of a general function involving only simple calculations of variance and covariances.

Using Taylor series approximations for mean and variance, we get a generalization of the central limit theorem called the delta method.

**Theorem: (Delta method)** let $Y_N$ be a sequence of random variables such that $\sqrt{N}(Y_n-\theta)$ converges in distribution to $\mathcal{N}(0,\sigma^2)$. For a given function $g$ and a specific value of $\theta$, suppose $g'(\theta)$ exists and is not zero. Then $\sqrt{N}(g(Y_N)-g(\theta))$ converges in distribution to $\mathcal{N}(0,\sigma^2g'(\theta)^2)$.

There are some cases where $g'(\theta)=0$, in which case we take one more term in the Taylor series expansion, giving the following result.

**Theorem: (Second-order Delta method)** Let $Y_N$ be a sequence of random variables such that $\sqrt{N}(Y_n-\theta)$ converges in distribution to $\mathcal{N}(0,\sigma^2)$. For a given function $g$ and a specific value of $\theta$, suppose that $g'(\theta)=0$ and $g''(\theta)\neq 0$. Then $N(g(Y_N)-g(\theta))$ converges in distribution to $\sigma^2\frac{g''(\theta)}{2}\chi_1^2$.


# Sampling from location and scale family 
Suppose $X_1,\dots,X_N$ is a random sample from $(1\sigma)f((x-\mu)/\sigma)$, a member of a [[Location and scale families of distributions]]. Then the distribution of $\bar{X}$ is closely related to that of $\bar{Z}$, the sample mean from a random sample from the standard pdf $f(z)$. By definition, there exists random variables $Z_1,\dots,Z_N$ such that $X_i = \sigma Z_i+\mu$. Furthermore, it must be that $Z_1,\dots,Z_N$ are mutually independent. Thus, $Z_1,\dots,Z_N$ is a random sample of $f(z)$ and so $$\bar{X} = \frac{1}{N}\sum_{Xi=1}^N X_i = \frac{1}{N}\sum_{i=1}^N (\sigma Z_i+\mu) = \sigma \bar{Z} +\mu.$$
Moreover, if $g(z)$ is the pdf of $\bar{Z}$ then, $(1/\sigma)g((x-\mu)/\sigma)$ is the pdf of $\bar{X}$. Thus, in situations where it is easier to work with $Z_1,\dots,Z_N$, and late derivate results for $\bar{Z}$.


# Sampling from the normal distribution 
[[Families of distributions#Gaussian Normal distribution]]

**Theorem:** Let $X_1,\dots,X_N$ be a random sample from a $\mathcal{N}(\mu,\sigma^2)$ distribution, and let $\bar{X} = (1/N)\sum_{i=1}^N X_i$ and $s^2 = 1/(N-1)\sum_{i=1}^N (X_i-\bar{X})^2$. Then
   1) $\bar{X}$ and $s^2$ are independent random variables;
   2) $\bar{X}$ has a $\mathcal{N}(\mu,\sigma^2/N)$ distribution; 
   3) $(N-1)s^2/\sigma^2$ has a chi-squared distribution with $N-1$ degrees of freedom.
_Proof: Proof of this theorem is based on [[Families of distributions#^70a18f]], see (p250)[[@Casella_2001]]._

## Students t-distribution 
The t-distribution is motivated by wanting to make inferences about $\mu$, by looking at the variability of $\bar{X}$, of a sampled normal distribution with unknown exact variance. 

**Definition: (t-distribution)** If $X_1,\dots,X_N$ are a random sample from a $\mathcal{N}(\mu,\sigma^2)$ distribution. The quantity $$\frac{\bar{X}-\mu}{s/\sqrt{n}} = \frac{(\bar{X}-\mu)/(\sigma/\sqrt{n})}{\sqrt{s^2/\sigma^2}}$$has Student's t-distribution with $N-1$ degrees of freedom. That is, a random variable $T$ has Students t-distribution with $p=N-1$ degrees of freedom, written $T\sim t_p$, if it has pdf $$f_T(t) = \frac{\Gamma((p+1)/2)}{\Gamma(p/2)}\frac{1}{\sqrt{p\pi}}\frac{1}{(1+t^2/p)^{(p+1)/2}}, \quad -\infty<t <\infty.$$
We calculate the expectation of a random variable $T_p$ that has $t_p$ distribution to be $$E[T_p] = 0,\quad \text{if $p>1$},$$with variance $$Var[T_p] = \frac{p}{p-2},\quad \text{if $p>2$}.$$
