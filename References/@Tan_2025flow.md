---
title: Flow matching-based autonomous driving planning with advanced interactive behavior modeling
authors: Tianyi Tan, Yinan Zheng, Ruiming Liang, Zexu Wang, Kexin Zheng, Jinliang Zheng, Jianxiong Li, Xianyuan Zhan, Jingjing Liu
year: 2025
---
---
This paper makes a number of statements about what the authors sees as the major performance limitations of current learning based planning methods (as opposed to rule based methods); namely, architectural limitations and trajectory tokenization. Their proposed model does beat prior methods but it is unclear, from their small ablation work, if their critiques line up with model behaviours.

# Overview 
This paper presents some [[Deep neural networks|neural network]] architectural improvements for joint interaction [[Motion planning]] for autonomous driving tasks. The authors focus on imitation learning (or behaviour cloning) without rewards, like [[@Janner_2022]] [[@Carvalho_2024]] however these two papers focus on single agent planning.

# Primary results
The authors exclusively use the nuPlan (https://github.com/motional/nuplan-devkit) dataset with closed-loop evaluation for training and model evaluation. Let the ego agent, the which the model is controlling, be denoted $a_{ego}$, and scene dataset items be of the form $C=\{N,L,O\}$ where $N=KNN(a)$ is the $k$-nearest neighbours surrounding the agent at time $t=0$, $L=\{(p_{i_j})_{j=1}^{M_j}\}_{j=1}^N$ is the set uniformly spaced points on the lane-lines of the road, and $O=\{o_i\}_{i=1}^B$ is a set of point representing static obstacles in the scene. First $C$ is padded with the past $T$ observations (2sec) and are (each) rotated and centred around $a$, $C_a=T(C)$, at time $t=0$ (first frame). The scene features are then encoded using [[Perceptrons||MLPs]] as follows:

The authors propose a transformer based (stacked decoder layers) with adaptive layer norms and distance annealed attention weights, trained as a [[Flow-matching generative models]]. In particular, given a scene 


## Empirical results 


![[Pasted image 20251203111254.png]]