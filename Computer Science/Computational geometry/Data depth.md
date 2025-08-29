---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - data_depth
  - computational_geometry
  - statistics
references:
---
---
# Overview
The concept of data depth is that of providing a measure of centrality to sample points within a multivariate data set. Many different notions of data depth exit, presented both from inside [[computational geometry]] and [[statistics]].

# Data depth for point sets
## Tukey depth
The Tukey depth (1975) (or _halfspace depth_ or _location depth_) was one of the fist notions of data depth proposed. 

**Definition: (Tukey depth)** Given set $S$ of points and a point $p\in\mathbb{R}^d$ , the Tukey depth of $p$ is defined as the minimum number of points of $S$ contained in any closed halfspace that contains $p$; i.e., $$D_T(p,S)=min\{|h\cap S| : h \text{ is a closed halfspace containing } p\}.$$The point with the largest depth is called the _Tukey median_. 

## Oja depth
**Definition: (Oja depth)** Given set $S$ of $n$ points in $\mathbb{R}^d$. the _Oja depth_ of a point $p$ is $$D_O(p,S) = \sum_{y_1,\dots,y_d\in \binom{S}{d}}vol(p,y_1,\dots,y_d),$$ where $vol(p,y_1,\dots,y_d)$ denotes the volume of the simplex with vertices $p,y_1,\dots,y_d$. A point of minimum depth is called an _Oja center_. 

## Majority depth
**Definition: (Majority depth)** Let $S$ be a set of points in $\mathbb{R}^d$. If the points in $S$ are in general position, any $d$ points of $S$ define a unique hyperplane $h$. With $h$ as a common boundary, two closed halfspaces are obtained. The one containing at least $\frac{n+d}{2}$ points is called the major side of $h$. The _majority depth_ of $p$ is the number of major sides it forms.

# Data depth for functions and curves
Many depth measures for curves originating from Computational Geometry resemble (at least on a cursorily level) notions of [[Curve morphology and similarity analysis]], as they tend to emphasise geometric aspects (or shape) of the input data. Reinforcing this connection, observe that one could conceivably define a _depth ranking_ for a given sample of curves based by applying a similarity measure and ordering the curves based on similarity to the curve of _median_ features. However, unlike depth measures (or statistical measures in general) that focus on absolute data, it is commonly desired that notions of curve similarity be invariant to both spatial and temporal transforms, so much of the absolute positional and temporal information of the data is either ignored or not directly used in the comparison between curves.

## Functional data
Functional data sets consist unsurpassingly of functions in the form $x=x(t)$, each typically being represented by a discretized sequence of observations $x=(x(t_1),x(t_2),\dots,x(t_n))$ due to physical sampling limitations. Each datum being called a functional observation. See [[Functional data analysis]] for more material on functional analysis methods in statistics. 

## Curve data
Curve data is similar to functional data, differing in that observations don't need to satisfy a functional relation, nor needing to be explicitly parameterized. Hence, curve data is more general in form than functional data.

