---
title: "Fast monte carlo tree diffusion: 100x speedup via parallel and sparse planning"
authors: Jaesik Yoon, Hyeonseo Cho, Yoshua Bengio, Sungjin Ahn
year: 2025
tags:
  - diffusion
  - motion_planning
  - monte_carlo
  - search_algorithm
references:
  - https://arxiv.org/abs/2506.09498
  - https://arxiv.org/abs/2502.07202
---

---

This note treats the two papers (linked above) as a singular paper, as it is necessary to read both to understand the materials. 

# Overview
Existing diffusion trajectory generation methods, e.g., [[@Janner_2022]] [[@Carvalho_2024]], apply model predicted control by sampling multiple candidate trajectories in parallel and pruning these based on selection (or trained critic) criteria. These methods accrue high computational expense when the probability of a sample begin accepted is low since the entire candidate trajectory need to be diffused (generated) before it is evaluated.

The authors propose a method of breaking up trajectory generation into sub-segments which are composed into a [[Monte Carlo simulation|Monte Carlo]] tree search algorithm to control the exploration exploitation trade off of a trajectory and enable speculative reward computation for partially diffused trajectories (or coarsely diffused later stages of the trajectory). This method reduces the computational expense of generating (entire) trajectories using diffusion in a model predictive control loop compared to contemporary methods. 

# Primary results
The authors build off the method proposed in [[@Chen_2025diffusion]] incorporating the control-as-inference diffusion trajectory formulation used in [[@Janner_2022]]; that is, let $\mathcal{X}$ be a scene (data domain) and suppose trajectories, of finite time horizon $h$, are of the form $\tau = ((s_i,a_i))_{i=0}^h$ where $s_i\in \mathcal{X}$ encodes the state information and $a_i$ the action need to move from state $s_{i}$ to $s_{i+1}$, $D=\{\tau_j\}_{j=0}^N$ be a dataset of trajectories, $(\beta_{k})_{k=1}^K$ be a noise schedule and $\mathcal{K}$ be a diffusion forcing noise index matrix, from [[@Chen_2025diffusion]], for varying the noise schedule over the trajectory -- that is for a given trajectory waypoint its noise is set as $\beta_{k_\mathcal{K}[i,j]}$.

The paper mentions parameterizing the model output using classifier free guidance, see (https://github.com/JiaqingNie/classifier-free-guidance-on-DDPM), but you can just as well use a classifier as in [[@Chen_2025diffusion]] and a environmental reward function used during inference; i.e., if the model is parameterized for noise prediction $\epsilon_\theta(\tau_i^{k_i},k_i)$ this means the output is of the from  $$\epsilon_\theta(x_i^{k_i}, k_i, \lambda, y)=(1-\lambda)\epsilon_\theta(x_i^{k_i}, k_i)-\lambda\epsilon_\theta(x_i^{k_i}, k_i, y)$$for $\lambda\geq 0$ (in practice this is not restricted to unit interval) with class label $y\in \mathcal{Y}$ encoding end goal information, and (differentiable) reward (or many return) function $r(\tau_i):\mathcal{X}\to \mathbb{R}_{\geq 0}$.

## Method
Given a pre-trained model $\epsilon_\theta$ trained using the procedure [[@Chen_2025diffusion#^ac4f92|diffusion forcing]] for causal sequences and a planning horizon $h$, to apply Monte Carlo tree search to trajectories the authors break up the trajectory and add dynamic guidance scheduling to sub-trajectory searches.

In particular, given a noisy trajectory $\tau^K\sim \mathcal{N}(0,I)$, it is partitioned (disjoint) into $s$ sub-trajectories $\tau=[\tau_0^K|\tau_2^K|,\dots,|\tau_{s-1}^K]$ and compoased with a guidance scale vector $g=[\lambda_0,\lambda_1,\dots,\lambda_{s-1}]$, where for simplicity of formation assume $\lambda_i\in \{0,1\}$, to create the "meta action" trajectory $\hat{\tau}^K = [(\tau_0^K, \lambda_0)|(\tau_1^K, \lambda_1)|\dots|(\tau_{s-1}^K,\lambda_{s-1})]$.  

Now, beginning with $\hat{\tau}_0^K$ build a search tree $T$ with root node $n_0=\hat{\tau}^K$. Then given parameter $\rho>0$, you create $\rho$ many candidate samples of $\hat{\tau}^K$ as children; that is, $$n_1 = \{n_{1,i} = Euler(\epsilon_\theta(\hat{\tau}^K_0,K),M)_i\}_{i=1}^\rho$$where $M$ is the number of sampling steps (e.g., $K$), where during sampling $\lambda_i$ is used to control whether guidance is used or not -- either encouraging exploration or exploitation in parts of the scene. Then, in order to evaluate the candidacy of a node $n_{1,i}\in n_1$ the remainder of its trajectory is coarsely integrated to get a full solve; for each $n_{1,i}\in n_1$, $$\tau(n_{1,i}) = [n_{1,i}|Euler(\epsilon_\theta([\hat{\tau}_{i+1}^K,\dots,\hat{\tau}_{s-1}^K],K),N)],$$with $N<<M$ many steps, and the reward(s) $r(\tau(n_{1,i}))$ is computed and used to update the [[Reinforcement learning]] upper confidence bound associated with the node Q-value and upper confidence bound associated with the node:
$$\begin{cases}&N(n_{1,i}) = N(n_{1,i})+1,\\ &Q(n_{1,i})=Q(n_{1,i})+\frac{r(\tau(n_{1,i}))-Q(n_{1,i})}{N(n_{1,i})},\\ &U(n_{1,i})=Q(n_{1,i})+c\sqrt{\frac{\ln N(n_{0})}{N(n_{1,i})}}\end{cases}$$
where $c\geq 0$ controls the exploration-expoitation trade-off in selecting nodes.  The node with the largest $U(n)$ is then selected as the new root node, $$n_{1,*} = \arg\max_{n_{1,i}\in n_1}U(n_{1,i})$$via greedy policy selection. The reward siginal is propagated up the tree (backpropagation) to modify the values of $g$ dynamically to better reach the goal;
$$\lambda_i \leftarrow \lambda_i + \eta_\lambda (r(\tau(n_{1,*})) - Q(n_0))$$
where $\eta_\lambda > 0$ is the guidance learning rate. This adaptive mechanism increases $\lambda_i$ (encouraging exploitation) for sub-trajectory segments when the goal conditioned model performs well and leads to high rewards and decreases it when rewards are below average, dynamically balancing exploration and exploitation at both the tree search level and the diffusion sampling level throughout the search process.

This process continues until the entire trajectory is denoised completely, following $s$ node selection steps. 

Here is a figure of the process of denoising the trajectory sub-components.
![[Screenshot From 2025-11-06 14-46-58.png|500]]

Arithmetically, the above procedure can be written out as: [TODO]

## Accelerating the method
In the follow up work the authors propose using a method of paralleling node child expansion and pruning using delayed synchronised updated to the upper confidence bounds and distilling their trained model to sample better using few step diffusion generation.

# Empirical results
The authors evaluate their method on both 2D planning tasks and some computer vision conditioned robotic arm object manipulation tasks. 

![[Screenshot From 2025-11-07 17-48-41.png]]

It is worth noting, the authors do not compare their method using NFE rather the success rate on a task; however, it is unclear what exactly the common limit of sampling is -- presumably the authors allow a finite number of samples to be drawn from each method and time the evaluation. The authors should have fixed the NFE allowed (or time) and allowed more samples from competing methods, or timed how long it took to draw a acceptable sample and averaged this.

# Issues
The authors do not mention if they are encoding a hidden state (such as in [[@Chen_2025diffusion]]) or if they assume the model has latent variables sufficient for this propose. 

There are a number of viable artefacts in the generated trajectories (doubling back on paths) from this method; the authors should have ablated applying a smoothness penalty to the trajectories which would have better aligned this method with the competing works trying to reduce sampling time of planning methods by constraining the diffusion models during sampling (and training) e.g., [[@Lou_2023]], etc.