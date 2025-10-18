---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - machine_learning
  - neural_networks
---
---

Neural networks (or Neural nets) originate from an attempt at modelling the processes of the human brain, but are drastically simplified in terms of neuron dynamics. Neural nets are a class of mathematical compositions of linked differentiable functions with both linear and nonlinear elements (both are required for universal function approximation) represented by nodes and [[Activation functions]]. 

# Classical feedforwards neural networks
Classical, or rather feedforwards neural networks (FNN), is a form of neural network wherein connections between layers (nodes) do not form cycles. In such networks, information only moves unidirectionally towards the output layer from the input layer. These remain a predominate model within literature.

The most primitive, and fundamental, form of a neural network is that representing a linear combination of values, which servers as a predictor function, taken with respect to a threshold value (indicator activation function). See (p147)[[@Natagrajan_1991]]. This form of neural network called a [[Perceptrons|perceptron]]. 

**Definition: (Linear-threshold unit)** Let $\vec{x} = (x_1,\dots,x_d)$ be a vector of inputs and $\vec{w}=(w_1,\dots,w_d)$ be a vector of real value weights. For a threshold value of $b$ the linear-threshold unit (neuron) is formulated as $$f(\vec{x}) = \begin{cases}1 &\text{if } \vec{w}^\intercal\vec{x}>b\\ 0 &\text{otherwise.}\end{cases}$$(The threshold value is sometimes implicitly assumed and dropped from notation.)

Networks of this kind, and likewise perceptron's, are only capable of learning linearly separable classes.

We might attempt to extend the functionality of [[Artificial neural networks#Linear-threshold units|linear-threshold units]] by replacing the threshold parameter by a nonlinear [[Activation functions|activation function]], $\sigma$, so that $f(\vec{x}) = \sigma(\vec{w}^\intercal\vec{x})$. However, the resulting network is still only able to perform linear classification, essentially, since the inputs leading into the activation function remains only a linear combination of $\vec{x}$. However, careful selection of this function can enable the ability to learn $XOR$ operations unlike before (recall [[Perceptrons]] can't learn $XOR$ directly), see [[@Kwon_1991]].

Furthermore, we might consider a change of basis used for representing $\vec{x}$; a method called feature engineering/design The basis functions typically used are those composed of linear combination of nonlinear function of the inputs. Such a change allows for nonlinear prediction, see [[Knowledge representation and features#Nonlinear predictors|transformation based nonlinear predictors]]. Human designed features are no longer commonly used, rather various neural network based training methods for discovering "rich features" have been developed that commonly outperform manual feature designs.

More generally, we can extend the definition of neural networks to include multiple layers, each of the following form.

**Definition: (Feedforwards neural network)** Let $\vec{w}$ and $\vec{b}$ be weight and bias vectors, $A$ a matrix, and $\sigma$ a component wise nonlinear function which applies the same nonlinear function to each of its input components, such that $$f(\vec{x}) = w^\intercal\sigma(A\vec{x}+\vec{b})$$is well defined. This is the classical formulation of a neural network predictor. The nonlinear function $\sigma$ is an [[Activation functions|activation function]].  ^8b5b5d


# Back-propagation 
Backpropagation is a learning algorithm used for training feedforwarded neural networks. The use of automatic differentiation systems allows gradients to be computed for each layer in the network, the values of which are used in updating the layer parameters during optimization. 
