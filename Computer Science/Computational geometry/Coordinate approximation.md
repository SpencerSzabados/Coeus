---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - computational_geometry
  - approximation
references:
---
---

# Overview
In geometric settings, while often ignored, the kind of points a method can be apply to might be restricted to those with Integer valued coefficients where generalization to rationales might lead to a non-trivial increase in approximation error (or other computational costs). Thus, there is some body of work dedicated to methods of approximating non-integer valued coordinates.

# Epsilon-nets
An $\epsilon$-net is a method of approximating a general set by a collection of simpler subsets based around (equality) spaced points. This method is used in probability theory ([[L3 - Concentration inequalities|CS761 lecture3]]) to approximate distributions by "replacing their support with a simpler (finite) cover". Epsilon-nets are related to the concept of [[Generalization#VC-dimension|VC-dimension]] in machine learning.

**Definition: (Combinatorial Epsilon-net)** Let $\Omega$ be a set and $R$ be a collection of subsets from $\Omega$. The set $R$ is often called the _range space_ of the problem considered and the elements of $S$ the _ranges_ (or phrasing things in terms of [[Hypergraph|hypergraphs]] the elements of $R$ can be considered as hyperedges). An $\epsilon$-net of a subset $X\subseteq \Omega$, for a given $\epsilon >0$, is a subset $\mathcal{E}\subseteq X$ such that for any $r\in R$ with $|X\cap r|\geq \epsilon|X|$ then $|\mathcal{E}\cap r|\neq 0$.

Less generally we can look specifically at epsilon nets within [[Metric spaces]].

**Definition: (Metric space Epsilon-net)** Given a [[Metric spaces|metric space]] $(X,d)$ an $\epsilon$-net is a subset $\mathcal{E}\subseteq X$such that for any $x,y\in \mathcal{E}$, $d(x,y)\geq \epsilon$ and for each $x\in X$ there exists a $y\in\mathcal{E}$ such that $d(x,y)\leq \epsilon$.

**Lemma: (Sphere epsilon-net bound)** There exits an $\epsilon$-net of the unit sphere $S^{d-1}$ (under Euclidean distance) that needs at most $(4/\epsilon)^d$ vectors (points).


