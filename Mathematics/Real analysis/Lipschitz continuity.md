
# Overview
**Definition: (Lipschitz continuity)** A function $f:\mathbb{R}^d\to\mathbb{R}^m$ is _Lipschitz continuous_ with _Lipschitz constant $L$_ if for any $x,y\in\mathbb{R}^d$ $$\|f(y)-f(x)\|_2\leq L\|y-x\|_2.$$

The above formulation can be restated more generally for functions that map from one metric space into another, by using the norm associated with each space in place of the two Euclidean norms. See [Wiki](https://en.wikipedia.org/wiki/Lipschitz_continuity).

The Lipschitz constant of a differentiable function can be bounded by the norm of its Jacobian (wrt to the induced norm). This result can be seen as a generalization of applying the mean value theory to a function with a bounded derivative.

**Theorem:** Let $f:\mathbb{R}^d\to\mathbb{R}^d$ be a continuous function that admits a continuous Jacobian $\mathbb{J}_f$. If there exists a $L\geq 0$ such that $\|\mathbb{J}_f(x)\|\leq L$ for all $x\in\mathbb{R}^d$, then $\|f(x)-f(y)\|\leq L\|x-y\|$ for all $x,y\in\mathbb{R}^d$. Equivalently, if $\|\mathbb{J}_f\|$ is bounded, then $f$ is globally Lipschitz with (minimum) Lipchitz constant $L=\sum_{x\in\mathbb{R}^d}\|\mathbb{J}_f(x)\|$. See [[@Khalil_2014]] and [StackExchange-Paul-Wintz](https://math.stackexchange.com/questions/4663324/calculate-lipschitz-constant-of-continuously-differentiable-function-mathbbr).


# Bounded variation 
**Corollary:** If $f$ is Lipschitz on $[a,b]$ with Lipschitz constant $L$ then $f$ is uniformly continuous and of [[Functions of bounded variation and rectifiable curves#Functions of Bounded Variation|bounded variation]] on $[a,b]$ with $V(f,[a,b])\leq L|b-a|$.
_Proof:_ Direct consequence of applying Lipschitz definition.