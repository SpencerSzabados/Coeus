A radial [[Basis transformations|basis]] function is a function used for constructing a basis transformation based on the distance between an query point and a number of fixed points (called centers).

**Definition: (Radial basis function)** Given a set of points $\{c_i\}_{i=1}^N$, called _centers_, a real valued function $\phi:[0,\infty)\to \mathbb{R}$ is a radial basis function if the set of functions $\{\phi_i(x)=\phi(\|x-c_i\|)\}_{i=1}^N$ are linearly independent and they form a basis for a Haar space (or Chebyshev space); this last point meaning the matrix $$\begin{bmatrix}\phi(\|c_1-c_1\|) & \phi(\|c_2-c_1\|) & \dots & \phi(\|c_N-c_1\|)\\ \phi(\|c_1-c_2\|) & \phi(\|c_2-c_2\|) & \dots & \phi(\|c_N-c_2\|)\\ \vdots & \vdots & \ddots & \vdots\\ \phi(\|c_1-c_N\|) & \phi(\|c_2-c_N\|) & \dots & \phi(\|c_N-c_N\|)\end{bmatrix}$$is non-singular. See [Wiki](https://en.wikipedia.org/wiki/Radial_basis_function)


# Approximation methods
Radial basis function can be used to approximate (interpolate) various kinds of functions.
