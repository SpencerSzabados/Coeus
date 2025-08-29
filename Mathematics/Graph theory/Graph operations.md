**Definition: (Vertex deletion)** Let $G=(V,E)$ be a graph. If $v\in V$, then $G\backslash \{v\}$ is the graph with vertex set $V\backslash \{v\}$ and edge set $E=\{e\in E\mid v\not\in e\}$.

**Definition: (Graph partition)** A partition (or more specifically a vertex partition) of a graph $G=(V,E)$ is a family $\mathcal{V}$ of subsets that partition $V$, and [[Elementary graphs#^ac3e89|induce subgraphs]] that need not be connected; that is, edge properties need not be preserved. ^e93b09

**Definition: (Cut set)** Let $G=(V,E)$ be a connected graph and let $w\subseteq V$. If $G\backslash w=G[V\backslash w]$ is disconnected then $w$ is called a _vertex cut set_.

**Theorem: (Menger's)** Let $G=(V,E)$ be a connected graph and let $u,v\in V$ such that $uv\not\in E$, then the maximal number of pairwise internally disjoint $uv$-paths equals the size of the smallest cutset $S$ that separate $u$ and $v$ into different components in $G\backslash S$.

**Definition: (Edge contraction)** Given a graph $G$ and an edge $e=xy$, a graph $G_e$ is said to be obtained from $G$ by _contracting the edge $e$_ (identifying the vertices $x$ and $y$ with each other) if $G_e$ is isomorphic to the graph obtained by joining $x$ to any neighbor of $y$ not already adjacent to $x$ in the graph $G\backslash \{y\}$.

**Definition: (Minor)** A graph $H$ is called a _minor_ of a graph $G$ if $H$ is isomorphic to a graph obtained from $G$ by a sequence of edge contractions, edge deletions, or vertex deletions.

Graph subdivisions are minors of the child graph. The complete graph $K_j$ is a _minor_ of a graph $G$, if $G$ contains $j$ vertex disjoint connected subgraphs between every two of which is a connecting edge.

**Definition: (Graph decomposition)** A _decomposition_ of a graph $G=(V,E)$ is a family $\mathcal{F}$ of edge-disjoint subgraphs of $G$ such that $$\bigcup_{F\in\mathcal{F}}E(F)=E.$$
If a decomposition of a graph consists entirely of cycles (or any other singular graph class) the decomposition is called a _cycle-decomposition_.  ^c23c30

**Definition: (H-decomposition)** An $H$-decomposition of a graph $G$ is a decomposition $\mathcal{F}$ such that each subgraph $F\in\mathcal{F}$ is isomorphic to a graph $H$.
