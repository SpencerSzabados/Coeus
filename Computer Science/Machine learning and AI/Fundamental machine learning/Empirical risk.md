Empirical risk is formulated in terms of a [[Supervised learning]] problem, where we have access to a large set of matched (correct) training values.

Assume for the remainder that $L:\mathcal{Y}\times \mathcal{Y}\to \mathbb{R}$ is our loss function, where $\mathcal{Y}$ is the set of values the discrete random variable $Y$ can take on. Let $\hat{Y}=f(X)$ be the assumed form the the predictor, where $f:\mathcal{X}\to \mathcal{Y}$ is a function that maps the sample space $\mathcal{X}$ into the label space $\mathcal{Y}$. The risk to be minimized is then $R[f] = E[L(f(X),Y)]$, and is taken over all loss functions $f\in\mathcal{F}$.

**Definition: (Empirical risk of a predictor)** Given as set of labeled data points $S=\{(x_1,y_1),\dots,(x_N,y_N)\}$, the _empirical risk of a predictor_ $f:\mathcal{X}\to\mathcal{Y}$ with respect to the sample $S$, is the finite sample risk:
$$R_S[f] = \frac{1}{N}\sum_{i=1}^N L(f(x_i),y_i).$$

# Empirical risk minimization
Empirical risk minimization can be formalized as follows.

**Problem: (Empirical risk minimization)**  Given a function class $\mathcal{F}$ of functions from $\mathcal{X}$ to $\mathcal{Y}$, _empirical risk minimization_ of a set of labeled data points $S$ seeks to find a function $f\in\mathcal{F}$ that satisfies  $$R_S[f] = \min_{g\in\mathcal{F}}R_S[g].$$  ^444aa0

We can see from the trivial relation $$R[f] = R_S[f]+(R[f]-R_S[f])$$that minimizing empirical risk is only one component of the problem of global (population) risk minimization. We must also consider the quantity $R[f] - R_S[f]$, which is important enough to get a name.

**Definition: (Generalization gap)** The difference $$\Delta_{gen} = R[f]-R_S[f],$$ for a predictor $f$, is called the _generalization gap_. See [[Generalization]]. ^0b48ca

This term quantifies how much the empirical risk underestimates the actual risk, and serves to summarize how well the performance of the predictor can be expected to perform (generalize) to unseen examples. 


## Replacing zero-one loss 
The zero-one (LRT) [[Fundamentals of prediction#^5732be|loss function]] $$L(\hat{y},y) = \mathbb{1}\{\hat{y}y<0\},$$as used in [[Perceptrons]] see [[Fundamentals of prediction#^d0c89c]], turns out to be a poor choice when attempting to optimize using [[Gradient decent]] methods, since the gradient is zero almost everywhere. 

Thus, in practice the zero-one loss functions is often replaced by a _surrogate loss function_ that is easier to optimize. Popular choices being select [[Convex functions]], for which there are many. 

### Support vector machines
The support vector machine is based around implementing explicit [[Curve fitting#Regularization|regularization]] decisions in optimization, as there are explicit decision rules used to inform the optimization process.

Consider a binary prediction question with labels $y\in \{-1,1\}$. As before, we desire a vector $\vec{w}\in \mathbb{}R^d$ that satisfies $$\begin{cases}\vec{w}^\intercal x_i>0 & \text{ for } y_i=1\\ \vec{w}^\intercal x_i<0 &\text{ for } y_i=-1 \end{cases}$$for all $i=1,2,\dots,N$; i.e., $\vec{w}$ defines a half-space where all data points within it are matched to $1$ label value.

Now, rather than attempting to [[Classification and clustering|classify]] all the training values exactly we make allowance for mismatched examples by instead attempting to minimize the _support vector machine objective_ quantity$$SVM = \sum_{i=1}^N \max\{1-y_i\vec{w}^\intercal x_i,0\}$$over $\vec{w}$, where we pay a penalty of $1-y_i\vec{w}^\intercal x_i$ for training points that are mismatched by $\vec{w}$; this loss function is called _hinged loss_. (TODO - when you use a different loss function is it still called a support vector machine?)

We can compute the gradient of this objective function (SVM)wrt $\vec{w}$ to be $$\nabla SVM = -\sum_{i=1}^N \mathbb{1}(y_i\vec{w}^\intercal x_i\leq 1)y_ix_i.$$
Application of gradient decent methods using this loss function and decent vector is immediate.


### Logistic regression
TODO - update note [[Logistic regression]] $$L(\hat{y},y)=\log(1+e^{-\hat{y}y})$$can interpreted as an approximation of the error-counting zero-one loss function.


## Implicit convexity of empirical risk
Empirical risk optimization problems include a implicit form of convexity in which predictions should converge to a global optimum even if the optimum value can't be directly analyzed using convex analysis methods.

Assume we are attempting to minimize the risk of a predictor from a class of parametrized functions $\{f(\vec{x},\vec{w})\mid w\in\mathbb{R}^d\}$ with respect to a nonnegative loss function $L$ that satisfies $L(\hat{y},y)=0$ when $\hat{y}=y$. In this case, $0\leq R_S[\vec{w}]$ for all $\vec{w}$. Thus, a minimizing solution to $f(\vec{x}_i,\vec{w})=y_i$ for all $i$ is also a global minimum. 

Let $(\hat{y}_1,\dots,\hat{y}_N)=f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})$ denote the $N$ predictions for training values $\{(\vec{x}_1,y_1),\dots,(\vec{x}_N,y_N)\}$. For specificity, take $L$ to be the squared loss, that is $$L(f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}),(y_1,\dots,y_N))=\frac{1}{2}\|f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N)\|^2.$$This objective might be nonconvex as we are not assuming convexity of $f$. Running gradient decent on the weight vector (parameters) gives the update rule $$\vec{w}_{t+1} = \vec{w}_t-h \mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)(f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N)),$$where $\mathbb{J}$ is the Jacobian operator taken with respect to $\vec{w}$. Let $\mathbb{H}$ be the Hessian matrix of $f$ taken with respect to $\vec{w}$. By [[Taylor series|Taylors theorem]] we can write $$\begin{align}\hat{y}_{t+1} &= f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_{t+1})\\ &= f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)+\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)^\intercal(\vec{w}_{t+1}-\vec{w}_t)\\&+\int_0^1\mathbb{H}(\vec{w}_t+u(\vec{w}_{t+1}-\vec{w}_t))(\vec{w}_{t+1}-\vec{w}_t,\vec{w}_{t+1}-\vec{w}_t)\,du.\end{align}$$Then by the above gradient decent relation the above can be rewritten as $$\begin{align}\hat{y}_{t+1} &= f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_{t+1})\\ &= f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)+-h\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)^\intercal\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)(f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N))\\&+h\int_0^1\mathbb{H}(\vec{w}_t+u(\vec{w}_{t+1}-\vec{w}_t))(\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)((f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N)),\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)((f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N)))\,du.\end{align}$$The reducing to $$\begin{align}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_{t+1})-(y_1,\dots,y_N) &= (I-h\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)^\intercal\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t))(f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N))\\ &+ h\int_0^1\mathbb{H}(\vec{w}_t+u(\vec{w}_{t+1}-\vec{w}_t))(\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)((f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N)),\mathbb{J}f(\vec{x}_1,\dots,\vec{x}_N,\vec{w}_t)((f(\vec{x}_1,\dots,\vec{x}_N,\vec{w})-(y_1,\dots,y_N)))\,du.\end{align}$$If the last integral terms vanishes (or is sufficiently small) the predictions will converge to the training labels as long as the eigenvalues of the Jacobian-Jacobian product are strictly positive. See (p92)[[@Hardt_2022]].

(TODO - under what conditions does this occur? Explain exactly how this related to convexity by comparing the form of the equation and talking about positive definite properties of the jacobian.)

In practicality, this will likely be the case if we can ensure the Jacobian matrix are full rank most of the time (for most values and under stochastic gradients) and our chosen step size is not to large. If the number of parameters used in $f$ is larger than the number of data points (overparametrized model) the Jacobians are likely to be positive definite.


## Optimization via stochastic gradient decent
The justification for utilizing [[Gradient decent#Stochastic gradient descent|stochastic gradient descent]] in minimizing empirical risk, i.e., fitting a vector by way of loss minimization, is that the gradient of a sum is the sum of gradients of the summands. Additionally, from the above sections [[Empirical risk#Replacing zero-one loss|Replacing zero-one loss]] and [[Empirical risk#Implicit convexity of empirical risk|implicit convexity of empirical risk]] there is reason to believe the method will perform well in many cases.

The specific formulation of stochastic gradient decent for empirical risk minimization is the following.

**Algorithm: (Stochastic empirical risk optimization)** Let $f(\vec{x},\vec{w}])=\vec{w}^\intercal \vec{x}$ be a $d$-dimensional linear classifier, and $\vec{w}_0\in \mathbb{R}^d$ be an initial weight vector. At each step $t=1,2,\dots$
  1) Choose a step size $h_t>0$ and a random training data point $\vec{x}_i$, then
  2) Set $\vec{w}_{t+1} = \vec{w}_t-h_i \nabla_{w_t} L(f(x_i,w_t),y_i)$

Assuming application to convex $f$ it is observed that SGD converges at a rate of $1/\sqrt{T}$, where $T$ is the number of steps, see [[Gradient decent#Stochastic gradient descent#Convex optimization|convex optimization]]. While this rate is slow, it is independence of the problem dimension.


## Stability of empirical risk minimization 
The process of empirical risk minimization is in fact [[Generalization#Uniform algorithm stability|unifromly stable]], and thus leads to a small generalization gap, provided the loss function, assumed to be of the from $f(x)=\vec{w}^\intercal \vec{x} = \hat{y}$, used is a differentiable function that obeys the strong [[Convex functions|convexity]] inequality $$L(\vec{v}^\intercal\vec{x},y)\leq L(\vec{w}^\intercal\vec{x},y)+\langle\nabla L(\vec{w}^\intercal\vec{x},y),\vec{v}-\vec{w}\rangle+\frac{\alpha}{2}\|\vec{w}-\vec{v}\|^2,$$where $\vec{v},\vec{w}$ are both weight vectors from the same domain $\mathcal{W}$ and $\alpha >0$. Additionally, we require $L$ to be a bounded Lipschitz function with $\|\nabla L(\vec{w}^\intercal\vec{x},y)\|\leq M$.

We are now ready to state the theorem.

**Theorem:** Let $L$ be a strongly convex loss function over the domain $\mathcal{W}$, with bounded gradient $\|\nabla L(\vec{w}^\intercal\vec{x},y)\|\leq M$ for all $\vec{x}\in \mathcal{X}$. Under these conditions, the empirical risk minimization (ERM) process satisfies $$\Delta_{sup}(ERM)\leq \frac{4M^2}{\alpha N},$$where $N$ is the size of the training set.
_Proof:_ See (p113)[[@Hardt_2022]].

It is worth noting that in the above theorem, ERM is assumed to be a deterministic map that takes a sample to the minimizing weight vector for the predictor function.

More specific bounds exists for loss functions that don't satisfy the exact assumptions of the above theorem, or can be modified sufficiently to apply the theorem, e.g., turning convex loss functions into strongly convex loss functions by the addition of a regularization term.





