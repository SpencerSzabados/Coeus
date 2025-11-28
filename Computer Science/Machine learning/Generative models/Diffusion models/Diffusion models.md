---
doc type: Note
authors: Spencer Szabados
year: 2023
tags:
  - diffusion
  - machine_learning
  - generative_models
  - flow
references:
  - "[[@Ho_2020]]"
---
___

Diffusion models are form of ([[Push-forwards models]]) [[Generative models]] that can be characterized, under sufficient assumptions, by differential [[Stochastic Process]] in combination with ODE [[Linear dynamical systems#Flows|flows]] to transform one probability distribution to another.

# Overview
Diffusion probabilistic models (DDPM) [[@Ho_2020]] are a parameterized [[Markov chains|Markov chain]] model trained using [[Variational Bayesian inference]] to produce samples matching the distribution of the training data provided. The chain transitions are learned to reverse a diffusion process, described in terms of [[Fokker-Planck equation]], where noise is gradually added to the input samples until they are indistinguishable from whichever distribution of noise is chosen (e.g., [[Families of distributions#Gaussian (Normal) distribution|Gaussian]] being the most commonly used).

Suppose our data originates from a distribution (density) $p$, that is $X\sim p$, which is unknown. Diffusion models attempt to approximate $p$ by learning a reverse of a stochastic process that takes $X$ to a known distribution $P_T$ by gradually corrupting $x\sim X$ by progressively adding noise in the form $$x_t=\mu(x_{t-1},t)x_i+\beta(t)\sigma_t$$ where $\mu(x_{t-1},t)$ is the mean of the latent distribution $p_t$ and $\beta(t)$ controls the amount of added noise in terms of variance, over a series of discrete time steps, $i=0,1,2,\dots, T$ with $x=x_0$. Thus, diffusion models are considered to be latent space models with $$p(x_0) = \int p(x_0,x_1,\dots,x_T)\,dx_0dx_1\cdots dx_T$$where the joint distribution $p(x_0,x_1,\dots, x_T)$ is the reverse process mentioned and constructed in terms of a Markov chain (of noise of the form above)

## Probability flow ODE
TODO - add notes about DDIM and the different assumptions made between the two models on the shape of the distribution at each time step.

# Diffusion objective 

## Training 
TODO - discuss the various training objectives used for training diffusion models 

# Applications 
Diffusion models, and more generally diffusion equations, have been applied to a verity of different problems.

## Diffusion for optimization 
Diffusion has been applied to the problem of convex (and [[Quasi-convex functions|quasi-convex]]) optimization, see [[@Chiang_1987]].

## Diffusion for optimal control 
Much of diffusion modeling can be framed as a [[Stochastic optimal control]] problem, where at each state in the diffusion process we are attempting to control the signal to noise ratio in the image (signal).

