---
doc type: Note
authors: Spencer Szabados
date: 2024-02-28
tags:
  - linear_algebra
  - abstract_algebra
references:
  - "[[@Spivak_1995]]"
---
---

Multilinear maps generalize the idea of [[Linear transformations]] (linear maps) and [[Tensor#^dff04a|bilinear maps]].

**Definition: (Multilinear map)** A _multilinear map_ is a function of several variables that is linear wrt to each component; i.e., a multilinear map, a $n$-linear map, is a function of the form $f:V_1\times \cdots V_n \to W$ where $V_1,\dots,V_n$ and $W$ are [[Vector space|vector spaces]] (or [[Rings]]) s.t. that for all $i\in \{1,\dots,n\}$ the $f$ is linear in that component:  $$f(v_1,\dots,v_i+a,\dots,v_n) = f(v_1,\dots,v_i,\dots,v_n)+f(v_1,\dots,a,\dots,v_n)$$and$$f(v_1,\dots,av_i,\dots,v_n) = af(v_1,\dots,v_i,\dots,v_n).$$
A multilinear function of the above form is also called a $k$-[[Tensor]] on $V$ if $V_i=V$ for all $i$.

**Lemma:** A linear combination of $n$-linear functions is $n$-linear. 

**Definition: (Alternating map)** A multilinear map $f$ is called alternating (or alternate) if the following conditions are satisfied: ^03db95
1. $f(A)=0$ whenever two rows of $A$ are equal;
2. if $A'$ is obtained from interchanging from $A$, then $f(A')=-f(A)$.