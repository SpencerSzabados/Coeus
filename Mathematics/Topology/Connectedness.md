---
doc type: Note
authors: Spencer Szabados
date: 2024-07-03
tags:
  - topology
  - geometry
references:
  - "[[@Munkres_2014]]"
---
---

Connectedness of spaces is an important topological characterization used to classify different spaces as either equivalent or not.

# Overview

**Definition: (Connected)** Let $X$ be a [[Topological spaces|topolgoical space]]. A separation of $X$ is a pair $U, V\subseteq X$, $U\cap V=\emptyset$ with $U\cup V=X$. The space $X$ is called connected if no separating pair exists.

**Definition: (Path connected)** Let $X$ be a [[Topological spaces|topological space]]. The space $X$ is called path connected if $\forall x_0,x_1\in X$ there exists a $f:[0,1]\to X$ continuous  with $f(0)=x_0$ and $f(1)=x_1$. 

The next definition (simply connected) serves to identify properties of a space similar to convexity. Informally speaking, a space $X$ is simply connected if every closed curve in $X$ can be shrunk to a point in $X$. Before introducing this idea we must develop some ideas of group theory for topological spaces.

**Definition: (Fundamental group of a topological space)** Let $X$ be a [[Topological spaces|topological space]] and $x_0\in X$ be an arbitrary point. A (continuous) path $f:[0,1]\to X$ with $f(0)=x_0=f(1)$ is called a loop based at $x_0$. The set all path homotopy classes of loops based on $x_0$, equip with the piecewise splicing operation $\oplus$, is called the fundamental group of $X$ relative to the base $x_0$, and is denoted $\pi_1(X,x_0)$.

**Corollary:** If $X$ is path connected and $x_0,x_1\in X$, then $\pi_1(X,x_0)\cong \pi_1(X,x_1)$ are isomorphic; under the isomorphism(s) of connecting a forwards and reverse path from $x_0$ to $x_1$ and piecewise splicing this into the loops of $\pi_1(X,x_0)$. i.e., for path connected spaces the base point does not matter, rather the fundamental group depends on the path homotopy within the space. 

**Definition: (Simply connected)** A topological space $X$ is simply connected if it is path connected and its fundamental group $\pi_1(X,x_0)$ is the trivial, one element under [[Path homotopy]] equivalence, group.