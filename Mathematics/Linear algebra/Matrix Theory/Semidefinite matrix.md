**Definition: (Semidefinite matrix)** Let $A$ be a [[Symmetric matrix|symmetric]] $n$-by-$n$ matrix. Then $A$ is _positive semidefinite_ if for all $x\in\mathbb{R}^n$, $x^\intercal Ax\geq 0$. Moreover, $A$ is positive definite if $x^\intercal Ax>0$ for all $x\neq 0$.   ^3592f0

A note on the structure of $A$, if $A$ is positive semidefinite, and $a_{ii}=0$ it is necessary that $a_{ij}=0$ and $a_{ji}=0$ for all $j$; that is, the row and column of the zero diagonal entry are all zeros.

A unique value associated with each positive semidefinite matrix is the square root $$A^{1/2}=Q\,diag(\lambda(A))\,Q^\intercal$$where $Q$ is a [[Orthogonal matrix]] which is part of the spectral decomposition of $A$. Moreover, as a direct consequence of the definition, $A$ is positive semidefinite if and only if $\lambda(A)_j\geq 0$ for all $j$; meaning, all its eigen values are nonnegative.

Another important decomposition for positive semidefinite matrix is the following:

**Theorem: (Cholesky decomposition)** Let $A$ be a real [[Symmetric matrix|symmetric]] $n$-by-$n$ matrix. Then $A$ is positive semidefinite if and only if there exits a lower triangular matrix $L\in\mathbb{R}^{n\times n}$ such that $$A=LL^\intercal.$$
**Characterization: (Diagonally dominant)** A matrix $A\in\mathbb{R}^{n\times n}$ is called _diagonally dominant_ if $$a_{ii}\geq \sum_{j\neq i}|a_{ij}|.$$Then, if $A$ is (strictly) diagonally dominate it follows that $A$ is positive semidefinite (positive definite).
  