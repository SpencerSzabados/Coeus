---
doc type: Note
authors: Spencer Szabados
tags:
  - linear_algebra
---
---

# Overview
**Definition: (Vector space)** A _vector space_ over a [[Fields|field]] $\mathbb{F}$ is a set $V$ together with two binary operations $+:V\times V\to V$ and $\cdot:\mathbb{F}\times V\to V$ that satisfies the conditions:
1. Associativity: $\forall u,v,w\in V$, $u+(v+w)=(u+v)+w$;
2. Commutativity: $\forall u, v\in V$, $u+v=v+u$;
3. Identity: $\exists 0\in V$ s.t., $\forall v\in V$, $v+0=v$;
4. Inverse: $\forall v\in V$, $\exists -v\in V$ s.t., $v+(-v)=0$;
5. Associativity of multiplication: $\forall a,b\in \mathbb{F}$, $\forall v\in V$, $a(bv)=(ab)v$;
6. Multiplicative identity: $\forall v\in V$, $\exists 1\in \mathbb{F}$ s.t., $1v=v$;
7. Distributivity of multiplication: $\forall a\in \mathbb{F}$, $\forall u,v\in V$, $a(u+v)=au+av$;
8. Distributivity of field multiplication: $\forall a,b\in \mathbb{F}$, $\forall v\in V$, $(a+b)v=av+bv$. 

**Definition: (Span)** Let $v_1,\dots,v_n$ be vectors in a vector space $V$ defined over a field $\mathbb{F}$. The _span_ of $v_1,\dots,v_n$ is defined as the smallest subspace $W\subseteq V$; Equivalently,  $$span(v_1,\dots,v_n) = \left\{\sum_{i=1}^nc_iv_i\mid c_i\in \mathbb{F}\right\}.$$  ^318dc4

**Definition: (Basis vectors)** Let $V$ be a finite dimensional vector space. A set of linearly independent vectors $B=\{v_1,\dots,v_n\}$ that span $V$ is known as a basis of $V$. 

Due to the strictures of linear independences of basis vectors, each element $v$ of $V$ can be written uniquely as a linear combination of said basis vectors, $$v = c_1v_1+c_2v_2+\cdots+c_nv_n.$$Moreover, by fixing the order of the basis vectors considered, say $B=(v_1,v_2,\dots,v_n)$, we can refer to elements of $V$ by way of their linear combination coefficients; i.e., $v=(c_1,c_2,\dots,c_n)$. Fixing an ordering to basis vectors induces a coordinate systems on $V$ where the $i$-th coordinate $c_i$ of $v$ equals the magnitude of the $i$-th (ordered) basis vector in the linear combination of $v$, see [StackExchange-ConfusedMonkey](https://math.stackexchange.com/questions/2299345/coordinate-system-vs-ordered-basis).

**Theorem:** Let $V$ be a $n$-dimensional vector space and let $B$ be a set of exactly $n$ vectors from $V$. Then $B$ is a basis of $V$ if and only if $B$ spans $V$ or all the vectors of $B$ are linearly independent.

**Corollary: (Basis size)** All basis for a finite-dimensional vector space contain an equal number of vectors. 


# Dual vector space

**Definition: (Algebraic duel space)** 


# Normed vector spaces

**Definition: (Euclidean norm)** A vector norm is any function $\|\cdot\|:V\to \mathbb{R}$ that satisfies: for any $v\in V$ ^e3d7ec
  1) $\|v\|\geq 0$ and $\|v\|=0$ if and only if $v=0$; (definite)
  2) For all $\lambda \in \mathbb{F}$, $\|\lambda v\|=|\lambda|\cdot\|v\|$; (homogeneous)
  3) For all $v,w\in v$, $\|v+w\|\leq \|v\|+\|w\|$; (triangle inequality).

**Definition: (p-norm)** For any vector $v\in V$ the $l_p$ norm of the vector is defined as $$\|x\|_p = \left(\sum_{i=1}^d |v_i|^p\right)^{1/p}$$and by convention $p=\infty$ is taken to be $$\|v\|_\infty = \max_i |v_i|$$ ^f3101d

**Theorem: (Norm equivalence)** For any two (Euclidean) norms $\|\cdot\|_a$ and $\|\cdot\|_b$ defined on the same vector space $V$ which is of dimension $d$, there exists constants $c_d,C_d\in \mathbb{R}$ such that $$c_d\|v\|_a\leq \|v\|_b\leq C_d\|v\|_a.$$An important subtlety is that these constants depend on the dimension of the vector space.


**Definition: (Dual norm)** The dual $\|\cdot\|_\circ$ of a norm $\|\cdot\|$ is defined as $$\|v\|_\circ = \max_{w\neq 0}\frac{w^\intercal v}{\|w\|} = \max_{\|w\|=1}w^\intercal v.$$
The dual norm of the $l_p$ norm is the $l_q$ norm where $1/p+1/q=1$. The dual norm satisfies the inequality $$w^\intercal v\leq |w^\intercal v|\leq \|w\|\cdot \|v\|_\circ$$from which the [[Cauchy-Schwarz inequality]] an be derived from. 


# Subspaces

**Definition: (Direct sum)** Let $V$ be a vector space and $U_1,U_2\subseteq V$ be subspaces. Then $V$ is the direct sum of these subspaces; that is, $$V=U_1\oplus U_2=\{u_1+u_2\mid u_1\in U_1, u_2\in U_2\},$$ provided that:
1. $\forall v\in V$, $\exists u_1\in U_1,u_2\in U_2$ s.t., $v=u_1+u_2$; 
2. $U_1\cap U_2 = \{0\}$. [math.libretexts](https://math.libretexts.org/Bookshelves/Linear_Algebra/Book%3A_Linear_Algebra_(Schilling_Nachtergaele_and_Lankham)/04%3A_Vector_spaces/4.04%3A_Sums_and_direct_sum)

