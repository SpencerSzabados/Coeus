---
doc type: Note
authors: Spencer Szabados
date: 2023-10-08
tags:
  - numerical_approximation
  - integration
  - differential_equations
  - simulation
references: "[[@Staniforth_1991]]"
---
___

The semi-Lagrangian scheme (integration method) is a numerically stable method of  approximating the total Lagrangian time derivative of differential equations (typically fluid flow equations). Unlike true Lagrangian integration which seeks to describe a fluid by tracking the evolution of various particles through their trajectories within the fluid, the positions of which are prone to diverge from regularity thereby increase computational costs, at each time step the semi-Lagrangian scheme realigns of the tracked particles and estimates the new change in trajectory for each by interpolating the discretized Lagrangian trajectory between points along a prescribed regular Euclidian (or with modification non-uniform) grid. This resting of position and trajectory interpolation allows for the use of comparatively larger time steps that permissible for the standard Eulerian finite differences method while still remaining reasonably accurate and more computationally efficient, and simpler to implement, than the full Lagrangian scheme.sfire

# Overview 
Supposed we are given a fluid flow ODE/PDE equation (e.g., the Advection equation) say $F(x,t)$ with a constraint of the form $dx/dt=p(x,t)$. The Semi-Lagrangian scheme is a method of numerically integrating the trajectory of a particle, i.e., the evolution of its distribution, subject to the vector field $F$ over a course set of grid points without constraining either the particle's origin or intermediate trajectory locations to one (or only) of the grid points after each time step. This is done by integrating a straight line path (or other curve) interpolation of the true trajectory from nearby grid point.

The semi-Lagrangian scheme is typically applied to conservative quantities (physical), in particular linear advection equations.

**Definition: (Linear Advection equation)** The advection equation models the drift (left and right transport) of a particle's density, say $p(x,t)$, within a fluid, i.e., it is a special case of the [[Diffusion models#^083a90|Folker-Planck equations]], which is assumed to only change according to the convection equation: $$p(x,t+\Delta t) = p(x-d(\Delta t), t).$$Expanding this via [[Taylor series]] gives the Euclidian formulation of the advection equation: $$\frac{\partial p}{\partial t}+d\frac{\partial p}{\partial x}=0,$$where velocity $d$ is assumed constant above, with initial condition of the form $p_0(x) = p(x,0)$. This has the general (uniquely determined) solution, formulated in terms of the characteristic), $$p(x,t) = p_0(x-dt).$$This system is typically re-expressed using [[Characteristic curves]] into the so called Lagrangian form. Expanding via the chain rule, implicitly assuming $x$ and $t$ vary in terms of a third parameter (curve) $s$, gives $$\frac{d p}{ds} = \frac{\partial p}{\partial t}\frac{\partial t}{\partial s}+\frac{\partial x}{\partial s}\frac{\partial p}{\partial x}=0$$where we take $$\frac{\partial t}{\partial s} = 1 \quad\text{ and }\quad \frac{\partial x}{\partial s} = d.$$This admits the same general solution as before, with the initial condition $$s(0) = p_0(x_0).$$See [uni-muenster Advection equation](https://www.uni-muenster.de/imperia/md/content/physik_tp/lectures/ws2016-2017/num_methods_i/advection.pdf).

A common choice is to reparametrize the Advection equation with $x=x(t)$ and $t=t$, when possible, to get the simple Lagrangian form $$\frac{dp}{dt}= 0,$$with the physical interpretation that the transport of $p$ is constant for a single particle.


## Semi-Lagrangian approximation scheme 


Assume we have access to a prescribed set of regular grid points, of the form $$(x_i,t_j)\in\{(x,t)\mid x\in \{x_0,\dots,x_M\}\text{ and }t\in\{t_0,\dots,t_N\}\}$$which are laid over the function domain, where the values $p(x_i,t_j)$ are known or can be well approximated; .e.g., the grid, or rather the step size, is typically chosen so the values $p(x_i,t_j)$ are well approximated using a Eulerian finite difference method over the regular grid. The exact trajectory (up to approximation error) of a fluid particle $x$ that does not traverse identically through the grid points 
 



