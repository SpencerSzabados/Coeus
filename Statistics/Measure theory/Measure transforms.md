
# Overview

**Definition: (Rearrangement)** Let $p\in\mathbb{R}_{\geq 1}$ and $d\in\mathbb{Z}_{\geq 1}$. A _rearrangement_ of $u\in L^p(X,\mu)$ , where $X$ is a subspace of $\mathbb{R}^d$, on the measure space $(Y,v)$, again with $Y$ being a subspace of $\mathbb{R}^d$, any $w\in L^p(Y,v)$ such that $$\int_X f(u(x))\,d\mu(x)=\int_Y f(w(y))\,dv(y)$$for any $f\in C(\mathbb{R}^d)$ such that $|f(\epsilon)|\leq$


## Measure preserving transforms 

**Definition: (Measure preserving)** Let $(X,\mu)$ and $(Y,v)$ be two [[Measure spaces|measure spaces]] (probability spaces). A function $T:X\to Y$ is said to be _measure preserving_ if for every $v$-measurable $B\subseteq Y$, $T^{-1}(B)$ is $\mu$-measurable and $\mu(T^{-1}(B))=v(B)$. Equivalently, $T$ is said to be measure preserving if for every $v$-measurable function $f$, $f\circ T$ is $\mu$-measurable and $$\int_X f\circ T\,du=\int_Yf\,dv.$$
Note that such measure preserving mapping are not necessarily one-to-one, and consequently not necessarily invertible. 



**Theorem: (Constructing measure preserving transform)** If $f$ is a measurable function on $[0,1]$, define $$\phi(x)=\lambda\{y\mid f(y)>f(x)\}+\lambda\{y\mid f(y)=f(x), y\leq x\}.$$Then $\phi$ is measurable. Moreover this function is measure preserving.
_Proof:_ (p450)[[@Ryff_1970]]

The above theorem states that any function defined in terms of the (TODO - how does this relate to inverse of cdf)

**Theorem:** If $\mathcal{F}$ is a equivalence class of measurable functions and $\phi$ is defined as above, then $$\mathcal{F}^*\circ\phi=\mathcal{F}$$where $\mathcal{F}^*$ is the [[Measure spaces#^aba5de|decreasing rearrangement]] of $\mathcal{F}$. 
_Proof:_ (p452)[[@Ryff_1970]].

**Theorem:** If $\phi$ is a measure preserving function and differentiable at $x_0$, then $|\phi'(x_0)|\geq 1$.
_Proof:_ [[@Ryff_1970]].

Moreover, if $X$ is an open subset of $\mathbb{}R^d$, equipped with the $d$-dimensional [[Lebesgue integration#^c700cf|Lebesgue measure]] $\lambda$. It follows by the [[Statistical transformations#^2e88f0|change of variables formula]] that a continuously differentiable (or continuous almost everywhere differentiable) [[Normalizing flows#^2ea514|diffeomorphism]] $T:X\to X$ is measure preserving if and only if $|\det(\mathbb{J}_T)|=1$.


## Decompositions 

**Theorem: (Helmholtz decomposition)** Let $X$ be a smooth bounded connected open set in $\mathbb{R}^d$. Then, any smooth vector field (vector valued function) $f:X\to\mathbb{R}^d$ can be written in a unique way as $f=h+\nabla g$, where $g$ is a smooth real valued function defined on $X$ and $h$ is  is a smooth divergence free vector field.


**Theorem: (Brenier polar factorization)** Let $X$ be a bounded subset of $\mathbb{R}^d$ with positive Lebesgue measure. Let $f:X\to\mathbb{R}^d$ be an $L^2$ integrable vector-valued function (vector field) that satisfies the condition: for any Lebasque negligible set $B$ in $\mathbb{R}^d$, e.g., sets with zero measure, $|f^{-1}(B)|=0$. Then, there exists a unique rearrangement $\nabla \phi$ of $f$ in the class of $L^2$ gradients of convex functions, and a unique measure preserving map $g$ such that $$f=\nabla\phi\circ g.$$
_Proof:_ See [[@Brenier_1991]], [[@Villani_2003]].

