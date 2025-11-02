---
doc type: Note
authors: Spencer Szabados
date: 2023-05-01
tags:
  - machine_learning
  - gan
  - variational_methods
  - generative_models
---
___

Variational autoencoders are a kind of [[Generative models|generative model]], specifically a [[Push-forwards models|push-forwards model]], that consists of two coupled independently parametrized models that work in tandem. 

# Overview
We begin by exploring probabilistic autoencoders which serve as the support for variational autoencoders. 

Autoencoders, in essence, attempt to learn an efficient transformation, $f_\theta$, for compressing a collection of inputs into a latent space, $Z$, from which the inputs can be accurately recovered using another transformation, $g_\phi$, that is learned in tandem with $f_\theta$; structurally, this take the form $$\begin{align}p_X\sim X: f_\theta&\to U\\\ U:g_\phi&\to\hat{X}\approx X,\end{align}$$where $X\in\mathbb{R}^d$ and $U\subseteq \mathbb{R}^p$ with $p<d$.  Thus, we desire that $g_\phi\approx f_\theta^{-1}$ over the domain of interest; however, as $p<d$ , $g_\phi$ will not be the true inverse of $f_\theta$.

The encoder is then treated as a generative model, where a sample is drawn from $U$ and passed through $g_\phi$ to generate a new sample $\hat{X}$. 


## Training autoencoders 
During training, under no additional constraints, we attempt to minimize the reconstruction error between inputs and the generated output: 

Empirically this is approximated as:
$$\arg\min_{\theta,\phi}\frac{1}{2}\sum_{i=1}^N \|g_\phi(f_\theta(x))-x_i\|^2$$


## Variational autoencoders
Much of the following is taken from [[@Kingma_2019]] unless otherwise stated.

VAEs consist of two probabilistic models respectively referred to as the encoder $f_\theta$ and decoder $g_\phi$ (the decoder is sometimes also called the generator) each with sperate parameter sets $\theta$ and $\phi$. The encoder $f_\theta$ models the conditional Bayesian $p(u|x)$ and the generative model, $g_\phi$, attempts to fit $q(x|u)$ where $u\sim p_U$ is randomly sampled from the latent space $U\sim q_U$ where is fit as part of the training procedure.

Structurally, this take the form $$\begin{align}p_X\sim X: f_\theta&\to U\sim q_U\\ U:g_\phi&\to\hat{X}\approx X,\end{align}$$where $X\in\mathbb{R}^d$ and $U\subseteq \mathbb{R}^p$ with $p<d$; or rather probabilistically $$\begin{align}p(x,u) &= p(u|x)p_X(x)\\ q(x,u)&=q(x|u)p_U(u),\end{align}$$with conditional distributions $$\begin{align}p(x|u)&=\frac{p(x,u)}{p_X(u)}=\frac{p(u|x)p_X(x)}{\int_{\mathcal{X}}p(u|x)p_X(x)\,dx}\\ q(u|x)&=\frac{q(x,u)}{q(x)}=\frac{p(u|x)p_X(x)}{\int_{\mathcal{X}}p(u|x)p_X(x)\,dx}\end{align}$$

This model comes about from the question of how to chose the prior $p_U$. Ideally, we would sample from $p(u|x,\theta)$ directly, but this is conditioned on $x$ which is inaccessible during the generative procedure outside of training. Consequently, instead $q_U$ is fixed beforehand, typically as a Gaussian, and is sampled randomly and fed into $g_\phi$.


## Training variational autoencoders 
The training objective taken to train VAEs is the empirical [[Evidence lower bound|evidence lower bound]]$$\max_{\theta,\phi}\left\{\sum_{i=1}^N\log p(x_i|\theta,\phi)-\lambda\mathbb{KL}[p(u|x_i,\theta)|p_u]\right\}$$which is a weighted linear combination between the reconstruction loss and [[Information theory#Kullback-Leibler divergence|Kullback-leibler divergence]] between the encoded distribution and desired (fixed) distribution, where $0\leq \lambda\leq 1$ is a hyperparameter used during training and $$\begin{align}p(x_i|\theta,\phi) &= \int_U q(x_i|u,\phi)p(u|x_i,\theta)\,du\\ &\approx \int_Uq(x_i|u,\phi)p_U(u)\,du.\end{align}$$
Critically, as sampling $u$ from $p_U$ is stochastic process we cannot effectively utilize backpropagation from the generator though to the encoder for the model as described; this is due to gradient estimates of this loss having large variance as a result of the stochastic sampling required to approximate the gradient, see [[@Tan_2019]]. Thus, instead of sampling from $p_U$ directly we reparametrize this process. If $\mu_x$ and $\sigma_x$ are the parameters output from $f_\theta (x)$, then instead of drawing a sample $u\sim p_U(\mu_x,\sigma_x)$ we draw a sample $z\sim N(0,1)$ and set $u=\mu_x+z\sigma_x$. This allows us to remove the stochastic sampling procedure from the forwards process of the network to be able to utilize standard backpropagation to train the network.


# Vartiational autoencoders as flows
Variational autoencoders can be seen as a kind of [[Normalizing flows|flow model]] within the joint space (TODO)


# Modeling different latent space (priors)
## Mixture model latent spaces
[[@Jiang_2017]] 


## Multimodal priors (noise) 
