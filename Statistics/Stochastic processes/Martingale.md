---
doc type: Note
authors: Spencer Szabados
date: 2024-06-12
tags:
  - stochastic_processes
  - maringales
references:
  - "@Taylor_1998"
---
---

**Definition: (Martingale)** A [[Stochastic Process]] $\{X_t\}_t$, with $t=0,1,2,\dots$, is _martingale_ if for all $t$:
  1) $E[|X_t|]$ is finite;
  2) $E[X_{t+1}\mid X_0,\dots,X_t]=X_t$ 
