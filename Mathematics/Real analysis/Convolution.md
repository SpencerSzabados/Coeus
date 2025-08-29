Many functions in analysis can be represented as [[Lebesgue integration|Lebesgue integral]] (or improper Riemann integrals) of the form $$g(y) = \int_{-\infty}^\infty f(x)K(x,y)\, dx.$$The function $K$ is referred to as the _kernel_ of the transformation (just as in [[Parzen-Kernel density estimators]]). This representation is called a _integral transform_.

A convolution is a kind of [[Integral transform]] where the kernel $K(x,y)$ is defined in terms of the difference $x-y$; that is, $K(x,y)=k(y-x)$, for some function $k$. 

**Definition: (Convolution)** The convolution between two functions $f$ and $k$, both Lebesgue integral on $(-\infty,\infty)$ is equal to $$(f*k)(x)=\int_{-\infty}^\infty f(x)k(y-x)\, dx$$with $x$ taken on the set of values for which the integral exits. [[@Apostol_1973]].

Convolutions express how the shape of one function is modified by the other, in terms of sliding one over the other and forming a weighted average between overlapping (vertically) points.
