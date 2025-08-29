
A planar embedding of a graph divides the plane into regions called _faces_; the infinite region is called the _outer face_. Each face, excluding the outer face, is bounded by the vertices and edges of the graph. The _degree_ of a face $f$ is the number of edges traversed along the bounding walk, denoted $deg(f)$; segments the protrude into a face are counted twice along this walk.

**Theorem:** If $G=(V,E)$ is a planar graph with $|V|\geq 3$ then $$|E|\leq 3|V|-6.$$

**Theorem: (Kuratowski's)** A graph is planar if and only if it does not contain a subdivision of $K_5$ or $K_{3,3}$.