---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - statistics
  - probability_theory
references:
---
---

Probability theory (or mathematical statistics) focuses on what are called a probabilistic models which have three constituent components: 1) A sample space, 2) The events under consideration, and 3) A probability function; all these are defined below. This is different from a statistical model which is just a class of distributions over some data, such as used in fitting and prediction.

**Definition: (Sample space)** The set, $S$ (or often denoted $\Omega$), of all possible outcomes of an experiment is called the _sample space_ of the experiment. 

Once the sample space of an experiment is formalized, with all possible values being defined or enumerated, we can begin considering collections of possible outcomes of the experiment mathematically. 

**Definition: (Event)** An _event_ is any collection of possible outcomes of an experiment; in other words, an event is a subset of the sample space. ^4b13e7

The _realization_ of an experiment is the occurred outcome from the events sample space. If the same experiment is performed a number of times, the _frequency of cooccurrence_ of each outcome can be thought of as the probability. More specifically, the probability of any particular outcome is the proportion of all experiments taken at infinitum that realize this outcome. ^7d2bad


# Axiomatic foundations
For each event $A$ in the sample space $S$ of an experiment, we want to associate to it a number between zero and one, denoted $P(A)$, called it's probability. Before doing so, we must define the system being operated within; we must give a more formal definition of what an event is.

**Definition: (field)** A collection of sets $S$ that is closed under complements and finite unions is called a _field_; that is, $S$ is a field if 
  1) For any $B\in S$ we have $B^c\in S$; and 
  2) For any finite collection $\{B_i\}_{i\in I}\subset S$ it is true $\bigcup_{i\in I}B_i\in S$.

**Definition: (Sigma algebra)** A collection of subsets of $S$ is called a _sigma algebra_ (or _sigma field_), denoted by $\mathcal{B}$, provided it satisfies: ^9dcf42
  1) $\emptyset \in \mathcal{B}$;
  2) If $A\in \mathcal{B}$, then $A^c \in \mathcal{B}$ (closed under complementation);
  3) If $\{A_i\}_{i\in I} \in \mathcal{B}$ is a countable collection of sets, then $\bigcup_{i\in I} A_i\in \mathcal{B}$ (closed under countable unions).
Properties (1) and (2) imply that $S$ is always in $\mathcal{B}$. There can be many different sigma algebras associated with a single sample space, with the trivial sigma algebra $\{\emptyset, S\}$ and power set $\mathscr{P}(S)$ being most commonly discussed.

When the $\sigma$-algebra is defined over a [[Topological spaces]] in terms of the collection of open sets, the field is refereed to specifically as a _Borel field_. This is the most commonly used $\sigma$-algebra over continuous domains.

Sigma algebras represent the elements (_events_) that can be assigned probabilities, and can be consistently operated on under the rules of probability analysis. (Note, the definition of a sigma algebra is different, more general in some ways, than the definition of a topology constructed from open sets.)

A elementary class of functions that show up in statistical literature are Borel functions, which are closely related to the definition of continuity in [[Topological spaces|topology]] under the perspective that a $\sigma$-algebra of a Borel set of $X$ is the smallest $\sigma$-algebra containing the open sets of $X$.

**Definition: (Borel function)** A function $f:X\to Y$ between two topological spaces is called a _Borel function_ (or _Borel measure_) if $f^{-1}(A)$ is a Borel set for any set $A$. ^9e67e5

**Definition: (Probability function)** Given a sample space $S$ and an associated $\sigma$-algebra, $\mathcal{B}$, a _probability function_ is a function $P:\mathcal{B}\to[0,1]$ that satisfies:
  1) $P(A)\geq 0$ for all $A\in \mathcal{B}$;
  2) $P(S)=1$;
  3) If $A_1,A_2,\ldots\in \mathcal{B}$ is a countable collection of pairwise disjoint (events), then $P(\cup_{i=1}^\infty A_i)=\sum_{i=1}^\infty P(A_i)$; this is called the axiom of countable additive probability, and is not accepted as a base axiom when following the deFinetti school of thought. 
The above properties are typically referred to as the _Kolmogorov's Axioms of probability_. 

**Definition: (Finite probability spaces)** A _finite probability space_, denoted by the ordered pair $(S,P)$, consists of a finite sample space $S$ along with a probability function ([[Measure spaces#^535f6f|probability measure]] on $S$) $P:\mathcal{B}\to [0,1]$, which recall is built on a sigma algebra of $S$. (p15)[[@Molloy_2002]].  ^2f36d7

Finite probability spaces of higher dimensions, specifically product spaces, can be constructed from the cross products of several different lower dimensional finite probability spaces.

While these axioms are core to probability functions, it can be laborious to check them all every time we set up a problem for analysis. Thus, the following theorem is developed to help solve this problem of practicality.

**Theorem:** let $S=\{s_1,s_2,\dots,s_N\}$ be a finite set, $\mathcal{B}$ be any sigma algebra of subsets of $S$, and let $p_1,p_2,\dots,p_N$ be nonnegative numbers associated to each element of $S$ that sum to one. Then $P$ is a probability function on $\mathcal{B}$ if for any $A\in \mathcal{B}$ $$P(A) = \sum_{i \;:\; s_i\in A}p_i$$holds. 

**Theorem:** If $P$ is a probability function and $A$ and $B$ are sets in $\mathcal{B}$, then 
  1) $P(B\cap A^c) = P(B)-P(A\cap B)$;
  2) $P(A\cup B) = P(A)+P(B)-P(A\cap B)$;
  3) If $A\subset B$, then $P(A)\leq P(B)$.

**Theorem: (Broole's Inequality or Subadditivity of probabilities)** If $P$ is a probability function, then $$P\left(\bigcup_{i=1}^\infty A_i\right) \leq \sum_{i=1}^\infty P(A_i)$$for any sets $A_1,A_2,\dots$ from $\mathbb{B}$.


# Enumerating outcomes and basic probabilities 
When the sample space $S$ considered is finite and all the outcomes in $S$ are equally likely, the probabilities of events can be calculated by counting the outcomes, e.g., combinatorics [[Basic counting]], in the event. 

Suppose $S=\{s_1,s_2,\dots,s_N\}$ is a finite sample space. Then for an event $A\subset S$, $$P(A) = \sum_{s_i\in A}P(\{s_i\}) = \sum_{s_i\in A}\frac{1}{N} = \frac{\text{\# of elements in } A}{\text{\# of elements in } S}.$$
Probabilities should be assigned based on the sampling mechanism, not whether the objects being counted are necessarily physically distinguishable or indistinguishable - with or without order.


# Conditional probability and independence

**Definition: (Conditional probability)** If $A$ and $B$ are events from a sample space $S$, and $P(B)>0$, then the conditional probability of $A$ given event $B$ occurring, is $$P(A|B) = \frac{P(A\cap B)}{P(B)}.$$
**Definition: (Statistical independence)** Two events ([[Random variables#^5ceb15|random variables]]) $A$ and $B$ are statistically _independent_, denoted $A\perp\!\!\!\perp B$, if $P(A\cap B) = P(A)P(B)$.  ^a6f427

The relationship between disjoint events and independent events should be explained in more detail, as it is tempting to say one implies the other or vice versa. Two events $A$ and $B$, assumed to have non-zero probabilities of occurring, are disjoint if they cannot simultaneously occur, i.e., $P(A\cap B)=0$. On the other hand, if $A$ and $B$ are independent, again assumed to have non-zero probabilities, they may simultaneously appear but one event has no influence on the other, where, $P(A\cap B)=P(A)P(B)$. Thus, if $P(A\cap B)=0$ this would imply $P(A)=0$ (or vice versa with changes to conditionality) a violation of the assumptions of non-zero probability. The only relation between disjoint and independent events is: two disjoint events can be said to be independent if one o them is impossible (the $\emptyset$ event). 

Two events $A$ and $B$ are _conditionally independent_ given a third event $C$, if they are independent after conditioning on the third; that is, events $A$ and $B$ are conditionally independent given $C$ if $P(A\cap B|C)=P(B|A\cap C)P(A|C)=P(B|C)P(A|C)$. ^1bae84

An expression that can be derived using Baye's rule (below) working under the assumption that the occurrence of event $B$ has no effect on the probability of event $A$; i.e., $P(A|B)=P(A)$. 

**Theorem: (Baye's rule)** Let $A_1,A_2,\dots$ be a partition of the sample space $S$, and let $B$ be any set. Then, for each $i=1,2\dots,$ $$P(A_i| B) = \frac{P(B|A_i)P(A_i)}{\sum_{j=1}^\infty P(B|A_j)P(A_j)}.$$
Bayes rule gives a way of "reversing" conditional probability statements. Due to the importance of this rule, especially within the context of [[Bayesian probability theory]], certain rearmaments and components of the equation are given specific names; $P(A_i)$ is the _prior probability_ of $A_i$ and represents our belief of $A_i$ before any additional information (observation) is given; $P(A_i|B)$ is the _posterior probability_ and is the refined belief of $A_i$ given the new evidence $B$; $P(B|A_i)$ is the _likelihood_ of $B$ given $A_i$; $\sum_{j=1}^\infty P(B|A_j)P(A_j)$ is the _evidence_ and represents the probability of the observed data given all possible choices for $A_i$. ^4b7ad7

**Definition: (Mutual independence)** A collection of events $A_1,\dots,A_n$ are mutually independent if for any subcollection $A_{i_1},\dots,A_{i_k}$, we have $$P\left(\bigcap_{j=1}^k A_{i_j}\right) = \prod_{j=1}^kP(A_{i_j}).$$ ^09a32c