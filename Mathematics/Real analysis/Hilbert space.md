---
doc type: Note
authors: Spencer Szabados
date: 2024-03-07
tags:
  - real_analysis
  - measure_theory
references:
  - https://people.eecs.berkeley.edu/~jordan/kernels/0521813972c03_p47-84.pdf
---
---

**Definition: (Hilbert space)** A _Hilbert space_, $\mathcal{H}$, is a complete [[Inner product space#^9508af|inner product space]]; where, a space is complete, if every Cauchy sequence $\{a_i\}_{i\geq 1}$ converges to an element $a\in \mathcal{H}$. See [[@Kreyszig_1978]]. 

**Definition: (Separable Hilbert space)** A Hilbert space $\mathcal{H}$ is separable, if for any $\epsilon >0$ there exists a finite set $a_1,\dots,a_N\in \mathcal{H}$ such that for all $a\in \mathcal{H}$, $\min_i\|a_i-a\|\leq \epsilon$; i.e., the space is dense.

Hilbert spaces are a subset of [[Banach space|Banach spaces]] that have more structure imposed; in particular, if a [[Banach space]] is equipped with an inner product that induces a valid norm the resulting space is a Hilbert space.
