---
doc type: Note
authors: Spencer Szabados
date: 2024-06-11
tags:
  - complex_analysis
  - real_analysis
---
---

**Definition: (Analytic function)** If $f:U\to \mathbb{C}$ is a function on a domain $U\subseteq \mathbb{C}$ and $p\in\mathbb{C}$, then $f$ is said to possess a complex derivative, or be complex differentiable, at $p$ if $$f'(p)=\frac{\partial f}{\partial z}(p)=\lim_{z\to p}\frac{f(z)-f(p)}{z-p}$$exists; such functions are called _analytic (or holomorphic) functions_. 

Analytic functions are also characterized by the Cauchy-Riemann equations (meaning they satisfy them); writing $f=u+iv$ (for some $u$ and $v$) then $$\frac{\partial u}{\partial x} = \frac{\partial v}{\partial y}\quad\text{and}\quad \frac{\partial u}{\partial y}=-\frac{\partial v}{\partial x}.$$
