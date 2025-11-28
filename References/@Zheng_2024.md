---
title: Trajectory consistency distillation
authors: Jianbin Zheng, Minghui Hu, Zhongyi Fan, Chaoyue Wang, Changxing Ding, Dacheng Tao, Tat-Jen Cham
year: 2024
tags:
  - machine_learning
  - diffusion
  - generative_models
references:
  - "[[@Song_2023]]"
  - https://arxiv.org/abs/2402.19159
resource: unpublished
---
---

This paper seeks to improve the Consistency Distillation method proposed by [[@Song_2023]] by altering the boundary and self consistency condition to admit successive model evaluations -- a technique that was used in the insighting paper but not fully justified in its application. It is experimentally demonstrated, along with some approximation results, that the development method outperforms its contemporary.

The authors experimentally, and numerically, examine what steps in the CM distillation/sampling accumulate the most numerical error and frame their method in terms of addressing these sources of error; namely, targeting error from 1) Estimation errors in score prediction; 2) Distillation errors in CM training; 3) Discretization errors accumulated during repeat sampling due to trajectory misalignment. 
[[@Wang_2024]] 

# Primary results
Begin by considering a common diffusion equations used. Let $p_0(x)$ denote the data distribution, $\mu$ and $\sigma$ be smooth scalar functions, and consider the [[Diffusion processes]] over $T>0$, $t\in[0,T]$ defined by the [[Stochastic differential equations]] $$dx_t = \mu(x_t,t)dt+\sigma(t)d\overrightarrow{W}_t;$$
where the authors, unlike [[@Song_2023]], pick for the main body the VP-SDE parameters $$\mu(x_t,t)=\frac{dlog\alpha_t}{dt}\quad\text{ and }\quad \sigma(t)=\sqrt{\frac{ds^2_t}{dt}-2s^2_t\frac{dlog\alpha_t}{dt}}$$giving the forward transition kernel $$q_t(x_t|x_0)=\mathcal{N}(x_t; \alpha_tx_0, s^2_t\mathbb{I})$$ which has limiting distribution $\pi_T=\mathcal{N}(0,\mathbb{I})$. 

Now, we will define multi-step consistency sampling, which is where the output of a consistency models is re-sampled using the consistency model in an attempt to further refine the output; that is, we evaluate the algorithm 
```pseudo
\begin{algorithm}
\caption{Multi-step Consistency Sampling}
\begin{algorithmic}
\Input Let ,$\{t_i\}_{i=1}^N$ be a discretization of the time horizon from $T$ to $\epsilon$, and $f_\phi$ a pre-trained diffusion model (with score estimator $s_\phi$).
\Output Sample $\hat{x}_0^{(N)}$.
    \State Sample $z\sim \mathcal{N}(0, \mathbb{I})$\Comment{ Init. sample. }
    \State Sample $\hat{x}_0^{(0)}\gets f_\phi(z, T)$
    \For{$i = 1,\dots,N$}
        \State Sample $z\sim\mathcal{N}(0,\mathbb{I}])$
        \State Sample $x_{t_i}\gets \alpha_{t_i}\hat{x}_0^{(i-1)}+s_{t_i}z$\Comment{Forward SDE.}
        \State Sample $\hat{x}_0^{(i)}\gets f_\phi(x_{t_i}, t_i)$
    \EndFor
\end{algorithmic}
\end{algorithm}
```

The authors then give two results to motivate both the importance of using multi-step consistency sampling to reduce total variation error and a numerical bound on the error accumulated from applying it to consistency models -- this leading to the authors contribution of reducing said error via alteration of the boundary and consistency condition during training.

**Theorem:** Given a trained CM model $f_\theta$ and $\{t_i\}_{i=1}^N$ a discretization sequence of the time horizon from $T$ to $\epsilon$ for performing multi-step sampling, noting via the [[Push-forwards models|push-forward]] $\hat{x}_0^{(i)}\sim q_\theta^{(i)} = {f_\theta}_\sharp \mathcal{N}(\alpha_{t_i}\hat{x}_0^{(i-1)}, s_{t_i}\mathbb{I})$, the [[Information theory#^7edae7|total variation]] between the target and model is $$\delta(q_\theta^{(i)},p_0) \in O(2^{-i}T(\epsilon_{CD}+\epsilon_{SE}L)),$$where $\epsilon_{CD}$, $\epsilon_{SE}$, and $L$ are respectively the consistency distillation error, score matching error, and model Lipschitz constant.
 
The borrowing from another paper, the authors get that the total accumulated between sampling steps is bounded by $$\delta(q_\theta^{(i)},p_i)\in O(\sqrt{t_i}).$$

To reduce this error the authors define the following condition used in distillation in place of the previous consistency condition of Song.

**Definition: (Trajectory consistency function)** Given an [[Ordinary differential equations|ODE]] of the form $$dx_t = g(x_t,t)dt$$where $g:\mathbb{R}^d\times [0,T]$  is Lipschitz in $x$, and a sequence of points $(x_t)_{t=\epsilon}^T$ that lie along a single ODE trajectory $\tau(x_0,t)$, then a function $f:\tau(x_0,t)\to \tau(x_0,t)$, with imposed boundary condition $f(x_t,\epsilon)=x_\epsilon$ for any $0<\epsilon\leq t$, is said to be _consistent_ if $$f(x_t,\epsilon)=f(x_{t'}, \epsilon)$$for all $0<\epsilon\leq t, t' \leq T$. 

Thus, ensuring any point can be mapped to any other point closer to the origin of the trajectory conditioning the network to both do one sample inference and to be well defined for multi-step sampling.

The authors chose to parameterize the model in terms of of exponential integrator to try and remove the stiffening from the sampling PF-ODE; namely, $$f_\theta(x_t,\epsilon) = \frac{s_\epsilon}{s_t}x_t + s_\epsilon\int_{\omega_t}^{\omega_\epsilon}e^\lambda F_\theta(x_\omega, \omega)d\omega$$where $\omega_t)=\log(\alpha_t/s_t)$ and $F_\theta$ is a trainable network; this is then evaluated using a computational molecule estimate of the integral.

The authors do not specify what the network $F_\theta$ is predicting, but based on form of the equation it is the score -- likely parameterised in terms of the noise estimate.

The authors only focus on distillation training, not self consistency, and present a version of the following training algorithm in the appendix.

```pseudo
\begin{algorithm}
\caption{Consistency Distillation}
\begin{algorithmic}
\Input Let $D$ be the dataset, $\{t_i\}_{i=1}^N$ be a discretization of the time horizon, $\eta$ the learning rate, $\delta$ the loss tolerance, $\mu$ the EMA decay rate, $f_\phi$ a pre-trained diffusion model (with score $s_\phi$) and $f_\theta$ be the initialised student model.
\Output Trained diffusion model $f_\theta$.

    \While{$L > \delta$}
        \State Sample $x\sim D$
        \State Sample $i,k\sim \mathcal{U}\{2,\dots,N\}$\Comment{ Take $k<i$.}
        \State Sample $j\sim \mathcal{U}\{1,i\}$
        \State Sample $x_{t_k}\sim \mathcal{N}(\alpha_{t_i}x_,s^2_{i}\mathbb{I})$\Comment{Forward SDE.}
        \State $\hat{x}_{t_i} \gets \text{Solver}(f_\phi(x_{t_k}, t_i))$\Comment{ Int. steps. }
        \State $L \gets \lambda(t_{i-1})d(f_\theta(x_{t_k},t_j),f_{\overline{\theta}}(\hat{x}_{t_i},t_j))$
        \State $\theta \gets \theta - \eta\nabla_\theta L$
        \State $\overline{\theta}\gets \text{stopgrad}(\mu\overline{\theta}+(1-\mu)\theta)$
    \EndWhile
\end{algorithmic}
\end{algorithm}
```

The author go on to define a stochastic re-sampling method for selecting noise variance/schedule values during multi-step sampling.

# Issues
I note there is an error on p3 of this paper where the authors conflate the consistency condition with the boundary condition. 


