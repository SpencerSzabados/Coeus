Generalization, in machine learning, refers to the performance of model on examples outside of the original training (fitting) data.

**Definition: (generalization gap)** For a predictor $f:\mathcal{X}\to\mathcal{Y}$ and loss function $L:\mathcal{y}\times\mathcal{Y}\to \mathbb{R}$, and subsequent risk $R[f] = E[L(f(X),Y)]$ for random variables $X$ and $Y$ from $\mathcal{X}$ and $\mathcal{Y}$. Assuming $f$ to been fitted using a sample of matched pair observations $S=\{(x_1,y_1),\dots,(x_N,y_N)\}\subset \mathcal{X}\times\mathcal{Y}$ the _generalization gap_ is defined as $$\Delta_{gen}(f) = R[f]-R_S[f],$$where $R_S[f]$ is the empirical (in sample estimator of) risk.

Generalization gap illustrates the error between the unknown population risk and that of the sample since $R[f] = R_S[f]+\Delta_{gen}(f)$. That is, if we manage to shrink empirical risk, thought optimization, all that remains is the generalization gap.


# Overparameterization in models
[[Overparameterized neural networks]] are commonly use in machine learning, so it is important to ask if these practices help generalization? As it turns out, large models often lead to better generalization performance. 

However, despite many advances in our understanding of models the empirical body of evidence and "rules of thumb" still dominate the domain.


## Effects of model complexity on generalization
The classical view of generalization posits that as model complexity (e.g., number of parameters) increases initially both [[Empirical risk]] and risk decrease; however, past a certain point risk begins to increase while empirical risk continues to decrease (overfitting). On the other than, many current practitioners have observed that that complex models can simultaneously achieve close to zero training loss and still generalize well with risk continuing to decrease towards a convergence point as the model complexity grows, albeit with marginal returns after a certain point.


## Optimization versus generalization 
According to [[@Hardt_2022]], it is commonly believed that what makes optimization procedures feasible (and efficient) in machine learning models (optimized using [[Gradient decent#Stochastic gradient descent|stochastic gradient descent]] for possibly non-convex optimization problems) is the practice of designing these models with more parameters than training points (overparameterizing). However, as mention above, there is no known rigorous link between optimization performance and generalization performance, experiments can be constructed that optimize well but generalize poorly despite high model complexity.


## The effect of explicit regularization methods
Regularization is an important method that is used all over in machine learning (with equivalences in deep learning) optimization. It is thought that regularization may help generalization performance, but is perhaps not necessary in heavily overparameterized models.


# Generalization theories 
Much of current machine learning is based on empirical evidence, rather than explicit mathematical theory. However, there is still many key theories and theorems.

## Algorithmic stability
The theory of algorithmic stability posits that generalization arises in models that are insensitive to perturbations in training data.

To introduce the idea of algorithmic stability, suppose we are operating on the training set $S=((X_1,Y_1),\dots,(X_N,Y_N))\in (\mathcal{X}\times\mathcal{Y})^N$, which is represented by a vector for ease of notation. Now consider two random independent samples $S$ and $S'$ from the same population $(X,Y)\in\mathcal{X}\times\mathcal{Y}$. Let for $i=1,\dots,N$ $$S^{(i)} = ((X_1,Y_1),\dots,(X_{i-1},Y_{i-1}),(X'_i,Y'_i),(X_{i+1},Y_{i+1}),\dots,(X_N,Y_N)),$$where the $i$ data point comes from $S'$ and the others from $S$.

**Definition: (Algorithm average stability)** Let $A$ be an algorithm, a deterministic map taking training samples from $(\mathcal{X}\times\mathcal{Y})^N$ to a function space $\mathcal{F}$ of predictor functions of the from $f:\mathcal{X}\to\mathcal{Y}$, and let $S=((X_1,Y_1),\dots,(X_N,Y_N))\in (\mathcal{X}\times\mathcal{Y})^N$ be a random training sample. The _average stability of and algorithm A_ is $$\Delta(A) = E_{S,S'}\left[\frac{1}{N}\sum_{i=1}^N \left(L(A(S)(X'_i),Y'_i)-L(A(S^{(i)})(X'_i),Y'_i)\right)\right],$$where the $i$ items are replacement substitutions as defined above.

The value $\Delta(A)$ measures that average loss difference between examples from the original training set and that of randomly selected replacement examples. As risk is defined in terms of the expected risk, we suspect that an algorithms stability related to its generalization gap as the next theorem states.

**Theorem:** The expected generalization gap equals the average stability, that is $$E[\Delta_{gen}(A(S))] = \Delta(A).$$_Proof:_ Before proceeding observe that since elements of $S'$ are independently drawn and identically distributed as those of $S$, $E[L(A(S)(X_i),Y_i)]=E[L(A(S^{(i)})(X'_i),Y'_i)]$. Then by linearity of expectation $$\begin{align} E[\Delta_{gen}(A(S))] &= E[R[A(S)]-R_S[A(S)]]\\ &= E\left[\frac{1}{N}\sum_{i=1}^NL(A(S)(X'_i),Y'_i)\right]-E\left[\frac{1}{N}\sum_{i=1}^NL(A(S(X_i),Y_i)\right]\\ &= E\left[\frac{1}{N}\sum_{i=1}^NL(A(S)(X'_i),Y'_i)\right]-E\left[\frac{1}{N}\sum_{i=1}^NL(A(S^{(i)})(X'_i),Y'_i)\right]\\ &= \Delta(A).\end{align}$$

### Uniform algorithm stability
There is a more powerful notion of algorithm stability known as uniform stability which replaces the average by a supremum making it at times easier to work with.

**Definition: (Uniform stability)** The _uniform stability of an algorithm A_, a deterministic map taking training samples from $(\mathcal{X}\times\mathcal{Y})^N$ to a function space $\mathcal{F}$ of predictor functions of the from $f:\mathcal{X}\to\mathcal{Y}$, is defined as $$\Delta_{sup}(A) = \sup_{S,S'\in (\mathcal{X}\times\mathcal{Y})^N}\sup_{(X,Y)\in\mathcal{X}\times\mathcal{Y}}|L(A(S)(X),Y)-L(A(S')(X),Y)|,$$where $S$ and $S'$ differ in exactly one entry. The value of $(X,Y)$ is chosen independent of both $S$ and $S'$.

**Corollary:** For any algorithm $A$ we have $E[\Delta_{gen}(A(S))]=\Delta(A)\leq \Delta_{sup}(A)$. 


## Function approximability
One of the most fundamental ways of interpreting model generalization is by counting the number of different functions that can be described by a models parameters. 

Let $S$ be a iid sample of $N$ draws from $\mathcal{X}\times\mathcal{Y}$, and $f$ be a predictor from the function space $\mathcal{F}$. Assume for simplicity that the loss function used $L$ has range in $[0,1]$. Then by Hoeffding's bound we have $$P(R_S[f]>R[f]+t)\leq e^{-2Nt^2}.$$Then by taking the union bound on a finite subset $F\subset\mathcal{F}$, we can guarantee within a probability of $1-\delta$, that for all $f\in F$ $$\Delta_{gen}(f)\leq \sqrt{\frac{\ln|F|+\ln(1/\delta)}{N}}.$$Thus, if $F$ is the set of functions representable by a model, it maybe thought of as a measure of complexity that bounds the generalization gap.


### VC-dimension 
Bounding the generalization gap above for all functions in a function space $\mathcal{F}$, as introduced in [[Generalization#Function approximability]], is called _uniform convergence_. In the same sense, VC-dimension measures the ability of a model to replicate arbitrary labelings of a set of points.

**Definition: (VC-dimension)** The Vapnik-Chervonenkis dimension (VC-dimension) of a function class $\mathcal{F}$ of functions mapping $X\to Y$, denoted $VC(\mathcal{F})$, is the cardinality of the largest set $Q\subset X$ such that any Boolean function $h:Q\to \{-1,1\}$, there exists a predictor $f\in\mathcal{F}$ such that $f(x)=h(x)$ for all $x\in Q$.

In other words, if for a $d$-sized sample $Q$ there exists functions in $\mathcal{F}$ that admit all $2^d$ possible binary parametrizations (bit sequences), then the VC-dimension of $\mathcal{F}$ is at least $d$. Generally, VC-dimension tends to grow with the number of model parameters.

A famous inequality, called the VC-inequality, implies that with probability $1-\delta$, we have for all functions (predictors) $f\in\mathcal{F}$ $$\Delta_{gen}(f)\leq \sqrt{\frac{VC(\mathcal{F})+\ln(1/\delta)}{N}}.$$ (note, $VC(\mathcal{F})\leq \ln(\mathcal{F})+1$, as it relates to the previous inequality.)


### Rademacher complexity  
Similar to VC-dimension is Rademacher complexity, which is often more easily calculated and incorporates problem specific aspects. Rademacher complexity measures the ability of a model to interpolate a random sign pattern assigned to a point set.

Rademacher complexity is typically not applied to the predictor function class directly but implicitly through the loss function used.

**Definition: (Rademacher complexity)** Let $\mathcal{F}$ be the function space for the predictors $f$ considered, and $L$ the loss function. Furthermore, let $S=\{(x_1,y_1),\dots,(x_N,y_N)\}\subset \mathcal{X}\times\mathcal{Y}$ be a random iid sample drawn according to the distribution $p(x,y)$ on $\mathcal{X}\times\mathcal{Y}$. Lastly, let $\mathcal{H}$ be the class of functions of the form $h(x,y)=L(f(x),y)$. The _empirical Rademacher complexity_ of the function class (space) $\mathcal{H}$ is defined as $$\hat{\mathfrak{R}}_N = E_{\sigma\in\{-1,1\}^N}\left[\frac{1}{N}\sup_{h\in\mathcal{H}}\left|\sum_{i=1}^N\sigma_i h(x_i,y_i)\right|\right].$$The _Rademacher complexity_ is then defined as $$\mathfrak{R}_N(\mathcal{H}) = E[\hat{\mathfrak{R}}_N(\mathcal{H})].$$ 

### PAC-Bayes bounds 


