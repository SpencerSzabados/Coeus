---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - statistics
  - statistical_learning
  - approximation
  - random_sampling
---
---
 
 While, in general, [[Random variables]] can have only one distribution, it is often easier to model a situation by thinking of things in a hierarchy. Where a complicated process is modeled by a sequence of relatively simple models with limited regimes. This form of modeling is very natural within the context of [[Classification and clustering|clustering]] with different observations originating from different clusters within the overarching distribution.  


# Overview
One of the central properties underpinning mixture modeling is that any continuous distribution can be approximated arbitrarily well by a finite mixture of normal densities with shared variance, see [[@McLachlan_2000]].

For the remainder, let $X_1,X_2,\dots,X_N$ denote a continuous [[Random samples|random sample]] where $X_i$ is a $d$-dimensional [[Random variables#Multiple random variables|random vector]] with [[Distribution functions of random variables#^c46bbe|probability density function]] $f(x_i)$ on $\mathbb{R}^d$; note, we can still view $f(x_i)$ as a density when $X_i$ is discrete by using a counting measure. It is assumed that we can model $f(x_i)$ of $X_i$ can be expressed as $$f(x_i) = \sum_{j=1}^m w_jf_j(y_i)$$where $f_j(y_i)$ are densities and $w_j$ are non-negative weights, called the _mixing proportions_, with $\sum_{j=1}^m w_j=1$. Densities of this form are called _finite mixture models_.

**Definition: (Mixture distribution)** A random variable $X$ with density $f(x)$ is said to have a _mixture distribution_ if it can be expressed as a weighted sum of densities of the form $$f(x) = \sum_{j=1}^m w_jf_j(x).$$If the number of components in the mixture is proportional to the number of elements in the random sample and the components are Gaussian in form, the model is referred to as a mixture of Gaussians.

As outlined, a common interpretation of a $m$ component mixture model is to consider $X$ to be drawn from a population with groups ([[Classification and clustering#Classification|classes]]) $C_1,C_2,\dots,C_k$ in proportions $p_1,p_2,\dots,p_k$. If the density of $X$ is group $C_i$ is given by $f_i(X)$ for $i=1,\dots,m$, then the density of $X$ has a $m$ component mixture. Now, we might not know if $X$ posses this group structure beforehand and we would need to estimate them; e.g., clustering data and then forming estimates of the group proportions (e.g., [[Parzen-Kernel density estimators]]).

Sometimes calculations can be simplified by using the following theorem.

**Theorem: (Mixed expectation)** If $X$ and $Y$ are two random variables, then $$E[X] = E[E[X|Y]],$$provided these expectations exist. 


