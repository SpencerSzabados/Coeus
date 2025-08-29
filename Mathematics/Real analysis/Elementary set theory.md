**Definition: (Relation)** A _relation_ is a set of ordered pairs. A _function_ is a relation $F$ such that if $(x,y)\in F$ and $(x,z)\in F$, then $y=z$. If $F$ is a function, the domain of $F$ written $\text{dom} F$, is defined to be $$dom F = \{x : (x,y)\in F \text{ for some } y\},$$ and the image of $F$, written $im F$, is defined to be $$im F = \{y : (x,y)\in F \text{ for some } x\in dom F\}.$$ 
If $R$ is a relation, then the converse of $R$, denoted $\hat R$, is defined by $\hat R = \{(x,y) : (y,x)\in R\}.$

**Definition: (injective)** A function is _injective_ (one-to-one) iff for all $y,z \in dom f$, we have that $f(y)=f(z)$ implies $y=z$.

**Theorem:** Let $F$ be a function. Then $\hat F$ is a function iff $F$ is one-to-one.  

**Definition: (Interval partition)** If $[a,b]$ is a compact interval, a set of points $P=\{x_0,x_1,\dots,x_n\}$ satisfying $a=x_0<x_1<\dots<x_{n-1}<x_n=b$ is called a partition of $[a,b]$. The collection of all possible partitions of $[a,b]$ is denoted $\mathscr{P}[a,b]$. [[@Apostol_1973]]

**Definition: (Compact set)** A [[Topological spaces#^8d2d2b|topological space]]  $X$(e.g., [[Metric spaces#^888aae|metric space]]) is _compact_ if every open cover of $X$ admits a finite subcover.

**Theorem: (Heine-Borel theorem)** A subset $X\subset \mathbb{R}^n$ is compact if and only if it is closed and bounded.