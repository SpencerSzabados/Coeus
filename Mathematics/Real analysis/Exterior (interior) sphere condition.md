---
doc type: Note
authors: Spencer Szabados
date: 2024-06-13
tags:
  - optimization
  - differential_geometry
  - topology
---
---

The exterior and internal sphere condition nicely characterize several results within [[Convex optimization]] and [[Quasi-convex functions]] optimization.

**Definition: (Exterior sphere condition)** Let $U$ be a domain, in a [[Metric spaces]] for instance, with boundary $\partial U$. The domain $U$ is said to satisfy the _(uniform) exterior sphere condition_ if there exists a $r>0$ s.t. for all $x\in\partial U$ there exists a $z\not\in U$ with $\|x-z\|=r$ and $$B(z,r)\cap U = \emptyset.$$The domain $U$ is said to satisfy the _(uniform) Interior sphere condition_ if $({\rm int U})^c$, the complement of the interior, satisfies the (uniform) exterior sphere condition. See [[@Nour_2009]].

