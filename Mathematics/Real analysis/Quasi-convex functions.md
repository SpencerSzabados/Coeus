---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - convex_functions
  - optimization
  - real_analysis
references:
  - https://sites.pitt.edu/~luca/ECON2001/lecture_14.pdf
---
---

# Quasi-convexity 
**Definition: (Quasi-convex sequence)** A sequence $\{a_i\}_{i=1}^N$ with terms that satisfy the condition $$\lambda a_i+(1-\lambda)a_j\leq \max\{a_i,a_j\}$$ for all $i,j$, and all $\lambda\in[0,1]$ is called quasi-convex.

**Definition: (Quasi-convex function)** A function $f$ is quasi-convex if for all $x,y$ in the (convex) domain of $f$ and $\lambda\in [0,1]$ we have $f(\lambda x + (1-\lambda)y)\leq \max\{f(x),f(y)\}$; alternatively, a function $f$ if for all $x,y$ in the convex domain, $f(x)\leq f(y)$ implies $f(\lambda x+(1-\lambda)y)\leq f(y)$ for all $\lambda\in [0,1]$.

On the other hand, a sequence is quasi-concave if for all $i,j$ and all $\lambda\in[0,1]$, $$\lambda a_i+(1-\lambda)a_j\geq \min\{a_i,a_j\}.$$

Just like for [[Convex functions]] quasi-convexity can be characterized by its sublevel set. A function $f:\mathbb{R}^d\to\mathbb{R}$ is quasi-convex if and only if the set $$\{x\in\mathbb{R}^d\mid f(x)\leq t\}$$is convex for all $t\in\mathbb{R}$.


**Theorem:** Any increasing or decreasing function is both quasi-convex and quasi-concave. [Luca lectures](https://sites.pitt.edu/~luca/ECON2001/lecture_14.pdf)


# Differentiable quasi-convex functions 
**Theorem:** Let $f:D\to \mathbb{R}$ be a $C^1$ function on the open set $D$. Then, $f$ is quasi-convex if and only if $f(y)\leq f(x)$ implies $\nabla f(y-x)\leq 0$. [Luca lectures](https://sites.pitt.edu/~luca/ECON2001/lecture_14.pdf)


# Maximizing quasi-convex functions
**Theorem: (Convex maximizers)** If $f:D\to\mathbb{R}$ is a quasi-concave function that attains a maximum in $D$, then the set of maximizers is convex. Moreover, if $f$ is strictly quasi-concave, the set of maximizers of $f$ is unique. [Luca lectures](https://sites.pitt.edu/~luca/ECON2001/lecture_14.pdf)

