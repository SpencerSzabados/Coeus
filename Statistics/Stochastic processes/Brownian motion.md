---
doc type: Note
authors: Spencer Szabados
date: 2024-06-12
tags:
  - stochastic_processes
  - diffusion
  - markov_chains
---
---

**Definition: (Wiener process)** Let $(\Omega, \mathcal{B}, P)$ be a [[Measure spaces#^535f6f|probability space]]. A (standard - one-dimensional) Wiener process (or Brownian motion) is a [[Stochastic Process]] $\{W_t\}_{t\geq 0}$, for $t\in \mathbb{R}_{\geq 0}$, that satisfy:
  1)  $W_0 = 0$;
  2) Almost surely $t\to W_t$ is continuous in $t$; i.e., the Wiener process is a continuous stochastic process where for all $t\geq 0$ $$P(\{z\in\Omega\mid \lim_{s\to t}|W_s(z)-W_t(z)|\}=0)=1;$$
  3) The process $\{W_t\}_t$ has stationary (fixed) independent increments; with the increment constraint $W_{t+s}-W_{s}\sim \mathcal{N}(0,t)$.
See [Galton](https://galton.uchicago.edu/~lalley/Courses/313/BrownianMotionCurrent.pdf).