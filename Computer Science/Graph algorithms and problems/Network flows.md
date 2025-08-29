
Network flows are a class of problems concerned with transport costs over graphs. These problems may often by formulated in terms of [[Linear programming]] problems.

# Overview

# Electrical flows (networks)
A classic sub-category of network flow problems are those that are characterized by Kirchoffs law and Ohm's law of electrical flow.

**Definition: (Electrical network)** An electrical network is an undirected (typically) graph $G=(V,E)$ where each edges $e$ is modeled as a resistor with resistance $r_e$ (or weight, called _conductivity_, of $c_e=1/r_e$). Along with a voltage vector function $\phi:V\to\mathbb{R}$ that obeys Ohm's law so for any edge $uv\in R$ the voltage difference $\phi(u)-\phi(v)=f(u,v)r_{uv}$ where $f(u,v)$ is the (signed) electrical flow across the edge.

**Problem statement: (Electrical flows)** The problem of solving electrical flows can be stated as flows: Given a Electrical network (the graph along with resistance values of edges) along with a collection of input currents to vertices $\{b_u\}_{u}$, where $b_u$ has non-zero coordinate value at index $u$ and zero elsewhere, we want to solve for all the voltages across all edges and vertices in the network.

