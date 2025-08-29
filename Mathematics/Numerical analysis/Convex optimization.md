
# Overview 
Recall some definitions.

**Definition: (Local optimality)** A point $x$ is _locally optimal_ if it is a feasible point (satisfies the constraints of the problem) and there exists a $r>0$ such that for all feasible points $z$ within $\|x-z\|\leq r$, the inequality $f(x)\leq f(z)$ is satisfied.

**Definition: (Global optimality)** A point $x$ is _globally optimal_ if it is feasible and for all other feasible points $z$, $f(x)\leq f(z)$. ^e55e01

There exists various local optimization methods for solving various problems, which are based on progressively refining an initial guess at the solution until a local optimal is reached that we hope is close to the global optimal. 

In the case of convex optimization, all locally optimal points are in fact globally optimal, and consequently unique. This follow directly from the definition of function convexity.

Formally convex optimization problems take the following form.

**Problem: (Convex optimization)** Let $f$ be the [[Convex functions|convex function]] we are interested in optimizing. Our optimization problem then takes the general form $$\begin{align}\text{minimize}&\quad f(x)\\ \text{subject to}&\quad g_i(x)\leq 0,\text{ for }i=1,\dots,m\\ &\quad h_i(x)=0,\text{ for }i=1,\dots,p\end{align}$$where $g_1,\dots,g_m$ are convex functions and $h_1,\dots,h_p$ affine (linear) functions which impose restrictions on the set of feasible solutions. 

The direction of the inequalities is important in the above definition, as the conditions $g_i(x)\leq 0$ ensure the feasible region (solution space) is itself a convex region (intersection of the set of convex regions defined by the functions).

The above problem statement is also commonly formulated as follows: $$\begin{align}\text{minimize}&\quad f(x)\\ \text{subject to}&\quad g_i(x)\leq b_i,\text{ for }i=1,\dots,m\end{align}$$where $b_i$ are limiting values.


# Special cases of convex problems
There are several special classes of convex optimization problems that lead to very efficient solutions, which are well studied and appear commonly within [[computer science]] problems.

**Problem: (Linear program)** A convex optimization problem is called a _linear program_ (LP) if both the objective function $f$ and inequality constraints, $g_i$, are affine functions; in other words the problem can be expressed as  $$\begin{align}\text{minimize}&\quad f(x)=\vec{w}^\intercal \vec{x}+b\\ \text{subject to}&\quad G\vec{x}\leq \vec{g} &&\text{(elementwise)}\\ &\quad H\vec{x}=\vec{h}\end{align}$$where $\vec{x}\in\mathbb{R}^d$, $\vec{w}\in\mathbb{R}^d$, $b\in\mathbb{R}$, $G\in\mathbb{R}^{m\times d}$,$\vec{g}\in\mathbb{R}^m$, and $H\in\mathbb{R}^{p\times d}$ with $\vec{h}\in\mathbb{R}^p$. See [[Linear programming]], and its generalization [[Semidefinite programming]].

**Problem: (Quadratic program)** A convex optimization problem is a _quadratic program_ (QP) if the objective function $f$ is convex quadratic and the inequality constraints $g_i$ are affine; that is, $$\begin{align}\text{minimize}&\quad f(x)=\frac{1}{2}\vec{x}^\intercal A\vec{x}+\vec{w}^\intercal \vec{x}+b\\ \text{subject to}&\quad G\vec{x}\leq \vec{g} &&\text{(elementwise)}\\ &\quad H\vec{x}=\vec{h}\end{align}$$where $\vec{x}\in\mathbb{R}^d$, $A\in\mathbb{R}^{d\times d}$ is symmetric positive semidefinite, $\vec{w}\in\mathbb{R}^d$, $b\in\mathbb{R}$, $G\in\mathbb{R}^{m\times d}$,v$\vec{g}\in\mathbb{R}^m$, and $H\in\mathbb{R}^{p\times d}$ with $\vec{h}\in\mathbb{R}^p$. See [[Quadratic programming]].

Examples of quadratic programs are: [[Empirical risk#Support vector machines|support vector machines]].


**Problem: (Quadratically constrained quadratic program)** A convex optimization problem is called _quadratically constrained quadratic program_ (QCQP) if both the objective function $f$ and inequality constraints $g_i$ are convex quadratic functions; that is,  is, $$\begin{align}\text{minimize}&\quad f(x)=\frac{1}{2}\vec{x}^\intercal A\vec{x}+\vec{w}^\intercal \vec{x}+b\\ \text{subject to}&\quad g_i(x) = \frac{1}{2}\vec{x}^\intercal G_i\vec{x}+\vec{r}_i^\intercal \vec{x}+s_i\leq 0,\text{ for }i=1,\dots,m\\ &\quad H\vec{x}=\vec{h}&&\text{(elementwise)}\end{align}$$where $\vec{x}\in\mathbb{R}^d$, $A\in\mathbb{R}^{d\times d}$ is symmetric positive semidefinite, $\vec{w}\in\mathbb{R}^d$, $b\in\mathbb{R}$, $G_i\in\mathbb{R}^{d\times d}$ is symmetric positive semidefinite, $\vec{r}_i\in\mathbb{R}^d$, $s_i\in\mathbb{R}$, and $H\in\mathbb{R}^{p\times d}$ with $\vec{h}\in\mathbb{R}^p$.


# Solving convex optimization problems 
