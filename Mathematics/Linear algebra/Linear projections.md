---
doc type: Note
authors: Spencer Szabados
tags:
  - linear_algebra
---
---

The dot product between two vectors in a measure of their similarity in terms of the projection of one onto the other.

**Definition: (Vector projection)** Let $u$ and $v$ be two vectors in the same [[Inner product space]]. The projection of $u$ onto $v$ is defined as the vector $$\text{proj}_v(u) = \frac{\langle u,v\rangle}{\|v\|^2}v=\|u\|\cos\theta,$$where $\theta$ is the angle between $u$ and $v$. Notably, the difference vector $u-\text{proj}_v(u)$ is orthogonal to the projection.

Projections can be generalized and written in terms of matrices, the so called projection matrices. Assuming we are working in the Euclidean Inner Product Space, we can write $$\begin{align}\text{proj}_v(u) &= \frac{v(v^\intercal u)}{v^\intercal v}\\ &= \frac{(vv^\intercal)u}{v^\intercal v}\\&=\frac{vv^\intercal}{v^\intercal v}u,\end{align}$$where $vv^\intercal$ is the outer-product of $v$ with itself. The projection formula can be written in terms of$$\text{proj}_v(u) = Pu,$$where $$P=\frac{vv^\intercal}{v^\intercal v}$$is the _projection matrix_ of $v$. This formula is most useful for projecting a bunch of vectors that are arranged into a matrix, $U=[u_1\mid u_2\mid \cdot \mid u_n]$, along the same vector by calculating the matrix product $\text{proj}_v(U)=PU$ and extracting the resulting column vectors.