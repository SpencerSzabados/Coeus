---
doc type: Note
authors: Spencer Szabados
date: 2025-11-10
tags:
  - calculus
  - real_analysis
  - integration
references:
  - "[[@Apostol_1973]]"
---
---

The Riemann-Stieltjes integral is a slight generalization of the (identity measure) [[Riemann integration#^def40d|Riemann integral]] and is natural to consider before [[Lebesgue integration]].

# The Riemann-Stieltjes Integral
The _Riemann-Stieltjes integral_ incorporates a variable measure function, opposed to the previous formulation that uses the spaces metric.

**Definition: (Riemann-Stieltjes Sum)** Let $P=\{x_0,x_1,\dots,x_n\}$ be a [[Riemann integration#^858e92|partition]] of $[a,b]$ and let $t_k\in [x_{k-1},x_k]$. A sum of the form $$S(P,f,\alpha) = \sum_{k=1}^nf(t_k)\Delta\alpha_k$$ is called a _Riemann-Stieltjes sum_ of $f$ with respect to a (continuous real valued) function $\alpha$, where $\Delta\alpha_k = \alpha(x_k)-\alpha(x_{k-1})$.

**Definition: (Riemann-Stieltjes Integral)** A function $f$ is said to be _Riemann-integrable_ wrt $\alpha$ on $[a,b]$, denoted $f\in R(\alpha)$ on $[a,b]$, if there exists a number $A$ s.t. $\forall\epsilon >0$, $\exists P_\epsilon$ of $[a,b]$ such that for every finer partition $P_{\delta}$, i.e., $\delta \leq \epsilon$, and $\forall t_k\in [x_{k-1},x_k]$, we have $|S(P,f,\alpha)-A|< \epsilon$ for some $A\in \mathbb{R}$. When such an $A$ exists, it is uniquely determined, and is denoted $$A= \int_a^bf\, d\alpha \quad\text{ or }\quad A= \int_a^bf(x)\,d\alpha(x).$$In other words, $$\lim_{\epsilon\to 0}S(P_\epsilon,f,\alpha) = \lim_{\epsilon\to 0}\sum_{k=1}^{n(\epsilon)}f(t_k)\Delta\alpha_k = \int_a^bf\, d\alpha = A,$$ by tolerating some abuse of notation.


## Reduction of Riemann-Stieltjes integral to the Riemann Integral.
There are a number of elementary relations that hold between $\int f\,d\alpha$ and $\int \alpha\, df$.

**Theorem: (Integration by parts)** if $f\in R(\alpha)$ on $[a,b]$, then $\alpha\in R(f)$ on $[a,b]$ and $$\int_a^bf(x)\, d\alpha(x)+\int_a^b \alpha(x)\, df(x) = f(b)\alpha(b)-f(a)\alpha(a).$$
_Proof:_

**Theorem: (Change of variables)** Let $f\in R(\alpha)$ on $[a,b]$ and let $g$ be a strictly monotonic continuous function defined over an interval $I=[c,d]$. Assume that $a=g(c)$ and $b=g(d).$ Let $h$ and $\beta$ be composite functions with $$h = f(g(x)) \quad\text{ and }\quad \beta(x)=\alpha(g(x))\quad\text{ if }x\in I.$$Then $h\in R(\beta)$ on $I$ and $$\int_{g(c)}^{g(d)}f(t)\, d\alpha(t) = \int_{c}^d f(g(x))\, d\alpha(g(x)).$$

As mentioned above the Riemann integral is nothing but a special case of the Riemann-Stieltjes integral, however, more generally we can reduce Riemann-Stieltjes integral into  simpler Riemann counterparts if the measure $\alpha$ obeys certain restrictions. That is, we can replace the symbol $d\alpha$ by the more familiar $\alpha'\, d\alpha$ in the integral $\int_a^b f\, d\alpha$ when the following theorem is satisfied.

**Theorem:** Assume $f\in R(\alpha)$ on $[a,b]$ and that $\alpha$ has a continuous derivative $\alpha'$ on $[a,b]$. Then the Riemann integral $\int_a^bf(x)\alpha'(x)\, dx$ exists and we have $$\int_a^bf(x)\,d\alpha(x) = \int_a^bf(x)\alpha'(x)\, dx.$$


## Sufficient conditions for the existence of Riemann-Stieltjes Integrals. 

**Theorem:** Assume that $c\in[a,b]$ and that two of the three following integrals exist $$\int_a^c f\, d\alpha+\int_c^bf\,d\alpha = \int_a^bf\,d\alpha.$$Then the first integral exists and the equality holds.
_Proof:_ (p143)[[@Apostol_1973]].

**Theorem:** If $f$ is continuous on $[a,b]$ and if $\alpha$ is of bounded variation on $[a,b]$, then $f\in R(\alpha)$ on $[a,b]$.

**Corollary: (Sufficient condition for Riemann integrals)** Each of the following conditions is sufficient for the existence of the Riemann integral $\int_a^b f(x)\,dx$
    a) $f$ is continuous on $[a,b]$;
    b) $f$ is of bounded variation on $[a,b]$.


## Necessary conditions for the existence of Riemann-Stieltjes Integrals.

**Mean-value theorem:** Assume that $\alpha$ is monotonically increasing and let $f\in R(\alpha)$ on $[a,b]$. Let $M = \sup \{f(x) : x\in [a,b]\}$ and $m=\inf \{f(x) : x\in [a,b]\}$. Then there exists a real number $c$ satisfying $m\leq c \leq M$ such that $$\int_a^bf(x)d\alpha(x) = c\int_a^b d\alpha(x) = c[\alpha(b) - \alpha(a)].$$ In particular, if $f$ is continuous on $[a,b]$ then $c=f(x_0)$ for some $x_0\in [a,b]$.

**Second mean-value theorem:** Assume that $\alpha$ is continuous and that $f$ is monotonically increasing on $[a,b]$. Then there exists a point $x_0\in [a,b]$ such that $$\int_a^b f(x)d\alpha(x) = f(a)\int_a^{x_0}d\alpha(x) + f(b)\int_{x_0}^bd\alpha(x).$$