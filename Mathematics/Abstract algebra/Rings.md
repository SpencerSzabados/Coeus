**Definition: (Ring)** A non-empty set $R$ is a ring if it has two closed binary operations $+:R\times R\to R$ and $\cdot:R\times R \to R$ which satisfy: for any $a,b,c\in R$ ^2d41d7
 1) $a+b=b+a$
 2) $(a+b)+c = a+(b+c)$
 3) There exists a $0\in R$ such that $a+0=a$
 4) There exists a $-a\in R$ such that $a+(-a)=0$
 5) $(a\cdot b)\cdot c = a\cdot(b\cdot c)$
 6) $a\cdot(b+a)=a\cdot b+ a\cdot c$ and $(a+b)\cdot c = a\cdot c + b\cdot c$.

**Definition: (Ring characteristic)** Let $R$ be a ring. The characteristic of $R$ is the least positive integer $n$ such that $nr=0$ for all $r\in R$. If no such $n$ exists then the characteristic is defined as $0$.

**Definition: (Ring homomorphism)** A function $f:R\to S$ between two rings is _ring homomorphism_ if: for all $a,b\in R$,  ^a3e6f3
  1) $f(a+b)=f(a)+f(b)$;
  2) $f(ab)=f(a)f(b)$;
  3) $f(e_R)=e_S$; where $e_R$ is unity in ring $R$ and likewise for $e_S$ for ring $S$.