---
doc type: Note
authors: Spencer Szabados
date: 2023-11-15
tags:
  - generative_models
  - statistical_learning
  - random_sampling
  - diffusion
references:
---
___

Push-forwards models is a general class of method motivated from wanting to generate samples of the underlying distribution that our training data originates from without having to collect additional "true" sample data. 

**Examples of push-forward networks:** 
  + [[Variational autoencoder]]
  + [[Normalizing flows]]
      +  [[Diffusion models]] 
  + [[Generative adversarial networks]]
 
---
# Statistical background 
Supposed we want to sample from a [[Families of distributions#Gaussian (Normal) distribution|Gaussian distribution]] with mean $\mu$ and covariance matrix $\Sigma$. One approach to doing this is to sample from a simpler normal distribution $Z\sim \mathcal{N}(0,\mathbb{I})$ and transform this sample to yield a sample from the desired distribution. For the particular distribution described, this can be done using a [[Linear transformations|linear transformation]] ([[Affine transformation matrix]]) $T=\mu+\Sigma^{1/2}$, that is, $$X=T(Z)=\mu+\Sigma^{1/2}Z\sim\mathcal{N}(\mu,\Sigma).$$
The above reparameterization typically referred to as the "reparameterization trick" in literature. The transformation $\Sigma^{1/2}$ is referred to as the [[Distributions along projections#Cholesky transformation|Cholesky transformation]].

More generally, we can generate samples using the _push-forwards measure_ (or _push-forward operator_), commonly written in terms of the composition of a [[Measure spaces|measure]] $\mu$, defined on the support of $Z$, with the pre-image of the sought transform $T$, as $$T_{\sharp}\mu = \mu(T^{-1}(B))$$for any [[Fundamentals of probability theory#^9dcf42|Borel set]] $B$ on the support. Formulating things in terms of [[Distribution functions of random variables#^c46bbe|probability densities]], if $f$ is a density over the support of $Z$, the associated measure is$$\mu(A) = \int_A f(z)\, dz$$and the push-forwards measure $T_\sharp\mu$ defined over $X$ is $$T_\sharp\mu(B) = \int_{T^{-1}(B)}f(z)\,dz = \int_B f(T^{-1}(x))|det(\mathbb{J}_{T^{-1}}(x))|\, dx.$$Reducing back to densities, the push-forwards measure $T_\sharp\mu$ has density function $$dT_\sharp\mu(x)=f(T^{-1}(x))|det(\mathbb{J}_{T^{-1}}(x))|$$with $x\in B$ for a Borel set $B$ from the sigma algebra on $X$. See [Wiki](https://en.wikipedia.org/wiki/Pushforward_measure), [StackExchange-Ruy](https://math.stackexchange.com/questions/3834752/basic-confusion-on-push-forward-of-a-measure). From this, it can be seen that Push-forwards methods in machine learning are attempting to learn the push-forwards density/measure over $X$ indirectly by learning $T$. ^3b91f2

It should be noted that the above is simply a more general statement of the [[Statistical transformations#^2e88f0|change of variables formula]].

The above discussion is supported by the following theorem, which is taken from notes provided by my supervisor. 

**Theorem: (Probability measure transformation)** let $\mu_Z$ be a diffuse [[Fundamentals of probability theory#^9e67e5|Borel measure]] (continuous Borel measure such that any singular point has measure zero) on a polish space (a space hoeomorphic to a complete [[Metric spaces|metric space]] that has a countable dense subset) $Z$ and let $\mu_X$ be any Borel probability measure on another polish space $X$. Then there exists a measurable map $T:Z\to X$ such that, if $Z\sim \mu_Z$, then $X=T(Z)\sim \mu_X$.

In general the pushforward transform $T$ is not invertible. However, it is typically assumed (or desired) in practice that the transformations constructed are invertible. 


# Push-forwards generative models
The result of the above section motivates the approach of trying to learn a parametrized mapping $T_\theta$ from a embedding probability space $Z$ to our desired target distribution $X$, such that $T_\theta(Z)\sim X$, to enable us to generate samples from complex (unknown) distributions.

**Problem: (Push-forwards objective)** Given a collection of iid samples $X_1,\dots,X_N$ from an unknown density $\chi$, it is our objective to estimate $\chi$ using the _push-forward_ approach through minimizing the objective $$\inf_\theta \text{dist}(X,T_\theta(Z))$$for $X\sim\chi$ and some random variable $Z$ with known (controlled) distribution, typically taken to be the normal distribution, and $T_\theta:\mathbb{R}^p\to\mathbb{R}^d$ where it is typically assumed $p<d$.   ^599c6e

Due to the assumption that $p<d$, which is made for ease of computation, and the estimation of $T_\theta$ via [[Artificial neural networks]] (or other networks), we will not have a explicit analytical formulation of our density estimate that is suitable for [[Maximum likelihood|maximum likelihood estimation]] over $\theta$. Thus, alternative methods of optimization must be used. A commonly used method makes use of duality, where the difference between the desired density $X$ and that of the approximation $T_\theta(Z)$ is measured from within a chosen class of functions, $$\text{dist}(X,T_\theta(Z)) \approx\sup_{f\in\mathcal{F}}|\mathbb{E}[f(X)]-\mathbb{E}[f(T_\theta(Z))|.$$
The above is actually known more specifically as Maximum-Mean Discrepancy (MMD) which quantifies the match between two distributions by comparing their [[Expected values#Moments and moment generating functions|moments]]; i.e., it measures the largest distances between mean embeddings of the distributions. See [SiXUlm](https://stats.stackexchange.com/a/447629) for more details.


