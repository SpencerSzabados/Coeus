The standard treatment of [[Empirical risk]] for deep learning, starts with a reformulation of the prediction function weight vector, $\vec{w}$, to include the additional parameters that originating from the network layers. Similarly, gradient decent methods are used to attempt to find minimizers. With gradient calculations being performed via a method called automatic differentiation. 

Unfortunately, in the case of neural networks, even simple two-layer networks can admit exponentially many local minimizers and finding minimum is a $NP-Hard$ problem in the worst case. However, in practice, optimization of neural nets tends to be easy, especially if the loss is bounded below by zero.


## Convergence of predictions in nonlinear models
Under some assumptions, nonconvexity of deep network loss, does not stand in the way of empirical risk minimization via gradient decent methods.


## Automatic differentiation
In deep learning many operations are stacked on top of one another complicating differentiation, due to requiring application of high dimensional chain rule; moreover, implementation of chain rule is computationally inefficient. Furthermore, any alteration to the architecture would invalidate all prior calculations. These are the problems _automatic differentiation_ attempts to solve.

Beyond this, we need to be mindful of _vanishing and exploding gradients_. Generally speaking, chains of linear operators (such as those in neural networks) either tend to result in tiny gradient changes or very large gradients. Both result in failure as they are untenable for the purposes of training.

## Backpropagation 
https://en.wikipedia.org/wiki/Backpropagation

[[Artificial neural networks#Backpropagation|Backpropagation]] (methods) is a form of automatic differentiation commonly used for training [[Artificial neural networks#Classical feedforwards neural networks|feedforwards neural networks]], which makes use of dynamic programming, capable of adapting to most network architectures. 

Abstractly, consider a computation that proceeds in $L$ steps (layers) starting from an input $\vec{x}^{(0)}$ and produces output $\vec{x}^{(L)}$ with $L-1$ intermediate steps with $\vec{x}^{(t)} = f_t(\vec{x}^{(t-1)})$ for $t=1,\dots,L$. Backpropagation proceeds in this way, with the goal of computing the Jacobian of the output $\vec{x}^{(L)}$ with respect to $\vec{x}^{(0)}$ evaluated at $\vec{w}$, i.e., $\mathbb{J}_{\vec{x}^{(0)}}\vec{x}^{(L)}(\vec{w})$, and consequently ends up computing the Jacobians of each intermediate layer in the process.

**Algorithm: (Backpropagation)** 

The key observation of the backwards pass computation, is that computation of the partial derivatives takes place locally only requiring that partial derivative information passed to each layer during the forwards pass. 


## Vanishing and exploding gradients 
Vanishing and exploding gradients result from model architectures. As such, many architecture innovations in deep learning are aimed as addressing this problem.

### Residual connections
[[Residual neural networks]] are one method of countering vanishing gradients, which function by essentially making each layer close the identity map, taking the general form of $$f(\vec{x}) = \vec{x} + A_2(\sigma(A_1\vec{x})),$$where $A_1,A_2$ are affine transformations (representing the network interconnections), and $\sigma$ is a element wise nonlinearity. The addition of $\vec{x}$ is commonly represented using, so called _skip connections_, that connect the input to the output skipping the intermediate layers.

To see why such network layers aid in slowing gradients from vanishing, observe that $$\mathbb{J}_\vec{x}f(\vec{x}) = \mathbb{J}_\vec{x}I(\vec{x})+\mathbb{J}_\vec{x}A_2(\sigma(A_1\vec{x})).$$Hence, if the weights of the non-identity transform shrink, the Jacobian approaches the identity in the sense that its singular values are between $[1-\epsilon,1+\epsilon]$. Consequently, as the Jacobian for a deep network (made up of residual connection layers with differing wrights) is a produce of these matrices, its gradient should be well-behaved.


### (Batch) Normalization 
Batch normalization (or batch norm) is a method used in the training of neural networks to increase the speed and stability of convergence for stochastic gradient descent, initially proposed in [2015]. The methods effectiveness is shown through its empirical result, but theoretical reasoning is till not fully known. [Wiki](https://en.wikipedia.org/wiki/Batch_normalization).

The method operates by imposing a normal distribution on portioned parts of the input feature vector, re-centering and re-scaling these components. Suppose we have a feature vector $\vec{x}$. To derive the batch normalized vector, we partition $\vec{x}$  into subvectors $$\vec{x} = [\vec{x}_1|\cdots|\vec{x}_N],$$which are then normalize (statistical distribution) individually to form the new feature vector $$\vec{x}' = [\vec{x}_1'|\dots|\vec{x}_N']$$with $\vec{x}'_i = 1/s_i(\vec{x}_i-\bar{x}_i)$, where $\bar{x}_i$ and $s_i$ are the empirical mean and standard deviation of the components of $\vec{x}_i$. 