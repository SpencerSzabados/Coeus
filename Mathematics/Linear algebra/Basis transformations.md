---
doc type: Note
authors: Spencer Szabados
date:
tags:
  - linear_algebra
  - vector_space
references:
  - "[[@Hoffman_1971]]"
---
---

# Overview
**Definition: (Vector space basis)** Let $V$ be a vector space. A _basis_ for $V$ is a linearly independent set of vectors $\mathcal{B}\subseteq V$ with $span(\mathcal{B})=V$. The vector space $V$ is finite-dimensional iff it admits a finite basis. 

**Theorem:** If $A$ is a $n\times n$ symmetric matrix, then we can construct a orthonormal basis composed of the eigenvectors of $A$ (normalized).


# Transformations 
**Definition: (Basis transformation matrix)** If we change basis in a vector space $V$ from the ordered basis $B=(u_1,u_2,\dots,u_n)$ to $B'=(v_1,\dots,v_n)$. Then for each vector $w\in V$ the old coordinate vector $(w)_B$ is related to its new coordinate vector $(w)_{B'}$ by $$(w)_{B'} = P_{B\to B'}(v)_B,$$where $$P_{B\to B'} = \left[(u_1)_{B'}\mid(u_2)_{B'}\mid\cdots\mid(u_n)_{B'}\right]$$is the change of basis matrix from $B$ to $B'$.  ^2ddc4c

The change of basis matrix is always invertible by construction, as it is square and composed of linearly independent vectors.

**Observation: (Inverse of basis transformation matrix)** If $B$ and $B'$ are basis of a vector space $V$ and $P_{B\to B'}$ and $P_{B'\to B}$ are change of basis matrices. Notice, $$P_{B'\to B}P_{B\to B'} = P_{B\to B} = I,$$hence $P_{B\to B'} = (P_{B'\to B})^{-1}$. 

**Corollary:** Suppose $V$ is a finite dimensional inner product space and $P$ is a transition matrix between two orthogonal basis $B$ and $B'$, then the transition matrix $P_{B\to B'}$ is [[Orthogonal matrix|orthogonal]]. 

