---
doc type: Note
authors: Spencer Szabados
date: 2024-02-09
tags:
  - machine_learning
  - computational_geometry
  - geometry
  - dimension_reduction
  - topology
  - differential_geometry
references:
  - https://drewwilimitis.github.io/Manifold-Learning/
---
___

Manifold learning (also more generally called non-linear dimension reduction) is a set of methods for finding a low-dimensional embedding of a given collection of data (or distribution).

**Problem Statement: (Manifold learning)** Let $Y=\{y_1,\dots,y_N\}$ be a finite [[Random samples|random sample]] of $N$ datapoints that lie on some unknown smooth $d$-dimensional manifold $\cal M$ equipped the geodesic distance $$d(p,q)_{\cal M} = \inf_{c\in\mathcal{C}(p,q)} Arc(c).$$The points $Y$ are, assumed (the manifold assumption) to be, embedded by a smooth map $\psi:\mathcal{M}\to\mathcal{X}$ into a high-dimensional space $\mathcal{X}$, say $\mathcal{X} = \mathbb{R}^{D}$, with metric $\|\cdot\|_{\mathcal{X}}$ where $D>>d$. The problem of manifold learning is then to learn the manifold $\mathcal{M}$ and find the representation of $\phi$ for the purpose of transforming the points of $Y$ to $\{\psi^{-1}(y_1),\dots,\psi^{-1}(y_N)\}$ which are of lower dimension; ideally, we would learn $\psi$ exactly but in practice we must often settle for learning $\hat{\psi}$ and some manifold $\mathcal{T}$ of dimension $D>t>d$, which preserves as much of the 'structure' as possible. [[@Izenman_2012]].


# Locally-Linear embeddings 


# Non-linear embeddings 
  + [[Diffusion embeddings]]
