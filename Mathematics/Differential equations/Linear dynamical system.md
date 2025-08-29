Linear dynamical systems are [[Linear dynamical systems]] which are linear in terms of their variables and admit exact solutions. Linear dynamical systems are related to [[Network flows]]. [Wiki](https://en.wikipedia.org/wiki/Linear_dynamical_system).


# Introduction 
More specifically,

**Definition: (Linear dynamical system)** A state vector, $\vec{x}\in\mathbb{R}^d$, belongs to a linear dynamical system if its behaviour can be written in terms of a linear system of ordinary differential equations, that is, $$\frac{d}{dt}\vec{x}(t) = A\vec{x}(t)$$where $A$ is a constant matrix. Alternatively, in the discrete setting, if $\vec{x}_{t+1}=A\vec{x}_{t}$. 

There are a few special kinds of linear dynamical systems that are commonly explored.

**Definition: (Simple linear dynamical system)** If the initial vector $\vec{x}_0$ (for $t=0$) points in the direction with a (right) [[Eigenvalues and vectors|eigenvector]] $\vec{v}$ of $A$, the dynamics of the system are said to be simple with $$\frac{d}{dt}\vec{x}(t)=A\vec{v}=\lambda\vec{v}$$where $\lambda$ is the eigenvalue associated with the eigenvector $\vec{v}$.



# Methods of solving linear dynamical systems

**Theorem: (Solution to simple linear dynamical systems)** If the system considered is simple, then it admits the solution $\vec{x}(t)=\vec{v}e^{\lambda t}$, where $(\lambda, \vec{v})$ are the eigenvalue-vector pair of $A$ aligned with the initial state vector $\vec{x}_0$ of the system.

**Theorem:** Consider a linear dynamical system $\frac{d}{dt}\vec{x}=A\vec{x}$ with initial state vector $\vec{x}_0$. If $A$ can be [[Similar matrix#Diagonalizable matrices|diagonalized]], then as any vector in an $d$-dimensional space can be represented by a linear combination of the right, denoted $r_i$, and left, denoted $l_i$, [[Eigenvalues and vectors|eigenvectors]] of $A$, we can write $$\vec{x}_0 = \sum_{i=1}^d (l_i\cdot \vec{x_0})r_i.$$Consequently, the system has as a solution $$x=\sum_{i=1}^d(l_i\cdot\vec{x}_0)r_ie^{\lambda_it}$$(This can be seen as an application of the solution to simple linear systems over each eigenvector of $A$ based on the projection of $\vec{x}_0$ onto each.)

TODO - how can we write any vector in terms of the left and right eigenvectors of a diagonalizable matrix?