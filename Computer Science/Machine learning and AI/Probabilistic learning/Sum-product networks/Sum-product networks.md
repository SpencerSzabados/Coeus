---
doc type: Note
authors: Spencer Szabados
tags:
  - generative_models
  - statistical_learning
  - graphical_models
---
---

Sum-product networks (SPNs), which are a _form_ of [[Probabilistic circuits]], can be seen as a probabilistic approach to deep learning methods. With SPNs being a form of [[Artificial neural networks#Classical feedforwards neural networks|feedforwards network]]. However, unlike most deep learning methods, sum-product networks have a probabilistic interpretation and are capable of expressing uncertainties over the generated outputs directly, rather than through an subsidiary mechanism or approximation. More specifically, SPNs represent a probability distribution that results from a hierarchy of combined distributions, which are combined through various weighted sums and products, [[@Sanchez-Cauce_2022]]. SPNs are capable of performing exact inference (computation of any marginal probability) in linear time in terms of the size of the model (number of nodes); this is especially advantageous in automatic decision-making processes that require some form of certainty or copiability, .e.g., medical diagnosis. SPNs were first introduced in [[@Poon_2011]].

SPNs, in think, are a nice balance between a theoretically appeasing model and computationally approachable solution, as least compared to more general graphical networks (e.g., Bayesian networks).


# Preliminary probability setup
Much of the following is taken from [[@Sanchez-Cauce_2022]], [[@Vergari_2019]].

Let $\vec{V}=(V_1,V_2,\dots,V_N)$ be a random vector with $\vec{v}=(v_1,\dots,v_N)$ a random realised sample. The set of all possible configurations, that is the set of all possible vector values, for $\vec{v}$ is denoted $conf(\vec{V})$, with $conf^*(\vec{V})$ denoting the set of all possible configurations that include subsets of elements present in $\vec{V}$ where not all variables are assigned values; That is, $$conf^*(\vec{V}) = \bigcup_{\vec{X}\in\mathcal{P}(\vec{V})}conf(\vec{X}).$$
**Definition: (Configuration restriction)** If $\vec{X}\subseteq \vec{V}$, the restriction (or marginal sample) of a configuration $\vec{v}$ from $\vec{V}$ onto $\vec{X}$, is denoted $\vec{v}|_\vec{X}$, equals the configuration of $\vec{X}$ where every variable $V\in\vec{X}$ takes on the same value as in $\vec{v}$.

**Definition: (Composition)** Given two configurations (realised samples), $\vec{x}$ and $\vec{y}$, of two disjoint sets, $\vec{X}$ and $\vec{Y}$, the _composition_ of the two, denoted $\vec{x}\vec{y}$, is the configuration of $\vec{X}\cup \vec{Y}$ such that $\vec{x}\vec{y}|_\vec{X}=\vec{x}$ and $\vec{x}\vec{y}|_\vec{Y}=\vec{y}$.

We must formalize how probability distributions are defined over configurations.

**Definition: (Extended probability distributions)** A probability distribution defined on $\vec{V}$ is a function $P:conf(\vec{V})\to [0,1]$ such that $P(\vec{v})\geq 0$ and $\sum_{\vec{v}}P(\vec{v})=1$; as expected. We then define an extended probability distribution on $\vec{V}$ similarly as a function $P:conf^*(\vec{V})\to [0,1]$ such that the restriction of $P$ to $conf(\vec{V})$ is a valid probability distribution; that is, for every $\vec{x}$ from $\vec{X}\subseteq \vec{V}$ we have $P(\vec{x}) = \sum_{\vec{v}|_{\vec{X}}=\vec{x}}P(\vec{v})$. Meaning the marginal probabilities within $conf^*(\vec{V})$ agree with those probabilities on $conf(\vec{V})$.

Just as with regular probabilities, a convex sum (weighted) of extended probabilities results in an extended probability distribution. Moreover, a product of extended probability distributions results in another extended probability distribution.


# Fundamentals of SPNs
**Definition: (SPN graph)** A sum-product network (SPN) graph $S$ is a rooted acyclic directed graph where:
  1) Each leaf node represents a probability distribution for a finite-state variable (generalises to continuous variables) $V$; that is, each leaf node is a  indicator variable dependent on the input vector and a discrete probability distribution.
  2) All non-leaf nodes are either a type of sum or product;
  3) Every edge $n_i\to n_j$ outgoing (propagating up) from a sum node has an associated weight $w_{ij}>0$.
It is assumed that for all SPNs the sum of child weights are normalized, i.e., $$\sum_{j\in ch(i)}w_{ij}=1$$where $ch(i)$ is the set node $i$'s children, and $w_{ij}\geq 0$.

SPN networks are built bottom-up in a recursive node by node fashion which defines a distribution, $S_n$ , to each node. 

**Definition: (Sum and Product nodes)** Let $n_i$ be a node of $S$ and $\vec{x}\in conf(S)$, a vector composed of leaf variables (perhaps not all) from $S$. If $n_i$ is a leaf node with (extended) probability distribution $P$, then $$S_i(\vec{x}) = P(\vec{x});$$if $n_i$ is a sum node, $$S_i(\vec{x}) = \sum_{j\in ch(i)}w_{ij}S_j(\vec{x}),$$and if it is a product node, $$S_i(\vec{x}) = \prod_{j\in ch(i)}S_j(\vec{x}).$$

**Definition: (Scope of a node)** The _scope_ of a node $n_i$ is denoted $sc(n_i)$ and equals, for a leaf node the the set of variables on which the probability distribution is defined, and for a non-leaf node the union of scopes of its children, that is, $sc(n_i)=\cup_{j\in ch(i)}sc(n_j)$. The scope of a SPN graph $S$ is the scope of the root node $sc(S)=sc(n_r)$.

A sum node is called _complete_ if all its children have the same scope. A product node is _decomposable_ if its children have pairwise disjoint scopes; that is, a product node $n_i$ is decomposable if and only if no node in the SPN is a descendant of two different children of $n_i$; i.e., no cycles in the non-directed graph.

If the probability distribution of $n_i$ is _degenerate_, meaning there is only one value of $V$, say $v$, for which $P(V=v)=1$ with $P(V\neq v)=0$ otherwise, then the above equations for nodal values in the SPN reduce to indicator functions of the form $S_i(x)=\mathbb{I}_{v}(x)$. 

**Theorem:** For every node $n_i$ in an SPN, the associated function $P_i:conf(S)\to \mathbb{R}$, with $$P_i(x)=S_i(x)$$is a valid (extended) probability distribution on $sc(n_i)$; that is, each node has associated to it a probability distribution that is defined on its leaf variables and results from recursive construction.


## Latent data encoded in sum nodes
Sum nodes can represent model variables in addition to latent random variables. In fact, all sum nodes that represent model variables are selective nodes.


## Selective SPNs
An SPNs is selective if for any node $n_i$ its distribution $S_i(\vec{x})$, for any $\vec{x}\in conf(S)$, only depends on one of its children's distribution; i.e., all weights are zero but one.

**Definition: (Selective SPN)** A sum node $n_i$ in an SPN is selective if for any $x\in conf(S)$ there exists exactly one $j\in ch(i)$ such that $S_j(x)> 0$ with $S_k(x)=0$ for all other $k\in ch(i)\backslash \{j\}$. A SPN is selective if all its sum nodes are selective. Selectivity only depends on the links in the SPN.

Note a SPN can be selective and still have partial configurations that result in positive contributions to $S_i(\vec{x})$.


## Inducted trees
**Definition: (Induced sub-SPN)** Let $S$ be a SPN and $\vec{v}\in conf(S)$ such that $S(\vec{v})\neq 0$. The sub-SPN induced by $\vec{v}$, denoted $S_\vec{v}$, is a non-normalized SPN obtained by (1) removing every node $n_i$ with $S_i(\vec{v})=0$ along with their associated edges, (2) removing all zero weight edges $n_i\to n_j$, and (3) removing recursively (bottom up) all nodes without parents, except for the root.

The value $S_v(\vec{\vec{v}})$ returned from $S_\vec{v}$ equals the value returned from the original SPN for input $\vec{v}$; that is, $S(\vec{v})=S_\vec{v}(\vec{v})$.

Moreover, if $S$ is selective, $\vec{v}\in conf(S)$, and $S(\vec{v})\neq 0$, then $S_v$ is a tree where every sum node has exactly one child. 


# The design of SPN graphs 
SPNs need to obey a strict structural conditions, compared to the more or less homogeneous structure of traditional [[Artificial neural networks]], in order to facilitate tractable inference. This either requires careful hand design or dynamic structure creation learned from training data. Consequently, SPNs have proven hard to scale, precluding them from many tasks, see [[@Peharz_2020]].

## Random SPNs (RAT-SPNs)
## Conditional SPNs 
[[@Gens_2012]]

## Learning SPN structures from data
Structural learning is the process of finding the graph of an SPN (forming links or configurations of templates) that closely fits the available training data. This is one of the differences between the creation of SPNs and [[Artificial neural networks]], though the latter's structure can also be computational learned it is very difficult in practice. See [[@Sanchez-Cauce_2022]]. 

[[@Gens_2012]] [[@Gens_2013]]

### Learned knowledge representations
One of the central motivators of [[Deep neural networks|deep learning]] methods is the abstraction (automation) of [[Knowledge representation and features]], see [[Deep network knowledge and feature representation]], rather than being reliant on hand design of feature extraction and representations. Exploration of the form of features within SPNs is explored within [[@Vergari_2019]]. 


# Learning parameters
The process of parameter learning consists of finding the best fit parameters for an SPN, i.e., finding values for the edge weights and parameters of the terminal node probability distributions, given a graph configuration and training dataset. In _generative learning_ (models designed to learn joint probabilities for estimating the likelihood of data or generating new data) the most common optimality criterion is applying [[Maximum likelihood]] to parameter values, while in _discriminative learning_ (models designed to learn conditional probabilities, e.g., those used for [[Classification and clustering]]) the goal is to maximize the conditional likelihood of the classes considered.

Let $\vec{D}=(\vec{v}^{(1)},\vec{v}^{(2)},\dots,\vec{v}^{(N)})$ be a dataset with $N$ (assumed) iid instances (samples) of the variables $\vec{V}$. Let $W$ be the set of weights in the SPN, a collection of matrices, and let $\Theta$ be the collection of parameters for the probability distributions of the leaves. Both the connection weights and distribution parameter values condition the probabilities of the SPN.

If we take the log-likelihood for our objective function$$\mathcal{L}_\vec{D}(W=\vec{w},\Theta=\vec{\theta}) = \log(P(\vec{D}|\vec{w},\vec{\theta}))=\sum_{i=1}^N\log(S(\vec{v}^{(i)}|\vec{w},\vec{\theta})),$$the learning goal is to find values for $W$ and $\Theta$ that maximize the log-likelihood.

In SPNs there is no restrictions placed on the parameters of one node from those of another, so optimization of parameters can be performed independently for each node (in the same vein as for NNs). Optimization of parameter values for leaves depends on the nodes distribution.



### Sample complexity
It was shown by [aden-ali] the number of samples necessary to learn tree structured SPNs with discrete or Gaussian leaves grows linearly (up to logarithmic factors) with the number of parameters in the SPN.


# Performing inference in SPNs
For an SPN, say $S$, and a realised vector $\vec{v}$ we have $$P(\vec{v})=S(\vec{v})=S_r(\vec{v}),$$where these values can be computed by an upwards pass from the leaves to the root of the SPN in linear time proportional to the number of edges. Moreover, if $\vec{X}$ and $\vec{Y}$ are two disjoint subsets of $\vec{V}$, then $$P(\vec{x}|\vec{y})=S(\vec{x}\vec{y})/S(\vec{y}),$$where $\vec{x}\vec{y}$ is the composition of $\vec{x}$ and $\vec{y}$. 

The task of performing inference based on some evidence $\vec{e}$ provided by observed values for a set of variables $\vec{E}$ of interest (e.g., input features) comes down to predicting values for some $\vec{X}\subseteq \vec{V}$. If $\vec{X}\cap \vec{E}=\emptyset$, meaning $\vec{X}$ and $\vec{E}$ are two disjoint subset of $\vec{V}$, then $P(\vec{x}|\vec{e})=S(\vec{x}\vec{e})/S(\vec{e})$ where $\vec{x}\vec{e}$ is the composition of $\vec{x}$ with $\vec{e}$.   


## Most probable explanation (MPE) inference
Most probable explanation (MPE) inference is a kind of inference that can be computed in linear time for SPNs in all cases.

**Definition: (MPE inference)** Most Probable Explanation (MPE) inference is of common interest in machine learning, where the most probable vector of variable values $\vec{x}\in \vec{X}$, where $\vec{X}=\vec{V}\backslash \vec{E}$ is intendent of evidence, is sought $$\begin{align} MPE(\vec{e}) &=\arg\max_\vec{x} P(\vec{x}|\vec{e})\\ &=\arg\max_{\vec{x}}P(\vec{x}\vec{e})/P(\vec{e})\\ &= \arg\max_{\vec{x}}S(\vec{x}\vec{e})\end{align}$$where $\vec{E}\cap \vec{E}=\emptyset$.

MPE inference is a special case of [[Maximum posterior]] (MAP) inference, where in MAP inference we are seeking values for a subset $\vec{y}$ of the components of the model (such as $\vec{y}\subset \text{components of }\vec{x}$) that maximizes the probability $P(\vec{y}|\vec{e})$. Moreover, simply projecting the MAP values of $\vec{x}$ onto the subset considered for a MAP problem is not guaranteed to be optimal (correct). 


# Applications 
## Image processing and classification 
## Natural language processing (NLP) 


# Advantages and Limitations


# Relation to other graphical models