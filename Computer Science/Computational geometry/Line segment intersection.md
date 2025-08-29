---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - computational_geometry
  - algorithms
references:
  - "[[@ORourke_1982]]"
  - "[[@Chazelle_1983]]"
---
---

Unless otherwise stated the method considered is assumed to be operating in the plane (2D space).

# Ray shooting
**Problem statement: (Ray shooting)** Given a collection of $n$ objects $S$, preprocess the space into a data structure that can quickly return the first object of $S$ hit by a given query ray $\overrightarrow{r}$  or the point of intersection between $\overrightarrow{r}$ and said object.

## Simplex range searching methods
In the paper, [[@Agarwal_1993_1]], a method was proposed that is capable of performing quasi-optimal ray shooting queries among segments that allows for a preprocessing decision tradeoff between maximum required space and query times. The method works in any finite dimension and is based on a special partitoning [[Range searching and space partitoning]] scheme using spanning trees with low stabbing number.

Particularly, for any fixed $\epsilon >0$ by utilizing $n^{1+\epsilon}\leq s\leq n^{2+\epsilon}$ storage this method can preprocesses $S$ in $O(s^{1+\epsilon})$ time and can answer any ray shooting query within $O(n^{1+\epsilon}/\sqrt{s})$ time. The same algorithm can be applied to solve [[Line segment intersection#Segment intersection searching|segment intersection searching]] problems for counting the number of intersections in $O(n^{1+\epsilon}/\sqrt{s})$ time or reporting all $k$ intersections in $O(n^{1+\epsilon}/\sqrt{s}+k)$ time.

The $\epsilon$ term appearing in the bounds of this method can be reduced (or reformulated) to a $\log^{O(1)} n$ factor as mentioned in [[@Agarwal_1996]], [[@Agarwal_1993_2]]. Thus, the bounds can be restated as requiring $O(s^{1+\epsilon})$ preprocessing time and $O(\frac{n}{\sqrt{s}}\log^{O(1)}n)$ query time.

# Line segment intersection
The (original) line segment intersection problem can be stated as follows. 

**Problem statement: (Line segment intersection)** Given a collection $S$ of $n$ distinct line segments in the plane, identify all points of intersection between them (or equivalently identify all pairwise segment crossings).

The line segment intersection problem can be solved using $O(n+k)$ storage with $O(n\log n +k)$ worst case time for computing $k$ intersections in the plane, see [[@Chazelle_1992]] [[@Balaban_1995]].

# Segment intersection searching
**Problem statement: (Line segment intersection searching)** Given a collection of $n$ segments $S$, preprocess the space so that the intersections between segments of $S$ and a query segment $\overline{q}$ can be efficiently counted or reported. See [[@Cheng_1992]] [[@Agarwal_1993_2]].

## Colored segment intersection searching
**Problem statement: (Coloured segment intersection searching)** Given a collection of $n$ line segments $S$ (or more generally polygons, polylines, etc.) each with an associated (mapped) colour from $\{1,2,\dots,m\}\leq n$ possible colour options, and a query segment $\overline q$, count or report the number of distinctly colored segments of $S$ that intersect $\overline q$.  

A number of problems solved by [[Reductions|reduction]] to colored segment intersection searching are studied in [[@Agarwal_1996]]. Problem (1), for any constant $\epsilon > 0$, $\mathcal{P}$ can be preprocessed in $O(n^{1+\epsilon})$ time into a data structure of size $O(n^{1+\epsilon})$ so that all $k$ polygons intersecting $\overline q$ can be reported in $O(n^{1+\epsilon} + k)$ time. For a fixed value, the epsilon factor can be reduce to a logarithmic factor, to yield $O(n\log ^{O(1)} n + k)$ query time; moreover, as in [[@Agarwal_1993_1]] a time-space tradeoff can be employed to further reduce query times at the cost of more space. Problem (2), for any fixed $\epsilon >0$ a set $S$ can be preprocessed using $O(n^{4/3+\epsilon})$ space and $O(n^{3/4 + \epsilon})$ time into a data structure of size $O(n\log^3 n)$, that can report all $k$ connected components intersecting a query segment $\overline q$ in $O(n^{1/2+\epsilon} + k\log^2 n)$ time. If the space is allowed to increase to $O(n^{1+\epsilon})$ then queries can be answered in $O(n^{1/2+\epsilon} + k)$ time. Again the epsilon factor can be reformulated, and a time-space tradeoff can be used to further reduce query times at the cost of more storage. 

Among the problems considered in [[@Gupta_1994]], a method for reporting the $k$ colours intersected by a query segment $\overline q$ among a set $S$ of $n$ arbitrarily oriented colored segments is given, requiring $O((n+\mathcal{X})\log n)$ space with $O(\log^2 n + k\log n)$ query time, where $0\leq \mathcal{X}\leq \binom{n}{2}$ is the number of pairwise intersections between line segments in $S$.

### Colored line intersection searching
This problem is also considered in the _simpler_ case of colored lines, not segments, a variation that is more closely related to [[Range searching and space partitoning]] problems.

A number of results for various cases of this generalized problem are given in [[@Bozanis_1995]]. For set of arbitrarily oriented lines (not segments), the $k$ distinct colors of the lines that an arbitrary query segments intersects can be reported using $O(n^2)$ space and $O((1+k)\log n)$ query time. This method makes use of geometry duality and the data structure given in [[@Chazelle_1985]]. 
