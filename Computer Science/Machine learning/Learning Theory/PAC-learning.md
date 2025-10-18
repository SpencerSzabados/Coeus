---
doc type: Note
authors: Spencer Szabados
tags:
  - machine_learning
  - machine_learning_theorey
  - pac_learning
  - complexity_theory
---
___
Probably approximately correct (PAC) learning model is a useful notation to quantify how suboptimal a learned representation of a [[Reinforcement learning#Dynamical systems|dynamical system]] (also [[Linear dynamical systems]]) based on the data available (p237)[[@Hardt_2022]]. Similarly, it can be understand how large a data set needs to be in order to give good generalization results; however, the bound on these results are typically not very tight or applicable to many problems without making many assumptions. 


# Original PAC model
The following definitions are taken from [[@Kearns_1994]].

**Definition: (Instance space)** Let $S$ be a set of possible encodings (i.e., [[Representation scheme]]) of problem instances under consideration, $S$ is called the _instance space_.

**Definition: (Concept)** A _concept_ over a instance space $S$ is a subset $c\subseteq S$ of the instance space; concepts are equivalent to classification categories in the context of classification or Boolean functions (e.g., all pixel arrays that are representations of a specific letter).

**Definition: (Concept class)** A _concept class_ $C$ over a instance space $S$ is a collection of concepts over $S$. ^37eec5

Under the PAC model a learning algorithm will have access to positive and negative examples of an unknown target concept $c$, that belongs to a known concept class $C$. The learning algorithm is then judged based on ability to identify a hypothesis concept that accurately [[Classifiers|classifies]] instances as either positive (belonging to the concept $c$) or negative.

In classical learning problems, the target of a learning algorithm is the estimation of the underlying probability distribution of the instance space.

**Definition: (Target distribution)** Let $f$ be any fixed probability distribution over the instance space $S$. The distribution $f$ is called the _target distribution_.

If $h\in C$ is a concept over $S$, then a distribution $f$ over $S$ provides a natural measure of error between $h$ and the target concept $c$ by way of $$err(h) = P_{x\sim f}(c(x)\neq h(x)),$$where $x$ is a random draw of $C$ under $f$.

**Definition: (PAC Model)** Let $C$ be a concept class over $S$. We say that $C$ is PAC-learnable if there exists an algorithm $A$ with the following property: For every concept $c\in C$, for every distribution $f$ on $S$, and for all $0<\epsilon<1/2$ and $0<\delta<1/2$, if $A$ is given access to an Oracle $OS(c,f)$ and input $\epsilon$ and $\delta$, then with probability at least $1-\delta$, $A$ outputs a hypothesis concept $h\in C$ satisfying $err(h)\leq \epsilon$; that is, $$P_X(err(A(X)=h)\leq \epsilon)\geq 1-\delta.$$This probability is taken over random examples drawn from $C$ wrt $f$ by calls to $OS(c,f)$.

If $A$ runs in time polynomial in $1/\epsilon$ and $1/\delta$, the concept class $C$ is called _efficiently_ PAC-learnable. 

Notice that a PAC-learnable algorithm is demanded to perform well with respect to any distribution $f$. This requirement is moderated by only evaluating the probability of classness with respect to the same distribution.


## Representation size and instance dimension
The particular [[Representation scheme]] learned (and used to encoded problems) affects the run-time analysis of the learning problem. As such, a particular representation $R$ is typically fixed for a given concept class $C$, along with the corresponding size measure. In particular, the underlying instance space $S$ is typically chosen to be a finite dimensional binary domain; i.e., $S^n=\{0,1\}^n$.

**Definition: (Dimensional PAC Model)** Let $C^n$ be a concept class with fixed representation over $S^n$ (same presentation) and let $S=\cup_{i=1}^n S^i$ and $C=\cup_{i=1}^n C^i$. The modified definition of PAC learning is otherwise identical to the first, except now the algorithm $A$ is allowed to run in time polynomial to $n$ and $\|c\|$ as well as $1/\epsilon$ and $1/\delta$ when learning a target concept $c\in C^n$.


# PAC-learning in reinforcement learning

The methods that admit favorable PAC-error or PAC-regret indeed turn out to be powerful in practice.

## PAC-error 
Consider a [[Reinforcement learning#^d3d55b|SDM optimal policy problem]], with optimal fixed policy $\pi^*$. Suppose we allocate $N$ steps (samples) to probe the system and built policy $\pi^{(N)}$. The optimization _PAC-error_ of this policy is then give as $$\mathcal{E}(\pi^{(N)}) = E\left[\sum_{t=1}^T R_t(X_t,\pi^*(X_t),W_t)\right]-E\left[\sum_{t=1}^T R_t(X'_t,\pi^{(N)}(X'_t),W_t)\right],$$where $X'_t$ are the states induced (as they are not directly given) by policy $\pi^{(N)}$.

A model has $(\delta,\epsilon)$-PAC-error if $\mathcal{E}(\pi^{(N)})\leq \epsilon$ with probability at least $1-\delta$; i.e., $P(\mathcal{E}(\pi^{(N)})\leq \epsilon)\geq 1-\delta$ with respect to the sampling process probability distribution.

It is important as a designer to understand $\pi^*$ and ensure optimal results given perfect information; moreover, as PAC-error is a difference in value, it is possible for a method to have favorable PAC-error but be practically useless if what is being learned does not admit a good optimal policy.

## PAC-regret
PAC-Regret is better suited for the analysis of online problems where the reward function is newly evaluated at each time steps, even if that step is spent probing the system for learning.

Suppose we allow $T$ total actions and we instead want to know the cumulative award achieved after these $T$ actions are taken over the course of the algorithm running. A balance between the number of inputs used to construct a policy (exploration) and the number of inputs used to achieve the best reward (exploitation) must be struck. Let $\pi^*$ be some fixed policy (may not be optimal) and $\pi_1,\dots,\pi_T$ be the sequence of polices used to chose our actions. The _regret_ of the sequence of policies $\pi_1,\dots,\pi_T$ is defined as $$\mathcal{R}_T(\pi_1,\dots,\pi_T) = E\left[\sum_{t=1}^T R_t(X_t,\pi^*(X_t),W_t)\right]-E\left[\sum_{t=1}^T R_t(X'_t,\pi_t(X'_t),W_t)\right],$$which is the expected difference in rewards generated between the two policy choices.

One of the key differences between PAC-regret and PAC-error is that polices can change at each step under PAC-regret.

Likewise, it is important as a designer to understand $\pi^*$ and ensure optimal results given perfect information; moreover, as PAC-regret is a difference in value, it is possible for a method to have favorable PAC-regret but be practically useless if what is being learned does not admit a good optimal policies.