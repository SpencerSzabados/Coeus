---
title: Deep sets
authors: Manzil Zaheer, Satwik Kottur, Siamak Ravanbakhsh, Barnabas Poczos, Russ R Salakhutdinov, Alexander J Smola
year: 2017
---

# Overview 
The primary goal of the paper is to explore the theory necessary to ensure a network is either invariant to permutations in its inputs (which are allowed to be sets), something that is desirable when your input can be a unordered collection of information, or if not invariant have it be equivariant; the paper relates to methods for performing set-valued or multilabel [[Classification and clustering|classifications]]. 


# Primary results
The first desirable property studied is the following: A function $f:2^\Omega\to \mathcal{Y}$, where $\mathcal{Y}$ is the sample space for classified outputs, acting on sets must be permutation invariant to the order of the objects in the input set; i.e., for any permutation $\pi$ we require $f(\{x_1,\dots,x_M\})=f(\{x_{\pi(1)},\dots,f_{\pi(M)}\})$.

Phrased in terms of a supervised learning problem, the above is equivalent to requiring that for any given training collection of sets, say $X^{(1)},\dots,X^{(N)}$ with corresponding labels $Y^{(1)},\dots,Y^{(N)}$, a resulting predictor (or set of predictors) should be invariant to the arrangement of elements within $X^{(i)}$ and possibly $Y^{(i)}$.

**Theorem:** A function $f(X)$ operating on a set $X$ (from a countable universe of elements) is permutation invariant if and only if if can be decomposed into the from $$\rho\left(\sum_{x\in X}\phi(x)\right)$$for some transformation functions $\rho$ and $\phi$ that do not depend on other variables outside their scope.

The key observation is the above formulation is akin to the equation for layers in [[Artificial neural networks]], where $\rho$ and $\phi$ layer [[Activation functions]]; the particular activation functions selected must however admit this decomposition and therefore $\phi$ must only act element wise from one layer to the other. More generally, $\rho$ and $\phi$ can take the from of universal function approximators (each being a hidden layer in a neural network).

An outline for neural networks that satisfy the above theorem is the following:
  1) Each input instance $x_m$ is transformed (possibly by several layers of a neural network) into $\phi(x)$; the functions $\phi$ can be replaced by conditional mappings $\phi(x|m)$ where $m$ represents some additional external information (bias) separate from the information contained in $x$.
  2) The representations $\phi(x)$ (features) are then summed up and output by $\rho$ in the typical fashion for a neural network.

