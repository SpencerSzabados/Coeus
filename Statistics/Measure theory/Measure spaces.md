---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - statistics
  - measure_theory
references:
  - "[[@Schervish_1995]]"
  -  [[@Ryff_1970]]
---
---
# Overview
Measurable spaces and functions play an central role in [[Riemann-Stieltjes Integrals]] (and analysis in general) and statistical probability measures. In fact, [[Random variables]] are a special case of random quantities studied in measure theory.

We begin with the definition of a measure and then will spend some time talking about its relation to probabilities as the two are intimately related (by definition).

**Definition: (Measure)** Let $X$ be a set and $\mathcal{B}$ a [[Fundamentals of probability theory#^9dcf42|sigma algebra]] over $X$. A function $\mu:\mathcal{B}\to\mathbb{R}$ is called a _measure_ if it satisfies the following conditions:  ^c048df
  1) For all $B\subseteq \mathcal{B}$, $\mu(B)\geq 0$;
  2) $\mu(\emptyset)=0$
  3) For all countable collections $\{B_i\}_{i\in I}$ of pairwise disjoint sets, $\mu\left(\bigcup_{i\in I} B_i\right) = \sum_{i\in I}\mu(B_i)$.
The pair $(X,\mathcal{B})$ is referred to as a measurable space.  ^7ac46e

**Definition: (Measure space)** A measure space is a triple $(X,\mathcal{B}, \mu)$ where $X$ is a set, $\mathcal{B}$ is a [[Fundamentals of probability theory#^9dcf42|sigma algebra]] on the set $X$, and $\mu$ is a measure on $(X,\mathcal{B})$, e.g,. [[Fundamentals of probability theory#^2f36d7|finite probability spaces]]. ^26a5cd

If $(X,\mathcal{B},\mu)$ is a measure space and $\mu(X)=1$, then $\mu$ is called a [[Fundamentals of probability theory#^0d5a58|probability]] (probability measure) and $(X,\mathcal{B},\mu)$ is also called a _probability space_. ^535f6f

I was confused about the difference between a measure (probability measure) and a [[Distribution functions of random variables#^1a548c|cdf]] or [[Distribution functions of random variables#^c46bbe|pdf]] when refereeing to a random variables probability distribution, i.e., in the statement, $X\sim p$ what is $p$, as the specific quantity referenced in literature is often inconsistent between sources. Recalling a [[Random variables#^5ceb15|random variable]] on $(\Omega,\mathcal{B},\mu)$ is a [[Functional measure spaces#^f47214|measurable function]] with a distribution that is itself a measure on $\mathbb{R}$; in particular, the distribution of a random variable is defined as the [[Push-forwards models#^3b91f2|push-forward measure]] $\mu_X=\mu\circ X^{-1}$ from $\Omega$ to $\mathbb{R}$. On the other hand, the pdf of $X$ is $f=d\mu_x/d\lambda$, where $\lambda$ is the [[Lebesgue integration#^c700cf|Lebesgue measure]] (or any other [[Convergence of measures#^d5a421|dominating measure]]). Thus, if the pdf exists (which is not always the case) it will entirely capture the probability measure of $X$, i.e., $\mu_X=\int f\,d \lambda$; likewise, the cdf captures all the relevant information about the pdf or measure. Thus, while these quantities are distinct (especially when the pdf does not exist) it is common to switch between the terms as the two are equivalent whenever the pdf exists. See [StackExchange](https://stats.stackexchange.com/questions/563949/difference-in-probability-measure-vs-probability-distribution), and [StackExchange](https://math.stackexchange.com/questions/1073744/distinguishing-probability-measure-function-and-distribution).

**Theorem:** If $\lambda$ represents the [[Lebesgue integration#^c700cf|Lebesgue measure]] on $[0,1]$ and $\mathcal{F}$ is a (equivalence) class of measurable functions then the distribution $$p(x)=\lambda\{y\mid \mathcal{F}(y)>x\}$$is a right continuous nonincreasing function. Moreover, the right continuous inverse of $p$ is $$f^*(y) = \sup_{p(x)>y}x$$where $f^*$ is called the _decreasing rearrangement_ of $\mathcal{F}$. ^aba5de

Many sets have zero measure but are non-empty. If a property holds for all points in a set $S$, with non-zero measure, except for a set $E\subset S$ with $\mu(E)=0$, this property is said to hold _almost everywhere_ on $S$. If $\mu$ is a probability, this statement is replaced with _almost surely_. This property is common in the literature surrounding [[Lebesgue integration]] (or more general notions of integration wrt measures). 
