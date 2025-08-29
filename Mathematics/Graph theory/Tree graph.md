**Definition: (Tree)** A connected graph with no cycles is called a tree.

**Definition: (Spanning tree)** Let $G$ be a graph. A _spanning tree_ of $G$ is a [[Elementary graphs#^5ff823|spanning subgraph]] of $G$ that is a tree.

**Definition: (Forest)** A graph with no cycles is a forest; that is, each component of the graph is a tree.

The idea of how similar a graph is to a tree is useful for comparing different problems in computer science, especially with regards to difficulty. Thus, the measure of _treewidth_ was created which makes use of _tree decompositions_.

**Definition: (Tree-decomposition)** Let $G=(V,E)$ be a graph. A _tree-decomposition_, see [[Graph products#^c23c30|decomposition]], of $G$ is an ordered pair $(T,\mathcal{T})$, where $T$ is (hyper-forest) tree and $\mathcal{T}=\{T_v:v\in V\}$ is a family of subtrees of $T$ such that $T_u\cap T_v\neq \emptyset$ if (but not necessarily only if) $uv\in E$, [[@Bondy_2008]]. Alternatively, a _tree-decomposition_ of $G$ is an ordered pair $(T,\mathcal{V})$, where $T$ is hyper-tree on the elements of $\mathcal{V}$ which is a family of subsets of elements from $V, that satisfies:
 1) $\bigcup_{V_i\in\mathcal{V}} V_i = V$;
 2) Each $e\in E$ is included in at least one of the subgraphs of $G$ induced by $V_i$; 
 3) For all $v\in V$, the subtree (sub-hyper-tree) $T_v$ of $T$, which has vertex set $\{V_i\in \mathcal{V} \mid v\in V_i\}$, is connected.
Properties (2) and (3) establish that vertices are adjacent in $T$ only when the corresponding subtrees have a vertex in common.

Equivalently, $(T,\mathcal{T})$ is a tree-decomposition of a simple graph $G$ if and only if $G$ is a [[Elementary graphs#^5ff823|spanning subgraph]] of the [[Chordal graph]] with tree representation $(T,\mathcal{T})$.

Every simple graph $G$ has a trivial tree-decomposition $(T,\mathcal{T})$, where $\mathcal{T}$ is an arbitrary tree and $T_v=T$ for all $v\in V$. Each graph admits many possible tree-decompositions.

**Definition: (Width of tree-decomposition)** The _width_ of a tree-decomposition $(T,\mathcal{V})$ of a graph $G$ is $$\max_{V_i\in\mathcal{V}}\{|V_i|-1\}.$$

**Definition: (Treewidth of a graph)** The _treewidth_ of a graph $G$, denoted $tw(G)$, is the minimum width among all its possible tree-decompositions of $G$; that is, if $\mathcal{T}(G)$ is the set of all possible tree-decompositions of $G$ then $$tw(G) = \min_{(T,\mathcal{V})\in \mathcal{T}(G)}\max_{V_i\in\mathcal{V}}\{|V_i|-1\}.$$