---
title: Diffusion for global optimization in Rⁿ
authors: Tzuu-Shuh Chiang, Chii-Ruey Hwang, Shuenn Jyi Sheu
year: 1987
---
---
# Overview
This paper investigates the use of diffusion (e.g., [[Diffusion models]]) to optimize smooth functions over $\mathbb{R}^d$ by proving the intermediate distributions that result from the diffusion process (as modeled by the [[Diffusion models#^083a90|Fokker-Planck equation]]) [[Random samples#^f340e3|converge weakly]] towards an equilibrium Gibbs distribution, which concentrates around the minimum of the objective function. Precise (non-asymptotic) analysis of the [[Monte Carlo simulation#^549186|mixing time]] is not given, nor is a guarantee on the quality of the resulting minimize; however, bounds needed on the [[Simulated annealing process|annealing schedule]] for the Brownian noise (variance schedule) to guarantee the aforementioned weak convergence are studied.

**Problem statement:** Let $U:\mathbb{R}^d\to [0,\infty)$ be the objective function we are interested in minimizing and $p(x,t)$ be the corresponding probability distribution of the argument of the objective function as it evolves according to the diffusion process; i.e., we consider $$dX(t)=-\nabla U(X(t))dt+\sigma(t)dW(t)$$ with initial condition $X(0)=x$. Then, we want to know under what conditions does $p(x,t)$ concentrate around the global minimizer of $U$, in particular, what conditions must $U$ satisfy and $\sigma(t)$ equal to ensure convergence.
  

# Primary results 
The papers primary result is the following theorem and accompanying lemmas. 

**Theorem:** Let $U:\mathbb{R}^d\to [0,\infty)$ be twice differentiable and satisfy the following conditions:
  1) $\min_{x\in\mathbb{R}^d}U(x)=0$ (up to shifting)
  2) $U(x)\to\ \infty$ and $\|\nabla U(x)\|\to \infty$ as $\|x\|\to \infty$, moreover, $\|\nabla U(x)\|^2-\nabla\cdot\nabla U(x)>-\infty$ as $\|x\|\to \infty$;
  3) $\pi^{\epsilon}=\frac{1}{Z(\epsilon)}e^{-2U(x)/\epsilon^2}$ where $Z(\epsilon)=\int_{\mathbb{R}^d}e^{-2U(x)/\epsilon^2}\,dx<\infty$ has a unique weak limit $\pi$ as $\epsilon \to \infty$ (monotonically decreasing); note that if $\pi$ exits it concentrates on the global minima of $U$. 
Then for $\sigma^2(t)<1$ and $\sigma^2 (t)=c/\log(t)$ for large $t$ with $c>c_0$ (where $c_0$ is upper bounded in the proof) $p_t\to\pi$ as $t\to \infty$ uniformly for all $x$ in a compact set.

In particular, $p_t$, the intermediate distribution at time $t$, is the transition probability of the continuous [[Markov chains|Markov process]] defined by the stochastic differential equation given in the problem statement.  

Property (2) can be achieved by a observation made within the paper, namely, as the weak limit $\pi_t\to\pi$ is unchanged by perturbations to $U$ sufficiently far away from the minima we can consider a modified objective with $U(x)=\|x\|^s$ for large $\|x\|$. This condition ensuring $X(t)$ has high probability of remaining within a bounded spherical region, i.e., $X(t)$ may diverge away from the minima but will quickly walk back to a fixed finite ball in finite many steps which is independent of the form of $\sigma(t)$. 

The proof of the theorem follows form three supporting lemmas.


# Connections
This paper (as also mentioned briefly in one of its references) shows that a sufficiently damped (meaning the variance schedule decreases towards zero quickly and is never too large) diffusion process written in terms of the gradient of a objective function is a gradient accelerated [[Simulated annealing process]] (especially in the view of [[Stochastic optimization]]). As a concrete example of this gradient acceleration, we can consider the Metropolis Adjusted Langevian Algorithm studied in [[@Ma_2019]]. 