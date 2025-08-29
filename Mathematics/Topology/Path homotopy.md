---
doc type: Note
authors: Spencer Szabados
date: 2024-07-03
tags:
  - topology
  - geometry
  - differential_geometry
  - curves
---
---

**Definition: (Path homotopy)** Let $X$ be a [[Topological spaces|topological sapce]]. Two paths (curves) $f:[0,1]\to X$ and $g:[0,1]\to X$ are _path homotopic_ if $$f(0)=x_0=g(0)\quad\text{and}\quad f(1)=x_1=g(1)$$and there exists a continuous function $F:[0,1]^2\to X$ s.t., $$\begin{align}F(s,0)&=f(s)&&\text{and}\quad F(s,1)=g(s),\\ F(0,t)&=x_0&&\text{and}\quad F(1,t)=x_1.\end{align}$$If $f$ is homotopic to $g$ it is denoted $f\cong_P g$.
