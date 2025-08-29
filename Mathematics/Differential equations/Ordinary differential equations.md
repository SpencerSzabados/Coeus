---
doc type: Note
authors: Spencer Szabados
date: 2024-08-03
tags:
  - differential_equations
  - review
  - real_analysis
references:
  - lecture_notes
---
---

**Definition: (Differential equation)** An equation containing the derivative of one (or more) dependent variable(s) wrt one (or more) independent variable(s) is called a _differential equation_.

**Definition: (First order differential equation)** A first order differential equation can be represented as $$\frac{dx}{dt} = f(t,x)\quad \tag{normal form.}$$where $x$ depends on $t$, with the exact argument $x(t)$ supressed. ^7995af

A solution to a (first order) differential equation (above) on a prescribed interval (support) $I=(a,b)$ is a function $\phi\in C^1(I,\mathbb{R})$ s.t. $(t,\phi(t))\in D\subseteq \mathbb{R}^2$ and for all $t\in I$ $$\frac{d}{dt}\phi(t) = f(t,\phi(t)).$$ ^3dd249

**Definition: (Initial value problem)** Given a domain $D\subseteq \mathbb{R}^2$ and $(t_0,x_0)\in D$ the _initial value problem_ for $$\frac{dx}{dt}=f(t,x)$$ is to find $\phi\in C^1(I,\mathbb{R})$ s.t. $\frac{d}{dt}\phi = f(t,\phi)$ and $\phi(t_0)=x_0$ or equivalently $$\phi(t) = \phi(t_0)+\int_{t_0}^tf(s,\phi(s))\, ds;$$however, this integral might be difficult or impossible to integrate analytically, so there exists a number of different techniques to find classes of solutions (under different assumptions). ^053777


 
 