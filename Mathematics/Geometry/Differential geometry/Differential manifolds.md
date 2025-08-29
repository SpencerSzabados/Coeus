---
doc type: Note
authors: Spencer Szabados
date: 2024-02-11
tags:
  - manifolds
  - differential_geometry
  - topology
references:
  - "[[@Spivak_1995]]"
  - "[[@Munkres_1991]]"
---
---

Differential [[Subspace manifolds]] generalize the definition of manifolds given in the aforementioned note such that these abstract spaces can be defined without explicitly describing them as subspaces of Euclidean space. Now with that said, due to the Nash imbedding theorem [[@Nash_1956]] this differentiation is not as significant for [[Riemannian manifolds]] the subclass of differentiable manifolds.

# Overview 
The most common definition of a differentiable [[Subspace manifolds#Manifolds via topology|(topological) manifold]] is that of $C^\infty$ class; the below definition can be extended to include $C^k$ differentiable manifolds readily by replacing the overlap constraints to be $C^k$. 

**Definition: (Differentiable manifold)**  Let $(\mathcal{M},d)$ be a [[Metric spaces|metric space]] and $\{\phi_i:U_i\to V_i\}$ be a collection of [[Charts and Atlases|charts]] (that is, a collection of homeomorphisms) where each $U_i$ is either open in $\mathbb{H}^k$ or $\mathbb{R}^k$, and $V_i$ is open in $\mathcal{M}$, such that the sets $\{V_i\}$ form an open cover of $\mathcal{M}$. Further suppose, the maps $\{\phi_i\}$ overlap with class $C^\infty$, meaning, $\phi^{-1}_i\circ \phi_j\in C^\infty$ provided $V_i\cap V_j\neq \emptyset$. Then the metric space together with the set of charts, say $(\mathcal{M},d,\{\phi_i\})$, is a differentiable $k$-manifold of class $C^\infty$. ^419b6f

**Definition: (Derivative on manifold)** Let $\mathcal{M}$ be a $k$-dimensional manifold and $p\in\mathcal{M}$. A _tangent vector_ of $\mathcal{M}$ at $p$ is a function $D_p$ that assigns, to each (chart) [[Topological spaces#^ef5c73|coordinate patch]] $\phi:U\to V$ in $\mathcal{M}$ about $p$, a tensor (vector) via the relation: Given a curve $f\in C^\infty$ with $f:[a,b]\to\mathcal{M}$ and $f(t_0)=p$, for some $t_0\in[a,b]$, the tangent vector about $p$ of $f$ is $$D_p(f) = \nabla(\phi^{-1}\circ f)(t_0).$$The set of all tangent vectors, similarly defined in [[Subspace manifolds#^fa350c|tangent space]] of Euclidean embeddings of manifolds, is denoted $T_p\mathcal{M}$. 

