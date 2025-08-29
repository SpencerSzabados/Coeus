---
doc type: Note
authors: Spencer Szabados
date: 2023-11-03
tags:
  - measure_theory
  - statistics
  - real_analysis
---
___

This is the most general form of integration, generalising [[Lebesgue integration]] and [[Riemann-Stieltjes Integrals]]. 

# Overview 
Before proceeding we must recall some definitions from [[real analysis]].

**Definition: (Simple function)** A function $f:X\to\mathbb{R}$, on a [[Measure spaces|measurable space]] $(X,\mathcal{B})$, is simple if it can be expressed as $$f(x) = \sum_{i=1}^N a_i\mathbb{1}\{x\in A_i\}$$with $a_i$ distinct and $A_i$ mutually disjoint measurable sets. This is the standard form of simple functions.

The integral of a non-negative simple functions with respect to a [[Measure spaces#^c048df|measure]] $\mu$ is $$\int f(x)\,d\mu(x) = \sum_{i=1}^Na_i\mu(A_i).$$By convention, if zero times infinity occurs in this sum the product is taken to be zero.