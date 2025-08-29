---
doc type: Note
authors: Spencer Szabados
date: 2024-06-16
tags:
  - manifolds
  - topology
---
---

This note servers to outline what a topological manifold is and how it differs from other kinds of manifolds (e.g., [[Differential manifolds]], [[Riemannian manifolds]], [[Combinatorial manifolds]]). 

The central distinction between topological manifolds and [[Combinatorial manifolds]] is in their methods of construction, where topological manifolds are constructed using (as one method) [[Charts and Atlases]] Combinatorial manifolds are typically defined by glue-ing together euclidean manifolds (simplexes or rectangles - PL manifolds). Now while [[Differential manifolds]] are a subclass of topological manifolds, one typically only calls a manifold topological if there are no assumptions placed on differentiability of the charts used, unlike for differentiable manifolds. 

# Overview 
Rather than defining a manifold as a subspace of some ambient space, as is commonly done for differentiable manifolds, they can be defined using topological tools directly.

**Definition: (Topological manifold)** A _Topological manifold_ is a [[Topological spaces#^8d2d2b|topological space]] $(\mathcal{M},\Omega)$ such that: 
  1) it is [[Hausdorff]];
  2) for all $x\in\mathcal{M}$ there exists a [[Charts and Atlases#^8405be|chart]] $(U,\phi)$ with $x\in U$;
  3) the space $(\mathcal{M},\Omega)$ has a countable basis of open sets.