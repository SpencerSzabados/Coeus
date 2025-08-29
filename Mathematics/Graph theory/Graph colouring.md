**Definition: (k-colouring)** Let $G=(V,E)$ be a graph and let $k\in\mathbb{N}$. A $k$-colouring of $G$ is a function $C:V\to \{1,\dots,k\}$ such that for all $uv\in E$, $c(u)\neq c(v)$. 

**Definition: (Colour class)** Let $G=(V,E)$ be a graph and $C:V\to \{1,\dots,k\}$ a $k$-colouring of $G$. A set $S_j=\{v\in V \mid c(v)=j\}$ is called a _colour class_ of $G$ under $C$.

Colour classes [[Elementary graphs#^ac3e89|induce]] subgraphs with no edges; i.e., they are independent sets.

**Definition: (Chromatic number of a graph)** The _chromatic number_ of a graph $G$, denoted $\chi(G)$, is the minimum value of $k\geq 0$ such that $G$ is $k$-colourable. One can also consider colouring the edges of $G$, opposed to colouring vertices, such that no vertex has two edges of the same colour adjacent to it; the minimum $k$-edge-colouring is denoted $\chi_e(G)$. Furthermore, we can consider the problem of simultaneously colouring the vertices and edges of a graph, with the joining restriction that no edge gets assigned the same colour as one of its endpoints; this is called a _total colouring_ of $G$ and the number of colours required is denoted by $\chi_T(G)$.  ^ffe8b2

**Observation: (Clique colouring)** The chromatic number of a graph $G$ is at least the size of the largest clique subgraph of $G$, denoted $\omega(G)$. [[@Molloy_2002]].

**Lemma**: For all $G$, $\chi(G)\leq \Delta(G)+1$, where $\Delta(G)$ denoted the maximum degree in $G$.

**Theorem: (Brooks')** $\chi(G)\leq \Delta(G)$ unless a component of $G$ is a clique with $\Delta(G)+1$ vertices or $\Delta(G)=2$ and $G$ contains an odd length cycle.

**Corollary:** $\Delta(G)\leq \chi_e(G)\leq \Delta(G)+1$, as $\chi_e(G)=\chi(L(G))\geq \omega(L(G))\geq \Delta(G)$ in combination with the above theorem.

**Definition: (Perfect graph)** A graph $G$ is _perfect_ if every induced subgraph $H$ of $G$ satisfies $\chi(G)=\omega(G)$; that is, every induced subgraph of $G$ has chromatic number equal to the largest clique in $G$.

**Theorem: (The strong perfect graph characterization)** A graph is perfect if and only if it contains no induced subgraph that is isomorphic to either an odd cycle of length at least $5$ or the complement of such a cycle. (p8)[[@Molloy_2002]](Theorem was proved in 2002-2006).