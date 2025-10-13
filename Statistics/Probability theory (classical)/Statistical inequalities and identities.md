---
doc type: Note
authors: Spencer Szabados
date: 2025-10-09
tags:
  - statistics
  - identities
references:
---
---

This note contains some useful concentration (probability bounds) inequalities.

# Probability inequalities
**Theorem: (Chebychev's inequality)** Let $X$ be a random variable and let $g$ be a nonnegative function. Then, for any $r>0$, $$P(g(X)\geq r)\leq \frac{E[g(X)]}{r}.$$ 
Let $g(x)=(x-\mu)^2/\sigma^2$, where $\mu=E[X]$ and $\sigma^2=Var[X]$. Then for $r=t^2$, $$P\left(\frac{(X-\mu)^2}{\sigma^2}\geq t^2\right)\leq \frac{1}{t^2}E\left[\frac{(X-\mu)^2}{\sigma^2}\right]=\frac{1}{t^2}.$$ Consequently, we also get, $P(|X-\mu|\geq t\sigma)\leq 1/t^2$ and $P(|X-\mu|<t\sigma)\geq 1-1/t^2$. 

Chebychev's inequality is conservative due to it's generality. We can often derive tighter bounds when working with specific distributions.


# Probability identities
There is an entire class of identities that rely on integration by parts. 

**Theorem: (Stein's lemma)** Let $X\sim \mathcal{N}(\theta,\sigma^2)$, and let $g$ be a differentiable function satisfying $E[|g'(X)|]<\infty$ (finite). Then $$E[g(X)(X-\theta)] = \sigma^2 E[g'(X)].$$ ^3a15e0
