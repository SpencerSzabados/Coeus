---
doc type: Note
authors: Spencer Szabados
tags:
  - linear_algebra
  - multilinear_algebra
references:
  - "[[@Spivak_1995]]"
---
---

Tensors are a topic closely related to [[topology]], [[category theory]], and [[linear algebra]]. They describe a [[Multilinear maps|multilinear]] relationship between sets of algebraic objects related to a [[Vector space]]; and generalise the notion of a scalar, vector, and matrix (e.g., three dimensional matrices [O'Rourke](https://mathoverflow.net/questions/48045/why-are-matrices-ubiquitous-but-hypermatrices-rare) are a kind of simple tensor).


# Overview 
There are two common delivery methods for defining tensors, the one chosen here is based on tensor products formulated in terms of bilinear functions [[@Roman_2008]]; however, this definition is given in a very general fashion rather than the more direct definition over $\mathbb{R}$ given in [[@Spivak_1995]].

**Definition:(Measuring family)** Let $A$ be a set and let $\mathcal{X}$ be a family of sets. Let $$\mathcal{F} = \{g:A\to Y|Y\in\mathcal{X}\}$$be a family of functions, all having domain $A$ and range $Y\in\mathcal{X}$. Secondly, let $$\mathcal{H}=\{\alpha:X\to Y|X,Y\in\mathcal{X}\}$$be a family of functions, where 
  1) $\mathcal{H}$ contains the identity function $I_X$ for each member of $\mathcal{X}$;
  2) $\mathcal{H}$ is closed under composition of functions, which is an associative action on the set;
  3) For any $\alpha\in\mathcal{H}$ and $f\in\mathcal{F}$, the composition $\alpha\circ f$ is well defined and belongs to $\mathcal{F}$; that is, $\alpha\circ f:A\to Y$ for $Y\in\mathcal{X}$. 
The set $\mathcal{H}$ is called the _measuring family_ of $\mathcal{X}$ and its members are referred to as _measuring functions_. A pair $(X,f:A\to X)$ with $X\in\mathcal{X}$ and $f\in\mathcal{F}$ has the _universal property_ for $\mathcal{F}$ as measured by $\mathcal{H}$, or is called a _universal pair_ for $(\mathcal{F},\mathcal{H})$, if for every $g:A\to Y$ in $\mathcal{F}$, there is a unique $\alpha:X\to Y$ in $\mathcal{H}$ for which $g=\alpha\circ f$. The unique measuring function $\alpha$ is called the _mediating morphism_ of $g$.

![[factored_function.svg|200]]

**Example:** An example of a universality are bases. Let $B$ be a nonempty set and assign $\mathcal{X}=V(\mathbb{F})$ (the class of all vector spaces over the field $\mathbb{F}$), $\mathcal{F}$ the set of all functions of the form $f:B\to Z$, and $\mathcal{H}$ the set of all linear transformations $T:S\to Z$ where $S,Z\in V(\mathbb{F})$. Then, if $V_B$ is a vector space with basis $B$, the pair $(V_B,\iota:B\hookrightarrow V_B)$, where $\iota:B\hookrightarrow V_B$ is the inclusion map $\iota(v)=v$ and $B\hookrightarrow V_B$ indicates $B\subseteq V_B$. , is universal for $(\mathcal{F},\mathcal{H})$. To see why this is the case, observe the condition $g=\alpha\circ \iota$ is equivalent to writing $\alpha(v)=g(v)$ for a basis vector $v$; with this also uniquely determining the [[Basis transformations|basis transform]] (linear transform) $\alpha$ from $\mathcal{H}$.


The universality that defines a tensor product is based on the notion of a bilinear map.

**Definition: (Bilinear map)** Let $U$, $V$, and $W$ be [[Vector space|vector spaces]] each defined over the field $\mathbb{F}$, and let $U\times V$ be the cartesian product of $U$ with $V$ with no assigned algebraic structures. A function $f:U\times V\to W$ is a _bilinear map_ if it is linear in both variables, that is $$\begin{align*}f(a_1u_1+a_2u_2,v) &= a_1f(u_1,v)+a_2f(u_2,v)\\ f(u,b_1v_1+b_2v_2) &= b_1f(u,v_1)+b_2f(u,v_2).\end{align*}$$The set of all bilinear maps of the form $f:U\times V\to W$ is denoted by $\mathcal{B}(U\times V,W)$. A bilinear function $f:U\times V\to \mathbb{F}$ that takes elements to values in the underlying field $\mathbb{F}$ is called a _bilinear form_. ^dff04a

The above definition can be restated in terms of matrices as follows: Let $a=(a_1,\dots,a_n)\in \mathbb{F}^n$, $b=(b_1,\dots,b_m)\in \mathbb{F}^m$, and $u=(u_1,\dots,u_n)\in U^n$, $v=(v_1,\dots,v_m)\in V^m$, then $f:U\times V\to W$ is a bilinear map if $$f(au^\intercal,bv^\intercal)=aFb^\intercal$$ where $F=[f(u_i,v_j)]_{ij}$ (matrix entry).


Tensors products are then build by taking $\mathcal{F}$ to be all bilinear maps over the class of vector spaces over a common field $\mathbb{F}$ and $\mathcal{H}$ equal to set of all matching linear transformations (e.g., basis transformations from one vector space to the other). In particular, take the following definition.

**Definition:(Tensor product measuring family)** Let $\mathcal{X}=V(\mathbb{F})$ be the class of all vector spaces defined on $\mathbb{F}$, and let $U\times V$ be a cartesian product between two vector spaces from $\mathcal{X}$. Take $$\mathcal{F} = \bigcup_{W\in \mathcal{X}}\mathcal{B}(U\times V, W)$$to be the family of all bilinear maps from $U\times V$ to any vector space $W$. Then take $\mathcal{H}$ to be the set of all linear transformations between spaces in $\mathcal{X}$.

A pair $(Y,f:U\times V\to Y)$ is _universal for bilinearity_ if it is universal for $(\mathcal{F},\mathcal{H})$.

**Definition: (Tensor product)** Let $U$ and $V$ be [[Vector space|vector spaces]] over a [[Fields|field]] $\mathbb{F}$. Any universal pair $(Y,f:U\times V\to Y)$ of $(\mathcal{F},\mathcal{H})$ is a _tensor product_ of $U$ and $V$. The resulting vector space $Y$ is denoted as $U\otimes V$. The underlying map is called the _tensor map_ and the elements of $U\otimes V$ are correspondingly called _tensors_. 


Alternatively, we can construct tensors products (that are not coordinate free) building on the notion of basis in vector spaces. To start with let $B_U=\{u_i\mid i\in I\}$ be a basis for a vector space $U$ and likewise let $B_V = \{v_j\mid j\in J\}$ be a basis for $V$. Then a bilinear map $f$ on $U\times V$ is uniquely determined (up to isomorphism) by assigning arbitrary values to the "basis" pairs $(u_i,v_j)$ and extending by bilinearity the result, that is, if $x=\sum_{i}a_iu_i$ and $y = \sum_j b_jv_j$, then $f(x,y) = f(\sum_i a_iu_i, \sum_j b_jv_j) = \sum_{i,j} a_ib_jf(u_i,v_j)$. The tensor map (quantified here) must satisfy the above while performing no further alterations to the resulting space. Such a map can be constructed by taking each basis pair $(u_i,v_j)$ to a corresponding element denoted $u_i\otimes v_j$, which is given by evaluation by the underlying bilinear map (the tensor map), and extending by bilinearity as before. Then defining the basis $B_{U\times V}=\{u_i\otimes v_j\mid i\in I,\, j\in J\}$ for the resulting space $U\otimes V$. Tensors are then elements in this final space. 


An important aspect for all mathematical spaces is the form of the zero element. 

**Theorem: (Zero tensor)** If $u_1,\dots,u_n$ are linearly independent vectors in $U$ and $v_1,\dots,v_n$ are arbitrary vectors chosen from $V$, then $$\sum_i u_i\otimes v_i=0 \Rightarrow v_i = 0\text{ for all $i$}.$$In particular, $u\otimes v=0$ if and only if either $u=0$ or $v=0$.
_Proof:_ By definition the bilinearity of the tensor product gives that $$0\otimes v = (0+0)\otimes v = 0\otimes v + 0\otimes v\Rightarrow 0\otimes v = 0,$$and likewise for the symmetric relation of $u\otimes 0 = 0$. Now consider the expression $$\sum_i u_i\otimes v_i = 0,$$where no $u_i$ or $v_i$ is zero. Let $f:U\times V\to W$ be a bilinear map and let $\alpha:U\otimes V\to W$ be the associated mediating morphism, that is, $\alpha\circ t=f$. Then $$0 = \alpha\left(\sum_{i}u_u\otimes v_i\right)=\sum_i (\alpha\circ t)(u_i,v_i) = \sum_i f(u_i,v_i).$$Suppose, without loss of generality, $f(u_i,v_i) = \gamma_k(u_i)\phi(v_i)$ for $\gamma_k\in U^*$ and $\phi\in V^*$ be functions from the [[Dual vector space|dual vector spaces]] of $U$ and $V$ respectively, where $\gamma_k$ are the matching dual vectors of $u_i$ which we assume $u_i$ are all linearly independent (or likewise for $v_j$). The above then reduces to$$0 = \sum_i \gamma_k(u_i)\phi(v_i) = \phi(v_k)\Rightarrow v_k=0$$as the first relation holds for all $\phi\in V^*$. $\square$ 

**Theorem:** For finite-dimensional vector spaces $U$ and $V$, $$dim(U\otimes V)=dim(U)dim(V).$$
