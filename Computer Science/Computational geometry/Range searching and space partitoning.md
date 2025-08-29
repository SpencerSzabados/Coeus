---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - space_partitoning
  - computational_geometry
references:
---
---

# Planar subdivisions
A planar subdivision is any partition of the plane into (possibly unbounded) polygonal regions. See [[@Agarwal_1997]]

**Edge-ordered representation:** The _edge-ordered representation_ of a planar subdivision assumes an ordering to wedges and vertices: (1) If $e$ is a line segment joining vertex $v$ to $w$, then $e$ is represented as the pair of directed edges $\{(v,w),(w,v)\}$; (2) each vertex $v$ has associated with it location coordinates and a counterclockwise ordered list of all directed edges originating from $v$; (3) each directed edge $(v,w)$ has associated with it a pointer to the complement edge $(w,v)$ and the region lying immediately to the right of $(v,w)$, where "right" it taken with respect to the direction of the vector. This representation occupies $O(|S|)$ space, and can be constructed in $O(|S|\log |S|)$ time from a list of vertex adjacencies, in $O(|S|)$ time from the natural graph representation, or in $O(|S|)$ time if the underlying planar graph has bounded degree (independent of $n$ ?).

## Planar subdivision searching
**Problem statement (Subdivision search):** Given a subdivision $S$ of the plane with $n$ line segments and a query point $q$, determine which region (face) of $S$ contains $q$. This problem is also sometimes called _region searching_. Moreover, as a finite planar subdivision (segments are all finite) is equivalent to a straight-line embedding of a planar graph many problems of these categories might be equivalent.

Subdivision searching is a slight generalization of _point-location searching_.

 In [[@Kirkpatrick_1983]] a optimal method was given that requires $O(n)$ storage and $O(n)$ preprocessing time, on top of a supplied edge-ordered planar subdivision representation, is capable of returning the face containing a query point in worst case $O(\log n)$ time.