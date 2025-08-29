Regularization is a technique used to constrain optimization objectives to produce outputs with reduced oscillations, speaking in graphically, in an attempt to prevent [[Curve fitting#^024b32|overfitting]].  

# Overview 
Stated in terms of a learning problem, as in the context of [[Overview of machine learning|machine learning]], regularization is a technique that tries to improve [[Generalization|generalization performance]] of a model.  


# Tikhonov regularization
The most common form of regularization used in machine learning is that popularized by Andrey Tikhonov. Where for a learning problem of fitting a linear function $f=w^\intercal x$ (e.g., least squares regression) we can add a $L_2$-[[Metric spaces|norm]] of the weight vector $w$ to the expected surrogate [[Point estimation#^45314f|loss]] between predictions and known training data we are attempting to minimizes, that is, we are seeking$$\arg\min_w\sum_{(x,y)\in D}L(f(x),y)+\frac{\lambda}{2}\|w\|_2^2$$where $\lambda$ is a hyperparameter used to give more or less importance to the penalty of large weights in the resulting minimizer. When $w$ is a matrix, the $L_2$-norm is substituted by the Frobenius norm (matrix norm). More generally, for any function $f_\theta$ with parameters $\theta$ the norm of the function is used, provided sufficient conditions are placed on the form of $f_\theta$ (e.g., differentiability).

There is some heuristic arguments, in the case of $L_2$-regularization, that the weights will decay till they are proportional to $\sqrt{N}$ where $w$ is assumed to have $N$ components, see [StackExchange](https://datascience.stackexchange.com/questions/17921/heuristic-argument-for-weight-decay-and-regularization).


# Regularizing for sparsity 
