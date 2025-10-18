---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - machine_learning
  - fundamentals
---
---

Activation functions, as used in machine learning, are functions associated with nodes (and therefore layers) in [[Artificial neural networks]] and are responsible introducing nonlinear aspects into the models; these nonlinear transformation are required for these networks to be able to approximate general functions (not just linear ones). 

For a given (sum) node $\Sigma$ in an NN equip with an activation function $\sigma$ the output of the node is simply $\sigma(\Sigma)$; that is, the output of a node equip with an activation function is the value of the activation function evaluated using the nodes value as input. 


# Sigmoid nonlinearities 
Historically the most commonly used activation functions where sigmoid based functions; however, there are a plethora of different activation functions one can use.

**Definition: (Sigmoid function)** A sigmoid functions is a bounded real valued function $\sigma:\mathbb{R}\to \mathbb{R}$ that posses a non-negative derivative with exactly one inflection point.

An argument (theorem) presented in [[@Cybenko_1989]] tells us that any sigmodial function used in combination with others yields a universal function approximator. However, this argument does not provide a bound on the required number of terms to achieve a select quality of approximation to a given function. Refined results, which include bounds, were shown for step functions in [[@Barron_1993]], for general sinusoids in [[@Jones_1992]], and ReLU networks in [[@Breiman_1993]]. Where, overall, two-layer networks prove to be sufficient for universal function approximation.