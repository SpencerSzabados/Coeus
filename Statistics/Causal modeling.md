---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - statistics
  - causal_modeling
references:
  - "[[@Hardt_2022]]"
  - https://medium.data4sci.com/causal-inference-part-iv-structural-causal-models-df10a83be580
---
---
# Overview
A causal model is a method of attempting to describe causal, as opposed to correlated, relationships within a system. 

# Structural causal models
A structural causal model (SCM) is a sequence of assignments for generating a joint distribution starting from independent (random) noise variables. Through sequential execution of these assignments a set of jointly distributed random variables are built. The model thus serves as a generator of explanatory information for how things came to be and are potentially related to one another.

**Definition: (Structural causal model)** A _structural causal model_ $M$ is given by a set of [[Random variables#^5ceb15|random variables]] $X_1,\dots,X_d$ and corresponding assignments $$X_i = f_i(S_i,U_i),\quad\text{for } i=1,\dots,d,$$where $S_i\subseteq \{X_1,\dots,X_d\}$, dubbed _parent sets_, and $U_i$ are random variables, called the _noise variables_ (or _exogenous factors_), which are jointly independent (not necessarily mutually independent). The assignment functions $f$ are commonly called _response functions_.

Structure causal models can be visualised using a [[Elementary graphs#^040136|directed graph]] with a node for each variable $X_i$ with incoming arcs from the elements of the parents $S_i$. Looking at structure models in reverse, wrt to the direction of the edges, we can utilize the graph to construct unspecified models based on observed relationships. 

## Interventions
In a structural causal model $M$ we can take any assignment of the from $X=f(S,U)$ and replace it by any other we wish. The most common is to set $X=x$ a constant value. These substitutions are denoted $$M' = M[X=x].$$The assignment operator is called the _do-operator_ in this context.


## Causal effects
The causal effect of an action, say $X=x$ on a variable $Y$, refers to the distribution of the variable $Y$ in the new model $M[X=x]$. Causal effects are population quantities, often looked at though expectation differences for one change or another.

