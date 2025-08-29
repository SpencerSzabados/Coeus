---
doc type: Note
authors: Spencer Szabados
date: 2024-05-28
tags:
  - random_sampling
  - statistics
references:
---
---

# Overview 
Inverse sampling is a method of sampling distributions, that are not [[Families of distributions#Discrete uniform distribution|uniformly distributed]] which are among the only distributions we can directly sample at random (pseudo-random), by making use of the inverse of the [[Statistical transformations#^a89d65|probability integral transform]]. 

## Inverse sampling 
Inverse sampling takes samples from a $U\sim Uniform(0,1)$ distribution and treats these values as probabilities that are then passed through the target distributions [[Statistical transformations#^f0ea0a|inverse cdf]], $F_X^{-1}(U)$, to yield random samples, $X(U)=F_X^{-1}(U)$, from the desired distribution.

The cdf of a distribution may not have a close form inverse, as such the values of $F_X^{-1}(U)$ will need to be empirically evaluated which is computationally inefficient for many distributions. See [Wiki](https://en.wikipedia.org/wiki/Inverse_transform_sampling), [ttested](https://www.ttested.com/generating-normal-random-variables-part-1/).