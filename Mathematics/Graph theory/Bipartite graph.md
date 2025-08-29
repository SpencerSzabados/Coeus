
**Definition: (Bipartite graph)** A graph $G=(V,E)$ is bipartite if there exists a [[Graph operations#^e93b09|partition]] of $V$, say $(A,B)$, such that ever edge $ab\in E$ has exactly one end in $A$ and the other in $B$.

**Definition: (Complete bipartite graph)** For each $m,n\in \mathbb{N}$, the complete bipartite graph $K_{m,n}$ is the bipartite graph with vertex set $V=\{u_1,\dots,u_m,v_1,\dots,v_n\}$ and maximal edges set $E=\{u_iv_j\mid i\in \{1,\dots,m\}, j\in \{1,\dots,n\}\}.$  

**Theorem: (Odd cycle)** A graph is bipartite if and only if it does not contain an odd length cycle.

**Theorem:** If $G=(V,E)$ is a [[Planar graph|planar]] bipartite graph, then $$|E|\leq 2|V|-4.$$
