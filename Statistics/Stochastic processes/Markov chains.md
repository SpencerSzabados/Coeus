---
doc type: Note
authors: Spencer Szabados
date: 2024-07-09
tags:
  - markov_chains
  - stochastic_processes
references:
---
---

Markov chains are a [[Probabilistic graph models]] commonly used for analysing (or generating) the convergence behaviour of random processes.

# Overview 
**Definition: (Markov process)** A _Markov process_ $\{X_t\}$ is a [[Stochastic Process]] with the property that, given the value of $X_t$, the values of $X_{i}$ for $i>t$ are not influenced by the values of $X_j$ for $j<t$; that is, each state is memoryless. More formally, the _Markov property_ states $$\mathbb{P}(X_{t+1}=s_{t+1}|X_0=s_0,\dots,X_t=s_t)=\mathbb{P}(X_{t+1} = s_{t+1}|X_t = s_t)$$for all time points $t$ and states $s_0,\dots,s_{t+1}$. [[@Taylor_1998]]


## Discrete time Markov chains 
**Definition: (Discrete-time Markov chain)** A _discrete-time Markov chain_ is a Markov process $\{X_t\}$ whose state space is a finite or countable set, and whose time index set $T=0,1,\dots$ is discrete. The probability of $X_{t+1}$ being in state $s_j$ given that $X_t$ was in state $s_i$ is called the _one-step transition probability_ and is denoted $P^{t,t+1}_{s_i,s_j} = P(X_{t+1}=s_j|X_t=s_i)$. 

When the one-step transition probabilities are independent of the time variable $t$, the Markov chain is said to have _stationary transition probabilities_, and the time index is dropped from the notation. The values $P_{i,j}$ are typically arranged into a matrix of values, $$\pmb{P} = \begin{bmatrix}P_{00} & P_{01} & P_{02} & \cdots\\
P_{10} & P_{11} & P_{12} & \cdots\\
\vdots &\vdots &\vdots &\\\end{bmatrix}$$The $i-th$ row is the state transition probability distribution of the values of $X_{t+1}$ under the condition $X_t = S_i$. Clearly we have the conditions $$P_{ij}\geq 0\quad\text{ and }\quad\sum_{j=1}P_{ij}=1.$$
A Markov process is completely defined once its transition probability matrix is given along with an initial state $X_0=s_0$ (more generally a probability distribution for the initial state value of $X_0$). To see why this is, suppose $P(X_0=s_i)=p_i$ and we are given $\pmb{P}$. Then it is sufficient to show that we can compute the quantities $$P(X_0=s_0,X_1=s_1,X_2=s_2,\dots,X_T = s_T),$$since any other probability an be obtained from terms of this form due to the axiom of total probability. We have $$P(X_0=s_0,X_1=s_1,X_2=s_2,\dots,X_T = s_T) = P(X_0=s_0,X_1=s_1,X_2=s_2,\dots,X_{T-1} = s_{T-1})P(X_T=s_T|X_0=s_0,X_1=s_1,X_2=s_2,\dots,X_{T-1} = s_{T-1})$$and by definition of the Markov process $$P(X_T=s_T|X_0=s_0,X_1=s_1,X_2=s_2,\dots,X_{T-1} = s_{T-1}) = P(X_T=s_T|X_{T-1} = s_{T-1})=P_{T-1,T}.$$Applying the same argument to all the previous states, we get $$P(X_0=s_0,X_1=s_1,X_2=s_2,\dots,X_{T-1} = s_{T-1},X_T=s_T)=p_{0}P_{01},\dots,P_{T-1,T}.$$ 

### Large-step transition probability matrices 
We are often interested in what the transition matrix looks like after $n$ steps have already been completed. 

The $n-th$ step transition probability matrices $\pmb{P}^{(n)}=[P_{ij}^{(n)}]$, where $P^{(n)}_{ij}=P(X_{t+n}=s_j|X_t=s_i)$, give the probabilities of state transitions after $n$ previous states have been carried out. These matrices can be computed by taking the $n$ power of $\pmb{P}$, that is, $$\pmb{P}^{(n)} = \pmb{P}\times \pmb{P}\times \cdots\times \pmb{P}.$$ 

**Definition: (State period)** Given a Markov chain with finitely many states $\{s_1,\dots,s_N\}$ and corresponding probability transition matrix $P$. The period of a state $s_i$ is defined as $$d(s_i)=gcd\{t\mid P_{ii}^{(t)}>0\}.$$If $d(s_i)>1$ then the Markov chain is said to be _periodic_. Otherwise, if all states have $d(s_j)=1$ the Markov chain is called _aperiodic_. ^b152c9

The period can be interpreted as the shared looping path within the Markov chain's underlying graph used to return to the starting state. Equivalently, we can define the period of a state as follows, if there exists a integer $T>1$ such that $$P(X_{t+m}=s_j|X_t=s_i)=P^{(m)}_{ij}=0$$unless $m$ is divisible by $T$.

Another property that is closely related to periodicity of a state is _return time_ of a state.

**Definition: (State return time)** Given a Markov chain with finitely many states $\{s_1,\dots,s_N\}$. The _return time_ from state $s_i$ to $s_i$ is $$H(s_i) = \min\{t\geq 1\mid x_t=s_i,x_0=s_i\}.$$When $t\geq 0$ this value is called the _hitting time_ of a state. The return time of a state is typically stated in terms of the expected $t$ to return to the state.

Clearly, for a given Markov chain state $d(s_i)\leq H(s_i)$.

### Irreducible Markov chains 
**Definition: (Irreducible Markov chain)** A Markov chain is _irreducible_ if the corresponding [[Elementary graphs#^040136|directed graph]] is [[Elementary graphs#^314a8e|strongly connected]]; equivalently, if for every $s_i,s_j\in \{s_1,\dots,s_N\}$ there exists some $m$ such that $P(X_{t+m}=s_j|X_t=s_i)=P^{(m)}_{ij} >0$.  ^128f40

**Lemma:** For any finite state, irreducible, aperiodic Markov chain, there exists a finite $T>0$ such that $$P_{ij}^{(t)}>0$$for all states $s_i,s_j$ and $t\geq T$.


### Regular transition probability matrices
Regular (definite below) Markov chains are important to study since they admit limiting distributions.

**Definition: (Regular Markov chain)** Given a finite state Markov chain with probability matrix $P$. If there exists a $k\geq 0$ such that $P^k>0$ (element wise), then $P$ , and the Markov chain, is called _regular_.

Clearly irreducible Markov chains are also Regular Markov chains.

**Theorem: (Limiting distribution)** A regular Markov chain $\{X_i\}$ with finitely many states $s_1,\dots,s_N$ has a _limiting probability distribution_ $\pi=(\pi_1,\dots,\pi_N)$ with $\pi_i>0$ with $\sum_{i=1}^N \pi_i=1$ that is independent from the initial state; more specifically, for the regular transition matrix $P$, there exists $\pi_i>0$ such that $$\lim_{n\to\infty}p^n_{ij}=\pi_j$$for $i=0,1\dots,N$, or equivalently $$\lim_{n\to\infty}P(X_n=s_j|X_0=s_i)=\pi_j.$$
Observe for the discrete state (discrete time) Markov chain, as given above, the limiting distribution is Categorical by construction. Moreover, a limiting distribution of a Markov chain, if it exits, is a [[Markov chains#^4746aa|stationary distribution]] of the Markov chain. ^a024ae

One simple test to determine if a Markov chain is regular is the following. If the transition probabilities matrix $P$ on $N$ sates is regular, then $P^{N^2}$ will have no zero elements. Conversely, if $P^{N^2}$ is not strictly positive, i.e., posses at least one non-positive element, the underlying Markov chain is not regular.


## Convergence of Markov chains
**Definition: (Stationary distribution)** Let $\{X_i\}$ be a finite state Markov chain with transition probability matrix $P$. A probability distribution $\pi$ (of being in a select state) is called a _stationary distribution_ of the Markov chain if $$\pi=\pi P.$$ ^4746aa

The properties of irreducibly and aperiodicity are often only listed when formulating a Markov chain problem in terms of random walks, these properties are equivalently combined into the following definition.

**Definition: (Ergodic)** A Markov chain that is _ergodic_ is one that has a unique invariant distribution, its equilibrium (stationary) distribution, to which it converges to given any initial state; that is, the random walk associated with the Markov chain is irreducible and aperiodic.

Clearly, all regular Markov chains are Ergodic but they might not be the only form of Markov chain with this property.

If a Markov chain is ergodic with equilibrium distribution $\pi$ then we can use this process to generate samples $\theta^{(1)},\dots,\theta^{(N)}$ from $p(\theta)$ by reporting the values of sates along the chain after equilibrium is reached (knowing when equilibrium is reached can be difficult); this concept is the premise for [[Monte Carlo simulation#Markov chain Monte Carlo|Markov chain Monte Carlo]].


**Theorem: (Fundamental theorem of Markov chains or Ergodic theorem)** For any finite, irreducible, aperiodic Markov chain, the following are equivalent:
  1) The Markov chain admits a stationary distribution $\pi$ (which is equal to its equilibrium distribution);
  2) For any initial distribution $p_0$, the distribution $p_t=p_{t-1}P$ with converge to $\pi$ (convergence is typically stated with respect to [[Information theory#Total variation distance|total variation]]);
  3) The Markov chain has a unique stationary distribution, as defined above, which is equal to $\pi$;
  4) The equilibrium distribution $\pi=(\pi_1,\dots,\pi_N)$ is given by $$\pi_i = \lim_{t\to\infty}P^{(t)}_{ii}=\frac{1}{E[\min\{t\geq1\mid X_t=s_i,x_0=s_i\}]}=\frac{1}{H(s_i)}$$which is defined in terms of the expected return time of the states.


### Markov chain mixing time
In order to better characterize the behaviour of (sequential) samples from a Markov chain (as mentioned above) we define the following properties.

As the current state in a Markov chain depends on the previous one, the samples generated from a Markov chain process will have some amount of dependence that can effect the sample quality; that is, samples drawn from the Markov process may not fit the target distribution within a tolerable error range. The effect of this dependencies on accuracy is quantified in terms of _autocorrelations_ between values of $f(x,\theta^{(i)})$ for values of $\theta^{(i)}$ drawn after equilibrium has been reached.

**Definition: (Autocorrelation)** For (sequential) samples $\theta^{(1)},\dots,\theta^{(N)}$ drawn from a Markov chain and a function $f$ of random variables,  
$$Var\left[\frac{1}{N}\sum_{i=1}^N f(x,\theta^{(i)})\right] = \frac{Var[f(x,\theta)]}{N/\tau}$$where $\tau=1+2\sum_{i=1}^\infty \rho(i)$, where $\rho(i)$ measures the autocorrelation; for Markov chains typically $\tau\geq 1$. 

When the fundamental theory of Markov chains can tell us how to derive the stationary distribution of a Markov chain it is not capable of telling us, for the purposes of simulation, how many samples are needed before a given Markov chain will sufficiently converge to the desired density (e.g,. this exact density might not easily computed). This is characterized by the following definition. 

Informally, per [[@Dwivedi_2018]], the mixing time of a Markov chain is a lower bound on the number of steps the sampling procedure (e.g., [[Monte Carlo simulation#Metropolis-Hasting algorithm|Metropolist-Hasting algorithm]] or [[Monte Carlo simulation#Gibbs sampling|Gibbs sampling]]) must be executed, expressed as a function of the distribution dimension $d$ and desired error tolerance $\epsilon$, to obtain samples that are $\epsilon$-close to the targets distribution in terms of [[Information theory#Total variation distance|total variation]] or some other measure.

**Definition: (Mixing time)** Let $\{X_i\}_{t\geq 1}$ be a Markov process with finitely many states $\{s_1,\dots,s_N\}$ and unique stationary distribution $\Pi$; .e.,g the Markov chain is [[Markov chains#^128f40|irreducible]] and [[Markov chains#^b152c9|aperiodic]]. The $\epsilon>0$ _mixing time_ of the Markov process is the time  $T>0$ needed so that given any initial distribution $p_0$ (of the states) $\delta(p_t,\Pi)=\frac{1}{2}\|p_t-\Pi\|_1\leq \epsilon$ (the [[Information theory#Total variation distance|total variation]] is less than the desired bound) for any $t\geq T$. ^549186


# Continuous state Markov chains
If the state space $\Omega$ for a Markov process $\{X_i\}_{i>0}$ is continuous then we must reformulate the transition probability definition to work with subsets $S\subseteq \Omega$ of the domain rather than singular points (as these would have zero probability); that is, we define the transition probability to be of the form $$P(X_{t+1}\in S|X_{t}=s),$$for some $s\in\Omega$, noting that conditioning on fixed observed states (equality condition) is permissible. Likewise, one-step transitions (entries of the stochastic matrix) must be stated in terms of joint [[Distribution functions of random variables#^c46bbe|probability density functions]], which are referred to as _Markov Kernels_ in the continuous setting, of the form $p(x,y)$, where $x,y\in\Omega$ with $y$ given as the current state. Continuing in this manner, the $t$-step transition densities are analogously $p^{(t)}(x,y)$ with the added constraint of $\int_\Omega p^{(t)}(x,y)\,dx=1$, and the special case that $p^{(0)}(x,y)=\delta_x(y)$.

**Definition: (Stationary density)** A stationary density of a continuous state Markov chain $\{X_i\}_{i\geq 0}$ on $\Omega$ with transition probability $p(x,y)$ is a probability density function $\pi(x)$ on $\Omega$ that satisfies $$\pi(x)=\int_\Omega\pi(y)p(x,y)\, dy$$



