---
title: "Diffusion forcing: Next-token prediction meets full-sequence diffusion"
authors: Boyuan Chen, Diego Martí Monsó, Yilun Du, Max Simchowitz, Russ Tedrake, Vincent Sitzmann
year: 2025
tags:
  - diffusion
  - motion_planning
  - machine_learning
references:
  - https://arxiv.org/pdf/2407.01392
  - "[[@Yoon_2025fast]]"
---

---

This paper makes use of the term "tokens" but this is bait, as nothing in the paper relates to designing, performing, or handling discrete tokens created from continuous data.

# Overview
The authors in this work propose a method of training and sampling from a [[Diffusion models]] sequentially to generate long trajectories (e.g., such as in planning, or video sequences) by varying the noise schedule over the trajectory. This is related to "rolling diffusion" methods. The intuition of the idea is to only partially denoise components of trajectories that are later in time than those earlier to try and capture deterministic relationships between later and earlier actions (or some form of uncertainty).

# Primary results 
The authors begin by outlining their diffusion setup over sequences using DDPM notion, namely: Suppose $\mathcal{X}$ is the data domain, denote by $(x_t)_{t=0}^h$ a sequence with time horizon $h$, let $p^{k}((x_t)_{t=0}^h)$ denote the data distribution with no noise, denoted using a super script, and consider the [[Diffusion processes]] over $K>0$, $k_t\in \{0,\dots, K\}$, $t\in\{0,\dots, h\}$ with variance schedule $(\beta_{k})_{k=1}^K$ defined by the [[Markov chains]] where for $x_t$ in the sequence $$p^k(x_t^{k_{t}}|x_t^{k_{t-1}})=\mathcal{N}(x^{k_t}; \sqrt{1-\beta_{k_{t-1}}}x_t^{k_{t-1}}, \beta_{k_{t-1}}I);$$or for $$\overline{\alpha_{k_t}} = \prod_{i=1}^{k_t}(1-\beta_i)$$we have $$x_t^{k_t} = \sqrt{\overline{\alpha_{k_t}}}x^0 + \sqrt{1-\overline{\alpha}_{k_t}}\epsilon,\quad \epsilon\sim\ \mathcal{N}(0,I).$$
The model is then parameterized to try and learn the reverse process as $$p_\theta(x_t^{k_t-1}|x_t^{k_t})=\mathcal{N}(x_t^{k_t-1}; \mu_\theta(x^{k_t}_t,k_t),\beta_{k_t}I)$$with $$\mu_\theta(x_t^{k_t},k_t) = \frac{1}{\alpha_{k_t}}\bigg(x_t^{k_t}-\frac{\beta_{k_t}}{\sqrt{1-\overline{\alpha_{k_t}}}}\epsilon_\theta(x_t^{k_t},k_t)\bigg).$$
As expected, the authors mention including some form of classifier guidance to the model, if $c(y|x^{k_t})$ is a classifier (or energy function) with some goal/class target $y$, the models sampling can be modified by taking $$\epsilon_\theta(x_t^{k_t}, k_t)=\epsilon_\theta(x_t^{k_t}, k_t)-\sqrt{1-\overline{\alpha_{k_t}}}\nabla_{x^{k_t}}\log c(y|x^{k_t})$$in the above parameterization.

## Method
In order to simplify the implementation, the authors parameterize the model using a [[Recurrent neural networks]] of the from $$z_{t}\sim p_\theta(z_{t}|z_{t-1},x_t^{k_t},k_t)$$with the assumption that for $k_t=K$, and $p^K\approx \mathcal{N}(0,I)$, $$p_\theta(z_t|z_{t-1},x_t^K,K)=p_\theta(z_t|z_{t-1})$$reducing to modelling the prior and similarly if $k_t=0$ this is modelling the posterior of latent variables. While a observation model learns to predict $x_t^{0}$ given $z_{t-1}$; i.e., $$x_t^0\sim p_\theta(x_t^0|x_t^{k_t}, z_t),\quad z_t\sim p_\theta(z_t|z_{t-1},x_t^{k_{t}},k_t).$$
This approach, of varying the noise over the sequence length, is referred to by the authors as partial token masking.

In order to construct the index $k_t$ the authors propose the following triangular matrix for causal sampling $$\mathcal{K} = \begin{bmatrix} K & K & K & \cdots & K\\ K-1 & K & K & \cdots & K\\ K-2 & K-1 & K & \cdots & K\\ \vdots &\vdots &\vdots &\ddots &\vdots\\ 1 & 2 & 3 & \cdots & h\\ 0 & 1 & 2 &\cdots & h-1\\ 0 & 0 & 1 &\cdots & h-2\\
\vdots & \vdots &\vdots &\ddots &\vdots\\ 0 & 0 & 0 & \cdots &1\\ 0 & 0 & 0 & \cdots &0\end{bmatrix}$$where $(x_t)_{t=0}^h$ is denoised row wise where $k_t=\mathcal{K}_{t}$. More specifically, the model is trained following the algorithm.

```pseudo
\begin{algorithm}
\caption{Diffusion forcing training}
\begin{algorithmic}
\Input Let $D$ be the dataset of sequences (trajectories) $(x_t)_{t=0}^h$ (assuming some fixed sampling rate in time), $(\beta_k)_{k=1}^K$ the diffusion variance schedule, $\eta$ the learning rate, $\delta$ the loss tolerance, and $p_\theta$ the initialized model (latent and observation models combined) with $h_0$ initialized.
\Output Trained diffusion model $p_\theta$.

    \While{$L > \delta$}
        \State Sample $(x_t)^h_{t=0}\sim D$
        \For{$t = 0,\dots, h$}
            \State Sample $k_t\sim \mathcal{U}\{0,\dots,K\}$\Comment{The authors don't sample dependent on t.}
            \State Sample $x_t^{k_t} = \sqrt{\overline{\alpha_{k_t}}}x^0 + \sqrt{1-\overline{\alpha}_{k_t}}\epsilon,\quad \epsilon\sim\ \mathcal{N}(0,I)$\Comment{Forward Markov process.}
            \State $h_t \sim p_\theta(h_t|h_{t-1},x_t^{k_t},k_t)$
            \State $\hat\epsilon_t \gets \epsilon_\theta(h_t,k_t)$
            \State $\mathcal{L} \gets \mathcal{L} + \|\epsilon - \hat\epsilon_t\|^2$
        \EndFor
        \State $\theta \gets \theta - \eta\,\nabla_\theta\!\Big(\frac{1}{h+1}\mathcal{L}\Big)$
    \EndWhile
\end{algorithmic}
\end{algorithm}
```
^ac4f92

```pseudo
\begin{algorithm}
\caption{Diffusion forcing sampling}
\begin{algorithmic}
\Input Trained model $p_\theta$ with $h_0$ initilized, schedule $(\beta_k)_{k=1}^K$, triangular index matrix $\mathcal{K}$ (e.g., that above).
\Output Generated sequence $(\hat{x}_t^0)_{t=0}^h$

    \State Sample $x_t^{K}\sim\mathcal{N}(0,I)$
    \For{$t=0,\dots,h$}
        \For{$k_t=K,\dots,1$}
            \State $h_t \sim p_\theta(h_t|h_{t-1},x_t^{k_t},k_t)$
            \State $\hat\epsilon_t \gets \epsilon_\theta(h_t,k_t)$
            \State $\mu_\theta \gets \frac{1}{\sqrt{\alpha_{k_t}}}
                \Big(x_t^{k_t}-\frac{\beta_{k_t}}{\sqrt{1-\overline{\alpha}_{k_t}}}\hat\epsilon_t\Big)$
            \State $\sigma_{k_t}^2\gets
                \frac{\beta_{k_t}(1-\overline{\alpha}_{k_t-1})}{1-\overline{\alpha}_{k_t}}$
            \State Sample $z\sim\mathcal{N}(0,I)$ if $k_t>1$, else $z=0$
            \State $x_t^{k_t-1} \gets \mu_\theta + \sigma_{k_t}z$
        \EndFor
        \State $\hat{x}_t^0 \gets x_t^0$
    \EndFor
\end{algorithmic}
\end{algorithm}
```

In this way, each trajectory $(x_t)_{t=0}^h$ is supposed to be causally denoised along its length, producing temporally consistent samples.

The authors provide the following illustration of sampling from the method wrt $\mathcal{K}$.

![[Screenshot From 2025-11-04 19-53-40.png]]

# Empirical results
The authors report good results over moderate time horizon planning tasks and continuous auto-regressive video diffusion rollouts. They claim their method maintains generation coherence better than competing methods but they don't offer any compelling metrics for this claim only examples.

# Issues
In the appendix the authors mention, what is in my mind, the major feature of this work and why it is better formulated compared to its contemporary rolling diffusion methods which make independence assumptions between sequence elements.

The Markov property stated in Eq. (A.3),$$p_\theta(z_t, x_t^{k_t} \mid (z_i)_{i=0}^{t-1}, (x_s^{k_s})_{s<t}) = p_\theta(z_t, x_t^{k_t} \mid z_{t-1})$$is only valid in an *augmented state space* where the hidden variable $h_t$ encodes a [[Data reduction#^576682|sufficient statistic]] of the full diffusion history $(x_s^{k_s})_{s<t}$, which is unclear empirically; given the update rule $z_t = p_\theta(z_t|z_{t-1}, x_t^{k_t}, k_t)$ constitutes a "rolling update", the process is not strictly Markov in $(x_t^{k_t})_{t\leq h}$ alone, but rather satisfies a _Markov property_ in the joint space $(z_t, x_t^{k_t})_{t\ge 0}$. In any event, if this assumption holds, then the embedding allows inference and generation to be performed recursively, despite long-range dependencies in the observed trajectory.  

Put another way, since the model evolves multiple correlated diffusion chains $\{x_t^{k}\}_{k=0}^K$ along the temporal dimension, when sampling the noise from $\mathcal{K}$, the noise levels $k_t$ and $k_{t'}$ for $t \neq t'$ are not independent, as each forward transition $p^k(x_t^{k_t} \mid x_{t-1}^{k_{t-1}})$ depends on the entire sequence of previous noise levels. As a result, the conditional $p_\theta(z_t \mid z_{t-1}, x_1^{k_1}, \ldots, x_t^{k_t})$ cannot be defined unambiguously without specifying the diffusion schedule $\{k_1, \ldots, k_t\}$. Thus, to ensure that $p_\theta$ defines a proper measure, the authors index the latent variable as $z_t(k_1, \ldots, k_t)$ to explicitly conditioning the latent trajectory on the full sequence of noise indices; a notion that is not clear when reading the main body of the paper. This indexing distinguishes between diffusion paths generated under different trajectories $q(x_1^{k_1}, \ldots, x_t^{k_t} \mid x_0)$, which otherwise would correspond to distinct probability measures on the same sample space.
