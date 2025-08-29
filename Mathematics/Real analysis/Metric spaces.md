**Definition: (Metric)** Given the cartesian product $X\times Y$ between two sets (possibly infinite) a function $d:X\times Y\to \mathbb{R}_{\geq 0}$ that satisfies the following for all $(x,y)$: ^67481a
  1) $d(x,y)=0$ iff $x=y$;
  2) $d(x,y)+d(y,z)\geq d(x,z)$;
  3) $d(x,y)=d(y,x)$
is called a metric. 

A set $X$ on which is is possible to introduce a metric (meaning a metric on $X\times X$) is called metrizable

Note, in general metric spaces may not be equip with the structure necessary for performing addition (multiplication, etc...) between its elements. Metric spaces can often be extended to included such structure, see below example, but it isn't required.

If we are dealing with a [[Vector space]] $V$ equip with a [[Vector space#^e3d7ec|norm]] $\|\cdot\|$, a normed vector space, then the _induced metric_ is the map $d:V\times V\to \mathbb{R}_{\geq 0}$ defined as $$d(x,y)=\|x-y\|.$$

**Definition: (Metric space)** A set $X$ equip with a metric $d$ is called a metric space. The resulting space is denoted $(X,d)$.  ^888aae