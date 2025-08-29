---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - real_analysis
  - convex_functions
  - optimization
references:
---
---

# Convexity 
Informally, a convex function is one such that any segment between two points on its graph lies completely above the portion of the graph between the defining points.

**Definition: (Convex function)** A function $f:\mathbb{R}^d\to\mathbb{R}$ is convex, if for all $x_1,x_2\in\mathbb{R}^d$ and $\alpha\in[0,1]$ $$f(\alpha x_1+(1-\alpha)x_2)\leq \alpha f(x_1)+(1-\alpha)f (x_2).$$ ^b246dc

There is of course a close connection between convex functions and convex sets. Specifically, a function $f:\mathbb{R}^d\to\mathbb{R}$ is convex, if and only if the _epigraph_ of $f$, that is the area bounded by a level set of $f$, defined as $$\Gamma = \{(x,t)\in \mathbb{R}^d\times\mathbb{R}\mid f(x)\leq t\},$$ is a convex set. Likewise, if $f$ is concave then $$\{(x,t)\in \mathbb{R}^d\times\mathbb{R} \mid f(x)\geq t\}$$is a convex set.

A common class of convex functions considered is those that are said to have closed images.

**Definition: (Closed convex function)** A convex function $f:\mathbb{R}^d\to\mathbb{R}$ is said to be _closed convex_, if it is closed, that is, for each $\alpha\in \mathbb{R}$ the sublevel set $\{x\mid f(x)\leq \alpha\}$ is [[Basic set theory^closed|closed]]. [Wiki](https://en.wikipedia.org/wiki/Closed_convex_function).

**Theorem: (Combination of convex functions)** If $f$ and $g$ are convex functions and $a,b\geq 0$, then $h=af+bg$ is a convex function.

The convexity inequality can be expanded to more than two variables, resulting in a famous inequality.

**Corollary: (Jensen's inequality)** Let $f$ be a convex function, and let $\{(x_1,\alpha_1),\dots,(x_N,\alpha_N)\}$ be a collection of matched pairs with $x_i$ from the domain of $f$ and $\alpha_i\in[0,1]$ with $\alpha_1+\dots+\alpha_N=1$. Then $$f\left(\sum_{i=1}^N\alpha_ix_i\right)\leq\sum_{i=1}^N \alpha_if(x_i).$$More generally, let $p(x)$ be a probability density function; or any nonnegative function with $\int p(x)\,dx = 1$. Then $$f\left(\int p(x)x\,dx\right)\leq \int p(x)f(x)\,dx\quad \text{ or equivalently }\quad f(E[x]) \leq E[f(x)]$$see [[Expected values]].

**Corollary: (Affine composition)** If $f:\mathbb{R}^d\to\mathbb{R}$ is convex, then for any $A\in\mathbb{R}^{d\times m}$ and any $b\in\mathbb{R}^d$, the function $$h(x) = f(Ax+b)$$is convex.

Maintaining the convexity of a product function is more difficult than many other operations, and requires rather strong conditions placed on the component functions.

**Theorem: (Convex multiplication)** If $f$ and $g$ are both are non-negative non-decreasing convex functions, then $fg$ is convex.
_Proof_: See [StackExchange-Murthy](https://math.stackexchange.com/a/3854836).

**Theorem: (Composition of convex functions)** Let $f$ be a convex function with convex domain $D$ and $g$ be a convex nondecreasing function, then $h=g\circ f$ is a convex function.
_Proof:_ $$\begin{align}(g\circ f)(\alpha x_1+(1-\alpha)x_2) &= g(f(\alpha x_1+(1-\alpha)x_2))\\ &\leq g(\alpha f(x_1)+(1-\alpha)f(x_2)) &&\text{($f$ is convex and $g$ is nondecreasing.)}\\ &\leq \alpha g(f(x_1))+(1-\alpha g(f(x_2))) &&\text{($g$ is convex.)}\\
&=\alpha(g\circ f)(x_1)+(1-\alpha)(g\circ f)(x_2).\end{align}$$
**Corollary: (Convexity of p-norms)** All p-norms ([[Metric spaces]]), for $p>0$, are convex functions.

**Corollary: (Convexity of max)** If $f$ and $g$ are convex functions, then $h(x)=\max\{f(x),g(x)\}$ is convex.

# Strong convexity 
**Definition: (s-strongly convex)** A function $f:\mathbb{R}^d\to \mathbb{R}$ is said to be $s$-strongly convex if $$g(x)=f(x)-\frac{s}{2}\|x\|_2^2$$is convex on the domain of $f$. ^d1ebf5


# Differentiable convex functions
Here we will study what convexity implies about the behaviour of a differentiable function.

**Theorem:** If $f:\mathbb{R}^d\to\mathbb{R}$ is a differentiable function. Then $f$ is convex, if and only if for every $x,y\in\mathbb{R}^d$ the inequality $$f(y)\geq f(x)+\nabla f(x)^\intercal(y-x)$$is satisfied.
_Proof:_

This result is closely related to first order approximations of functions using their [[Taylor series]]; where a first order Taylor series approximation will always underestimate $f$ if and only if it is convex.

It follows directly from the above theorem that minimizers are unique (hence global) for differentiable convex functions.

**Corollary:** If $f$ is a differentiable convex function, then $x^*$ is a global minimum of $f$, if and only if $\nabla f(x^*)=0$.

**Theorem:** A (at least) twice differentiable function $f$ is convex (resp. concave), if and only if it's Hessian $\nabla^2 f$ is positive semi-definite (resp. negative semi-definite) for all values in the domain of $f$.
_Proof:_

Observe, a result often used in optimization applications, that for a quadratic function $f:\mathbb{R}^d\to\mathbb{R}$, which can therefore be expressed using the matrix equation $f(x) = \frac{1}{2}\vec{x}^\intercal A \vec{x} + \vec{b}^\intercal \vec{x} + \vec{c}$, if $A$ is symmetric positive semidefinite, then $\nabla^2 f = A$ and by the above theorem $f$ is convex.

If we constrain the shape of $f$ sufficiently then we can infer the invertibility of the gradient.

**Theorem:** If $f:\mathbb{R}^d\to\mathbb{R}$ is strictly convex and continuously differentiable then $\nabla f$ is one-to-one. See [StackExchange-Garrett](https://math.stackexchange.com/a/1670838).


# Generalizations of convexity
The following type of convexity generalization is not to be confused with, [[s-Concave densities]] which are a similar generalisation of convexities studied in [[Nonparametric statistics]] (or more generally in [[Families of distributions]]), nor should these be confused with $s$-strongly concave.

**Definition: (s-convex functions)** A function $f:\mathbb{R}_{\geq0}\to\mathbb{R}$ is said to be $s$-convex, for $0<s\leq1$, in the first sense if $$f(\alpha x+\beta y)\leq \alpha^s f(x)+\beta^s f(y)$$for all $x,y\in\mathbb{R}_{\geq0}$ and all $\alpha,\beta\geq 0$ with $\alpha^s+\beta^s=1$. A function $f$ is said to be $s$-convex in the second sense if the same inequality holds for all $x,y\in\mathbb{R}_{>0}$ and all $\alpha,\beta\geq 0$ with $\alpha+\beta=1$. See [[@Hudzik_1994]].

**Lemma:** All $s$-concave sequences are [[Quasi-convex functions|quasi-concave]].

**Theorem:** Let $f$ and $g$ be $s_1$-concave and $s_2$-concave functions respectively with $0<s_1,s_2,\leq 1$. Then 
  1) If $f$ is non-decreasing and $g$ is non-negative such that $f(0)\leq 0=g(0)$ then the composition $f\circ g$ is $s_1s_2$-concave.  
  2) If $0<s_1,s_2<1$ and $f$ and $g$ are non-negative such that either $f(0)=0$ and $\lim_{x\to 0^+}g(x)=g(0)$ or $g(0)=0$ and $\lim_{x\to 0^+}f(x)=f(0)$ then $fg$ is $\min(s_1,s_2)$-concave.
_Proof:_ [[@Hudzik_1994]].