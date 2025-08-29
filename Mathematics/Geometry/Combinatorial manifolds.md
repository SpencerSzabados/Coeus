---
doc type: Note
authors: Spencer Szabados
year: 2023-09-11
tags:
  - geometry
  - computational_geometry
  - machine_learning
  - topology
---
___

This note is primarily concerned with (combinatorial) manifolds which are surfaces that must obey "local flatness" properties and commonly connectedness. Manifolds, in a simplified view, are nothing but the underlying contagious support that data rests on (or is sampled from); ore more generally, manifolds are higher dimensional analogs of surfaces in three dimensions. Despite this simple intuitive expression manifolds are often very challenging to define or work with directly; this according to [TowardsDataScience-Z.Singer](https://towardsdatascience.com/manifolds-in-data-science-a-brief-overview-2e9dde9437e5). 

# Overview 
A manifold is a [[Topological spaces]] that is locally Cartesian (in terms of some properties). 

There are several ways to define a manifold, a common general approach is to use [[Topological spaces#^684817|topological atlas's]] or the topological property of second countability.

# Combinatorial (piecewise linear) manifolds

^48deab

Combinatorial manifolds are geometries that are constructed by "joining" various bounded regions. This style (as in how it is defined) is not discussed much in present literature, as is mainly referenced in literature on combinatorial topology before the 1990s, which has fallen out of favor in place of more modern (and general) topological definitions; in particular, combinatorial manifolds can be show to be homeomorphic to Piecewise linear (PL) manifolds.


## Simplicial manifolds 