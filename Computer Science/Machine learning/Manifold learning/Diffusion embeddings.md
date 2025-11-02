---
doc type: Note
authors: Spencer Szabados
date: 2024-02-18
tags:
  - diffusion
  - approximation
  - machine_learning
  - differential_geometry
  - topology
  - stochastic_processes
references:
---
___

Diffusion maps are a form of non-linear [[Manifold learning]] based on optimizing a [[Stochastic Process]] constructed from the assumption that the datapoints in $Y$ are part of a random walk. See [Tianlin Liu](https://tianlinliu.com/2021/05/29/difussion-maps/) for a detailed derivation.

# Overview
Given set $Y$ diffusion maps attempt to learn $\mathcal M$ by performing a random walk over a graph constructed over the data (somewhat similar to [[Simulated annealing process|simulated annealing]]). The idea is that as we take more steps along this walk different scales in the structure of the data is revealed, e.g., clusters of different scales are found. This method can also be understood as a form of approximating the solution to the eigenvalue problem, which seeks a solution to find a set of orthonormal basis functions $\psi_1,\dots,\psi_t$ for the learned manifold $\mathcal{M}$ given the sampling density $q$ of $Y$ such that $$q^{-1}(\nabla\cdot q(\nabla\psi_k(y))) = \lambda_k\psi_k(y).$$Diffusion maps make the assumption that $q$ is uniform (constant for all $y$) and therefore the above reduces to $$\nabla\cdot\nabla\psi_k(y)=\lambda_k\psi(y)$$and we approximate $\nabla\cdot\nabla$ by a kernel function (the Gaussian kernel is used below) treating the problem as a continuous signal reconstruction task. See [John_Harlim](https://www.sfb1294.de/fileadmin/user_upload/Spring_School_2019/John_Harlim_lecture_1.pdf), [Wiki](https://en.wikipedia.org/wiki/Discrete_Laplace_operator#Mesh_Laplacians).


# Stochastic construction
We will construct $X(t)$ a [[Markov chains|Markov random walk]] over $G$, the graph constructed from $Y$ in the follow way, with probability transition matrix 
$$P(X_j|X_i) = \frac{w_{ij}}{\sum_{j=1}^N w_{ij}}$$where the weighted adjacency matrix $W$ entries are computed according to an isotropic diffusion [[Parzen-Kernel density estimators|kernel]], typically taken to be the [[Families of distributions#Gaussian (Normal) distribution|Guassian kernel]] $$w_{ij}:=k(y_i,y_j)=\exp\left\{\frac{-1}{2\sigma^2}\|y_i-y_j\|_2^2\right\}$$and points $y_j$ are taken from some defined neighbour hood around $N_i$ around $y_i$.

The transition matrix $P$, is a stochastic matrix and therefore, has [[Eigenvalues and vectors|eigenvalues]] $1=\lambda_0\leq\cdots\leq\cdots \lambda_{N-1}\leq0$ and left $\phi$ and right $\theta$ eigenvector sets with $$\vec\phi_j^\intercal P = \lambda_j\vec\phi_j^\intercal \quad\text{and}\quad P\vec\theta_j=\lambda_j\vec\theta,$$where $\vec\theta_j = (\theta_j(y_1),\dots,\theta_j(y_N))$; that is the components of the eigenvector are indexed by the datapoints. Moreover, these eigenvector sets are pairwise orthogonal, i.e., $\vec\phi_j^\intercal\vec\theta_k = 0$ unless $k=j$ when $\vec\phi_j^\intercal\vec\theta_k = 1$. Consequently, we can [[Similar matrix#Diagonalizable matrices|diagonalize]] $P$ using the eigenvector decomposition $$P=\Theta^\intercal\Lambda\Phi$$with $\Theta = (\vec\theta_0,\dots,\vec\theta_{N-1})$ and $\Phi=(\vec\phi_0,\dots,\vec\phi_{N-1})$
 
Following this, the _diffusion distance_ between conditional probabilities with differing starting state is defined as: $$d_m^2(X_i,X_j) =\sum_{z}[P_m(z|X_i) - P_m(z|X_j)]^2w(z)$$where $P_m(\cdot|X)=P(X_{t+m})$ and $w(z)=1/\phi_0$ is the function that defines a unique stationary distribution (or also a [[Nonparametric statistics|nonparametric density estimate]]) and controls the penalty applied to regions of high and low density; i.e., $$\phi_0(z)=\frac{deg(z)}{\sum_{y\in Y}deg(y)}$$and is equal to the principle left eigenvector of $P$.

Now, as the final goal is to solve the graph Laplacian equation $Lv=\lambda Dv$ for the degree matrix $D$ in the limit, we want to approximate the diffusion distance for a number of annealing steps. 

Exploiting the properties of [[Markov chains#Large-step transition probability matrices|large-step transition probabilities]] we know $P^m=\Theta\Lambda^m\Phi$, due to the pairwise orthogonal property of the left and right eigenvectors, and $$P_m(X_j|X_i) = \phi_0(X_j) + \sum_{k=1}^{N-1}\lambda_k^m\theta_k(X_i)\phi_k(X_j).$$Substituting this into the diffusion distance and assuming $\phi_0$ is constant we get 
$$\begin{align} d_m^2(X_i,X_j) &= \sum_{z}\left(\sum_{k=1}^{N-1}\lambda_k^m\theta_k(X_i)\phi_k(z) - \sum_{k=1}^{N-1}\lambda_k^m\theta_k(X_j)\phi_k(z)\right)^2w(z)\\ &= \sum_{z}\left(\sum_{k=1}^{N-1}\lambda_k^m[\theta_k(X_i)-\theta_k(X_j)]\phi_k(z) \right)^2w(z)\\ &= \sum_{z}\sum_{k=1}^{N-1}\sum_{t=1}^{N-1}\big(\lambda_k^m[\theta_k(X_i)-\theta_k(X_j)]\phi_k(z)\big)\big(\lambda_t^m[\theta_t(X_i)-\theta_t(X_j)]\phi_t(z)\big)w(z)\\ &= \sum_{k=1}^{N-1}\sum_{t=1}^{N-1}\big(\lambda_k^m[\theta_k(X_i)-\theta_k(X_j)]\big)\big(\lambda_t^m[\theta_t(X_i)-\theta_t(X_j)]\big)\sum_zw(z)\phi_k(z)\phi_t(z)\tag{*}\\ &= \sum_{k=1}^{N-1}\lambda_k^{2m}[\theta_k(X_i)-\theta_k(X_j)]^2\sum_zw(z)\phi_k(z)\phi_t(z)\\ &= Trace(\Lambda)\sum_{k=1}^{N-1}\lambda_k^{2m}[\theta_k(X_i)-\theta_k(X_j)]^2\\ &\propto \sum_{k=1}^{N-1}\lambda_k^{2m}[\theta_k(X_i)-\theta_k(X_j)]^2\end{align}$$where the trace appears from line (*) by the analysis $$\begin{align}w(z)\phi_k(z)\phi_t(z) &= \frac{Trace(\Lambda)\cdot\phi_k(z)\cdot\phi_t(z)}{\phi_0(z)}\\ &= Trace(\Lambda)\cdot\theta_k(z)\cdot\phi_t(z)\\ &= \begin{cases}Trace(\Lambda) &\text{ if } k=t\\ 0 & \text{ otherwise.} \end{cases} \end{align}$$

Finally, due to the falloff in magnitude (and effect) of eigenvectors we can approximate the diffusion distance, ignoring the proportional constant, by truncating the sum at order $t$ as $$d_m^2(X_i,X_j) \approx \sum_{k=1}^t\lambda_k^{2m}[\theta_k(X_i)-\theta_k(X_j)]^2.$$
Finally this gives us a method of computing the manifold $\mathcal{M}$ coordinates of the points of $Y$; in particular, the transformed points $\hat{Y}$ under $\psi:\mathcal{M}\to\mathbb{R}^t$ are given by $$\hat{y_i} = (\lambda_1^m\theta_1(y_1),\dots,\lambda^m_t\theta_t(y_1)).$$


```pseudo
\begin{algorithm}
\caption{Diffusion manifold learning process}
\begin{algorithmic}
\Input Given a set of points $Y=\{y_1,\dots,y_N\}$ and the sets $N_i$ which contain the $k$-nearest-neighbour points (or $\epsilon$) to $y_i$, and a parameter $m$ for the number of diffusion steps.
\Output Approimate manifold $\mathcal{T}$ and map $\hat{\psi}$.\\
    \State Construct the normalized graph Laplacian $L$
    \State Compute the transition matrix $P = D^{-1/2}LD^{-1/2}$
    \State Compute the normalized matrix $M = (D^{1/2})^{-1}P$
    \State Compute the $t$ largest eigenvalues $\lambda_0,\dots,\lambda_t$ and associated vectors $\theta_1,\dots,\theta_t$ of $M^t$ 
    \State Construct diffusion map $\psi: y\to (\lambda_1^m\theta_1(y_1),\dots,\lambda^m_t\theta_t(y_1))$
    \Return $\psi$
\end{algorithmic}
\end{algorithm}
```

