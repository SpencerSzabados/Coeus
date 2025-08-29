A rotation matrix is a special form of [[Basis transformations|basis transformation]] that rotates a vector  through an angle $\theta$ via an orthonormal basis of rotated basis vectors; the resulting vector image when superimposed into the originating basis then appears to have been rotated.


# 2D rotation matrices 
**Definition: (Rotation matrix)** In $\mathbb{R}^2$ (the vector space - or any equivalent vector space) a vector $v=(v_1,v_2)$, or a point, is rotated through and angle of $\theta$ radians via (right) multiplication by the _rotation matrix_ $$R_2(\theta) = \begin{bmatrix}\cos\theta & -\sin\theta\\ \sin\theta & \phantom{-}\cos\theta\end{bmatrix}.$$That is, $R_2(\theta)v$ is the vector terminating at the point $\theta$ radians counter-clockwise from the terminus of $v$.

The equation for the rotation matrix can be derived by first writing the components of $v$, which we assume to be normalized, in polar form, that is $$v_1 = \cos\phi\quad v_2=\sin\phi$$for some $\phi$, and observing the structure of the matrix required to rotate $v$ by $\theta$ via the addition formula for sine and cosine: $$\begin{align*}\cos(\phi+\theta) &= \cos(\phi)\cos(\theta)-\sin(\phi)\sin(\theta),\\ \sin(\phi+\theta) &= \sin(\phi)\cos(\theta)+\cos(\phi)\sin(\theta).\end{align*}$$[[@Lang_1986]].

An alternative formulation for the rotation matrix based on vectors rather than angles is the following.

Suppose $v=(v_1,v_2)$ and $w=(w_1,w_2)$ are unit-vectors, as we wish to derive the rotation matrix $R_2(v,w)$ that will rotate $v$ into alignment with $w$, say this demands a rotation by $\theta$ radians. By recalling $\cos(\theta)=v\cdot w$ and $\sin(\theta)=\|v\times w\|$ we may write the corresponding rotation matrix $$R_2(v,w) = \begin{bmatrix}v\cdot w & -\|v\times w\|\\ \|v\times w\| & \phantom{-}v\cdot w\end{bmatrix}$$directly in terms of $v$ and $w$. [Kuba](https://math.stackexchange.com/a/897677).