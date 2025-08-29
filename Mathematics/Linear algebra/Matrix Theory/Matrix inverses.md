
# Generalizations of matrix inverse 
When not concerned so much with the injectivity of the [[Linear transformations]] underlying a matrix equation we can define a Pseudo-inverse of any matrix.

**Definition: (Matrix pseudo-inverse)** Let $A\in\mathbb{F}^{m\times n}$ be a matrix, the pseudo-inverse (or Moore-Penrose inverse) of $A$ is a matrix $A^+\in\mathbb{F}^{n\times m}$ such that: ^73409a
  1) $AA^+A=A$; thus, $AA^+$ need not be equal to $I$, but $AA^+$ must map all the column vectors of $A$ to themselves.
  2) $A^+AA^+=A^+$ (Weak inverse property)
  3) $(AA^+)^*=AA^+$ and $(A^+A)^*=A^+A$; meaning both $AA^+$ and $A^+A$ are Hermitian matrices.
The pseudo-inverse exits for all matrices. In the special case where $A$ is of full [[Matrix rank|rank]] (i.e., $rank(A)=\min\{m,n\}$) then $A^+$ has a simple expression, specifically if $A$ has linearly independent columns $$A^+=(A^*A)^{-1}A^*,$$and alternatively, if $A$ has linearly independent rows $$A^+ = A^*(AA^*)^{-1}$$which are the respective left and right inverses of $A$. See [Wiki](https://en.wikipedia.org/wiki/Moore%E2%80%93Penrose_inverse#Definition).

If $A$ is a real [[Symmetric matrix]] with eigenvalues $\lambda_1,\dots,\lambda_n$ and a corresponding eigenvector [[Orthogonal matrix|orthonormal]] basis $v_1,\dots,v_n$, the pseudo-inverse of $A$ is given as $$A^+ = \sum_{\lambda_i\neq 0}\frac{1}{\lambda_i}v_iv_i^\intercal$$
 
  