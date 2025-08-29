**Definition: (Similar matrix)** A $n$-by-$n$ matrix $A$ is said to be _similar_ to another $n$-by-$n$ matrix $B$ if there exists a nonsingular matrix $Q$ such that $A=Q^{-1}BQ$. This relation is typically denoted $A\sim B$.

**Properties:** If $A$ is similar to $B$ the the following properties hold: 
  1) $det(A)=det(B)=det(Q^{-1}AQ$;
  2) $rank(A)=rank(B)$
  3) $nullity(A)=nullity(B)$
  4) $A$ and $B$ have the same [[Eigenvalues and vectors#^5d1381|characteristic polynomial]];
  6) $A$ is invertible if and only if $B$ is invertible; (follows directly form 4)


# Diagonalizable matrices
**Definition: (Diagonalizable matrix)** A square matrix $A$ is said to be diagonalizable if it is similar to a diagonal matrix; in particular, a matrix $A$ is diagonalizable if there exists an invertible matrix $Q$ such that $Q^{-1}AQ=D$, where $D$ is a diagonal matrix.   ^335d8c

**Theorem: (Diagonalizable and eigenvalue multiplicity)** If $A$ is a square matrix, then it is diagonalizable if and only if the gematric multiplicity of all its eigenvalues are equal to their algebraic multiplicity.

**Theorem: (Triangle matrix)** A triangle matrix $A$ with distinct entries along its main diagonal is diagonalizable.
_Proof (idea):_ The eigenvalues of a triangular $n$-by-$n$ matrix $A$ lie on the main diagonal. Thus, if all the eigenvalues are distinct, $A$ is composed of linearly independent vectors (invertible) and the corresponding eigenvectors each have geometric multiplicity one and yield a invertible matrix $Q$ such that $Q^{-1}AQ$ is diagonal.

There is another important theorem relating [[Symmetric matrix|symmetric matrices]] to diagonalizable matrices (and likewise [[Eigenvalues and vectors#^a912fc|eigenvalue decompositions]]).

**Theorem: (Diagonalizability of real matrices)** If $A$ is a real valued symmetric matrix, then its is diagonalizable; moreover, the diagonalizing matrix $P$ is constructed using only real valued eigenvectors and $D$ using real eigenvalues.