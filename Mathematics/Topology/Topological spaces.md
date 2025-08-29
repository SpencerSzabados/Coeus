---
doc type: Note
authors: Spencer Szabados
date: 2023-09-11
tags:
  - topology
---
___
Much of the following is taken from [ncatlab](https://ncatlab.org/nlab/show/manifold).

**Definition: (Topological space)** A _topological space_ is a set $X$ along with a associated collection $\Omega\subseteq \mathcal{P}(X)$ of subsets of $S$ defined as the _open sets_ of $X$, which define the topology on the space, satisfying: ^8d2d2b
  1) $\emptyset \in \Omega$ and $X\in \Omega$;
  2) if $A,B\in \Omega$ then $A\cap B\in \Omega$;
  3) for any index set $I$, $\bigcup_{i\in I}A_i\in \Omega$; i.e., the arbitrary union of open sets is itself open.
The topological space is the ordered pair $(X,\Omega)$. [[@Munkres_2014]]

