---
doc type: Note
authors: Spencer Szabados
tags:
  - linear_algebra
  - determinant
  - matrix_theory
---
---

# Overview 
The determinate of a matrix is an important summary metric of a bunch of the matrices properties. 

**Definition: (Matrix Determinant)** Let $\mathbb{F}$ be a field and $A\in \mathbb{F}^{n\times n}$. The determinant is a function $det:\mathbb{F}^{n\times n}\to \mathbb{F}$ that is [[Multilinear maps|n-linear]], meaning for each $1\leq i\leq n$, $det$ is linear in the $i$-th row (or column) of $A$ when the other rows (columns) are fixed, and is [[Multilinear maps#^03db95|alternating]] with $det(I)=1$. The determinant is unique for any $n$, and for a given matrix $A$ can be computed as $$det(A)=\sum_{i=1}^n(-1)^{i+j}A[i|j]det(A[i|j])$$where $A[i|j]$ denotes removing the $i$-th row and $j$-th column of $A$; this equation is called the Laplace expansion. ^709aeb