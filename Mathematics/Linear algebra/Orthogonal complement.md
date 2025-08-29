

**Definition: (Orthogonal complement)** Let $W$ be a subspace of $\mathbb{F}^n$ (or in general a [[Vector space]] $V$), $$W^\perp = \{x\mid \langle x, y\rangle=0 \text{ for all } y\in W\}$$is called the _orthogonal complement_ of $W$ wrt the [[Inner product space#^dcb7c3|inner product]] $\langle\cdot \rangle$ and the zero element $0$. 

As a common example, take the vector space $W$ induced by a real valued matrix $A\in\mathbb{}R^{2\times 2}$ over all $x\in\mathbb{R}^2$; that is, $W = \{u\mid Ax=u \text{ with }x\in\mathbb{R}^2\}$ is the column space of $A$. The orthogonal complement of $W$ is then $W^\perp = \{v\mid u\cdot v=0 \text{ for }u\in W\}$. TODO - figure out how to write the orthogonal complement in term of the original matrix.

**Properties:** Let $W$ be a subspace of a vector space $V$, then
  1) $W^\perp$ is a subspace of $V$;
  2) $W\cap W^\perp = \{0\}$;
  3) $(W^\perp)^\perp = W$;
  4) $V^\perp = \{0\}$.

The row-space is the orthogonal complement of the null-space of a matrix.

**Theorem:** Let $A$ be a matrix and let $W=col(A)$. Then $$W^\perp = null(A^\intercal).$$

**Theorem:** Let $W$ be a subspace of a $n$-dimensional vector space $V$. Then $$dim(W)+dim(W^\perp) = dim(V)=n.$$

This last theorem is very notable, as it allows us to conclude concretely a useful fact about vector representations.

**Corollary:** Let $v\in\mathbb{R}^d$ be given. Then any vector $x\in\mathbb{R}^d$ can be expressed uniquely in the form $$x=cv+u,$$where $c\in\mathbb{R}$ and $u\in span(v)^\perp$, that is, $u$ is a vector from the orthogonal complement of the span of $v$.

This corollary can be helpful in reformulating integrals involving probability through, essentially, projection of the problem to another space.


# Computing orthogonal complements
Computing the orthogonal complement of a subspace is generally easier when you rewrite the subspace in terms of the column space or null space of a matrix. [Margalit](https://textbooks.math.gatech.edu/ila/orthogonal-complements.html)

