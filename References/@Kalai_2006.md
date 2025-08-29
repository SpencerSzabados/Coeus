---
title: Simulated annealing for convex optimization
authors: Adam Tauman Kalai, Santosh Vempala
year: 2006
---

This paper is one of the first to give concrete bounds on the mixing-time and convergence of simulated annealing for optimizing a simple class of convex functions (which form of subset of log-concave densities). The paper itself is not well organized with many connected elements spread throughout that should have been rearranged into single sections.

# Overview
This paper is focused on analysing the (non-asymptotic) [[Monte Carlo simulation#Markov chain mixing time|mixing time]] and consequently the convergence towards minimizers of linear [[Convex functions]] over a restricted [[Convex sets|convex set]] (domain) point membership of which is only provided by random sampling queries to a oracle using a [[Simulated annealing process|Simulated annealing]] algorothm. Thus, beyond simply searching for a minimizer this element must also lie in the feasible region. 

**Problem statement:** Let $U:\mathbb{R}^d\to \mathbb{R}$ be a function of the form $U(x)=c^\intercal x$ where $c$ is a unit-vector (.e.g., $c\in S^{d-1}$), $K\subseteq \mathbb{R}^d$ a convex feasible region, and $\mathcal{O}(x)$ a oracle that indicates whether or not a given point lies within $K$. Then we seek to find $$\arg\min_{x\in\mathbb{R}^d}U(x)$$ subject to $x\in K$. 


# Primary results 
The central result of this paper concerns analyzing the convergence (and mixing times for the sampling processes) of the following simulated annealing algorithm which is modified to improve convergence over arbitrary convex domains (connected closed shapes) by estimating the covariance matrix of the densities of the random walks. 

```pseudo
\begin{algorithm}
\caption{Simulated Annealing with Covariance Estimation}
\begin{algorithmic}
\Input  Objective function $U$ specified in terms of a unit direction vector $c$, Oracle $\mathcal{O}$, $x_0\in K$ initial starting point, minimum $R>0$ radius of ball $B_R(x_0)$ centered on $x_0$ containing $K$, maximum $r>0$ radius of ball $B_r(x_0)$ centered on $x_0$ contained within $K$. \\
    \Output Approximate minimizer $x\in K$.
    
    \State $x_1 \gets Uniform(x_0, R, r)$
    \State $\Sigma_1 \gets Uniform(x_0, R, r)$
    \While{$t=1,2,\dots,T$}
        \State Update the temperature schedule $\beta_t = R(1-1/\sqrt{n})^t$
        \State Draw sample point from a random walk in $K$ as $x_t \gets Sample(e^{-U(x)/\beta_t}, x_{t-1}, \Sigma_{t-1}, k)$ 
        \State Update covariance matrix:
        \For{$i=1,\dots, n$}
            \State $x_t^{(i)} \gets Sample(e^{-U(x)/\beta_t}, x_{t-1}, \Sigma_{t-1}, k)$
        \EndFor    
        \State $\Sigma_t \gets \frac{1}{n}\sum_{i=1}^n x_t^{(i)}(x_t^{(i)})^\intercal-\frac{1}{n}\sum_{i=1}^n x_t^{(i)}(\frac{1}{n}\sum_{i=1}^n x_t^{(i)})^\intercal$
    \EndWhile
\end{algorithmic}
\end{algorithm}
```

The sampling procedure used in the above algorithm is critical to its performance, and is known as a the Hit-and-Run sampling algorithm. It makes use of a random walk algorithm (in particular a version of the [[Monte Carlo simulation#Metropolis algorithm|Metropolis algorithm]]) to sample new points that are biased towards those that obtain lower values of the objective, these values being more concentrated near the mean of the intermediate distributions given below.

```pseudo
\begin{algorithm}
\caption{Sampling subroutine}
\begin{algorithmic}
\Input Objective function $U$ specified in terms of a unit direction vector $c$, Set membership oracle $\mathcal{O}$, Current minimizing estimate $x_t$, Estimate of covariance matrix $\Sigma_t$, Number of sampling steps (along random walk) $k>0$.
\Output Random sample $x\in K$ with density $p_t\propto e^{U(x)/\beta_t}$.
    \For{$i=1,\dots,k$}
        \State $v\gets u\sim N(0,\Sigma_t)$
        \State $l\gets$ Line through $x_t$ in direction $v$
        \State $x_t^{(i)} \gets x$ sampled proportional to $e^{-U(x)/\beta_t}$ resticted along $l\cap K$
    \EndFor
\end{algorithmic}
\end{algorithm}
```

(Note, the paper does not mention how samples restricted along the projected lines are drawn as this appears to itself require a additional rejection sampling process that is not accounted for.)

In particular, the random walk, after sufficiently many iterations $k\in O(d^3)$, converges to a [[Markov chains#^a024ae|stationary distribution]], namely the Gibbs distribution, of the form of a [[s-Concave densities#Log-concave densities|log-concave density]] $$p_t = \frac{e^{-U(x)/\beta_t^2}}{\int e^{-U(y)/\beta_t^2}\,dy}$$which is concentrated around the minimizer of $U$, i.e., $E_{p_t}[U(x)]\to \min_{x\in K} U(x)$. In particular the following lemma is provided.

**Lemma:** For convex objective function $U(x)=c^\intercal x$ for $c\in\mathbb{R}^d$, temperature $\beta$, and $X$ sampled with density $p\propto e^{-U(x)/\beta}$, $$E_{p}[U(X)]\leq +\min_{x\in K}U(x)+d\beta.$$

Note, since $K$ is bounded and compact this bound has a tight lower bound.  

Estimation of the covariance matrix $\Sigma_t$ uses a similar sampling procedure as just described, however, in order to use a known result concerning convergence the intermediate distribution $p_t$ is first transformed using the [[Distributions along projections#Cholesky transformation|cholesky transformation]] to allow samples to be drawn from a uniform distribution.

Lastly, note the initial uniform sampling step draws a random sample $X$ from $K$ uniformly at random, and estimates the covariance matrix $\Sigma$ using a uniform distribution over $K$.

**Theorem: (Algorithm convergence)** For any convex region $K$ with membership oracle $\mathcal{O}$, initial point $x_0\in K$, scalars $R$, $r$ such that $K\subseteq B_R(X_0)$ and $B_r(x_0)\subseteq K$ where $B_r(x_0)$ is maximal, the algorithm, with probability $1-\delta$, outputs a point $x_T\in K$ such that $$U(x_T)\leq \min_{x\in K}U(x)+\epsilon$$after $T=O(\sqrt{d}\log(Rd/\epsilon\delta))$ stages and $k=O(d^3\, polylog(d))$ intermediate iterations (samples along the random walk) per stage, and $n=O(d \,polylog(d))$ rounding samples for estimating the covariance matrix, with at most $O(d^{4.5}\, polylog (d))$ membership oracle calls.

The analysis of the above theorem is carried out by bounding the [[Information theory#Total variation distance|total variation distance]] between the intermediate distributions, and consequently that the value of $E_{x\sim p_t}[U(x)]$ converges towards the optimal value at rate proportional to the temperature schedule $\beta_t$ which itself decreases at a exponential rate. 


## Optimality
The authors provide some discussion on why simulated annealing works well in practice based on a optimality argument for sampling method that have intermediate distributions that take the form of Gibbs distributions.

**Theorem:** For any sequence of functions $f_1,f_2,\dots,f_m:K\to\mathbb{R}$ and corresponding densities $dp_i(x)=f_i(x)/\int_k f_i(x)\,dx$ that satisfy (1) $f_i$ are log-concave, and (2) the total variation distance $\delta(p_{i-1}-p_i)<1-\epsilon$ where $1/\epsilon\in poly(d)$. Then, for any axis $c=(1,\dots,0)$ and corresponding conic section $K=\{x\in\mathbb{R}^d\mid \|x\|\leq 2x_1\leq 2\}$, we have $$E_{dp_T}[c^\intercal X]\geq \frac{E_{dp_1}[c^\intercal X]}{e}$$after $T=\sqrt{d}/(2\ln(2e/\epsilon))\in\Omega(\sqrt{n})$ distributions (phases).

Thus, any stochastic process (such as simulated annealing) that can be put in terms of the above theorem can only drop the expected value of the process by a factor of $e$ towards the optimum after $\sqrt{d}$ phases. Consequently, such methods need at least $\Omega(\sqrt{d})$ phases to converge. 

(TODO) - how does this related to the given Lemma 4.1?


## Extensions to arbitrary convex functions
The authors give a lemma concerning the optimization of arbitrary [[Convex functions]] $U$; i.e., the intermediate distributions (energy) are any form of [[s-Concave densities#Log-concave densities|log-concave]] distribution.

At the time of writing sufficiently good results for bounding the mixing time of of log-concave distributions of simulated annealing do not exist. However, the authors do provided a (simple) bound on the Warm-start of the sampling process under the $L_2$ norm for such distributions. 

**Lemma:** Let $U$ be a convex function over a convex domain $K$ with range $M=\max_{x\in K} U(x)-\min_{x\in K}U(x)$. Then for temperature annealing schedule $\beta_t = M(1-1/\sqrt(d))^t$, and intermediate distribution $p_t\propto e^{-U(x)/\beta_t}$ we have $$\|p_t/p_{t+1}\|_2\leq 5$$for all $t\geq 0$.

Consequently, the total variation can be bounded as $\delta(p_t,p_{t+1})\leq \max\{1/2,1-\frac{1}{\|p_t/p_{t+1}\|_2}\}$.

Moreover, the following lemma can also be stated (while only mentioned in the paper)

**Lemma:** 