---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - computational_geometry
---
___

Graph burning is a simplified model for how influence spreads on a network, and relates to graph searching problems (information retrieval). Associated with the process is the rate of spread between nodes, called the _burning number_ of the graph, which is equal to the (optimal) minimum number of steps needed for the entire graph to be burned. The smaller the burning number, the faster the influence in the network is spread. 

# Overview
Much of the following is taken from [[@Bonato_2021]].

**Problem statement: (Graph burning)** Given a (simple) graph $G=(V,E)$ with finitely many edges. Starting at a chosen vertex begin burning the graph by expanding the set of burned vertices by the neighbouring elements of each burned vertex each step, and by choosing a new vertex to burn. The problem is then to determine a sequence of vertices $(v_1,v_2,\dots,v_n)$ that requires the fewest number of steps to burn all vertices of $G$. 

**Theorem: (Tree partitioning)** Burning a graph $G$ in $k$ steps is equivalent to finding a rooted tree partition of $G$ into $k$ trees $T_1,\dots,T_k$ with heights at most $k-1,k-2,\dots,0$ respectively, where for every $1\leq i,j\leq k$ the distance between roots of $T_i$ and $T_j$ is at least $|i-j|$.

**Corollary: (Tree reduction)** For a graph $G$ $$b(G) = \min\{b(T)\mid T\text{ if a spanning subtree of }G\}.$$
The above corollary ratifies the intuition that paths are central to the burning number of a graph. In particular,

**Corollary: (Path burning)** A path $P_n$ on $n$ vertices has $b(P_n)=\lceil \sqrt{n}\rceil$.

**Theorem: (Diameter radius)** For any graph $G=(V,E)$ with radius $r$ and diameter $d$, $\lceil \sqrt(d+1)\rceil\leq b(G)\leq r+1$.

**Conjecture: (Burning number conjecture)** For any connected graph $G=(V,E)$ we have $$b(G)\leq \sqrt{|V|}.$$No proof of this conjecture is currently known for general graphs (proofs for select graph categories are known). The best known (proven) upper-bound, as of [2016], is $$b(G)\leq \left\lceil\frac{\sqrt{24|V|+33}-3}{4}\right\rceil.$$

# Hardness 
The graph burning problem of computing a optimal burning sequence (burning number) is $NP-Complete$.

A graph decision problem is $APX-hard$; meaning, given a graph $G$ and a number $k$ determining if $b(G)\leq k$ is $NP-hard$ to compute exactly, but admits a constant factor approximation algorithm.

Moreover, the problem of computing the optimal burning sequence for a given graph and its optimal burning sources remains $NP-hard$.

# Special cases of graph burning 

## Path burning
The problem of path burning can be reframed into the following decision problem. 

**Problems statement:** Given a path $P_n$ and a set $\{c_1,c_2,\dots,c_k\}$ of circles of radii $1$-to-$k$ respectively, does there exist a arrangement of these circles along $P_n$ that encircle all vertices without overlap? If yes, then $b(P_n)=k$; otherwise, if there is overlap $b(P_n)<k$. On the other hand, if the number of circles is not sufficient to cover all the points then $b(P_n)>k$.

## Tree burning


## Caterpillar graphs
**Definition: (Caterpillar graph)** A caterpillar graph (or caterpillar tree) is a tree in which all vertices are within distance one of a central path; In other words, a caterpillar is a tree in which removal of all leaf vertices results in a path which is called the _spine_ of the caterpillar.

**Definition: (p-Caterpillar graph)**

## Spider graphs 
**Definition: (Spider graph)** A _Spider graph_ with $n$ nodes is a tree $S_n=(V,E)$ with exactly one vertex $v\in V$ with $deg(v)\geq 3$ with $\Delta(V\backslash v,E\backslash N(v)) \leq 2$; that is, only one vertex has degree at least three with all others having degree at most two. 

For a spider graph $S_n$ with radius $r$ has burning number $b(S_n)=r+1$. The burning sequence for a spider graph begins with its head, and then can proceed in any fashion without alteration. These results follow directly from an above theorem.


## Cactus graphs

### Necklace graphs


# Point burning in the plane
A new [2022] variation of the problem of graph burning that considers a configuration of points to be burned in the plane opposed to a graph.