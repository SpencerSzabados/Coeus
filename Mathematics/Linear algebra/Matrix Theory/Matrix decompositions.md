---
doc type: Note
authors: Spencer Szabados
date:
tags:
  - matrix_theory
references:
  - "[[@Fiedler_2013]]"
---
---

One of the more common decompositions of a square matrix is based on its [[Eigenvalues and vectors]], and converts the matrix to a matrix-matrix product composed of a transformation matrix and a diagonal matrix.

**Definition: (Eigenvalue decomposition)** If $A$ is a $n\times n$ matrix with eigenvalues $\lambda_1,\lambda_2,\dots,\lambda_n$ (with multiplicity) and $n$ linearly independent eigenvectors $v_1,v_2,\dots,v_n$. Let $Q=[v_1 | v_2 | \dots | v_n]$ and $D=diag(\lambda_1,\lambda_2,\dots,\lambda_n)$, then the _eigenvalue decomposition_ of $A$ is given as $AQ=QD$ or $A=QDQ^{-1}$; i.e., this is just a [[Similar matrix#^335d8c|diagonalization]] of the matrix and therefore $A$ possessing such a decomposition is equivalent to $A$ being diagonalizable. ^a912fc

The diagonal matrix is convenient for computing higher powers of a matrix, as $A^n = QD^nQ^{-1}$. Moreover, the inverse can be easily taken, since $A^{-1} = QD^{-1}Q^{-1}$ (with the two P's swapping positions and their inverses taken).

Note that the eigenvalue decomposition of a matrix need not be unique, see [StackExchange-Nick-Alger](https://math.stackexchange.com/questions/320220/intuitively-what-is-the-difference-between-eigendecomposition-and-singular-valu#320232).


# Cholesky decomposition 
The Cholesky decomposition appears naturally in many applications involving [[Statistical transformations]] as its convenient for transforming symmetric [[Semidefinite matrix | semidefinite matrices]]. 

![[Semidefinite matrix#^d24b4a]]

