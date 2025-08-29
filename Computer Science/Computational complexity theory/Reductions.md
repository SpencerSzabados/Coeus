---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - complexity_theory
references:
---
---

**Definition: (Karp reduction)** A _reduction_ given by a polynomial time computable transformation of one problem into another, see [NIST](https://xlinux.nist.gov/dads/HTML/karpreductin.html). More technically, if $A$ and $B$ are two decision problems, a _karp reduction_ from $A$ to $B$, denoted $A\leq_p B$, is a function $f:A\to B$ mapping instances of $A$ to instances of $B$ such that: ^fae59d
  1) $f(I)$ can be computed in polynomial-time for any $I\in A$, and
  2) $I$ is a yes-instance of $A$ if and only if $f(I)$ is a yes-instance of $B$, and vise versa.
^a0ff95

Reductions are a many-to-one mapping, which do not need to be injective or surjective.

**Theorem:** For two problems $A$ and $B$ where $A\leq_p B$, then 
  1) If $B\in P$ then $A\in P$;
  2) If $A\not\in P$ then $B\not\in P$.

**Lemma: (Transitivity of reductions)** If $A\leq_p B$ and $B\leq_p C$, then $A\leq_p C$.


