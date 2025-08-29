---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - statistics
  - density_estimation
  - random_sampling
references:
---
---

# Overview
The goal of _point estimation_ is to discover global properties, e.g., parameterization coefficients, of the underlying probability distribution of observed samples.

When sampling a population described by a pdf, $f(x|\theta)$, knowledge of the parameter $\theta$ yields knowledge of the entire population. Hence, it is desirable to find a good estimator of the point $\theta$ for when it is not known beforehand. Recall here, in the most general setting, $\theta$ is the index of the family of [[Measure spaces#^c048df|measures]] defined over the sample space.

**Definition: (Point estimator)** A _point estimator_ is any function $W(X_1,\dots,X_N)$ of a sample $X_1,\dots,X_N$; that is, any [[Random samples#^1176b9|statistic]] is a point estimator.

For clarity, an _estimator_ is a function of the sample, while an _estimate_ is the realized value of an estimator (a number/vector) that is obtained when a sample is taken and plugged into an estimator.

# Methods of finding estimators
There are several commonly used methods of point estimation found in literature. Most of these are parametric, meaning they assume the underlying distribution belongs to a parametric [[Families of distributions|family of distributions]].

## Method of moments 
This methods typically does not yield the best results, but is one of the oldest and is simple to implement and use.

**Method: (Method of moments)** Let $X_1,\dots,X_N$ be a sample from a population with pdf (or pmf) $f(x|\theta_1,\dots,\theta_k)$. Then equate the first $k$ sample [[Expected values#^82311d|moments]] to the corresponding $k$ population moments, and solve the resulting system of equations; that is, set up $$\begin{align}m_1 &= \frac{1}{N}\sum_{i=1}^N X_i^1,\quad \mu_1' = E[X^1]\\ m_2 &= \frac{1}{N}\sum_{i=1}^N X_i^2,\quad \mu_2' = E[X^2]\\ &\vdots\\ m_k &= \frac{1}{N}\sum_{i=1}^N X_i^k,\quad \mu_k' = E[X^k].\end{align}$$The population moment $\mu_j'$ is typically a function of $\theta_1,\dots,\theta_k$ of the from $\mu_j'(\theta_1,\dots,\theta_k)$. It follows that the method of moments estimator $(\tilde\theta_1,\dots,\tilde\theta_k)$ of $(\theta_1,\dots,\theta_k)$ is obtained by solving the following system of equations for $(\theta_1,\dots,\theta_k)$ in terms of $(m_1,\dots,m_k)$.$$\begin{align}m_1 &= \mu_1'(\theta_1,\dots,\theta_k)\\ m_2 &= \mu_2'(\theta_1,\dots,\theta_k)\\ &\vdots\\ m_k &= \mu_k'(\theta_1,\dots,\theta_k).\end{align}$$

## Maximum likelihood estimators 
The method of [[Maximum likelihood]] is, by far, the most popular for deriving estimates.

![[Maximum likelihood#^accd74]]

## Bayesian estimators 
The [[Bayesian probability theory|Bayesian]] approach to statistics is fundamentally different from the classical approach.  

## The EM (Expectation-Maximization) Algorithm 
The EM algorithm is based on replacing the difficult to optimize likelihood function used in maximum likelihood estimation with a sequence of easier maximizations that converge to the answer of the original problem. It is particularly well suited to "missing data" problems.


# Methods of evaluating estimators 
Once we have an estimator, or a method in mind, we must decide on how to discriminate the quality of solution between the true point value and that we have estimated. The difference between these values is referred to as the error. This topic of evaluating statistical procedures is part of the branch of statistics called decision theory.

## Mean square error 
By far the simplest and most common error estimate is the mean squared error.

**Definition: (Mean squared error)** The _mean squared error_ (MSE) of an estimator $\theta^*$ of a parameter $\theta$ is the expectation $E_\theta[(\theta^*-\theta)^2]$. ^c8b7fb

In general, any increasing function of the absolute distance $|\theta^*-\theta|$ would serve to measure the _goodness_ of an estimator, but MSE has at least two advantages over other distance measures: (1) It is very tractable analytically, and (2) it has the interpretation $$E_\theta[(\theta^*-\theta)]=Var_\theta[\theta^*]+(E_\theta[\theta^*]-\theta)^2 = Var_\theta[\theta^*]+Bias_\theta[\theta^*]^2,$$where the bias of an estimator is defined in the following section. Thus, the mean squares error incorporates both a measure of the variability of the estimator (precision) and the bias (accuracy). With a good estimator simultaneously minimizing the two quantities; however, as developed below, it is sometime more practical to construct unbiased estimators and then chose the one with the smallest variance. The two are not necessarily equivalent. 

## Best unbiased estimators
**Definition: (Estimator bias)** The _Bias_ of a point estimator $\theta^*$ of a parameter $\theta$ is the difference between the expected value of $\theta^*$ and the true value $\theta$; that is, $Bias_\theta[\theta^*] = E_\theta[\theta^*]-\theta$. An estimator with zero bias is called an _unbiased_ estimator and satisfies $E_\theta[\theta^*]=\theta$ for all values of $\theta$.

As there may be multiple MSE estimators, that is there can exist two unbiased estimators $\theta^*_1$, $\theta^*_2$ of a parameter $\theta$ with $E_\theta[\theta^*_1]=E_\theta[\theta^*_2]=\theta$ and mean squared errors equal to their variances, we would like to select the estimator with the smallest variance (if one exists). However, finding (constructing) such an estimator can be very difficult as there are many combinations of possible estimators in the unrestricted case.

**Definition: (Best estimator)** An estimator $\theta^*$ is a _best estimator_ of $\tau(\theta)$ if it satisfies $E_\theta[\theta^*]=\tau(\theta)$ for all values of $\theta$ and, for any other estimator $\tilde\theta$ with $E_\theta[\tilde\theta]=\tau(\theta)$, we have $Var_\theta[\theta^*]\leq Var_\theta[\tilde\theta]$. Also called the _uniform minimum variance unbiased estimator_ of $\tau(\theta)$.

**Theorem: (Cramer-Rao information inequality)** Let $X_1,\dots,X_N$ be a sample with pdf $f(\vec{x}|\theta)$, and let $\theta^*(\vec{X})$ be any estimator satisfying the restrictions $$\frac{d}{d\theta}E_\theta[\theta^*(\vec{X})] = \int_{\mathcal{X}}\frac{\partial}{\partial\theta}(\theta^*(\vec{x})f(\vec{x}|\theta))\, d\vec{x} \quad\text{and}\quad Var_\theta[\theta^*(\vec{X})]<\infty.$$Then $$Var_\theta[\theta^*(\vec{X})]\geq \frac{(\frac{d}{d\theta}E_\theta[\theta^*(\vec{X})])^2}{E_\theta[(\frac{\partial}{\partial\theta}\log f(\vec{X}|\theta))^2]}.$$While this theorem is stated in terms of pdfs (i.e., for continuous random variables), it also applies to discrete random variables. If $f(x|\theta)$ is a pmf, then we must be able to interchange differentiation and summation, assuming that even though $f(x|\theta)$ is a pmf and _not_ differentiable in terms of $x$, it is differentiable in $\theta$, which is the case for many common pmfs.

The bound depends only on $\tau(\theta)=E_\theta[\theta^*]$ and $f(x|\theta)$ and is a uniform lower bound on the variance, so any candidate estimator satisfying the restrictions and attaining this lower bound is a best unbiased estimator of $\tau(\theta)$. Importantly, it should be noted this lower bound may not be _tight_, that is to say, the lower bound may be strictly smaller than the variance of any unbiased estimator. 

**Corollary: (Cramer-Rao attainment)** Let $X_1,\dots,X_N$ be iid $f(x|\theta)$, where $f(x|\theta)$ satisfies the conditions of the Cramer-Rao Theorem. Let $L(\theta|\vec{x})=\prod_{i=1}^N f(x_i|\theta)$ denote the likelihood function. If $\theta^*(\vec{X})$ is any unbiased estimator of $\tau(\theta)$, then $\theta^*(\vec{X})$ attain the Cramer-Rao lower bound if and only if $$a(\theta)(\theta^*(\vec{x})-\tau(\theta^*))=\frac{\partial}{\partial\theta}\log(L(\theta|\vec{x}))$$for some function $a(\theta)$.


## Sufficiency and unbiasedness 
**Theorem: (Rao-Blackwell)** Let $\theta^*$ be any unbiased estimator of $\tau(\theta)$, and let $T$ be a [[Data reduction#^576682|sufficnet statistic]] for $\theta$. Define $\phi(T)=E[\theta^*|T]$. Then $E_\theta[\phi(T)]=E_\theta[E_\theta[\theta^*|T]]=E_\theta[\theta^*]=\tau(\theta)$ and $Var_\theta[\phi(\theta^*)]\leq Var_\theta[\theta^*]$ for all $\theta$; that is, $\phi(T)$ is a uniformly better estimator of $\tau(\theta)$. (p342)[[@Casella_2001]]

Therefore, conditioning any unbiased estimator on a sufficient statistic will result in a uniform improvement, provided $\theta^*$ is not already the best estimator, see below theorem. The sufficiency of the statistic is of critical importance, otherwise, $\phi(T)$ cannot be guaranteed to be a valid estimator of $\tau(\theta)$.

**Theorem:** If $\theta^*$ is a best unbiased estimator of $\tau(\theta)$, then $\theta^*$ is unique.

This then gives us another means of testing if an estimator is best. Specifically, if $\theta^*_1$ satisfies $E_\theta[\theta^*_1]=\tau(\theta)$ and $\theta^*_2$  satisfies $E_\theta[\theta^*_2]=0$, both are unbiased estimators. Then $$\phi_a=\theta^*_1+a\cdot\theta^*_2,$$where $a$ is a constant, satisfies $E_\theta[\phi_1]=\tau(\theta)$ and so is also an unbiased estimator of $\tau$. With variance $$Var_\theta[\phi_a]=Var[\theta^*_1+a\cdot\theta^*_2]=Var_\theta[\theta^*_1]+2a\cdot Cov_\theta[\theta^*_1,\theta^*_2]+a^2\cdot Var_\theta[\theta^*_2].$$Then if there exists a (single or multiple) value of $\theta$ such that $Cov_\theta[\theta^*_1,\theta^*_2]<0$, then we can make  $2a\cdot Cov_\theta[\theta^*_1,\theta^*_2]+a^2\cdot Var_\theta[\theta^*_2]<0$ by choosing $a\in (0,-2Cov_\theta[\theta^*_1,\theta^*_2]/Var_\theta[\theta^*_2])$, contradicting the possibility that $\theta^*_1$ is the best unbiased estimator. Likewise, if $Cov_\theta[\theta^*_1,\theta^*_2]>0$ for any $\theta$. This results in the following theorem.

This relationship is expressed in the following theorem.

**Theorem:** If $E_\theta[\theta^*]=\tau(\theta)$, $\theta^*$ is the best unbiased estimator of $\tau(\theta)$ if and only if $\theta^*$ is uncorrelated with all unbiased estimators of $0$.


## Loss function optimality
^da930c
The [[Point estimation#Mean square error|mean squared error]] performance of an estimator is a particular kind of _loss function_. Loss functions in the context of point estimation problems mean, if an action $a$ is close to $\theta$, then the decision $a$ is reasonable and little loss is incurred as a result. Likewise, if $a$ is far from $\theta$, then large loss is incurred. 

**Definition: (Loss function)** A loss function is a non-negative function, that typically increase in value as the distance between $a$ and $\theta$, the parameter being estimated, grows. ^45314f

The quality of an estimator can be quantified using a _risk function_, which represents the expected loss of a estimator (predictor).

**Definition: (Risk function)** For an estimator $W(\vec{x})$ of $\theta$, the risk function, a function of $\theta$, is $$R(\theta,W(\vec{x})) = E_\theta[L(\theta,W(\vec{X}))],$$for loss function $L(\cdot)$. ^1832d6

As the true value of $\theta$ is typically not known when estimating, we would like to use an estimator that has a small $R(\cdot)$ value for all values of $\theta$ possible under our model assumptions. Two estimator could then be be compared based on their risk values, comparison of the two based on plotting their values as $\theta$ varies, with the less of the two being selected.

We can also use a [[Bayesian probability theory|Bayesian]] approach to optimizing loss functions, e.g., [[Maximum posterior]]. If we have [[Fundamentals of probability theory#^4b7ad7|prior distribution]] $p(\theta)$, we can compute the average risk $$\int_\Theta R(\theta,W)p(\theta)\, d\theta,$$known as [[Maximum posterior#Bayes risk|Bayes risk]]. This gives us a number for assessing the performance of an estimator with respect to a give loss function, and find a estimator with the smallest Bayes risk. 