---
doc type: Note
authors: Spencer Szabados
date: 2023-09-11
tags:
  - random_sampling
  - statistical_convergence
  - random_variables
---
___

There are a few ways someone could consider random variables to be equal.

**Definition: (Equality in distribution)** Let $X$ and $Y$ be two [[Random variables]] over a shared sample space $\mathcal{X}$. These random variables are said to be _equal in distribution_, denoted $$X=^{d} Y,$$if $X$ and $Y$ have the same distribution function; i.e., $P(X\leq x)=P(Y\leq x)$ for all $x\in \mathcal{X}$. See [StackExchange-whuber](https://stats.stackexchange.com/questions/66522/how-to-visualise-equal-in-distribution-in-the-context-of-stochastic-dominance).

Observe that if two random variables that are equal in distribution need not be identically equal. Moreover, if two random variables are equal in distribution and generate two respective [[Stochastic Process]], e.g., $\{X_t\}$ and $\{Y_t\}$, since at each step the random variables are equal in distribution it follow immediately the stochastic processes [[Random samples#^9a4542|converge in probability]].