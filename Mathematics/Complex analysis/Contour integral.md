---
doc type: Note
authors: Spencer Szabados
date: 2024-06-11
tags:
  - complex_analysis
  - real_analysis
  - integration
---
---

Contour integrals (also called line integrals or path integrals) express how to integrate a function along a curve.

# Overview 
We will being by presenting some simple results for contour integration for scalar functions.

**Definition: (Contour integral)** Let $f:U\to \mathbb{C}$ be a continuous function over a open set $U\subseteq \mathbb{C}$ and $\gamma:[a,b]\to U$ be a piecewise continuously differentiable curve, say with components $\gamma_1,\dots,\gamma_N$ and corresponding partition $a<t_1\leq t_2\leq \cdots\leq t_N<b$. The contour integral of $f$ along $\gamma$ is defined as $$\int_\gamma f(z)\,dz = \int_a^{t_1}f(\gamma_1(t))\cdot\gamma_1'(t)\,dt + \cdots+\int_{t_N}^{b}f(\gamma_N(t))\cdot\gamma_n'(t)\,dt.$$    
