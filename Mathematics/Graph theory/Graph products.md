**Definition: (Graph join)** Let $G$ and $H$ be graphs. If $V(G)\cap V(H)=\emptyset$, then $G+H$ is the graph with vertex set $V(G)\cup V(H)$ and edge set $E(G)\cup E(H)\cup \{uv\mid u\in V(G),v\in V(H)\}$.

**Definition: (Graph cartesian product)** Let $G$ and $H$ be graphs. The cartesian product between $G$ and $H$, denoted $G\times H$, is the graph with vertex set $V(G\times H) = V(G)\times V(H)$ and edge set $E(G\times H)$ with $(u_1,v_1)(u_2,v_2)\in E(G\times H)$ if and only if $u_1=u_2$ with $v_1v_2 \in E(H)$ and $v_1=v_2$ and $u_1u_2\in E(G)$.

**Definition: (Inflated graph)** Let $G=(V,E)$ be a graph. The replacement of elements $v\in V$ by graphs $G_v$ and edges $e\in E$ by non-empty subsets of edges from along the path $G_v-G_w$ (between $v$ and $w$ in $G$), results in what is called an _Inflated graph_ denoted $IG$.  [[@Diestel_2010]]
