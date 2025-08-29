There are several different kinds of graph duality and consequently different meanings to the term "dual graph".

**Definition: (Line graph)** The edge-to-vertex dual (or line graph) of a graph $G$ is is the ordered pair $L(G)=(V,E)$, where $V=E(G)$ with edges$$E = \{e_1e_2 \mid \text{for } e_1,e_2\in E(G)\text{ there exists a } v \in V(G) \text{ s.t. }v\in e_1\text{ and } v\in e_2\},$$that is, vertices of $L(G)$ are adjacent if and only if the corresponding edges in $G$ are adjacent to a common vertex.

The [[Graph colouring#^ffe8b2|chromatic number]] of $L(G)$ is the same as the edge chromatic number of $G$; in fact, $\chi(L(G)) = \chi_e(G)\geq \omega(L(G))\geq \Delta(G)$, where the last inequality is tight unless $G$ is a graph with $\Delta(G)=2$ and contains a triangle subgraph.