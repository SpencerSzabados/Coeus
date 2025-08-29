
**Definition:(Simple graph)**

**Definition: (Walk)** If $G=(V,E)$ is a graph, a walk in $G$ is a sequence of vertices (and edges) $v_1,\dots,v_k$ such that $v_{i-1}v_i\in E$ for all $i\in \{1,\dots,k\}$.

**Definition: (Cycle)** For each integer $n\geq 3$, the cycle of length $n$ denoted $C_n$ is the graph (subgraph) such that $V=\{v_1,v_2,\dots,v_n\}$ and $E\{v_1v_2,v_2v_3,\dots,v_nv_1\}$ where $E$ contains on repeat vertices.

**Definition: (Directed graph)** A _digraph (directed graph)_ is an ordered pair $D=(N,A)$ where $N$ is a finite non-empty set of vertices and $A$ is a set of ordered pairs of elements from $N$. ^040136

**Definition: (Connected)** A graph $G=(V,E)$ is connected if there exists a walk between any two vertices. The connectivity of a graph is the maximal values of $k$ for which $G$ is $k$-connected; meaning, for any subset of vertices $S\subseteq V$ of size $k$ the graph $G\backslash S$ remains connected. The connectivity of $G$ is denoted $\mathcal{K}(G)$. 

**Definition: (Connected digraph)** A diagraph (directed graph) $D=(N,A)$ is is said to be _weakly connected_ if the graph that results from replacing all its arcs with edges is connected. A digraph is said to be _strongly connected_ if for all $u,v\in N$ there exists a directed $uv$-path and $vu$-path. ^314a8e

**Theorem: (Whitney's)** A graph $G=(V,E)$ is $k$-connected if and only if for every pair of vertices $u,v\in V$ there are $k$-pairwise internally disjoint $uv$-paths.

**Definition:(Multigraph)**

**Definition: (k-regular graph)** Let $k\in \mathbb{N}$ and let $G=(V,E)$ be a graph. A graph is $k$-regular if $deg_G(v)=k$ for all $v\in V$.

**Definition: ($k$-edge-connected)** A graph $G=(V,E)$ is a $k$-edge-connected if $G$ has no edge cut sets $S$ with $|S|< k$.

**Definition: (Induced subgraph)** Let $G=(V,E)$ be a graph, if $G'\subseteq G$ and $G'$ contains all the edges $xy\in E$ where $x,y\in V'$, then $G'$ is called an _induced subgraph of $G$_, and $V'$ is said to _induce_ (or _span_) $G'$. ^ac3e89

**Definition: (Proper subgraph)** If $H$ is a subgraph of $G$, then $H$ is called a _proper_ subgraph if $V(H)\neq V(G)$ or $E(H)\neq E(G)$.

**Definition: (Spanning subgraph)** Let $G$, $H$ be graphs, then if $H$ is a subgraph of $G$, then $H$ is a spanning subgraph of $G$ if $V(G)=V(H)$. ^5ff823

**Definition: (Graph component)** A component of a graph is a maximal connected subgraph. The number of components in a graph $G$ is denoted $\kappa(G)$; if $G$ is connected, then $\kappa(G)=1$. 

**Lemma: (Handshaking)** Let $G=(V,E)$ be a graph, then $$\sum_{u\in V(G)}deg_G(u)=2|E|.$$Moreover, if $S\subseteq V$, then $$\sum_{u\in S}deg_G(u)=2|E(G[S])|+|\partial(S)|,$$
where $G[S]$ is the subgraph that contains only vertices in $S$ and $\partial(S)$ is the number of edges 

**Definition: (Graph complement)** Let $G=(V,E)$ be a graph. The complement of $G$, denoted $\overline{G}$, is a graph such that $V(\overline{G})=V(G)$ and $uv\in E(\overline{G})$ if and only if $uv\not\in E(G)$.

