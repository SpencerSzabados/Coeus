---
doc type: Note
authors: Spencer Szabados
date: 2023-06-01
tags:
  - optimization
  - linear_programming
---
___

Linear programming questions are a class of optimization problem involving linear systems that can be solved in polynomial time (wrt to their input parameter size) due to the restriction that the domain of feasible solutions is [[Convex sets|convex]]. 


# Overview 
**Problem: (Linear programming or Integer programming)** A _linear programming problem_ attempts to optimize (computing the minimum or maximum) of a linear objective function of $n$ variables over a polyhedral domain in $\mathbb{R}^n$, which is defined as the intersection of finitely many closed half-spaces; that is, let $A\in \mathbb{R}^{m\times n}$, $b\in \mathbb{R}^m$, and $c\in\mathbb{R}^c$ be given. Then, we are searching for $$\begin{align}\min_x\quad& c^\intercal x\\\text{subject to:}\quad& Ax=b, x\geq 0.\end{align}$$This last constraint can also be written as $\{x\in\mathbb{R}^n \mid \bar{A}=\bar{b},\, \hat{A}x\leq \hat{b}\}$ where $\bar{A}\in\mathbb{R}^{r\times n}$ with $rank(\bar{A})=r$, that is, $\bar{A}$ is the full rank component of $A$, and $\hat{A}\in\mathbb{R}^{(m-r)\times n}$ is the null component. 

A linear programming problem also has an associated _dual problem_ defined in the form of: $$\begin{align}\max_y\quad&b^\intercal y\\ \text{subject to:}\quad& A^\intercal y+s=c, s\geq 0.\end{align}$$Where $s$ is referred to as the _slack_ vector.

**Definition: (Problem size)** The size of a given linear programming problem is taken to be the number of bits needed to store it; that is, given $A$, $b$, and $c$ the size of the associated problem is $$size(b)+size(c)+\sum_{i=1}^m\sum_{j=1}^n size(a_{ij})$$where $size(x)=\lceil\log_2(|x|+1)\rceil +1$, this kind of [[Representation scheme|representation scheme]] is the most common.
 

The Fourier-Motzkin Elimination method performs an equivalent role for linear inequalities as Gaussian Elimination does for linear systems of equations.
