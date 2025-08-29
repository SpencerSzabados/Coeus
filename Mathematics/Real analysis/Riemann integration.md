
# Differentiating under the integral

**Theorem: (Leibniz differentiation rule)** Let $F(x,t)$ be a function that is continuous in $t$ and $x$ within some region of the $xt$-plane along with $\frac{\partial}{\partial x}F(x,t)$ which includes the continuous curves $h(t)$ and $g(t)$, which are bounded from below and above respectively, then $$\frac{d}{dt}\int_{g(t)}^{h(t)}F(x,t)\, dx = [F(h(t),t)h(t)-F(g(t),t)g(t)]+\int_{g(t)}^{h(t)}\frac{\partial}{\partial t}F(x,t)\,dx.$$
The right most term can be seen as an application of Fubini's theorem, where for 

The most common use of this theorem is $$\frac{d}{dt}\int_0^\infty F(x,t)\,dx=\int_0^\infty \frac{\partial}{\partial t}F(x,t)\,dx.$$

