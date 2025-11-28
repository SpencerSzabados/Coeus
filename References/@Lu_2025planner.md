---
title: What makes a good diffusion planner for decision making?
authors: Haofei Lu, Dongqi Han, Yifei Shen, Dongsheng Li
year: 2025
tags:
  - diffusion
  - motion_planning
  - empirical_work
  - robotics
  - reinforcement_learning
references:
  - https://openreview.net/pdf?id=7BQkXXM8Fy
---

---

In this work the authors perform an empirical study over a bunch of different diffusion model architectures and training/sampling algorithms to try and determine what "general" design choices have the largest effects on boosting performance on long time horizon planning tasks. 

The authors focus on offline RL training, as used in works like [[@Jain_2024]], and the two classes of model: diffusion policy models and diffusion planning (trajectory) models [[@Janner_2022]]. In the study the authors distinguish these by stating diffusion policy models only predict the next action (or action state pair) without using look ahead planning; however, I don't believe this correctly characterizes all diffusion policy methods. 

# Primary results
The authors utilize the D4RL dataset (https://github.com/Farama-Foundation/D4RL) that contains dataset elements of the form $\tau_{t,t+1} = (s_t, a_t, s_{t+1}, r_t)$ with states $s_t$, actions $a_t$, and rewards $r_t$. Returns are computed over a trajectory (or sub-trajectory) using standard discounted rewards $R_t = \sum_{i=1}^h \gamma^ir_{t+i}$ for time horizon $h>0$.

After ablating the model features (joint action-state prediction, separate models for predicting first the state and then using "inverse dynamics" to reconstruct the actions, U-Net vs Transformer based diffusion backbone architecture, policy based predicting vis entire trajectory planning) the authors propose the following (general) approach for training and model sampling that yielded the best performance. 

**Method:** Parameterize the planner utilizing two sub-networks, $\epsilon_\theta$ and $\epsilon_{\phi}$, implemented using a (diffusion) transformer backbone (with [[Layer attention]]). The network $\epsilon_\theta:\mathcal{S}\to \mathcal{S}^{h/k}$ is conditioned on the initial observation and predicts a subset of the trajectory states $(s_{i})_{i=tk}^{(h-1)k}$ with some step size $k>0$, tuned as a hyperparamter for the dataset; while $\epsilon_\phi:\mathcal{S}^{h/k}\to \mathcal{A}^{h/k}$ is trained to perform "inverse dynamics" given the predicted states recovers the actions leading to these states. The final output is then the integral of these actions.

This is summarized in the following training algorithm outline. Based on the paper it is not clear if the steps listed are performed jointly or if it is recommended to train each component in isolation sequentially. 

```pseudo
\begin{algorithm}
\caption{Diffusion separate states inverse actions}
\begin{algorithmic}
\Input Let $D$ be a dataset of trajectories, $\{t_i\}_{i=1}^N$ be a discretization of the time horizon $h>0$, $k>0$ be a step size, $r:\mathcal{S}\to \mathbb{R}_{\geq 0}$ a state reward function, $\gamma>0$ a discount factor, $\epsilon_\theta$ a  diffusion model (noise prediction), $\epsilon_\phi$ the invserve dynamics model, and $V_\phi$ a (value function) critic network.
\Output Trained models $\epsilon_\theta$, $\epsilon_\psi$, $V_\phi$.
    \State Sample $\{(s_i,a_i)\}_{i=t+jk}^{(h-1)k}\sim D$ 
    \State Compute $\{R_i\}_{=t+jk}^{(h-1)k}$, where $R_i = \sum_{j=0}^h\gamma^j r_{i+j}$\Comment{Matching dense returns.}
    \State Train planner $\epsilon_\theta$ conditioning on $s_t$ and target $(s_i)_{i=t+jk}^{(h-1)k}$.
    \State Train aciton model $\epsilon_\psi$ conditioning on $s_t,s_{t+k}$ and target $a_t$
    \State Train critic $V_\phi$ conditioning on $(s_i)_{i=t+jk}^{(h-1)k}$ and target $R_t$
    \Return $\epsilon_\theta$, $\epsilon_\psi$, $V_\phi$.
\end{algorithmic}
\end{algorithm}
```

The proposed sampling proceedure is based the observation that [[Monte Carlo simulation]] (accept-reject) based sampling performs better (on the whole) than the direct gradient guidance methods tested; however, this recommendation ignores the incurred computational cost of the additional samples.

```pseudo
\begin{algorithm}
\caption{Sampling proceedure}
\begin{algorithmic}
\Input Let $\epsilon_\theta$ be a trained diffusion planner, $\epsilon_\phi$ the invserve dynamics model, and $V_\phi$ a (value function) critic network.
\Output Trained models $\epsilon_\theta$, $\epsilon_\psi$, $V_\phi$.
    \State Sample $\{\tau_i\}_{i=1}^N\sim \epsilon_\theta$
    \State Select $\tau^* \in \arg\max_{\tau \in \{\tau_i\}_{i=1}^N} V_\phi(\tau)$
    \State Sample $\{a_t\}_{t=1}^h\sim \epsilon_\psi(\tau^*)$
    \Return $\hat{\tau} = Solve(s_1, \{a_t\}_{t=1}^h)$
\end{algorithmic}
\end{algorithm}
```


# Issues and questions 
From the paper the training methodology for the inverse dynamics model does not make sense as you don't have a ground truth for $a_t$ corresponding to the state transition $f(s_t,a_t)=s_{t+k}$ but only $f(s_t,a_t)=s_{t+1}$; the authors must either mean $\epsilon_\psi(s_t,s_{t+k})=(a_t,\dots, a_{t+k-1})$ where the dense actions are predicted or the actions are auto-regressively predicted with $\epsilon_\psi(s_t,s_{t+k})=a_t$ then $s_{t+1}=Solve(s_t,a_t)$ and then you predict $\epsilon_\phi(s_{t+1},s_{t+k})=a_{t+1}$ etc.

I'm confused how this training methodology, for separating the models, differs from getting $\epsilon_\theta$ to jointly predict $(\hat{s}_t,\hat{a}_t)$ with a dynamics based model loss of the form $\mathcal{L} = \frac{1}{2}\|(s_1,\dots,s_h)-(\hat{s}_1,\dots,\hat{s}_h)\|+\frac{1}{2}\|(s_1,\dots,s_h)-Solve(s_1,\{\hat{a}_i\}_{i=1}^h)\|$ which just reduces to state prediction.

While reading this paper I had the thought of training a diffusion planner $\epsilon_\theta:\mathcal{S}^{(h-1)k}\times \{0,1\}\to \mathcal{S}^{(h-1)k}\times \mathcal{A}^{h}$ that regressively predicts the states then recovers the actions; first sampling $\tau=\{(s_i,a_i)\}_{i=t+jk}^{(h-1)}$, then set $\tau_1 = (1,0,\dots,0)^\intercal \tau$ and generate the sample $\epsilon_\theta(\tau_1, 0)=\{(\hat{s}_i),0\}_{i=t+jk}^{(h-1)k}=\hat{\tau}_s$ and then regressing to predict $\epsilon_\theta(\hat{\tau}_s,1)=\{(\hat{s}_i,\hat{a}_i)\}_{i=1}^h$ back propagating the loss $\mathcal{L}=\|(a_1,a_2,\dots,a_h)-(\hat{a}_1,\hat{a}_2,\dots,\hat{a}_h)\|$. However, If the model is performing $M>1$ diffusion steps it is not clear how to back propagate this loss efficiently other than caching the entire trajectory. One idea, is perhaps to pre-train $\epsilon_\theta$ to just predict the states and parameterize it to predict $x_0$, then I can sample the states from a one step sampling and efficiently compute the loss -- provided the $x_0$ predictions is sufficiently good (e.g., near perfect) it should be possible to then begin training the inverse action function. Similarly, I could fit the model with two heads (shared hidden state) one to predict the states and the other predicting the actions. After training of the model with one step $x_0$ predictions, I can run some multi-step fine tuning. 