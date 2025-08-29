Ridge functions are family of functions built by composing various univariate functions together; [[Activation functions]] are a form of ridge function. Ridge functions, in one interpretation, form the basis of [[Projection pursuit density estimation]].


# Overview
**Definition: (Ridge function)** Let $\theta_0$ be a nonzero vector, called the _direction vector_, and $\theta_1,\dots,\theta_{d-1}$ be a list of $d-1$ linearly independent vectors that are all orthogonal to $\theta_0$ (i.e., they span $d-1$ dimensions). Then any function $f:\mathbb{R}^d\to \mathbb{R}$ of the form $$f\left(x+\sum_{i=1}^{d-1}c_i\theta_i\right)=g\left(x\cdot \theta_0+\sum_{i=1}^{d-1}c_i\theta_i\cdot \theta_0\right)=g(x\cdot \theta_0)=f(x)$$where $g:\mathbb{R}\to\mathbb{R}$, is a ridge function; it may be assumed WLG that $\|\theta_0\|=1$. See [Wiki](https://en.wikipedia.org/wiki/Ridge_function), [EMath](https://encyclopediaofmath.org/wiki/Ridge_function#References). 

In the simplest case, a ridge function if it can be written as the composition (in argument) of a univariate function with a [[Affine transformation matrix|affine transformation]].

**Observation:** A ridge function, $f$, by construction is constant on the set $\{x\mid \theta_0\cdot x = t\}$ for any $t$. 

This corresponds to the set of input vectors whose projection onto the direction vector $\theta_0$ is constant, meaning all inputs within such a set point with the same magnitude towards $\theta_0$; i.e., $\{x\mid \theta_0\cdot x=t\}$ is a hyperplane.

**Definition: (Affine ridge function)** let $\Theta:\mathbb{R}^d\to\mathbb{R}^m$ be a [[Linear transformations|linear map]] and $g:\mathbb{R}^m\to \mathbb{R}$ be a univariate function. Then $$f(x)=g(\Theta x)$$is called a _affine ridge function_.


# Radon transformations
An useful transformation that shows up in the use of ridge functions is Radon transformations. The inverse of a Radon transformation can be used to reconstruct [[Distribution functions of random variables#^c46bbe|density functions]] from projected data (e.g., [[Projection pursuit density estimation]]).

**Definition: (Radon transformation)** Let $\theta\in S^{d-1}$ be a unit vector from the hypersphere of $d$ dimensions representing the direction of the ensuing transformation and let $t\in\mathbb{R}$ be the translate (the size of the translation). The Radon transformation of a function $f:\mathbb{R}^d\to\mathbb{R}$ is defined as the surface integral over the hyperplane $H_\theta = \{x\mid \theta\cdot x=t\}$, $$RT(f,\theta,t) = \int_{H_\theta}f(x)\,dx = \int_{H_\theta^\perp}f(t\theta+z)\, dz,$$where $H_\theta^\perp$ is the [[Orthogonal complement]] of $H_\theta$. The second equation, which is somewhat unintuitive in its equivalence at first, can be seen as performing the surface integral over the plane perpendicular (orthogonal) to $\theta$ at each point along the line determined by $t\theta$. See [Wiki](https://en.wikipedia.org/wiki/Radon_transform). ^789e2b

For ridge functions, this transformation simplifies integral computations. If $f$ is a ridge function, then $$\int_{\mathbb{R}^d}g(\theta\cdot x)f(x)\, dx = \int_{\mathbb{R}}g(t)RT(f,\theta,t)\, dt.$$Thus, we have "shifted" the dimensionality of the above integral into the computation of Radon transformation of $f$. In particular, $$\int_{\mathbb{R}^d}f(x)\, dx = \int_{\mathbb{R}}RT(f,\theta,t)\, dt.$$This transformation is seemingly similar to the derivation of a [[Distributions along projections|projected marginal distribution]], see [StackExchange-rezoons](https://math.stackexchange.com/a/4188534), and it is likely for this reason that it forms the basis of the method of projection pursuit.


## Function reconstruction via Tikhonov regularization 
The next question to ask is, if the Radon transformation has an inverse that can be exactly computed? That is, given a Radon transformation $RT(f,\theta,t)$ for some $\theta\in\Omega$ and all $t\in\mathbb{R}$ can be reconstruct $f$ exactly? If $\Omega= S^{d-1}$, meaning we have access to all transformations on the unit sphere, then $f$ can be exactly reconstructed. However, empirically we typically only have a sample of transformations with $\Omega=\{\theta_1,\theta_2,\dots,\theta_N\}\subset S^{d-1}$, in which case exact reconstruction is no longer possible and we must approximate $f$ from the available information. 

[[Regularization#Tikhonov regularization|Tikhonov regularization]] can be used to approximate the solution to the problem of finding and $f$ such that $$\min_{h:\mathbb{R}^d\to \mathbb{R}}\|h\|_2$$subject to $$RT(h,\theta,t)\approx RT(f,\theta,t).$$
The solution produced by this method is a Ridge network of the form $$h(x) = \sum_{i=1}^N g_i(\theta_i\cdot x)$$where $g_i$ is a Ridge function (as above). 

A secondary question then becomes, for a give number of possible observations, say $N$, how can we best select the set $\Omega$ such that the resulting observed transformations enable increased accuracy in reconstruction of $f$; that is, how can be select $\theta$ to generate a more accurate inverse transformation. 