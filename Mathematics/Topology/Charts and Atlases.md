---
doc type: Note
authors: Spencer Szabados
date: 2024-06-01
tags:
  - topology
  - fundamentals
references:
  - "[[@Munkres_1991]]"
---
---

**Definition: (Chart)** A _chart_ $(U,\phi)$ on a [[Topological spaces|topological space]] $(X,\Omega)$ is an open subset $U\subseteq X$ together with an open [[Topological embeddings|embedding]] $\phi:\mathbb{R}^d\hookrightarrow U$; if $p=\phi(x_1,x_2,\dots,x_d)\in U$ the components $\phi=(x_1,x_2,\dots,x_d)$ are called (local) coordinates of $p$ on $U$, more specifically, $x_j=\phi^{-1}(p)\cdot e_j$ where $e_j$ is the $j$-th standard (orthogonal) basis vector. See [[@DoCarmo_1976]], [[@Munkres_1991]], also [StackExchange-peek-a-boo](https://math.stackexchange.com/questions/3750478/why-x-has-superscript-i-in-the-expression-partial-partial-xi-different)  ^8405be

Charts are also referred to as _Coordinate patches_, see [[Differential manifolds]].  ^ef5c73

**Definition: (G-atlas)** A $G$-atlas on a topological space $X$ is a family of $G$-compatible charts $\{\phi_i:U_i\hookrightarrow X\}_{i\in I}$ such that $\{U_i\}_{i\in I}$ covers $X$. ^684817