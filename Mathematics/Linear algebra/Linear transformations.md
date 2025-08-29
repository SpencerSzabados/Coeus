---
doc type: Note
authors: Spencer Szabados
tags:
  - linear_algebra
---
---

Linear maps are the core underlying object of linear algebra.

# Overview 
**Definition: (Linear map)** Let $U$ and $V$ be vector spaces. A _linear mapping_ $T:U\to V$ (when $U=V$, $T$ is called a _linear operator_) is a mapping which satisfies the following two properties: for any elements $u,w\in U$ and any scalar $c$ taken from the underlying field ^e3ad7a
  1) $T(u+w) = T(u)+T(w)$;
  2) $T(cu)=cT(u)$.


**Definition: (Linear form)** A _linear form_ (or _covector_) is a linear map that takes vectors from their [[Vector space]] $U$ to the underlying field $\mathbb{F}$ in the form $T:U\to \mathbb{F}$ is called a _linear form_.

Where linear maps can be repressed as matrix-vector products, linear forms are more general (e.g., the trace of a matrix on the vector space of matrices) and can't always be represented using matrix products; however, a subset of linear forms can be represented as row-vectors-vector products. Thus, linear maps operation between vector spaces defined over the same field can be seen as the vertical concatenation of linear forms (also called linear functionals). That is, for vectors $x=(x_1,\dots,x_n)$ in a vector space $U$ on a field $\mathbb{F}$, linear forms can be expressed as row vectors of the from $a=[a_1\cdots a_n]$ where their functional form can be expressed as $$f_a(x)=a_1x_1+\cdots +a_nx_n = ax^\intercal.$$Obviously then, if we are given a linear map's matrix form $$T = \begin{bmatrix}a_{11} & a_{12} & \cdots &a_{1n}\\ a_{21} & a_{22} & \cdots & a_{2n}\\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn}\end{bmatrix}$$we can express this in terms of the vertical concatenation of $n$ linear forms $$T = \begin{bmatrix}a_{1}\\ \hline\\ a_{2}\\ \hline \\ \vdots\\ \hline\\ a_{n}\end{bmatrix}.$$
(Note, motivated by the fact the all linear operators can be represented by a matrix under an ordered basis, I was curious if you could construct a linear operator (or more general structure) that calculates the trace of a matrix without explicitly using index summation methods. Without resorting to writing the matrix as a large column vector or using other _hacks_ I could not find if it was possible. You can however definite the traces of a linear operator more directly using more general [[Tensor|tensor spaces]], see [blue](https://math.stackexchange.com/questions/850658/definition-of-trace-of-linear-operator).)

**Definition: (Nullspace or Kernel)** The _nullspace_ of a matrix $A$, which realises a linear mapping $T$, is the set of solutions to $Ax=0$, and is denoted $null(A)$. The term _kernel_ is used when, equivalently, referring to the set of solutions to the equation $T(x)=0$. [[@Lang_1986]].

**Theorem:** If $A\in\mathbb{R}^{m\times n}$, then $null(A)$ is a subspace of $\mathbb{R}^n$. Likewise, for more general vector spaces over a field.

**Definition: (Inverse map)** If $T:U\to V$ is a linear map and, if there exists another map $T^{-1}:V\to U$ where:
  1) $T\circ T^{-1} = 1\in V$; and 
  2) $T^{-1}\circ T = 1\in V$, 
then $T$ is said to be invertible with inverse $T^{-1}$. 

**Theorem: (Existence of inverse map)** A linear map $T:U\to V$ is invertible if and only if $T$ is one-to-one and onto. Thus, it must be possible to represent $T$ by a square matrix.

**Theorem:** If $T:U\to V$ is a linear map from a finite dimensional vector space $U$ to a vector space $V$, then the range of $T$ is finite dimensional and $rank(T)+nullity(T)=dim(V)$.

**Equivalences:** If $U$ and $V$ are finite-dimensional vector spaces with the same dimension and $T:U\to V$ is a linear map, then the following are equivalent:
  1) $T$ is one-to-one;
  2) $T$ is onto;
  3) $ker(T)=\{0\}$ (or $null(T)=\{0\}$).


# Continuity of linear transforms
The continuity of a linear transform is defined in terms of the so called operator norm.

**Definition: (Operator norm)** Suppose we are give two normed [[Vector space|vector spaces]] $U$ and $V$ defined over the same field $\mathbb{F}$ and a linear map $T:U\to V$. The operator norm of $T$ is defined as $$\|T\|=\sup_{\|v\|=1}\|T(v)\|=\sup_{\|v\|=1}\|Av\|,$$where $A$ is the matrix associated with $T$.   ^155a33

The operator norm expresses the maximum amount a linear operator stretches any vector. The operator norm is related to [[Matrix norm|matrix norms]] with operator norm being induced by the latter. More specifically, given two vector spaces $U$ and $V$ defined on $\mathbb{F}^n$ and $\mathbb{F}^m$ with vector norms $\|\cdot\|_u$ and $\|\cdot\|_v$. Then any $m\times n$ matrix $A$ induces a linear operator between $U$ and $V$  with induced operator norm on $\mathbb{F}^{m\times n}$ of $$\|A\| = \sup\{\|Au\|_v\mid u\in U \text{ with }\|u\|_u=1\}.$$ 

**Definition: (Continuous linear map)** A linear map $T:U\to V$ defined between two normed [[Vector space|vector spaces]] defined over the same field $\mathbb{F}$ is continuous if there exists a constant $L$ such that $$\|T(v)\|\leq L\|v\|$$for all $v\in V$ (or WLG all $v$ in the unit ball of same dimension as $V$). 

As a consequence, directly from the definition, we see if $T$ is continuous then it is also [[Lipschitz continuity|Lipschitz continuous]]. 

**Theorem: (Continuity of linear maps)** A linear transformation $T:U\to V$ between two normed vector spaces is continuous if $U$ is finite dimensional. 
_Proof:_ See [planetmath](https://planetmath.org/lineartransformationiscontinuousifitsdomainisfinitedimensional).

Moreover, if $T$ is invertible then $T^{-1}$ shares the same Lipschitz constant.


# Derivative of linear transforms
Special forms of linear transformations are outlined here, more generally see notes on real analysis.

When the transformation matrix $A$ considered is constant and acts on a vector $x$ directly, the derivative is trivial. In particular, if $f:\mathbb{R}^b\to\mathbb{R}^m$ by $f(x)=Ax+b$, then $\nabla f(x) = A$. See, [StackExchange-Xipan-Xiao](https://math.stackexchange.com/questions/153836/derivative-of-a-linear-transformation). More generally, if $g(t)$ is a differentiable function, we have $\nabla f(g(t)) = A(g'(t))$ by the chain rule.
