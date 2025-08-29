**Definition: (Skew-symmetric)** A matrix $A$ is _skew-symmetric_ if $A^\intercal = -A$; if $A$ is complex, then it is said to be _skew-Hermition_ if $A^* = -A$.

**Theorem:** If $A$ is any square matrix, then $A-A^\intercal$ is skew-symmetric.

**Definition: (Normal matrix)** A square matrix $A$ is said to be _normal_ if $$AA^*=A^*A,$$which includes Hermition matrices and Skew-Hermition matrices. ^00e6e9


# Eigenvalues and vector properties 
Symmetric (or generalization of such) matrices posses a number of nice properties relating to their [[Matrix decompositions]] and [[Eigenvalues and vectors]].

**Theorem:** If $A$ is a $n\times n$ symmetric matrix, then any two eigenvectors $u,v$ such that $Au\neq Av$ (i.e., have different eigenvalues) are orthogonal $u^\intercal v=0$ (or for the [[Inner product space#^dcb7c3|inner product]] of the space which $A$ resides). 

As a consequence of the above property symmetric matrices can admit orthonormal eigenvector basis. This follows from the fact that the algebraic and geometric multiplicity of eigenvectors match for symmetric matrices and so we can always find a sufficient number of mutually independent orthogonal eigenvectors (after normalization) to form a orthonormal basis.