---
doc type: Note
authors: Spencer Szabados
date: 2024-09-03
tags:
  - differential_equations
  - initial_value_problems
  - separable_equations
references:
  - lecture_notes
  - https://www.ncl.ac.uk/webtemplate/ask-assets/external/maths-resources/core-mathematics/calculus/homogeneous-first-order-differential-equations.html
---
---

**Definition: (Separable equation)** A [[Ordinary differential equations#^7995af|first order ODE]] is _separable_ if it can be expressed in the form $$\frac{dx}{dt} = f(t,x) = g(t)h(x);$$

To solve a separable first order ODE of the above form there is a general procedure: 
  1) Express the equation in the form $$\frac{1}{h(x)}\frac{dx}{dt} = g(t);$$
  2) Integrate (1) wrt. $t$ $$\int\frac{1}{h(x)}\frac{dx}{dt}\, dt = \int g(t)\, dt$$ and apply change of variables with $u=g(t)$ to simply the above to $$\int \frac{1}{h(u)}\, du = \int g(t)dt\Leftrightarrow\int \frac{1}{h(x)}\, dx = \int g(t)\, dt;$$
  3) Compute the integral (if possible) to get an equation of the form $$H(x)=G(t)+C$$where $H$ and $G$ are anti-derivatives of $1/h$ and $g$ respectively and $C$ is a constant of integration that can be determined based on the [[Ordinary differential equations#^053777|initial value problem]]. 
  4) Solve Eq.(3) for $x$ (if possible) and compute the value for $C$.

There are different classes of separable equations each of which has some additional (assumptions) techniques for solving it. 

**Definition: (Homogeneous equation)** A ODE is said to be a homogeneous equation of order $n$ if it can be expressed in the form $$\frac{dx}{dt} = f(t,x)=t^{n}g(u)$$with $u=x/t$. For [[Ordinary differential equations#^3dd249|first order ODE]], which are homogeneous of order zero, this form simplifies to $\frac{dx}{dt} = g(u)$. More generally, a differential equation of the form $$p(t,x)dt +q(t,x)dx = 0,$$ with $p$ and $q$ homogeneous of order $n$, can be made separable by substitution of $x=ut$ where $$dx=udt+tdu.$$

