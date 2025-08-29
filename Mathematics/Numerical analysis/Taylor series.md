**Definition: (Taylor series polynomial)** If a function $g(x)$ has $n$ continuous derivatives (is of order $n$), that is, $g^{(n)}(x) = \frac{d^n}{dx^n}g(x)$ exists, then for any constant $a\in \mathbb{R}$, the _Taylor polynomial of order $n$ about $a$_ (small region around) is $$T_n(x) = \sum_{i=1}^n\frac{g^{(i)(a)}}{i!}(x-a)^i.$$

The major theorem from Taylor is that the _remainder_ from the truncation of the infinite series, of which the Taylor series is derived, always tends to zero faster than the highest-order term in the series.

**Theorem: (Taylor)** If $g^{(N)}(a)=\frac{d^N}{dx^N}g(x)|_{x=a}$ exists, then $$\lim_{x\to a}\frac{g(x)-T_N(x)}{(x-a)^N}=0.$$

