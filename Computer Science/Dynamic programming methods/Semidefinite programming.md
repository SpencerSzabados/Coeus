---
doc type: Note
authors: Spencer Szabados
date: 2023-06-01
tags:
  - optimization
  - semidefinite_programming
---
___

# Overview 
Semi-definite programming is a generalization of [[Linear programming]] to the space of semi-definite matrix equations (operators) rather than just systems of linear equations.

**Problem statement: (Semidefinite programming)** Suppose $C$ is a symmetric $n$-by-$n$ matrix with entries in $\mathbb{R}$ and $b\in\mathbb{R}^m$, and $T:\Sigma^n\to\mathbb{R}^m$ be a [[Linear transformations|linear transformation]] from the space of symmetric $n$-by-$n$ matrices. Then, a semidefinite programming question is defined as $$\begin{align}\inf_X\quad&\langle C,X\rangle\\\text{subject to:}\quad& T(X)=b, X\text{ is positive semidfineite.}\end{align}$$
Each semidefinite programming question admits a dual form problem defined as: $$\begin{align}\inf\quad& b^\intercal y\\ \text{subject to:}\quad& T^*(y)+S=C, S \text{ is positive semidefinite.}\end{align}$$

