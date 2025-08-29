---
doc type: Note
authors: Spencer Szabados
date: 2024-03-07
tags:
  - kernel_methods
  - linear_algebra
  - machine_learning
  - probability_theory
  - dimension_reduction
references:
  - https://www.cs.princeton.edu/~bee/courses/scribe/lec_10_09_2013.pdf
---
---

# Overview 
Most generally a kernel is any function of the form $\kappa:X\times X\to \mathbb{R}$. Typically these functions are constructed to be analogous to [[Inner product space#^dcb7c3|inner products]] or report some notion of similarity between points.

Kernel functions can be defined by constructing a feature map $\phi:X\to \mathcal{H}$, which extracts important features in the data, and setting $\kappa = \langle \phi(\cdot),\phi(\cdot)\rangle$. However, it is often difficult to chose $\phi$, given that we often which $\kappa$ to obey various constraints. Consequently, it would be helpful to be able to construct new kernel functions from existing examples. The following theorem characterizes how to achieve this and when this is possible.

**Definition: (Finitely positive semi-definite function)** A function $\kappa:X\times X\to \mathbb{R}$ is _finitely positive semi-definite_ if (1) the function is symmetric, and (2) for any finite subset $\{(a_i,b_i)\}_{i\in I}\subset X\times X$ the matrix with entires $K_{ij} = \kappa(a_i,b_j)$ is [[Semidefinite matrix#^3592f0|positive semidefinite]].

**Theorem: (Kernel characterization)** A function $\kappa:X\times X\to \mathbb{R}$ that is either continuous (or has finite domain) can be decomposed into the form $\kappa(x,y)=\langle \phi(x),\phi(z)\rangle$, wrt a feature map $\phi:X\to \mathcal{H}$ mapping into a [[Hilbert space]], if and only if it is finitely positive semi-definite.


# Gram matrices
Gram matrices are a form of [[Linear transformations#^e3ad7a|linear transform]] whose entires are constructed using a kernel function defined over the space.

**Definition: (Gram matrix)** Let $\mathcal{H}$ be a [[Hilbert space]] and a collection of vectors, in this space, say $\{x_1,\dots,x_n\}$. The _Gram matrix_, corresponding to this set of vectors, is the $n\times n$ matrix with entires $G_{ij}=\langle x_i,x_j\rangle$.

Related to the gram matrix are kernel matrices, which differ by their use of kernel functions in place of the spaces inner product.

**Definition: (Kernel matrix)** Let $\mathcal{H}$ be a [[Hilbert space]] and $\{x_1,\dots,x_n\}$ be a collection of points from this space. If $\kappa: \mathcal{H}\times \mathcal{H}\to \mathbb{R}$ a kernel function, where $\kappa$ evaluates the similarity between points in a [[Knowledge representation and features#^6582bd|lifted]] space under the map $\phi$, the corresponding $n\times n$ kernel matrix has entires $K_{ij} = \langle \phi(x_i),\phi(x_j)\rangle = \kappa(x_i,x_j)$.


# Bergman (reproducing) kernel functions 