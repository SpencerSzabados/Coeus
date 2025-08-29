---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - computational_geometry
references:
---
---

**Definition: (Pseudo-lines)** A set of pseudo-lines in the plane is a set of infinite $x$-monotone curves each pair of which intersect at exactly one point.

# Piecewise linear pseudo-lines

## Upper and lower Envelopes
**Problem statement:** Given a collection of $n$ pseudo-lines construct the upper and lower envelopes of the curves, and report the segments (the segments resulting from a pseudo-line being cut at points of intersection) that occur along each.

A dynamic data structure capable of maintaining the lower envelope of a set of pseudo-lines is given in (pre-print)[[@Agarwal_2019]] requiring $O(n)$ space and supporting insertion and deletion operations in $O(\log^2 n)$ time and vertical [[Line segment intersection#Ray shooting|ray shooting]] (to determine which segment is directly above a query point) in $O(\log n)$ time. The given method can also compute the intersection between two lower envelopes of pseudo-lines in $O(\log n)$ time. For $n$ pseudo-lines it takes $O((n+1)\log^2(n+1))$ time to find their lower envelope by interactively inserting them and progressively building up the lower envelope. ^b9d2a0

A more general version of the problem is considered in [[@Edelsbrunner_1989]].