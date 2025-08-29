**Definition: (Matrix exponential)** Let $X$ be a constant $n\times n$ matrix with real or complex entries. Then the function $e^X$ is defined as $$e^X = I + \sum_{k=1}^\infty \frac{X^k}{k!} = \lim_{k\to \infty}\left(I+\frac{X}{k}\right)^k,$$where $I$ is the identity matrix. See [[@Arnold_1992]] [[@Miller_1982]].

The matrix exponential always converges so is well defined for any square matrix $X$.

**Theorem: (Matrix exponential convergence)** The series $e^X$ converges uniformly for any $n\times n$ matrix $X$ with $\|X\|\leq a$ for some $a\in \mathbb{R}$. 
_Proof:_ Let $\|X\|\leq a$. Then the series defining $e^X$ is majorized by the numerical series $1+\sum_{k=1}^\infty a^k$, which converges to $e^a$ by the series definition of $e^x$ for $x\in \mathbb{R}$. Then by the Weierstrass criterion the series $e^X$ converges uniformly for $\|X\|\leq a$. $\square$ 

The matrix exponential obeys serval elementary properties:
   1) $e^0 = I$;
   2) $e^{X^\intercal} = (e^X)^\intercal$;
   3) If $XY=YX$ for two $n\times n$ matrices $X$ and $Y$, then $e^Xe^Y = e^{X+Y}$.
   4) If $X$ is symmetric, then so is $e^X$.
   5) if $X$ is skew-symmetric, then $e^X$ is orthogonal. 
   6) $det(e^X)=e^{tr(X)}$ follows by Jacobi's formula and shows that the matrix exponential is always and invertible matrix.

**Theorem:** For a $n\times n$ real of complex matrix $X$ and real variable $t$, $e^{Xt} = T^t$, where $T^t$ is the [[shift operator]] which takes a function $f$ to its translation $f_t$; i.e., $T^t f(x) = f_t(x) = f(x+t)$. 

For polynomials this can be seen by applying Taylor's formula for polynomials$$\begin{align} p(x+t) &= p(x) + \frac{t}{1!}\frac{dp}{dx}+\frac{t^2d^2p}{2!dx^2}+\cdots\\ &=e^{t\frac{d}{dx}}p(x) = T^t p(x), \end{align}$$where $e^{\frac{d}{dx}}$ is a operator in which $\frac{d}{dx}$ (is a differential operator) maps the field of polynomials to their derivative that corresponds with the power of the operator.

**Theorem: (Trace identity)** For any $n\times n$ matrix $X$ with complex entries, $det(e^X) = e^{tr(X)}$, where $tr(X)$ denotes the sum of entries along the main diagonal of $X$.

