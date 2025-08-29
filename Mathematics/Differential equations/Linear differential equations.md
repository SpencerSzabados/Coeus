---
doc type: Note
authors: Spencer Szabados
date: 2024-08-18
tags:
  - differential_equations
references:
---
---

**Definition: (Linear differential equation)** A [[Ordinary differential equations#^7995af|first order ODE]] is one that can be expressed in the form $$\frac{dx}{dt} = p(t)x = g(x);$$where $x$ is dependent on $t$.


# Methods of solving linear differential equations
There are several well established methods of solving either exactly (analytically) or approximately linear differential equations. 

## Integrating factors 
The method of integrating factors relies on the form of the derivative of exponential operator.

**Method: (Integrating factors)** Given a differential equation of the form $$\frac{dx}{dt} = p(t)x - g(t).$$ The method is as follows:
  1) Create the integrating factor $\mu(t)$; a function which will allow us to transform the given function into a known integrable form upon multiplication by the integrating factor. That is, given $$\mu(t)\frac{dx}{dt} = \mu(t)p(t)x = \mu(t)g(t)$$we wish that $$\begin{align} \frac{d}{dt}(\mu x) &= \mu\frac{dx}{dt} + \frac{d\mu}{dt}x\\ &= \mu(t)p(t)x = \mu(t)g(t) \tag{above}\end{align}$$discovering that $$\mu(t) = \exp\left\{\int p(t)\, dt\right\}.$$
  2) Having constructed the integrating factor we then solve (if possible) the resulting equation for $x$. That is, $$\begin{align} &\frac{d}{dt}(\exp\left\{\int p(t)\, dt\right\} x) = \exp\left\{\int p(t)\, dt\right\}g(t)\\ \Rightarrow\quad& \mu(t)x = \int \mu(t)g(t)\, dt + C\\ \Rightarrow\quad& x(t) = \frac{1}{\mu(t)} \left( \int_{t_0}^t \mu(s)g(s)\, ds + C. \right)\end{align}$$
 