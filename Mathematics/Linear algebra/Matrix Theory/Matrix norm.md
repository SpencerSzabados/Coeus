**Definition: (Matrix norm)** Given a vector space $V$ of $n\times m$ matrices over a field $\mathbb{F}^{n\times m}$. A matrix norm $\|\cdot\|$ is a norm on spaces of the form of $V$; that is, that is $\|\cdot\|:V\to \mathbb{F}$ that satisfies the following for all $a\in\mathbb{F}$ and $A,B\in V$:
  1) $\|A\|\geq 0$;
  2) $\|A\|=0$ iff $A=0$;
  3) $\|aA\|= |a|\|A\|$;
  4) $\|A+B\|\leq \|A\|+\|B\|$.

One of the most commonly used norms is the Frobenius norm.

**Definition: (The Frobenius norm)** If $A$ is a matrix, its Frobenius norm is $$\|A\|_F = \sqrt{\sum_{{i,j}}a^2_{i,j}},$$which is analogous to the Euclidean norm.

**Definition: (Induced matrix norm)** Given two vector norms $\|\cdot\|_v$ and $\|\cdot\|_u$ defined respectively over [[Vector space|vector spaces]] $V$ and $U$ of dimensions $d$ and $n$ over a common field (e.g., $\mathbb{R}$), the _induced matrix norm_ (equivalent to [[Linear transformations#^155a33|operator norm]]) is defined as: for any $A\in V\otimes U$ (see [[Tensor]]), $$\|A\| = \max_{\|v\|_v\neq0}\|Av\|_u;$$which satisfies the inequality $$\|Av\|_u\leq \|A\|\cdot\|v\|_v$$

**Definition: (Spectral norm)** The _spectral norm_ is the matrix norm that is induced by the $\mathcal{l}_2$ [[Vector space#^f3101d|norm]] (Euclidean norm) and is equal to the maximum singular value of a matrix $A$; that is, $$\|A\|_2=\sup_{x\neq 0}\frac{\|Ax\|_2}{\|x\|_2}=\sqrt{\lambda_0}$$where $\lambda_0$ is the largest [[Eigenvalues and vectors|eigenvalue]] of $A^*A$ (with $A^*$ denoting the conjugate transpose of $A$); i.e., the spectral norm is equal to the largest [[Eigenvalues and vectors#^609241|singular value]] of $A$.

Observe, the [[Linear transformations#^155a33|operator norm]] induced by $\mathcal{l}^2$ is equal to the spectral norm. 