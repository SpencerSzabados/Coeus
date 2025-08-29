Gradient decent methods are used to solve many different optimization problems that can be phrased in terms of derivatives (or finite step changes), e.g., [[Supervised learning#^444aa0|empirical risk minimization]] as used in [[Overview of machine learning|machine learning]].

# Gradient decent
Gradient decent (also know as _steepest decent_) is an iterative optimization procedure.

Consider the problem of wanting to optimize a differentiable function $f:\mathbb{R}^d\to \mathbb{R}$ for the minimum value. Let $\vec{x}_0$ be our initial guess at the location of the minimizing value. We aim to construct a new point $\vec{x}_1$, that achieves a lower function value, by moving along the direction $\vec{v}$ (one of possibly many directions of similar behaviours) in which $f$ decreases in value.

**Definition: (Direction of decent)** A vector $\vec{v}$ points in a direction of decent relative to and initial starting point $x_0$ for a function $f$, if $f(\vec{x}_0+t\vec{v})<f(\vec{x}_0)$ for some $t>0$.

By application of [[Taylor series]] about $\vec{x}_0$ in the case where $f$ is has a continuous first derivative, we have for a sufficiently small step size $h$ $$f(\vec{x}_0+h \vec{v}) \approx f(\vec{x}_0)+h\nabla f(\vec{x}_0+h\vec{v})^\intercal \vec{v}$$and $\nabla f(\vec{x}_0+h \vec{v})<0$ so that $f(\vec{x}_0+h\vec{v})<f(\vec{x}_0)$. Thus, if $\vec{v}^\intercal \nabla f(\vec{x}_0)<0$ then $\vec{v}$ is a direction of decent.

Recall, a point $\vec{x}^*$ is a local minimizer if and only if $\nabla f(\vec{x}^*)=0$, and that $-\nabla f(\vec{x})$ is always a decent direction since $-\nabla f(\vec{x})^\intercal \nabla f(\vec{x})<0$.

**Algorithm: (Gradient descent)** Given an initial point $\vec{x}_0\in \mathbb{R}^d$. At each stage $t=0,1,2,\dots$ 
  1) Choose a step size $h_t>0$, and
  2) Set $\vec{x}_{t+1}=\vec{x}_t-h_t\nabla f(\vec{x}_t)$.
Stop iterating once $\|x_t-x_{t-1}\|<\epsilon$ for some chosen $\epsilon$.


## Application to convex optimization 
In the case where the function being optimized is [[Convex optimization|convex]], gradient decent is guaranteed to converge to the [[Convex optimization#^e55e01|global minimizer]].

**Theorem: (Convex gradient descent)** Let $f:\mathbb{R}^d\to \mathbb{R}$ be a [[Convex functions#^b246dc|convex function]]. Gradient decent is guaranteed to converge to the global minimizer.
_Proof:_ Recall, a point $x^*$ is a global minimizer of a convex function $f$ if and only if $\nabla f(x^*)=0$. See p(74)[[@Hardt_2022]].

(TODO - add (p78)[[@Hardt_2022]])


# Stochastic gradient descent 
Stochastic gradient descent is a version of the gradient decent method that uses stochastic selection to determine which updates are performed at each step, opposed to the block (batched) updates executed under normal gradient decent. The intuitive justification for doing so, is that by following a descent vector in expectation, we should be able to closely approximate the optimal solution after sufficiently many iterations.

Stochastic gradient descent is one of the most popular methods in machine learning, as it is effectively a generalization of the classic [[Perceptrons|perceptron learning rules]]; the method is also be seen as equivalent to backpropagation in neural networks.


**Algorithm: (Stochastic gradient descent)** Given an initial point $\vec{x}_0\in \mathbb{R}^d$. At each stage $t=0,1,2,\dots$ 
  1) Choose a step size $h_t>0$ and a random training point $\vec{x}_i$, then 
  2) Set $\vec{x}_{t+1}=\vec{x}_t-h_t\nabla f(\vec{x}_t)$.
Stop iterating once $\|x_t-x_{t-1}\|<\epsilon$ for some chosen $\epsilon$.


A limitation of stochastic gradient decent is that without additional assumptions on the function being optimized we can't expect exponential convergence rate, like see from standard gradient decent on convex functions.

 There are serval standard methods for improving the performance of stochastic gradient descent, see the following sections.


## Convex optimization
Suppose we are attempting to optimize a [[Convex functions|convex function]] $f:\mathbb{R}^d\to \mathbb{R}$ with optimal solution $\vec{x}^*$. For the sake analysis, suppose at each iteration of SGD we have access to a stochastic function $g(\vec{x},\vec{U})$ which depends on a random direction vector $\vec{U}$, such that $$E_\vec{U}[g(\vec{x},\vec{U})]=\nabla f(\vec{x}).$$ Additionally, assume a bound of $\|g(\vec{x},\vec{U})\|\leq b$.

Gradient decent iteration can then be studied by considering the update rule $$\vec{x}_{t+1} = \vec{x}_t-h_t g(\vec{x}_t,\vec{U}_t),$$for some iid sequence $\{\vec{U}_t\}$ taken from a predetermined distribution.

To begin we can calculate the distance between any iteration value to the optimal as $$\begin{align}\|\vec{x}_{t+1}-\vec{x}^*\|^2 &= \|\vec{x}_t - h_tg(\vec{x}_t,\vec{U}_t)-\vec{x}^*\|^2\\ &= \|\vec{x}_t-\vec{x}^*\|^2-2h_t\langle(\vec{x}_t,\vec{U}_t),\vec{x}_t-\vec{x}^*\rangle+h_t^2\|g(\vec{x}_t,\vec{U}_t)\|^2.\end{align}$$
By iterated expectation and independence of each $\vec{U}_i$ it can be see that $$\begin{align}E[\langle g(\vec{x}_t,\vec{U}_t),\vec{x}_t-\vec{x}^*\rangle] &= E[E_{\vec{U}_t}[\langle g(\vec{x}_t,\vec{U}_t),\vec{x}_t-\vec{x}^* \rangle\mid \vec{U}_0,\dots,\vec{U}_{t-1}]]\\ &= E[\langle E_{\vec{U}_t}[g(\vec{x}_t,\vec{U}_t)\mid \vec{U}_0,\dots,\vec{U}_{t-1}],\vec{x}_t-\vec{x}^*\rangle]\\ &= E[\langle\nabla f(\vec{x}_t),\vec{x}_t-\vec{x}^*\rangle],\end{align}$$which allows for us to replace the stochastic gradient with the true gradient. It follows that $$E[\|\vec{x}_{t+1}-\vec{x}^*\|]\leq E[\|\vec{x}_t-\vec{x}^*\|]-2h_tE[\langle\nabla f(\vec{x}_t),\vec{x}_t-\vec{x}^*\rangle]+h_t^2 b^2.$$Now define the sum of all step sizes up to iteration $t$ by $H_t = \sum_{i=0}^t h_t$, and define the average of the weighted iterates $\bar{x}_t = \frac{1}{H_t}\sum_{i=0}^t h_i\vec{x}_i$. Additionally, define $\rho_t = \|\vec{x}_t-\vec{x}^*\|$.

We will analyze the deviation between $f(\bar{x}_t)$ and the optimal value of $f(\vec{x}^*)$. Observe $$\begin{align}E[f(\bar{x}_t) - f(\vec{x}^*)] &\leq E\left[\frac{1}{H_t}\sum_{i=0}^t h_i(f(\vec{x}_i) - f(\vec{x}^*))\right] &&\text{($f$ is convex)}\\ &\leq \frac{1}{H_t}\sum_{i=0}^t h_tE[\langle\nabla f(\vec{x}_t),\vec{x}_t-\vec{x}^* \rangle] &&\text{(linearity of expectation and convexity of $f$)}\\ &\leq \frac{1}{2H_t}\sum_{i=0}^t\left(\|\vec{x}_t-\vec{x}^*\| - \|\vec{x}_{t+1}-\vec{x}^*\| + h_t^2b^2\right) &&\text{(above inequality)}\\ &= \frac{\|\vec{x}_0-\vec{x}^*\|-\|\vec{x}_{t+1}-\vec{x}^*\|+b^2\sum_{i=0}^t h_i^2}{2H_t}\\ &\leq \frac{\rho_0^2+b^2\sum_{i=0}^t h_i^2}{2H_t}. \end{align}$$
The above analysis, taken from (p86)[[@Hardt_2022]], underpins the following theorem.

**Theorem:** Suppose we run SGD on a convex function $f$ that has a minimum value $m$ for $T$ steps with fixed step size $h$. Let $\vec{x}_0$ be the initial starting value, $\rho_0 = \|\vec{x}_0-\vec{x}^*\|$, $b\geq 0$ be a bound on the stochastic gradient, and define the optimal values $h_{opt} = \rho_0/b\sqrt{T}$ and $\theta = h/h_{opt}$. Then $$E[f(\bar{x}_t) - f(\vec{x}^*)]\leq \frac{1}{2}\left(\theta+\frac{1}{\theta}\right)\frac{b\rho_0}{\sqrt{T}}.$$
The above theorem states that for constant step sizes we expect to pay in extra steps the difference between the optimal step size and that selected.  


## Data shuffling
In practice it is often more performant to randomly permute (order) the training data points and running SGD in the precomputed random order, rather than randomly sampling each gradient with replacement at run time. This method helps when training data are highly correlated. (Research into selection methods for SGD remains underway.)


## Step size selection methods
Step size selection in SGD is a much debated problem.

**Method: (Rule of thumb decay)** A rule of thumb that works quite well in practice is to simply pick the largest step size that does not result in the method diverging away from the solution. This can be tuned by iteratively reducing the step size from an initial large estimate until the method being to converge. While this method is not necessarily optimal it often proves significantly better than random initialization.

**Method: (Fractional step decay)** The step size used it typically reduces after a fixed number of passes over the training data, each of which is called an _epoch_. A common strategy to decide when to reduce the step size is to run with a constant step size for a predetermined number of iterations $T$, and then reduce the step size by a constant factor $\Delta$, often chosen between $0.8$ and $0.9$. The step size $h_k$ for the $k$-th epoch is then given as $h_k=\Delta^{k-1}h_k$. 

Another common method, called _epoch doubling_, is to first run $T$ steps with step size $h$, then run $2T$ steps with step size $h/2$, and then $4T$ steps with step size $h/4$, etc.


## Batching 
One method used to take advantage of parallelism in computing is to take averages of many stochastic gradients. Suppose at each iteration we sample a _batch_ $B_t$ (subset) of $m$ data points. The update rule in SGD then becomes $$\vec{x}_{t+1}=\vec{x}_t-h_k\frac{1}{m}\sum_{j\in B_t}\nabla f(\vec{x}_j).$$This method has the effect of reducing the variance of the stochastic gradient estimate of the true gradient value at each iteration, therefore, tending to produce a superior gradient decent direction. This comes at the cost of computation time.


## Momentum methods
Momentum based direction mixes the current gradient direction with that from the previous step. The idea being if the previous direction was good in the global sense, we may benefit, in the form of reduce osculation in convergence, by turning more gradually. The update rule then becomes $$\vec{x}_{t+1} = \vec{x}_t -h_t\nabla f(x_t)+\Delta(\vec{x}_t+\vec{x}_{t-1}),$$from some mixing constant $\Delta$ typically chosen between $0.8$ and $0.95$.

In practice, this method can provide significant speed up to convergence.


# Conjugate gradients  
