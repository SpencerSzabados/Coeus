---
doc type: Note
authors: Spencer Szabados
date: 2023-11-07
tags:
  - differential_equations
  - diffusion
  - stochastic_processes
---
___

# Overview 
The Fokker-Planck equation(s) characterize the evolution (forwards) through time of the a particles velocity distribution subject to drag forces and Brownian motion (noise); that is, the Fokker-Planck equation describes the behaviour of a particles density that is subject to a diffusion process. The equation is only accurate up to the first two modes, from the derivation in [[@KeilsonS_1952]].

**Definition: (Fokker-Planck equation)** Let $X(t)$ be a random variable, indexed in a continuous manner -- a [[Stochastic Process]], following a probability distribution $p(x,t)$, which evolves in time according to the stochastic differential equation $$dX(t)=\mu(X(t),t)dt+\sigma(X(t),t)dW(t),$$where $\mu(X(t),t)$, called the _drift_, controls the displacement of the expected value of $X(t)$, and $\sigma(X(t),t)$, called the _diffusion_ coefficient, controls the concentration of $X(t)$, and lastly $dW(t)$ is a [[Brownian motion]] process. The _Fokker-Plant equation_ (or Kolmogorov forwards equation) describes the probability distribution of $X(t)$ over time $$\frac{\partial}{\partial t}p(x,t)=-\frac{\partial}{\partial x}[\mu(x,t)p(x,t)]+\frac{\partial^2}{\partial x^2}\left[\frac{\sigma^2(x,t)}{2}p(x,t)\right],$$with the initial condition $p(x,0)$ being known. ^083a90
_Derivation:_ see [[@KeilsonS_1952]].

The [[@Uhlenbeck_1930]] process is a special case of the Fokker-Planck equation.

## Backwards equations
The Fokker-Planck equation only describes the forwards dynamics of the diffusion equation. In the context of [[Diffusion models]], and more generally for probability sampling, we are interested in transporting a latent distribution, e.g., some easy to sample distribution such as low dimensional [[Families of distributions#Gaussian (Normal) distribution|gaussian noise]], to a unknown target distribution. This task is modeled by a reverse stochastic process, and requires the used of a matching backwards diffusion equation. The Kolmogorov provides a reversed complementary solution to that given by the Fokker-Plank equation.

**Definition: (Kolmogorov backwards equation)**  Let $X(t)$ be a random variable, indexed (in a continuous manner), following a probability distribution $p(x,t)$, that evolves in time according to the stochastic differential equation $$dX(t)=\mu(X(t),t)dt+\sigma(X(t),t)dW(t).$$The Kolomogorov backwards equation is $$\frac{\partial}{\partial t}p(x,t)=-\mu(x,t)\frac{\partial}{\partial x}p(x,t)-\frac{\sigma^2(x,t)}{2}\frac{\partial^2}{\partial x^2}p(x,t)$$subject to the initial condition $p(x,t_0)=p(x)$ where we are taking $t$ from $T$ to $t_0$.
See [Ludwigwinkler](https://ludwigwinkler.github.io/blog/ReverseTimeAnderson/), however, note that the authors mixes up the forwards and backwards initial conditions in the first few paragraphs. 