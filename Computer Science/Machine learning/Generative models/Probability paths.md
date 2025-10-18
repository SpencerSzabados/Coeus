---
doc type: Note
authors: Spencer Szabados
date: 2024-05-28
tags:
  - statistics
  - measure_theory
  - diffusion
  - flow
  - differential_equations
references:
---
---

Probability paths (or trajectories) are a concept that form the basis of most, if not all, [[Push-forwards models]]. 

# Overview 
In the context [[Stochastic Process]], time-dependent [[Linear dynamical systems#Flows|flows]] are [[Normalizing flows#^2ea514|diffeomorphic]] maps constructed from a given [[Vector fields|vector field]] $v_t:[0,1]\times \mathbb{R}^d\to \mathbb{R}^d$ and the [[Ordinary differential equations|ordinary differential equation]] $$\begin{align}\frac{d}{dt}\phi_t(x) &= v_t(\phi_t(x))\\ \phi_0(x)&=x.\end{align}$$

**Definition: (Probability density path)** A [[Vector fields|vector field]] $v_t:[0,1]\times \mathbb{R}^d\to\mathbb{R}^d$ is said to generate a _probability density path_ $p:[0,1]\times\mathbb{R}^d\to\mathbb{R}_{>0}$, with $\int p_t(x)\,dx=1$ for all $t$, if its flow $\phi_t$ satisfies the [[Push-forwards models#^3b91f2|push-forwards equation]] $p_t = {\phi_t}_\sharp p_0$.

TODO - write out the derivation for when the push-forwards is satisfied for the given density assumption.