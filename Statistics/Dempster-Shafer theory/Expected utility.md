---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - belief_functions
  - dempster_shafer
  - statistics
  - classification
references:
  - "[[@Tong_2021]]"
---
---
# Overview

For decision making problems, such as [[Classification and clustering|classification]], one can define the lower and upper expected utilities that would be provided by making a certain discussion (e.g., selecting a particular class); similar to computing expected regret in [[Reinforcement learning]].

**Definition: (Expected utility)** Given a frame of decrement $\Theta=\{C_1,\dots,C_K\}$ of classes and a [[Belief functions#^e1a106|mass function]] $m:2^\Theta \to [0,1]$ define the _lower and upper expected utilities_ of assigning (selecting) some $C_i$ by $$\underline{E}_m[f_{C_i}] = \sum_{A\subseteq \Theta}m(A)\min_{C_j\in A}u_{ij}$$and $$\overline{E}_m[f_{C_i}] = \sum_{A\subseteq \Theta}m(A)\max_{C_j\in A}u_{ij}$$where $u_{ij}\in [0,1]$ is the utility value -- defined by some functional relation on belief -- provided by selecting class $C_i$ when the true class is $C_j$, and $f_{C_i}$ denotes the act (assignment function) of selecting $C_i$ in the face of some input. 

A pessimistic decision-maker would correspond to selecting the class with largest lower expected utility, while a optimistic (or risky) decision-maker would opt to select the class with the largest upper expected utility.

The expected utilities can be properly extended to all possible assignment actions in $\mathcal{P}(\Theta)$ by expanding the set of utility values to include all combinations of sets that contain the true class and those that do not contain the true class; i.e., constructing a matrix $U$ of size $2^{|\Theta|}$-by-$K$, whose entries could be denoted as $u_{A,j}$, where $A\subseteq \Theta$, store the utility value of taking the action of assignment of input to the class collection (subset) $A$ when the true class is $C_j$. 

The generalized Hurwicz decision criterion can be used to model a decision makers attuite (according to the above).

**Definition: (Pessimism index)** Let $f_{C_i}$ be an act of selecting class $C_i$, and let $v$ be the _pessimism index_ of taking this action. The weighted expected utility provided by taking this action is $$E_{m,v}=v\underline{E}_m[f_{C_i}]+(1-v)\overline{E}_m[f_{C_i}],$$in which a pessimistic attitude corresponds to $v=1$ and optimistic to $v=0$.