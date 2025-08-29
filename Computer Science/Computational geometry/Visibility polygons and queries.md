---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - computational_geometry
  - computer_vision
references:
---
---

The space considered for the following type of queries should be understood before moving further. 

**Definition: (Polygonal domain)** Let $\mathcal{D}$ be a planar polygonal domain with $h$ holes and $n$ vertices; $\mathcal{D}$ is a connected close subset of the plane whose boundary(s) consist of a set of $n$ line segments. ^bcd670

If $h=0$, then $\mathcal{D}$ is _simple connected_ and is called a _simple polygon_. If $h>0$, then $\mathcal{D}$ is _multiply connected_, and its holes from a set $\mathcal{P}=\{P_1,\dots,P_h\}$ of pairwise-disjoint simple polygons in the plane called obstacles.

# Visibility polygons
There are two main types of visibility typically considered in [[Visibility polygons and queries#^bcd670|polygonal domains]].

**Definition: (Complete visibility)** Given set $S$ of obstacles (segments or polygons), two objects $s_1,s_2$ are _fully or completely visible_ to one another, if for all  $p\in s_1$ and $q\in s_2$ the line segment $\overline{pq}$ joining the two objects is unobstructed.  

**Definition: (Weak visibility)** Given set $S$ of obstacles (segments or polygons), two objects $s_1,s_2$ are _weakly visible_ to one another, if there exists a unobstructed line segment $\overline{pq}$ with $p\in s_1$ and $q\in s_2$ joining the two objects. 

The _visibility polygon_ for a point $p$ in the plane among obstacles is the possible unbounded polygonal region of all points in the plane forming a unbroken straight line segment to $p$. 

**Definition: (Visibility polygon)** Given set $S$ of obstacles (segments or polygons) and a point $p\in\mathbb{R}^2$. The visibility polygon $Vis(p)$ is the set of all points in $q\in \mathbb{R}^2$ where the segment $\overline{pq}$ does not intersect any element of $S$. 

If the visibility polygon is bounded then it is a _star-shaped polygon_. For single point visibility this polygon is necessarily simple. 

**Problem: (Visibility polygon of a point)** Given a polygonal domain $\mathcal{D}$ and a query point (center) $q\in \mathcal{D}$, return the visibility polygon of $q$; that is, return the locus of points $p\in \mathcal{D}$ such that $\overline{qp}\in \mathcal{D}$. This problem is also known as the _hidden line removal_ problem.

## Visibility in simple polygons
A number of optimal solutions exists for computing the visibility polygon of a point within a simple polygonal domain that use $O(n)$ space and take $O(n)$ time for a query. Dynamic visibility queries are considered in [[@Aronov_2002]] [[@Chazelle_1989]] 

## Visibility with holes
In [[@Heffernan_1995]] an optimal algorithm was given, requiring $O(n)$ space and taking $O(n+h\log h)$ time to construct the visibility polygon of a query point within a polygonal domain with $h$ holes and $n$ segments. 

A more general problem of computing the viability polygon for a point among a set of line segments that do not intersect except possibly at their endpoints was considered in [[@Suri_1986]], which encompasses polygonal domains with holes. The proposed algorithm is optimal in the worst case, requiring $O(n)$ space and $O(n\log n)$ time.

## Line segment visibility in simple polygons
**Problem statement:** Given a simple polygonal domain $P$ with $n$ bounding segments, compute the visibility polygon of a segment observer $s$ (query) within the domain.

A simpler, less general, problem of illuminating the interior of a simple polygon from one of its edges was considered in [[@Avis_1981]]. Several kinds of visibility are considered, (1) Complete visibility, where every point along the query edge can see every point of the polygon, (2) Strong visibility, where there exists a point along the query edge that can see every point of the polygon, and (3) Weak visibility. The given algorithm is optimal and can return the visibility polygon of any of the three types of visibility queries using $O(n)$ space and $O(n)$ time. See [[@Suri_1986]] [[@Akbari_2010]] [[@Chazelle_1989]].

In [[@Chen_2015]] a method was presented for computing the weak visibility polygon of a query segment within a $n$ sided simple polygon $P$ in $O(k\log n)$ query time, where $k$ is the number of segments defining the visibility polygon, by taking $O(n)$ space, $O(n)$ preprocessing time. Additionally, by using $O(n^3)$ space and $O(n^3)$ preprocessing, queries can be answered in $O(k+\log n)$ time.  

# Vertex-edge visibility graphs
There are several kinds of visibility graphs, each corresponding to a different notion of visibility.

**Definition: (Visibility graph)** The visibility graph of a set of nonintersecting polygonal obstacles in the plane is an undirected graph whose vertex set consists of the vertices of the obstacles and whose edges are pairs of vertices $(u, v)$  
such that the line segment $\overline{uv}$ between $u$ and $v$ does not intersect any obstacles. 

An optimal output sensitive algorithm for computing the visibility graph with $E\in O(n^2)$ edges was given in [[@Ghosh_1991]], requiring $O(n + E)$ space and $O(n\log n + E)$ time. The $O(n \log n)$ term is overhead needed for computing a particular triangulation of the obstacle-free space, after which the algorithm runs in $O(E)$ time.

**Definition: (Vertex-edge visibility graph)** The vertex-edge visibility graph of a polygon $P$ is an undirected bipartite graph with vertex set $V=V(P)\cup E(P)$ equal to the vertices and edges of $P$, and edge set $E$ with an edge between $v\in V(P)$ and $e\in E(P)$ if and only if $v$ can weakly see the interior of $e$ (not including end points).

The vertex-edge visibility graph encodes weak visibility of edges from vertices, which contains more information than the traditional visibility graph which only deals with vertex-to-vertex visibility.

The vertex-edge visibility graph was proposed and studied in [[@ORourke_1998]] for simple polygons with a optimal output sensitive algorithm being given that requires $O(n+E)$ space and $O(n+E)$ time. 

# Shortest paths in polygonal domains
The problem of computing the shortest (Euclidean) geodesic path within polygonal domains can be considered a subproblem of computing visibility queries, as a number of methods for the latter utilize the former.

**Definition: (Shortest geodesic path)** The _shortest geodesic path_ is the shortest euclidean path consisting of the fewest possible joined line segments between two points.

**Problem:** Given a polygonal domain $\mathcal{D}$ with $n$ bounding segments and $h$ holes (obstacles), compute the minimum-length path connecting two points $p,q\in \mathcal{D}$ that avoid the obstacles (and the polygonal geometry).

## Shortest paths in simple polygons
In the case of a moving point within simple polygonal domains without holes, [[@Guibas_1989]], gave a optimal solution based on building hierarchical query data structure on top of a triangulation of the bounding polygon. Given a triangulation, the data structure requires $O(n)$ storage, can be build in $O(n)$ time, and return the length (?) of shortest path queries in $O(\log^2 n)$ time. An additional $O(n)$ preprocessing stage can reduce shortest path length queries to $O(\log n)$ time. The $k$ vertices (turns) along a shortest path can be reported in $O(\log n + k)$ time.

At the time of publication the fastest known algorithm for triangulating a simple $n$ sided polygon took $O(n\log\log n)$ time, so the papers algorithm incurred a $O(n\log\log n)$ time penalty if a triangulation was not provided. Afterwards, [[@Chazelle_1991]], found a $O(n)$ time method for triangulating simple polygons, _eliminating_ this shortcoming.
