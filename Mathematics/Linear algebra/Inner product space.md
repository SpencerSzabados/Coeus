**Definition: (Inner product)** Let $V$ be a [[Vector space]] over a [[Fields|field]] $\mathbb{F}$. An _inner product_ on $V$ is a function of the form $\langle \cdot,\cdot\rangle:V\times V\to \mathbb{F}$ satisfying for all $u,v\in V$: ^dcb7c3
  1) $\langle u,v\rangle = \langle v,u\rangle$;
  2) $\langle u+v,w\rangle = \langle u,w\rangle + \langle v,w\rangle$;
  3) $\langle cu,w\rangle = c\langle u,v\rangle$ for a scalar $c\in \mathbb{F}$;
  4) $\langle v,v\rangle \geq 0$ and $\langle v,v\rangle = 0$ if and only if $v=0$,
with respect to the underlying binary operations of $\mathbb{F}$. 

**Definition: (Inner product space)** A [[Vector space]] equipped with an inner product is called a _inner product space_. ^9508af

**Definition: (Matrix inner product)** Let $u$ and $v$ be vectors in $\mathbb{R}^n$. Then the Euclidean inner product $u\cdot v$ can be expressed using an invertible ([[Singular matrix#^afc451|singular]]) matrix $A\in \mathbb{R}^{n\times n}$ $$u\cdot v = Au\cdot Av = v^\intercal A^\intercal A u.$$Here we require $A$ to be invertible as inner product must satisfy the condition $$\langle u,v\rangle = 0 \text{ if and only if either }u=0\text{ or } v=0,$$which reduces to the requirement of $det(A)\neq 0$; otherwise, there exists a vector matrix pair whose product equals zero while neither are themselves zero.

**Observation: (Inner product norm)** Let $V$ be an inner product space. The norm, induced by the inner product placed on $V$, is $\|v\|=\sqrt{\langle v,v\rangle}$.

**Theorem: (Cauchy-Schwarz inequality)** If $u$ and $v$ are vectors from a inner product space $V$, then $$|\langle u,v\rangle| = \|u\|\|v\|$$

