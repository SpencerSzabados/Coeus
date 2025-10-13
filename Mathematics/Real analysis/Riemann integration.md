---
doc type: Note
authors: Spencer Szabados
data: 2025-10-11
tags:
  - calculus
  - integration
references:
  - https://web.ma.utexas.edu/users/m408m/Display15-2-3.shtml
  - "[[@Apostol_1973]]"
---
---

# Riemann integral
^def40d

The most basic integral is the Riemann integral over a bounded set.

**Definition: (Interval partition)** A partition, $P$, of an interval $[a,b]$ is a finite set of points $P=\{x_0,x_1,\dots,x_n\}$ with $a=x_0<x_1<x<\cdots<x_n=b$. 

A partition $P'$ is said to be _finer_ (or a _refinement of_) than another partition $P$, over the same interval, if $P\subseteq P'$; Intuitively this means, $\inf_{x_i,x_j\in P'}\{|x_i-x_j|\}\leq \inf_{x_i,x_j\in P}\{|x_i-x_j|\}$. The norm of a partition, denoted $\|P\|$, is equal to the largest subinterval length in the partition.

The set of all partition over a interval $[a,b]$ is denoted $\mathcal{P}[a,b]$. 

Beginning with the most well known and simplest integral definition, the _Riemann sum formulation of the integral_.

**Definition: (Riemann Integral)** Let $f:[a,b]\to\mathbb{R}$ be a bounded function bounded on its domain. For a partition $P=\{x_0,x_1,\dots,x_n\}\in\mathcal{P}[a,b]$, choose a sample point $\xi_i\in[x_{i-1},x_i]$ for each subinterval, and define the _Riemann sum_  $$S(f,P,\xi) = \sum_{i=1}^n f(\xi_i)\,(x_i - x_{i-1}).$$The function  is said to be _Riemann integrable_ on $[a,b]$ if there exists a $I\in \mathbb{R}$ such that for every $\epsilon>0$, there exists $\delta>0$ satisfying $$|S(f,P,\xi) - I| < \epsilon$$whenever the partition $P$ satisfies $\|P\|<\delta$ and $\xi_i\in[x_{i-1},x_i]$ for all $i=1,\dots,n$.  In this case, we write $$I = \int_a^b f(x)\,dx$$and call $I$ the _Riemann integral_ of $f$ over $[a,b]$.

The Riemann integral is the reduction of the [[Riemann-Stieltjes Integrals]] with respect to the measure $\alpha=x$ (identity) function rather than some monotone function.

**Definition: (Riemann Path Integral)**  
Let $\gamma:[a,b]\to\mathbb{R}^n$ be a continuous, piecewise continuously differentiable curve, called a _path_, and let $f:\gamma([a,b])\to\mathbb{R}$ be a real-valued function defined on the image of . Let  $P=\{t_0,t_1,\dots,t_n\}$ be a partition of $[a,b]$ and for each subinterval $[t_{i-1},t_i]$, choose a sample point $\tau_i\in[t_{i-1},t_i]$ to define the _Riemann path sum_ $$
S(f,\gamma,P,\tau) = \sum_{i=1}^n f(\gamma(\tau_i))\,\|\gamma(t_i)-\gamma(t_{i-1})\|.$$The function $f$ is said to be _Riemann integrable along the path_ $\gamma$ if there exists a real number $I$ such that for every $\epsilon>0$, there exists $\delta>0$ satisfying $$|S(f,\gamma,P,\tau) - I| < \epsilon$$whenever the partition $P$ satisfies $\|P\|<\delta$ and $\tau_i\in[t_{i-1},t_i]$ for all $i$. In this case, the limit value $I$ is called the _Riemann path integral_ of $f$ along $\gamma$, and is equal to $$
\int_\gamma f\,ds \;=\; \int_a^b f(\gamma(t))\,\bigg\|\frac{\partial}{\partial t}\gamma(t)\bigg\|\,dt.$$


# Iterated integrals
Evaluating higher dimensional integrals, such as over areas or volumes, using the definition can be challenging; however, the following theorem gives us a method of evaluating these integrals using a set of nested one dimensional integrals.

**Theorem: (Fubini's)** Let $f:[a,b]\times [c,d]\to \mathbb{R}$ be continuous over its domain. Then for $R=[a,b]\times [c,d]$ and the area element $dA$, [[Measure spaces#^c048df|measure]], we have $$\int\int_R f\,dA=\int_a^b\int_c^d f(x,y)\,dxdy=\int_c^d\int_a^bf(x,y)\,dydx.$$That is, the double integral is equal to either iterated integral order provided $f$ is continuous wrt both $x$ and $y$ over $R$. 


# Differentiating under the integral

**Theorem: (Leibniz differentiation rule)**  Let $f:\mathbb{R}^2\to \mathbb{R}$ be continuously differentiable with respect to $y$ on the rectangle $R=[a,b]\times [c,d]$. Then $$\frac{d}{dy}\int_a^b f(x,y)\, dx = \int_a^b \frac{\partial}{\partial y} f(x,y)\, dx.$$More generally, let $g,h:[c,d]\to\mathbb{R}$ be continuously differentiable functions satisfying $g(y)\leq h(y)$ for all $y\in [c,d]$, then $$\frac{d}{dy} \int_{g(y)}^{h(y)} f(x,y)\, dx = f(h(y),y)\, h'(y) - f(g(y),y)\, g'(y) + \int_{g(y)}^{h(y)} \frac{\partial}{\partial y} f(x,y)\, dx.$$
