Simulated annealing is a method of [[Stochastic optimization]] based on random sampling from distributions which are formulated to concentrate samples near (ideally) the desired quantity [[@Kalai_2006]]. More specifically, the distributions in question evolve from being uniform of the domain of interest to that of the target distribution (.e.g., one that is concentrated near the optimum value). 


# Overview
Per [[@Salamon_2002]], simulated annealing processes are defined as follows:

**Problem statement: (Simulated annealing optimization)** Given a configuration space $\Omega$ (e.g., list of states or domain of an objective function) and a objective function $U:\Omega\to\mathbb{R}$, which is typically modified to be stated in term of an energy function, and a graph $G$ defined on $\Omega$ that specifies allowed configuration changes, e.g., $G:\Omega\to\mathcal{P}(\Omega)$, from one state to another (this is called a Markov kernel). Simulated annealing then simulates a sequence of random walks (e.g., using the Metropolis algorithm as used in [[Monte Carlo simulation#Markov chain Monte Carlo|Markov chain Monte Carlo]]) which converge to low energy states as follows: 
  1) Given a initial state $s^{(t)}$;
  2) Draw a random sample of the neighbouring states of $s^{(t)}$ according to $G$, that is, $\hat{s}\in G(s)$;
  3) Accept this new state with some probability $P_t(\hat{s})$, otherwise reject this new state and remain at state $s$. 

The last step biases samples (moves along the random walk) in favor of those that decrease energy. In particular, if $E(s^{(t)})$ is the energy associated with the sate of the $t$ step, then rather than what is written we can equivalently choose to always accept the new sample $\hat{s}$ provided $E(\hat{s})-E(s^{(t)})\leq 0$, otherwise, if $E(\hat{s})-E(S^{(t)})>0$ accepting the sample with probability $P_t(\hat{s})$. Accepting this last sample despite it increase energy is done to help ensure the optimization process does not get trapped in (non-minimal) local optima. 

The form of the intermediate distribution $P_t$ is of critical importance to the performance of the algorithm. 

The intermediate distributions that result from this evolutionary process (not in the biological sense) satisfy the following two properties: 
  1) Any two consecutive distributions, say $p_t$ to $p_{t+1}$, must not be too different from one another; .e.,g the [[Information theory#^7edae7|total variation]] is bounded to be small, $\delta(p_t,p_{t+1})<1$.
  2) All intermediate distributions must be efficient to sample.

With all this in mind we can state a general version of the Simulated annealing algorithm:

```pseudo
\begin{algorithm}
\caption{Simulated Annealing}
\begin{algorithmic}
\Input Objective function $U$, A temperature schedual $\beta(t)$ with initial starting temperature $\beta(0)=T$, Initial state $s^{(0)}$.
\Output Approximate minimizer $\tilde{x}$ of objective.
    \State $s \gets s^{(0)}$
    \While{$t=1,2,\dots$}
        \State Sample a potential state $s$ from $G(s)$ by following the Metropolis algorithm for $k$ steps
        \If{$p(x)\geq p(\theta^{(t)})$}
            \State $\theta^{(t+1)}\gets s$ with probability $p(s)/p(\theta^{(t)})$
        \Else
            \State $\theta^{(t+1)}\gets \theta^{(t)}$ 
        \EndIf    
    \EndWhile
\end{algorithmic}
\end{algorithm}
```


