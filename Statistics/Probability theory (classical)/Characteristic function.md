---
doc type: Note
authors: Spencer Szabados
date: 2024-03-05
tags:
  - probability_measures
  - real_analysis
  - probability_theory
references:
  - https://www.statlect.com/fundamentals-of-probability/characteristic-function
---
---

Characteristic functions, usually denoted $\Phi$, is a complex valued function that characterizes the [[Families of distributions|distribution]] of a [[Random variables|random variable]]. 

**Definition: (Characteristic function)** Let $X$ be a [[Random variables#^5ceb15|random variable]] with [[Distribution functions of random variables#^c46bbe|distribution]] $p$. The random variable, and the distribution, are associated with the _characteristic function_: $$\Phi:\mathbb{R}\to\mathbb{C}\quad \text{where}\quad \Phi_X(t)=E[\exp(itX)]$$ 

The following theorem details how characteristic functions can be used to uniquely determine the distribution of a random variable.

Note, the existence of this for real-valued random variables can be seen as follows: If $X$ is a real-valued random variable, then $|\exp(itX)|\leq 1$ and so $|\Phi_X(t)|\leq 1.$

The computation of the characteristic function is most generally performed using [[contour integration]], however, we can also exploit Euler identity: $$\exp(itx)=\cos(tx)+i\sin(tx),$$to rewrite the necessary contour integral as the sum of two [[Riemann-Stieltjes Integrals]]. In particular, if $X$ is a [[Random variables#^1f3d1f|continuous random variable]] with density function $p$, then $$\int_{-\infty}^\infty \exp(itx)p(x)\,dx = \int_{-\infty}^\infty\cos(tx)p(x)\,dx+i\int_{-\infty}^\infty\sin(tx)p(x)\,dx.$$

**Theorem:** Suppose $X$ and $Y$ are [[Random variables|random variables]] with distributions $p_X$ and $p_Y$ respectively and characteristic functions $\Phi_X$ and $\phi_Y$. Then, $X$ and $Y$ follow the same distribution if and only if $\phi_X=\phi_Y$.


Characteristic functions are also well behaved under [[Linear transformations]].

**Theorem:** Let $X$ be a [[Random variables|random variable]] with characteristic function $\phi_X$ and set $$Y=a+bX$$where $a,b$ are constants and $b\neq 0$. The characteristic function of $Y$ is then $$\Phi_Y(t) = \exp(iat)\Phi_X(bt).$$
_Proof:_ (By [[Expected values#^90ccda|linearity of expectation]].)







