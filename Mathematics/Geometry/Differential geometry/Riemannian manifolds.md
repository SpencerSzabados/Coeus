---
doc type: Note
authors: Spencer Szabados
date: 2024-02-28
tags:
  - geometry
  - differential_geometry
  - topology
  - manifolds
references:
  - "[[@Munkres_1991]]"
  - http://people.maths.ox.ac.uk/lackenby/intriem.pdf
---
---

Riemannian manifolds (or geometries) are [[Topological spaces]], in particular, a generalized version of [[Metric spaces]]; a form of [[Differential manifolds|Differential manifold]]. Here I will try to introduce the relevant definitions in a very self contained fashion, calling on ideas from topology when needed, but without introducing extraneous information.   

Riemannian manifolds admit a notion of volume, unlike regular [[Differential manifolds]], by imparting (defining) a inner product structure on the manifold.

**Definition: (Riemannian metric)** Let $\mathcal{M}$ be a $k$-dimensional [[Differential manifolds#^419b6f|differential manifold]]. A _Riemannian metric_ on $\mathcal{M}$ is an [[Inner product space#^dcb7c3|inner product]] $g_p(v,w)=\langle v, w\rangle$ defined on each tangent space $T_p\mathcal{M}$ of class $C^\infty$.

**Definition: (Riemannian manifold)** A _Riemannian manifold_ is a [[Differential manifolds#^419b6f|differential manifold]] equipped with a Riemannian metric.

**Definition (Local isometry)** A _local [[Isometries|isometry]]_ between two [[Riemannian manifolds]] $\cal M$ and $\cal N$ is a local [[Normalizing flows#^2ea514|diffeomorphsim]] $\phi:\mathcal{M}\to\mathcal{N}$ s.t. for all $x\in\mathcal{M}$ and all vectors $v,w\in T_x(\mathcal{M})$ $$\langle v,w\rangle = \langle(D_x\phi)(v), (D_x\phi)(w) \rangle.$$


# Integration over Riemannian manifolds
