Kernels are used to estimate a random variables underlying density function (among various other applications, e.g., conditional expectation, etc.) in a [[Density estimation#Nonparametric methods|nonparametric]] fashion when the true underlying distribution is not known. See [Wiki](https://en.wikipedia.org/wiki/Kernel_(statistics)#Nonparametric_statistics), [Wiki](https://en.wikipedia.org/wiki/Kernel_density_estimation), [[@Bishop_2006]].

Kernel density estimates can be thought of as more sophisticated [[Histogram methods|histograms]] that are endowed with additional properties (e.g., smoothness) as they often rely on a indicator variable (so called bin counting method). 
![[Pasted image 20220901155429.png|500]]

The design of kernel functions is related to [[Classifiers]] in [[Overview of machine learning]] and [[Gaussian processes]].


# Introduction
The following motivates and then introduces the definition of a kernel density estimator (or Parzen–Rosenblatt window, [[@Parzen_1962]]) by first considering a binomial counting (gaussian) distribution underlying a set of observations.

Let $\vec{X}=(X_1,\dots,X_d)$ be a $d$-dimensional random vector with unknown [[Distribution functions of random variables#^c46bbe|probability density function]] $f_X(\vec{x})$ in some $d$-dimensional space (e.g., Euclidean) that we wish to estimate, and suppose we are given $N$ iid observations $\vec{x}_1,\vec{x}_2,\dots,\vec{x}_N$ from this same distribution. 

Let $A^d$ be some hypercubic region of $d$-dimensions. Then the probability mass associated with this region is given as $$P_{A^d} = \int_{A^{d}}f_X(\vec{x})\,d\vec{x}.$$
If we assume the region $A^d$ to be sufficiently small such that the probability density $f_X(\vec{x})$ is approximately constant. Then $P_{A^d}\approx f_X(\vec{x})V$, where $V$ is the volume of $A^{d}$.

For the $N$ observations we can estimate the probability of $K$ points falling into this region using the binomial distribution, $$Bin(K|N,P_{A^d}) = \binom{N}{K}P_{A^d}^K (1-P_{A^d})^{1-K},$$since each point has probability $P_{A^d}$ of falling into $A^{d}$. From this, we can calculate that $E[K/N] = P_{A^d}$, and $Var[K/N] = P_{A^d}(1-P_{A^d})/N$. Thus, for large $N$ this distribution is sharply peaked around $P_{A^d}$ and $K\approx NP_{A^d}$. 

Consequently, we can then estimate the probability density of $\vec{X}$ as $$f_X(\vec{x})\approx \frac{K}{NV}.$$
More specifically, take $A^d$ to be a hypercube of size length $h$, called the _bandwidth_ of the resulting _kernel_, centered on a point $\vec{x}$ at which we wish to derive an estimate for the probability density. 

The indicator function $$k\left(\frac{\vec{x}-\vec{x}'}{h}\right) = \begin{cases}1 & \text{ if } |\vec{x}_i-\vec{x}_i'|\leq h/2 \text{ for all } i=1,\dots,d\\ 0 & \text{ otherwise} ,\end{cases}$$will be used to count the number of observations that fall into $A^{d}$. This function is called the _kernel function_ (or Parzen–Rosenblatt window), and is said to have bandwidth $h$.

The total number of points lying inside of $A^d$ is therefore $$K = \sum_{i=1}^Nk\left(\frac{\vec{x}-\vec{x}_i}{h}\right).$$ By substituting $f_X(\vec{x})\approx K/NV$ into the above we get $$f_X(\vec{x}) \approx f^{(N)}_X(\vec{x})=\frac{1}{Nh^d}\sum_{i=1}^Nk\left(\frac{\vec{x}-\vec{x}_i}{h}\right),$$where $V=h^d$. Which can be reinterpreted, due to symmetry of $k(\cdot)$, as a sum over $N$ hypercubes centred on the $N$ observations. 

The validity of this estimate is dependent on the two opposed assumptions, that the region $A^d$ is sufficiently small such that the probability density is near constant within it and simultaneously large enough as to justify application of the binomial distribution model. Thus, the problem of selecting an appropriate $h$ value (see [[Kernel density estimators#Bandwidth selection|bandwidth selection]]), or more general selection of the kernel function itself, is key to the effectiveness of this method.


# Kernel functions and properties
Generally kernel functions can be defined in terms of any non-negative real-valued integrable function. Specifically, [[@Parzen_1962]] explored what conditions $h$ and $k$ must satisfy so that $$\begin{align*}\lim_{N\to \infty}h(N)=0 \Rightarrow &\lim_{N\to\infty}E[f^{(N)}_X(\vec{x})] = f_X(\vec{x})\\ \Leftrightarrow &\lim_{N\to\infty}E\left[\int_{\infty}^\infty\frac{1}{h(N)}k\left(\frac{\vec{x}-\vec{y}}{h(N)}\right)f(\vec{y})\, d\vec{x}\right] = f_X(\vec{x}).\end{align*}$$ 
The following theorem will provide some answers to this question.

**Theorem:** Assume $k$ is a Borel function that satisfies $\sup_{-\infty<y<\infty}|k(y)|<\infty$,  $\int_{-\infty}^\infty|k(y)|\,dy<\infty$, and $\lim_{y\to \infty}|yk(y)|=0.$ Let $g(y)$ be a faction such that $\int_{-\infty}^\infty |g(y)|\, dy<\infty$. let $\{h(N)\}$ be a sequence of positive constants with $\lim_{N\to \infty}h(N)=0$. Define $$g^{(N)}(\vec{x}) = \frac{1}{h(N)}\int_{-\infty}^\infty k\left(\frac{y}{h(N)}\right)g(\vec{x}-\vec{y})\, d\vec{y}.$$Then at every point $\vec{x}$ where $g$ is continuous we have $$\lim_{N\to \infty}g^{(N)}(\vec{x})=g(\vec{x})\int_{-\infty}^\infty k(\vec{y})\, dy.$$
From this theorem, it can be derived that the density estimates $f^{(N)}_X$ are asymptotically unbiased at all points at which the probability density function is continuous if the constants $h$ tend to zero and $k$ satisfies the conidiations requires by the theorem. 


With this said, often in practice the following definition is assumed and $h$ is chosen experimentally as a constant.

**Definition: (Kernel function)**  any non-negative real-valued integrable function, $k$, that satisfies the conditions:
   1) $k(\vec{u}) \geq 0$ for all $\vec{u}$ ,and
   2) $\int k(\vec{u})\, d\vec{u} = 1$,
 is said be a kernel function. 
 
 Symmetry of the kernel function, $k(-\vec{u})=k(\vec{u})$, can also be desirable, as it ensures the mean of corresponding distribution is close to that of the sample.

**Lemma:** If $k$ is a kernel function, then for any constant $c>0$ the function $c\cdot k(c\cdot \vec{u})$ is also a kernel. 
_Proof:_ Follows from properties of probability functions (cdfs).


## Bandwidth selection
The bandwidth of a kernel is a free-parameter that strongly influences the resulting estimate, specifically as a result of altering the sampling volume of the kernel (or whatever equivalence can be drawn for a specific kernel). Increasing the bandwidth has the affect of smoothing the resulting estimator and vice versa for reducing the bandwidth.


## Expectation and variance of estimates



# Limitations
The kernel density estimator suffers from the same discontinuities as the [[Histogram methods]] between regions. However, the selection of different kernel functions can lead to smoother density models than the latter. Another limitation of the kernel density method is that $h$ is fixed. Thus, regions of high data density, relative to the rest of the sample, may be over-smoothed; hence, the optimal choice of $h$ may be dependent on the location within the data space. Additionally, in order to perform these estimates the entire set of training observations must be maintained (stored), leading to expensive computation if the data set is large.