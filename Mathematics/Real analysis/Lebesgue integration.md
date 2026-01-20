---
doc type: Note
authors: Spencer Szabados
date: 2025-01-09
tags:
  - integration
  - real_analysis
  - measure_theory
references:
  - "[[@Apostol_1973]]"
  - https://www.stats.ox.ac.uk/~etheridg/integration.pdf
---
---

Lebesgue integration extends the notions [[Riemann-Stieltjes Integrals]] (and likewise [[Riemann integration]]) to more general function definitions and domains. The Lebesgue integral is better suited at dealing with the limiting behaviour of sequences of functions over "sparse domains" compared to the Riemann-Stieltjes integral. Whenever the [[Riemann integration#^f7b4df|Riemann integral]] exists then it will agree, in value, with the Lebesuge integral; moreover, in this setting, all methods for evaluating the integral carry over.

The Lebesuge integral is tightly related to notions of [[Measure spaces]] (measure theory); however, the following note is limited to techniques of integration, see related notes for topics of measure theory.

# Overview
Bellow is a simplified statement of Lebesgue's measure in terms of an outer-measure based on open interval lengths which is a valid characterization for $\mathbb{R}$, assuming we only consider measurable sets (i.e., sets with finite measure).

**Definition: (Lebesgue measure)** For an interval $I=[a,b]$ let $\mathcal{l}(I)=b-a$ denote its [[Rectifiable curves and arc length|length]]. Then for any subset $S\subset \mathbb{R}$, the Lebesgue outer measure $\lambda(S)$ is defined as $$\lambda(S) = \inf\left\{\sum_{i=1}^\infty \mathcal{l}(I_i)\mid \{I_i\}_{i\in\mathbb{N}} \text{ is a sequence of open intervals with } S\subset\bigcup_{i=1}^\infty I_i\right\};$$that is, $\{I_i\}_{i\in \mathbb{N}}$ is a open cover of $S$. More generally, we can consider $S$ to be any subset of $\mathbb{R}$, if it is bounded then it will have finite measure, if it is unbounded its measure is said to tend to infinity. See [[@Schervish_1995]]. ^c700cf

**Properties:** By construction of the above measure, for any $A,B\subseteq \mathbb{R}$ with $A\cap B=\emptyset$, $\lambda(A\cup B)=\lambda(A)+\lambda(B)$; and more generally, for any countable family $\{E_{i}\}_{i\in I}$ of mutually disjoint sets, we have $\lambda(\cup_{i\in I}E_i)=\sum_{i\in I}\lambda(E_i)$. Moreover, $\lambda((0,1))=1$. ^2849f0

In order to define the integral of a [[Functional measure spaces#^f47214|measurable function]] we begin by considering a simple class of functions which, by construction, are measurable and can be used to integrate more complex functions. The details of measurable functions is skipped here since most functions (paired with their support) are sufficiently nice (or [[Regularization|regularized]], in the domain of machine learning, that we don't need to check the definition directly; other than, for the Lebesuge measure, a function $f:\mathbb{R}\to\mathbb{R}$ is Lebesuge measurable iff $\forall I\subseteq \mathbb{R}$, $f^{-1}(I)=\{x\in \mathbb{R}\mid f(x)\in I\}$ is a Lebesuge measurable set. 

**Definition: (Simple function)** A function $f:X\to\mathbb{R}$, on a [[Measure spaces|measurable space]] $(X,\mathcal{B})$, is simple if it can be expressed as $$f(x) = \sum_{i=1}^N a_i\mathbb{1}\{x\in A_i\}$$with $a_i$ distinct and $A_i$ mutually disjoint measurable sets. This is the standard form of simple functions. 

By construction simple functions are measurable; and the integral of a non-negative simple functions with respect to a [[Measure spaces#^c048df|measure]] $\mu$ is $$\int f(x)\,d\mu(x) = \sum_{i=1}^Na_i\mu(A_i).$$By convention, if zero times infinity occurs in this sum the product is taken to be zero.
