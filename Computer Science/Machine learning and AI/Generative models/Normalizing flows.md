---
doc type: Note
authors: Spencer Szabados
year: 2023-08-28 Mon
tags:
  - flow
  - machine_learning
  - statistical_learning
  - random_sampling
---
___
Much of the following is taken from the survey paper [[@Kobyzev_2021]], in addition to [Daniel Daza](https://dfdazac.github.io/02-flows.html) and [Medha Agarwal](https://sites.stat.washington.edu/people/medhaaga/_downloads/9798bd8a2e0a0e86e18701d6384a9563/10_18_report.pdf). Normalizing flows originate from [[Optimal transport]] theory.

# Overview 
Normalizing flows are a [[Generative models|generative model]] that provide tractable distributions where both sampling and density evaluation can be performed efficiently. A normalizing flow is a transformation of a simple probability distribution into a more complex distribution by a sequence of invertible and differentiable mappings (e.g., upper triangular transformations defined below). Where, the density of a sample from the (target) more complex distribution can be evaluated by transforming it back to the corresponding point in simple distribution and multiplying it by a appropriate scaling factor (determinate of the Jacobian for the inverse transformation).

The transformations used within normalizing flows are typically taken to be _diffeomorphisms_. 

**Definition: (Diffeomorphism)** A function $T:\mathbb{R}^d\to \mathbb{R}^d$ is called a diffeomorphism, if is is bijective, differentiable, and has a differentiable inverse. ^2ea514

This assumption (construction constraint) is made since the [[Push-forwards models#^599c6e|push-forward]] of an absolutely continuous measure $\mu_Z$ with density $p_Z$ by a diffeomorphism $T$ is also absolutely continuous, the density of which can be calculated exactly as $$\begin{align}p_X(x) &= p_x(z)|\det(\mathbb{J}_T(z)|^{-1}\\ &=p_z(T^{-1}(x))|det(\mathbb{J}_{T^{-1}}(x))|,\end{align}$$that is, when $T$ is take to be a diffeomorphism the push-forwards is exactly the [[Statistical transformations#^2e88f0|change of variables]] formula.

Normalizing flows are typically structured (built-up) as the composition of various smaller invertible transformations: Let $T_1,T_2,\dots,T_N$ be a set of $N$ bijective (more specifically diffeomorphism) functions and set $T=T_N\circ T_{N-1}\circ \cdots \circ T_1$. Then $T$ is also a diffeomorphism and has inverse $T^{-1} = T_1^{-1}\circ \cdots \circ  T_N^{-1}$, and the determinate of the Jacobian is  $$\det(\mathbb{J}_{T^{-1}}(x)) = \prod_{i=1}^N \det(\mathbb{J}_{T_i^{-1}}(l_i))$$where $l_i=T_i\circ \cdots\circ T_1(z)=T_{i+1}^{-1}\circ \cdots\circ T_N^{-1}(y)$; I used $l$ here as these are latent variables (I think).  Formulating normalizing flows in this way is most common in the domain of Machine Learning since each layer in the [[Artificial neural networks|neural network]] architecture used to approximate the flow can (roughly) be see to correspond to one of the smaller constituent flows in the composition.


# Types of flows
The papers [[@Jaini_2020]] and [[@Kong_2020]] study the ability of various normalizing flows (presented below) to learn transport maps from one distribution to another. 

## Linear flows
Linear flows are the simplest mappings that can express correlation between the components of an input vector (between dimensions), which is necessary for all but the trivial normalizing flows.

**Definition: (Linear flow)** Linear flows take the form of composed [[Linear transformations|linear transformations]] together with a biasing term; that is, $$T_i=A_iz+b_i$$where $A_i\in\mathbb{R}^{d\times d}$ and $b_i\in\mathbb{R}^d$ are parameters. Recalling for linear transformations, if $A$ is invertible then so is $T$. Moreover, $\det(\mathbb{J}_T)=\det(A)$ for these transformations.  

### Triangular flows 
Triangular flows, in which $A$ is limited to be triangular, are the most common form of flow (transform) used as the computation of $\det(A)$ is cheap, requiring $O(d)$ time, compared to more general matrices, which in general can require $O(d^3)$ time to compute the determinate, while permitting $T$ to remain relatively expressive. More specifically, if we have $N$ triangular matrices $A_i$ each with ones along the diagonal (assumed) and a $p$-dimensional probability vector $p$ we take $$x=\left(\sum_{i=1}^p p_iA_i\right)z$$as the final transformation.

**Theorem: (Bogachev et.al., 2005)** If $\mu$ and $v$ are absolutely continuous [[Fundamentals of probability theory#^9e67e5|Borel]] probability measures on $\mathbb{R}^d$, then there exists an increasing triangular transformation $T:\mathbb{R}^d\to\mathbb{}R^d$, such that $v=T_\sharp\mu$. Moreover, this transformation is unique up to null sets of $\mu$ (i.e., up to elements that fall off the support of $\mu$). 

## Planar and Radial flows
Planar flows further generalize [[Normalizing flows#Linear flows|linear flows]] by incorporating a nonlinear [[Activation functions|activation function]] in the construction of $T_i$ along with a learnable scaling vector used for introducing further non-linear behaviours that might not be sufficiently captured by just the connecting weights of the network layers.

**Definition: (Planar flow)** Planar flows, $T$, are specified using two learnable vectors $u,w\in \mathbb{R}^d$, a non-linear activation function $h$, and a bias vector $b\in \mathbb{R}^d$ with $$T(z) = z+u\odot h(w^\intercal z+b).$$The Jacobian determinate of planar flows can be calculated as $$\det(\frac{\partial T}{\partial z}) = \det(1_d+u\odot h'(w^\intercal z+b)w^\intercal)=1+h'(w^\intercal z+b)u^\intercal w$$by the matrix determine lemma, which can be computed in $O(d)$ time.

Unfortunately, inverting planar flows is not always possible in closed form depending on the choice of $h$. This is partially addressed by a Sylvester flows, which are linear combinations of planar flows (used to achieve a higher degree of expressivity), where sufficient conditions for invertibility have been studied.

### Expressive power of planar flows 
The workshop paper [@Kong_2020](https://cseweb.ucsd.edu/~z4kong/files/The%20Expressive%20Power%20of%20Planar%20Flows%20(DL%20Workshop).pdf) describes the capabilities of planar flows to match/transport distributions. 


# Neural network implementation
Per [Daniel Daza](https://dfdazac.github.io/02-flows.html) one method of constructing a neural network, for the purposes of approximating a normalizing flow structured as a composition of smaller transformation, that results in a triangular Jacobian is to use so called _coupling layers_, as introduced by [Dihn etal 2015], which leaves the first $i$ elements of the input vector unchanged with the subsequent elements being transformed by scaling and translation functions which are implemented using neural networks; in particular, if $z^{(l)}$ is a input vector into layer $l$ then
$$\begin{align*}z^{(l+1)}_j &= z^{(l)}_j\quad \text{for }j=1,\dots,i\text{ and,} \\ z^{(l+1)}_k &= z^{(l)}_k\exp(s(z_1,\dots,z_i))+t(z_1,\dots,z_i). \end{align*}$$

TODO - how does $i$ correspond to the layer depth in the network?

The Jacobian of this coupling can be factored as $$\mathbb{J}_T= \begin{bmatrix}I_i & 0\\ A & diag(\exp(s(z_1,\dots,z_i))) \end{bmatrix},$$
where $A$ is discarded since we only care about computing the determinate of the Jacobian.

In practice the components of vectors are often permuted between layers (using bit masks) to transform all dimensions of the input vector as it passes through the network.

## Training
The most common objective for training a normalizing flows is the [[Information theory#Kullback-Leibler divergence|Kullback-Leibler divergence]], which appears in the optimization problem given by [Marzouk 2016]: $$\begin{align*}\text{Objective:}&\quad\min_{T} \mathbb{KL}(T_\sharp p |q)\\\text{Subject to:}&\quad \det(\mathbb{J}_T)>0 \text{ and }T\in\mathcal{F},\end{align*}$$which admits a global minimum. This can be equivalently stated as: $$\begin{align*}\text{Objective:}&\quad\min_{T} E_p[-\log(q\circ T(X))-\log(|\det(\mathbb{J}_T(X)|)]\\ \text{Subject to:}&\quad \det(\mathbb{J}_T)>0 \text{ and }T\in\mathcal{F},\end{align*}$$due to the relation $\mathbb{KL}(T_\sharp p|q)=\mathbb{KL}(p|T^{-1}_\sharp q)$.



# Applications 