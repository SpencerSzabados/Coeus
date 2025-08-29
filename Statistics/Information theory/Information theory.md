---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - information_theory
  - codes
  - statistics
references:
---
---

Information theory is concerned with representing data in a compact fashion (e.g., data compression) as well as with the transmission of data using error correcting codes. The topic of information theory is deeply connected to [[Overview of machine learning|machine learning]], in particular to the idea of [[Reinforcement learning]] and [[Empirical risk]] (such as [[Point estimation#Loss function optimality|loss functions]]).


# Overview 
**Definition: (Shannon Entropy)** The (Shannon) _entropy_ of a [[Random variables#^5ceb15|random variable]] $X\sim f$ is denoted $\mathbb{H}(X)$ and measures the level of uncertainty in observing any of $X$'s possible states; in particular, for a discrete random variable $X$ with $K$ states $$\mathbb{H}(X) = -\sum_{i=1}^K P(X=i)\log(P(X=i)).$$
The discrete distribution with maximum entropy is the discrete uniform distribution.

A form of entropy that is commonly used in [[Overview of machine learning|machine learning]], and related closely to [[Information theory#Kullback-Leibler divergence|Kullback-Libler divergence]], is cross-entropy.

**Definition: (Joint or cross entropy)** The so called _cross entropy_ (or _joint entropy_) between two probability distributions $f$ and $g$, defined over the same sample space $\mathcal{X}$, is given by $$\mathbb{H}(f,g) = -\sum_{x\in\mathcal{X}} f(x)\log g(x)$$and is a measure of the average number of bits needed to encode data coming from $f$ using model $g$. The cross-entropy between $f$ and $g$ in terms of Kullback-Libler divergence (below) can be stated as $$\mathbb{H}(f,g) = \mathbb{H}(f)+\mathbb{KL}(f|g).$$See [stack-exchange](https://stats.stackexchange.com/questions/357963/what-is-the-difference-cross-entropy-and-kl-divergence).

**Definition: (Conditional entropy)** For two random variables (discrete) $X$ and $Y$, _conditional entropy_, is defined as $$\mathbb{H}(X|Y) = \sum_{x}f_X(x)\mathbb{H}(Y|X=x).$$

## Kullback-Leibler divergence
Kullback-Leibler convergence (divergence), also called relative entropy, is a measure of how one [[Families of distributions|probability distribution]] differs from another. The measure is not a valid [[Metric spaces|metric]] as it is not symmetric and does not satisfy the triangle inequality.   ^26fd09

Kullback-Leibler divergence is typically used to compare the difference between a estimated probability (measured from data), say denoted $f$, and a theoretic distribution $g$. This difference can be interpreted as the average difference in the number of bits required to encode samples from $f$ using a code optimized for encoding samples from $g$ and the number of bits required using a code optimized for $f$ itself. Consequently, it is intuitive that $\mathbb{H}(g|f)\geq 0$.

**Definition: (Kullback-Leibler divergence)** In the discrete case, for probability distributions $f$ and $g$ defined over the same sample space $\mathcal{X}$, the relative entropy from $g$ to $f$ is $$\mathbb{KL}(f|g) = \sum_{x\in\mathcal{X}}f(x)\log\left(\frac{f(x)}{g(x)}\right) =- \sum_{x\in\mathcal{X}}f(x)\log\left(\frac{f(x)}{g(x)}\right) = -\mathbb{H}(f)+\mathbb{H}(f,g);$$that is, $\mathbb{KL}(f|g)  = \mathbb{E}_f[\log(f(X))-\log(g(X))]$. In the continuous setting, for probability densities $f$ and $g$, $$\mathbb{KL}(f|g) = \int_{-\infty}^\infty f(x)\log\left(\frac{f(x)}{g(x)}\right)\, dx$$or more generally for a [[Measure spaces#^26a5cd|measurable space]] $\mathcal{X}$ with $f$ being absolutely continuous with respect to $g$, $$\mathbb{KL}(f|g) = \int_{\mathcal{X}}\log\left(\frac{f(x)}{g(x)}\right)\, f(dx).$$ ^272741

Kullback-Leibler divergence is closely connected to [[Density estimation]] and [[Maximum likelihood]]. Given an iid [[Random samples|random sample]] $\{X_1,X_2,\dots,X_N\}$ from some unknown probability distribution $p$ that we whish to estimate over a candidate [[Families of distributions|family of distributions]], say $\mathcal{F}$, we can use KL-divergence as a distance objective to minimize. That is, given $\{X_1,X_2,\dots,X_N\}$ we seek to select an $f\in\mathcal{F}$ that minimizes the objective $$\min_{g\in\mathcal{F}}\mathbb{KL}(f|g) \Leftrightarrow \max_{g\in\mathcal{F}}\int_{-\infty}^\infty f(x)\log(g(x))\,dx\approx \max_{g\in\mathcal{F}}\frac{1}{N}\sum_{i=1}^N\log(g(X_i)),$$which is nothing but the classical maximum log-likelihood estimation over the family of candidate distributions.

Another useful property of Kullback-Leiber divergence for probability is its adherence to the chain rule of conditional probability. Namely, if $X$ and $Y$ are random variables with joint distributions $p(X,Y)$ and $q(X,Y)$ such that $p(X|Y)$ is defined with marginal $p(Y)$ and likewise for $q$, then  $$\mathbb{KL}(p(X,Y)|q(X,Y)) = \mathbb{KL}(p(X)|q(X))+\mathbb{KL}(p(Y|X)|q(Y|X)).$$
Observe that KL divergence is not symmetric, i.e., $\mathbb{KL}(f|g)\neq \mathbb{KL}(g|f)$; however, we can define the _symmetric Kullback-Leiber divergence_ as $$\mathbb{KL}(f|g)+\mathbb{KL}(g|f),$$see [Stack-Exchange](https://math.stackexchange.com/questions/1028224/is-there-a-symmetric-alternative-to-kullback-leibler-divergence). The difference between what the two measure is explained in [Mpatacchiola](https://mpatacchiola.github.io/blog/2021/01/25/intro-variational-inference.html) and [Stack-Exchange](https://stats.stackexchange.com/questions/488982/optimizing-forward-reverse-kl-divergence-for-gaussian-distributions).


## Total variation distance
The total variation distance (or statistical distance) is a metric of similarity between two probability distributions. ^ced5c3

**Definition: (Total variation - variational distance)** Let $(\Omega, \mathcal{B})$ be a [[Measure spaces|measureable space]] and $p$ and $q$ be probability measures defined on this space. The total variation distance between $p$ and $q$ is $$\delta(p,q)=\sup_{A\in \mathcal{B}}|p(A)-q(A)|.$$
This can also be written, for the case of $\mathbb{R}^d$, for measures $p$ and $q$ and associated densities $dp$ and $dq$ as $$\delta(p,q) = \frac{1}{2}\int_{\mathbb{R}^d}|dp(x)-dq(x)|\,dx.$$
 ^7edae7

The total variational distance lower bounds the square root of the [[Information theory#Kullback-Leibler divergence|Kullback-Leibler divergence]]; that is, $$\delta(P,Q)\leq \sqrt{\frac{1}{2}\mathbb{KL}(P|Q)}.$$

## Renyi divergence
Renyi entropy (or $\alpha$-divergence) is used in the [[Density estimation#Nonparametric methods|nonparametric density esitmation]] of [[s-Concave densities]] (a more general class of [[Distribution functions of random variables#^c46bbe|densities]]) as an optimization objective.  

**Definition: (Renyi Entropy)** Let $\alpha\geq 0$ with $\alpha\neq 1$, and let $X$ be a [[Random variables#^cc6415|discrete random variable]] that admits $N$ possible values according to a density $p$. Then the Renyi entropy of $X$ of order $\alpha$ is $$\mathbb{H}_\alpha(X) = \frac{1}{1-\alpha}\log\left(\sum_{i=1}^Np_i^\alpha\right).$$
From this we can define the Renyi divergence which generalises [[Information theory#Kullback-Leibler divergence|Kullback-Leibler divergence]].

In the analysis of $s$-concave densities KL divergence is no longer appropriate as these densities may not be of a form where taking a logarithm reduces them to a convex function to be analysed (bounded). 

**Definition: (Renyi divergence)** Let $\alpha\geq 0$ with $\alpha\neq 1$. In the discrete case, for probability distributions $f$ and $g$ defined over the same sample space $\mathcal{X}$ with $N$ possible values, the Renyi divergence of order $\alpha$ from $g$ to $f$ is $$\mathbb{D}_\alpha(f|g) = \frac{1}{\alpha-1}\log\left(\sum_{i=1}^N\frac{f_i^\alpha}{g_i^{\alpha-1}}\right).$$In the continuous setting, for probability densities $f$ and $g$ is $$D_\alpha(f|g)=\frac{1}{\alpha-1}\ln\left(\int \frac{f^\alpha(x)}{g^{\alpha-1}(x)}\,dx\right).$$

In the limit $\alpha\to1$ the Renyi divergence reduces to the Kullback-Leibler divergence. See, [Wiki](https://en.wikipedia.org/wiki/R%C3%A9nyi_entropy).


## Functional divergence
The $f$-divergence between two distributions is another notion of divergence, but one that is based on the use of a [[Measure spaces|measure]] function (or it can be interpreted in this way) between the two distributions.

**Definition: ($\mu$-divergence)** let $\mu:\mathbb{R}_{> 0}\to\mathbb{R}$ be a strictly [[Convex functions|convex function]] with boundary condition $\mu(1)=0$. The $\mu$-divergence between two distributions $f$ and $g$ is $$\mathbb{D}_\mu(f|g) = \int \mu(f(x)/g(x))\cdot g(x)\, dx,$$where it is assumed that $g(x)=0$ implies $f(x)=0$, otherwise the divergence is taken as $\infty$.

If we take $\mu=t\log t$ then $\mathbb{D}_\mu(f|g)=\mathbb{KL}(f|g)$.


## Bregman divergence
Bregman divergence is a measure of the difference between two points as measured by a strictly [[Convex functions|convex function]]; in the context of probabilities the aforementioned points are taken to be probability distributions or parameters that characterize said distributions.
 
**Definition: (Bregman divergence)** Let $d:\Omega\to\mathbb{R}$ be a continuously differentiable strictly convex function defined over a convex domain $\Omega$. The _Bregman divergence_ between two points $x,y\in\Omega$ is $$\mathbb{BD}_f(x|y) = f(x)-f(y)-\langle\nabla f(y),x-y\rangle$$which is the first order [[Taylor series]] of $f$ about $y$. See [Wiki](https://en.wikipedia.org/wiki/Bregman_divergence).


# Mutual information and inference 
Rather than measuring the correlation between two random variables a more general measurement of the relation between the two is the _mutual information_ they carry about one another.

**Definition: (Mutual information)** For two random variables $X$ and $Y$ (discrete) the _mutual information_ they carry about one another is given by $$\begin{align*}\mathbb{MI}(X,Y) &= \mathbb{KL}(f_{X,Y}|f_Xf_Y)\\ &= \sum_{x}\sum_{y}f(x,y)\log_2\left(\frac{f_{X,Y}(x,y)}{f_X(x)f_Y(y)}\right)\\ &= \mathbb{H}(X)-\mathbb{H}(Y|X),\end{align*}$$where $\log_2(f_{X,Y}(x,y)/f_X(x)f_Y(y))$ is the pointwise mutual information carried between the two events $x$ and $y$ about one another, and is a measure of the discrepancy between the events occurring together compared to expectation. $\mathbb{MI}$ is zero if and only if the two random variables are independent.

