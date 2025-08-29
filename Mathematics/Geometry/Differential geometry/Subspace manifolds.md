---
doc type: Note
authors: Spencer Szabados
date: 2024-03-11
tags:
  - manifolds
  - differential_geometry
references:
  - "[[@Spivak_1995]]"
  - https://www.math.utoronto.ca/vtk/1300Fall2015/lecture-oct29.pdf
  - https://www.epatters.org/wiki/geometry/manifolds-with-corners
  - "[[@Munkres_1991]]"
---
---

This note outlines the basic definitions of manifolds from a elementary (Euclidean) perspective. 

(TODO - add notes on cuvalinear coordinates https://math.stackexchange.com/questions/1319939/coordinate-systems-on-manifolds. )

# Manifolds defined via embeddings (subspaces)
The following is a elementary introduction to manifolds which makes use of embeddings into Euclidean space via diffeomorphisms. Since the following definitions are given in terms of diffeomorphisms, which are differentiable homeomorphisms and thus a special case of [[Topological spaces#^8405be|charts]], the statements can be simplified to avoid explicitly stating the [[Topological spaces#^8d2d2b|topological open sets]]. 

Importantly, no distinction is given between the manifold and its embedding in terms of notation. This introduction is taken from [[@Spivak_1995]]. 

**Definition: (Manifold in $\mathbb{R}^d$)** A subset $\mathcal{M}\subseteq \mathbb{R}^n$ is a $k$-dimensional manifold (in $\mathbb{R}^n$) if for every $x\in\mathcal{M}$, there exists a open set $U\subset \mathbb{R}^n$ with $x\in U$, an open set $V\subset \mathbb{R}^n$, and a diffeomorphism $h:U\to V$ such that $$h(U\cap \mathcal{M})=V\cap(\mathbb{R}^k\times \{0\}^{n-k})=\{y\in V\mid y_{k+1}=\cdots=y_n=0 \};$$i.e., $U\cap \mathcal{M}$ is identical to $\mathbb{R}^k\times \{0\}$ up to diffeomorphism. 

Manifolds in $\mathbb{R}^n$ can also be characterized via _coordinate systems_ (charts).

**Characterization: (Manifold in $\mathbb{R}^n$)** A subset $\mathcal{M}\subset \mathbb{R}^n$ is a $k$-dimensional manifold in $\mathbb{R}^n$ if and only if for each $x\in \mathcal{M}$ there exists an open set $U\subset \mathbb{R}^n$ with $x\in U$, an open set $V\subset \mathbb{R}^k$, and a injective differentiable function $f:V\to \mathbb{R}^n$ such that: 
  1) $f(V)=\mathcal{M}\cap U$,
  2) $\mathbb{J}_f(y)$, the Jacobian of $f$, has [[Matrix rank#^6a57b5|rank]] $k$ for all $y\in V$,
  3) $f^{-1}:f(V)\to V$ is continuous;
such a $f$ is called a (local) _coordinate system_ (or chart) around $x$.

Coordinate systems are the chosen [[Basis transformations#^532a8b|basis]] on that space, and as defined above are special cases of [[Charts and Atlases|charts]], with the extra requirement that the chart is differentiable, labeling what points exist within local regions of the manifold.

**Definition: (Manifold with boundary in $\mathbb{R}^n$)** A subset $\mathcal{M}\subset \mathbb{R}^n$ is a $k$-dimensional manifold with boundary if for every point $x\in \mathcal{M}$ either 
  1) the manifold definition is satisfied; or
  2) there exists a open set $U\subset \mathbb{R}^n$ with $x\in U$, an open set $V\subset\mathbb{R}^n$, and a diffeomorphism $f:U\to V$ such that $$f(U\cap \mathcal{M})=V\cap(\mathbb{H}^k\times\{0\}) = \{y\in V\mid y^k\geq 0,\, y^{k+1}=\cdots=y^n=0\}$$where $\mathbb{H}^k=\{x\in\mathbb{R}^k\mid x^k\geq 0\}$ is the $k$-dimensional half-space.
 

## Vector fields on manifolds 
Before progressing we must define the notion of a derivative on manifolds and the tangent space.

**Definition: (Tangent space)** Let $\mathcal{M}$ be a $k$-dimensional manifold in $\mathbb{R}^n$ and let $f:V\to\mathbb{R}^n$ be a coordinate system around $x=f(a)$, where $V\subset \mathbb{R}^k$ is a open set; i.e., a chart around $x$. Since $\mathbb{J}_f(y)$ is of rank $k$, the linear transformation induced from $f$, $D_x:\mathbb{R}^k_a\to \mathbb{R}^n_x$ (and corresponding to the Jacobian in this case at $x$) is injective and $D_x(\mathbb{R}^k_a)$ is a $k$-dimensional subspace of $\mathbb{R}^n_x$; moreover, this subspace, called the _tangent space_ at $x$, denoted $T_x\mathcal{M}$, is not depended on the particular $f$ used in its construction. ^fa350c

In the above definition, we made use of the pushforward function of the coordinate system $f$, denoted $D$ above. The [[Push-forwards models#^599c6e|pushforwards]] function, in the topological sense, is a linear approximation of smooth maps between tangent spaces of smooth manifolds, and generalizes the total derivative of vector calculus. E.g., if $f:V\to\mathbb{R}^n$, where $V\subset \mathbb{R}^k$ is open, and $x=f(a)\in U$, for $U\subset \mathbb{R}^n$ open set containing $x$ which is on the manifold $\mathcal{M}$, then the pushforwards (differential) of $f$ at $x$ is the linear map $D_x:T_x\mathcal{M}\to T_{f(x)}\mathbb{R}^n$; note, since $T_{f(x)}\mathbb{R}^n$ is [[isomporphism|isomorphic]] to $\mathbb{R}^n$ we can just write $D_x:T_x\mathcal{M}\to\mathbb{R}^n$.

**Definition: (Vector fields on manifolds)** Let $\mathcal{M}$ be a $k$-dimensional manifold in $\mathbb{R}^n$ and suppose $A\subset \mathbb{R}^n$ is an open set with $\mathcal{M}\subset A$. Let $F$ be a differentiable [[Vector fields|vector field]] defined over $A$ where for all $x\in\mathcal{M}$, $F(x)\in T_x\mathcal{M}$. If $f:V\to\mathbb{R}^n$ is a coordinate system, with $x=f(a)$ and derivation $D$, there exists a unique differentiable vector field $G$ on $V$ such that $$D_x(G(a))=F(f(a))$$for all $a\in V$. If $F$ assigns a vector value to each $x\in \mathcal{M}$, that is $F(x)\in T_x\mathcal{M}$, then it is called a [[Vector fields|vector field]] on $\mathcal{M}$.
