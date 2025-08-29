---
doc type: Note
authors: Spencer Szabados
tags:
  - machine_learning
  - kernel_machines
  - kernel_methods
  - statistical_learning
references:
  - http://www.kernel-machines.org/
---
---

[[Knowledge representation and features#Transformation lift methods|Transformation (lift) methods]] reduce the problem of constructing nonlinear predictors to a search for a linear decision boundary by embedding the data it into a higher dimensional space via a nonlinear transform. One such method, called kernel methods, attempt to avoid excessive growth in dimensionality by constraining the prediction function search space to a low dimensional subspace that lies in the [[Vector space#^318dc4|span]] of the training data. 

Kernel representations also translate into simple algorithms with bounded complexity,  due to the restriction placed on the predictors; unfortunately, this bound is often dependent on the amount of data used to train the model and its dimensionality. 

In the case of linear predictors, the primary area of kernel methods, the span of the training data is a natural and good choice. In fact this choice is optimal for most prediction optimization problems as a result of the _representer theorem_. In this setting, any vector can be written as a linear combination of vectors from the span of the training data and a (set of) mutually orthogonal vector(s); in particular, we can suppose the weight vector to be of the from$$\vec{w} = \sum_{i=1}^N \alpha_ix_i+v,$$where $v$ is mutually orthogonal to all $x_i$. Then $$\hat{y_i} = w^\intercal x_i = \sum_{j=1}^N\alpha_jx_j^\intercal x_i,$$and we see $v$ disappears in the expression for in-sample prediction calculations. Moreover, a prediction result is simply a function of the dot products between training values.

More generally, this notion can be expressed in terms of [[Parzen-Kernel density estimators#General Kernel functions and properties|kernels]].

**Definition: (Feature map kernel)** let $\Phi(\vec{x})$ denote any lifting function. Then $$k(\vec{x},\vec{z}) = \Phi(\vec{x})^\intercal \Phi(\vec{z})$$is the _kernel function_ associated with the feature map $\Phi$.
^38edf1

Kernel functions of this form, for any training data $S=\{\vec{x_1},\dots,\vec{x_N}\}$, gives rise to a positive semidefinite matrix with entries given by $$K_{ij} = k(x_i,x_j).$$
As it turns out this property in conjunction with symmetry is sufficient for constructing (select) kernel functions. 

**Lemma:** A symmetric function $k:\mathbb{R}^d\times \mathbb{R}^d \to \mathbb{R}$ is a kernel function if it gives rise to a positive semidefinite matrix with entries $K_{ij} = k(x_i,x_j)$.

**Lemma:** The nonnagative linear combination of kernel functions remains a kernel function. That is, given two kernel functions $k_1$ and $k_2$, the function $k=c_1k_1+c_2k_2$, for $c_1,c_2\geq 0$, is a kernel function. 
_Proof:_ This follows from properties of positive semidefinite matrices.


Continuing were we left off, the predictor functions within the considered subspace take the general form $f(x)=w^\intercal \Phi(x)$ for $w = \sum_{i=1}^N \alpha_i\Phi(x_i)$ so $$f(x) = \left(\sum_{i=1}^N \alpha_i\Phi(x_i)\right)^\intercal \Phi(x) = \sum_{i=1}^N \alpha_i k(x_i,x).$$Therefore, the problem of optimizing predictors based on kernels can be posed in terms of finding the best values for coefficients $\alpha_i$ for $i=1,\dots,N$.


This reduced form of $f$ allows for simple algorithmic implementations/statements for optimizing kernel functions. Moreover, we might be able to calculate the above without having the explicitly compute the feature embedding transformation if we know the expression of the kernel $k$. 


#### Optimization of kernel method
There exists many possible choices for $k$ within the same feature sets, so how does not determine a good selection? The norm of the kernel function, $f$, can be a good indicator (TODO - explain why this is the case.).

As alluded to above, functions learned by [[Supervised learning#^f14fbf|Empirical risk minimization]] (ERM) methods on kernel spaces result in weighted sums of the dot products between training data points. (It is perhaps worth nothing that if $\alpha_i\geq 0$ for all $i$ then as $K$ is positive-semidefinite $f$ will be convex and thus readily approachable using convex optimization techniques.)


#### Polynomial kernels

**Theorem: (Polynomial kernel)** For $a,b\geq 0$ and $p\in \mathbb{Z}^+$, $$k(\vec{x},\vec{z}) = (a+b\vec{x}^\intercal \vec{z})^p$$is a kernel function. This kind of kernel functions are called a _polynomial kernel functions_.
_Proof:_ Follows from the above lemmas. It follows that, for each polynomial kernel function, there exists a lifting function $\Phi$ with each coordinate of $\Phi$ being a monomial such that $k(\vec{x},\vec{z})=\Phi(\vec{x})^\intercal \Phi(\vec{z})$.


#### Taylor series kernels
[[Knowledge representation and features#Polynomial kernels|polynomial kernels]] can be generalized naturally using [[Taylor series]].

In particular, notice that $\langle x,z\rangle^p$ is a kernel function. Then it follows for any one-dimensional function $h$ that possesses a convergent Taylor series for $t\in [-r,r]$ $$h(t)=\sum_{i=1}^\infty a_it^i$$with $a_i\geq 0$ for all $i$, that $$k(x,v)=h(\langle x,z\rangle)$$is a kernel function. The feature space of this kernel is the span of the monomials of all degrees with non-zero $a_i$ coefficients.

One of the more influential kernels is the Gaussian kernel function, or more generally the [[Families of distributions#Exponential family of distributions|exponential family of distributions]] kernel, which is equal to $$k(x,z) = \exp(-\gamma\|x-z\|^2 /2).$$
