---
doc type: Note
authors: Spencer Szabados
date: 2024-02-26
tags:
  - abstract_algebra
  - topology
  - real_analysis
  - differential_geometry
---
---

There are two common methods of constructing the definition of a $R$-algebra: the first, constructs the definition using that of a $R$-module; the second, is based on homomorphisms.

**Definition: (R-module)** Let $R$ be a [[Rings|ring]]. An abelian additive [[Groups|group]] $A$ together with a scalar multiplication $\cdot:R\times A\to A$ is called an $R$-module if for all $a,b\in R$:
  1) $r\cdot (a+b) = r\cdot a+r\cdot b$;
  2) $(r+s)\cdot a = r\cdot a+s\cdot a$;
  3) $(rs)\cdot a=r\cdot(s\cdot a)$;
  4) if $R$ has identity $e$, then $e_R\cdot a=a$.

**Definition: (R-algebra)** Let $R$ be a [[Rings|ring]]. An $R$-module $A$ together with a multiplication $*:A\times A\to A$ is called an $R$-algebra if for all $a,b\in A$: the operation $\cdot$ is bilinear, ^ecd19a
  1) $a* (b+c)=a* b+a* c$;
  2) $(a+b)* c = a* c + b* c$;
  3) $(r\cdot a)*(s\cdot b) = (rs)\cdot(a*b)$.

**Definition: (R-algebra)** Let $R$ be a (commutative) ring. An $R$-algebra is a [[Rings#^a3e6f3|ring homomorphism]] $\phi_R:R\to A$.  

**Theorem: (R-algebra composition)** If $\phi_A:R\to A$ and $\phi_B:R\to B$ are $R$-algebras, a homomorphism of $R$-algebras from $\phi_A$ to $\phi_B$ is a ring homomorphism $\psi:A\to B$ such that $\psi\circ \phi_A=\phi_B$.

