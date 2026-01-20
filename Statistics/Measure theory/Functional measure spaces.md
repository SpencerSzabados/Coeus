---
doc type: Note
authors: Spencer Szabados
date:
tags:
  - measure_theory
  - functional_analysis
references:
  - https://www.stats.ox.ac.uk/~etheridg/integration.pdf
---
---

The topic of measurable functions comes up naturally when defining [[Lebesgue integration]] in the context of [[measure theory]] and [[Measure spaces]].

# Overview 
We can extend [[Measure spaces]] to function spaces in a straight forward manner.

**Definition: (Measurable function)** Let $(X, \mathcal{B})$ and $(Y,\mathcal{A})$ be two [[Measure spaces#^26a5cd|measure spaces]]. A function $f:(X,\mathcal{B})\to(Y,\mathcal{A})$ is measurable w.r.t $(X,\mathcal{B})$ if for each $A\in \mathcal{A}$, the pre-image $f^{-1}(A)\in\mathcal{B}$ is also a measurable set. ^f47214

E.g., In the simple case where $f:X\to \mathbb{R}$ is a real valued function, the function $f$ is measurable if for each [[Fundamentals of probability theory#^9dcf42|Borel set]] $A\in\mathcal{A}$ defined over $\mathbb{R}$, $\{w\mid f(w)\in A\}\in\mathcal{A}$.

The following result is immediate from the definition of the Borel field over a topological space; recalling the definition of continuity in terms of pre-images in [[Topological spaces]].

**Theorem:** All continuous function are measurable, and so are all monotone functions.


