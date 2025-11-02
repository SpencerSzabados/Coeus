---
doc type: Note
authors: Spencer Szabados
date: 2025-10-21
tags:
  - graphical_models
  - graph
  - neural_networks
references:
  - https://sassafras13.github.io/GNN/
  - https://distill.pub/2021/gnn-intro/
---
---

[[Elementary graphs#^1b6b29|Graph]] [[Artificial neural networks]] are a network capable of operating on relational data (nodes and edge connections) rather than grids, unlike [[Convolutional neural networks]], and are in principle invariant to the order of the data. These networks offer computational advantages over (standard) MLPs and CNNs for sparse data.

In the context of GNN nodes, of the data, are often considered to be some concatenation of feature embedding with the edges representing some relational information; thus, GNNs consist of some underlying machinery for dealing with the embedding of each graph attribute and some upper level method for aggregation of these features.

# Overview 
Consider the following setup, let $G=(V,E)$ be a instance of a graph and $U(G)$ represent some global (summary) attributes of $G$ (e.g., number of nodes, longest paths, etc..) with $V\subseteq \mathbb{R}^d$ and $E\subseteq \{0,1\}^{|V|}\times \mathbb{R}^m$; that is, we have some features in $\mathbb{R}^d$ and some one-hot encoded edge connections with additional attributes in $\mathbb{R}^m$. Then we can construct a GNN by constructing a network block $b_\theta(G):\mathcal{G}\to \mathcal{G}$ that applies transformations to each component independently like $$b_\theta(G) = [g_\theta(V)\mid  f_\theta(E)\mid h_\theta(U)],$$with independent network parameters, the output of which is then passed to aggregation layers, which should be permutation invariant, of the general form  
  
