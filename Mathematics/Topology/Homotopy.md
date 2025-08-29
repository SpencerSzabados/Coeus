---
doc type: Note
authors: Spencer Szabados
date: 2024-07-03
tags:
  - topology
  - abstract_algebra
  - group_theory
---
---

The notion of Homotopy is a weaker condition to that of [[Groups#^b4ee53|homomorphism]].

**Definition: (Homotopic functions)** Let $X$ and $Y$ be a topological spaces, and $f:X\to Y$ and $g:X\to Y$ be two continuous functions. The functions $f$ and $g$ are _homotopic_ if there exists a continuous map $F:X\times [0,1]\to Y$ s.t., $$F(x,0)=f(x)\quad\text{and}\quad F(x,1)=g(x)$$for all $x\in X$, and we write $f\cong g$.