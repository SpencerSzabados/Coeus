
**Definition: (eigen-values and eigen-vectors)** If $A$ is a $n$-by-$n$ matrix, then a non-zero vector $x$, from an appropriate vector space $V$ as determined by $A$, is called an eigenvector of $A$ if $$Ax=\lambda x \quad\text{or}\quad (\lambda I-A)x=0$$for some scalar value $\lambda\in\mathbb{F}$ taken from the underlying field of $V$. The scalar $\lambda$ is called an eigenvalues of $A$ corresponding to $x$.

The above definition is setup with right multiplication, resulting is what is more specifically called the right eigen-values of $A$. We can likewise analyse the left eigen-values of $A$, by inspecting $x^\intercal A = \lambda x^\intercal$.

**Theorem: (Eigenvalues of $A^k$)** Let $k\in\mathbb{Z}_{\geq 0}$ and $\lambda$ be an eigenvalue of a matrix $A$ with corresponding eigenvector $v$. Then $\lambda^k$ is an eigenvalues of $A^k$ and $v$ remains the corresponding eigenvector.

**Definition: (Characteristic polynomial)** If $A$ is a $n$-by-$n$ matrix, then $\lambda$ is an eigenvalue of $A$ if and only if it satisfies the equation (is a root) $$det(\lambda I -A)=0$$which is known as the _characteristic polynomial_ of $A$. ^5d1381

**Definition: (Eigenvalue multiplicity)** Let $A$ be a matrix. The number of times the (eigenvalue) term $\lambda-\lambda_0$ appears in the characteristic polynomial of $A$ is called the _algebraic multiplicity_ of $\lambda_0$. The dimension of the eigenspace corresponding to the eigenvalue $\lambda_0$ is called its _geometric multiplicity_.

**Theorem: (Geometric and algebraic multiplicity)** If $A$ is a square matrix, then for every eigenvalues of $A$ the geometric multiplicity is less than or equal to the algebraic multiplicity. 

**Theorem:** If $\lambda_1,\dots,\lambda_m$ are the eigenvalues of a $n\times n$ matrix $A$ and $v_1,v_2,\dots,v_m$ are the associated eigenvectors, then if $\lambda_1,\dots,\lambda_m$ are all distinct (meaning $m=n$), $v_1,\dots,v_m$ are necessarily linearly independent vectors and $n=m$.

**Definition: (Singular values)** The singular values of a matrix $A$ are the (nonnegative) square roots of the eigenvalues of $A^*A$ (adjoint operator); if $\lambda_i$ is and eigenvalue of $A$ then $\sigma_i=\sqrt{\lambda_i}.$  ^609241

