Ideas of the early work on perceptrons grew into the subject of _Pattern Recognition_, forming the core of modern (2022) machine learning, [[@Hardt_2022]].

Perceptrons are a class of binary [[Classifiers|classifier]] (predictor) algorithms, which aim to find a _linear separator_ of the data (space), that is, a hyperplane that partitions the input space so that all (most) examples of the same type lie on the same side of the hyperplane. 


# Introduction
More concretely, perceptrons are a type of [[Classifiers#Linear classifier|linear classifier]] (predictor), based on a function of the form (linear combination of inputs)$$f(x) = \langle \vec{w},\vec{x}\rangle,$$where $\vec{w}$ is a vector of coefficients that define a hyperplane, called the _weight vector_, and is such that for any matched value-label pair $(x,y)$, we have $y\langle w,x\rangle>0$; i.e., $x$ is matched with the correct label $y\in\{-1,1\}$. We then take as predictor $$\hat{Y}(x)=\begin{cases}1 & \text{ if } \langle w,x\rangle \geq 0\\ -1 & \text{otherwise}. \end{cases}$$
Algorithmically, the value of $w$ is constructed incrementally using a stochastic optimization method (the perceptron algorithm is equivalent to applying [[Overview of machine learning#^d6a173|stochastic gradient decent]] with a hinge loss activation function).

```pausdocode
Let S be a training set of N labled data points of the form (x,y)
Let e be a training cutoff threshold used to terminate training 
   once the difference between iterations reduces past e.
_________________________________________________________________
Perceptron_Algorithm(S,e)
    Initialize w_0 = 0
    For each step t = 0,1,...
        Select random index i in {1,...,N} from the training sample S
        If y_i*InnerProduct(w_t,x_i) < 1
            Set w_{t+1} = w_t + y_i*x_i //where the margin is 1
        else 
            Set w_{t+1} = w_t
```

The condition that $y_i\langle w_t,x_i\rangle<1$ is called a _margin mistake_, where the linear function might agree in sign with the label but not by a sufficient enough margin (must be at least one unit apart in this case). Then, after the update $$\langle w_{t+1},x_i\rangle = \langle w_t,x_i\rangle+y_i\| x_i\|^2,$$which has the intended affect of widening the margin between the hyperplane and the point $x_i$.

If there exists a set of weights consistent with the data, the perceptron algorithm is guaranteed to converge to it.


# Properties
There are two primary questions that need to be answered for perceptrons 1) does the preceptron algorithm(s) successfully fit training data and 2) how well does it generalize. 


## The Mistake bound 
This bound is originally due to [Novikoff], and says, in essence, if a linear separator of the data exists the perceptron algorithm will find it quickly provided the margin of the separating hyperplane isn't too small.

Before performing the analysis, we require some terminology. Suppose the hyperplane $\mathcal{H}_w=\{x\mid w^\intercal x = 0\}$, defined in terms of a vector $w\in \mathbb{R}^d$, perfectly separates the data in a sample $S$. Call the smallest distance between any element of $S$ and $\mathcal{H}_w$ the _margin_ of $\mathcal{H}_w$, that is, $$\gamma(S,w) = \min_{(x,y)\in S} \text{dist}(x,\mathcal{H}_w) = \min_{(x,y)\in S}\frac{|\langle x,w \rangle|}{\|w\|}.$$Recall, $w$ is normal to the hyperplane. In effect the margin tells us how large a perturbation in $S$ can be handled before a data point is misclassifed.

Define the _data set margin_ of $S$ to be the maximal achievable margin for any value of $w$, with $$\gamma(S) = \max_{||w||=1}\gamma(S,w).$$Additionally, define the _dimeter of $S$_ to be $$D(S) = \max_{(x,y)\in S}\|x\|,$$i.e., the Euclidean point set norm.

The worse case analysis of the preceptron algorithm is summarised in the following theorem. 

**Theorem: (Novikoff Mistake bound)** The perceptron algorithm makes at most $(2+D(S)^2)/\gamma(S)^{2}$ margin mistakes (corrections to $w$) on any sequence of examples from a data set $S$ that can be perfectly classified by a linear separator. 

The mistake bound does not depend on the dimensionality of the data in question. The bound also gives a bound on the number of passes required before the algorithm terminates, having reached its optimal solution, for a fixed data set. 

(TODO - this theorem says if the data is linearly separable. When is this condition guaranteed?)


## Generalization performance
Assume the training set values of $S=\{(x_1,y_1),\dots,(x_N,y_N)\}$ are all idd from a fixed underlying distribution $\mathcal{D}$ with labels from $\{-1,1\}$.

The following theorem states how the predictor trained on $S$ will perform on new data drawn from the same underlying population $\mathcal{D}$, by making a argument based on the _stability_ of the perceptron algorithm. Where stability in this case means, there is only a small effect on the derived separator from removing or replacing a single data point in $S$. This is the case for the perceptron algorithm as there is a bound on the number of margin mistakes made.

**Theorem: (Vapnik and Chervonenkis)** Let $S_N$ denote a training set of $N$ iid samples from a distribution $D$ that we assume has a perfect linear separator. Let $w(S)$ be the output of the perceptron on a dataset $S$ after running until the hyperplane makes no more margin mistakes on $S$. Let $Z=(X,Y)$ be an additional independent sample from $D$. Then, the probability of making a margin mistake on $(X,Y)$ is bounded above by $$P(Y\langle w(s_N), X\rangle < 1) \leq \frac{1}{N+1}E_{S_{N+1}}\left[\frac{2+D(S_{N+1})^2}{\gamma(S_{N+1})}\right].$$
_Proof:_ See (p46)[[@Hardt_2022]].


# Limitations
Perceptrons cannot learn certain concepts, e.g., $XOR$ of input bits, or more general parity functions. However, this limitation can be overcome by including an $XOR$ in the feature vector used, which allows for the continued use of linear methods in such cases that require $XOR$ operators.


# Connection to empirical risk minimization 
Before exploring the formal guarantees that are provided by the perceptron algorithm, we will explore its relation to [[Empirical risk#Empirical risk minimization|empiricial risk minimization]]. For the sake of analysis, and generalization of the method, we introduce two _hyperparameters_ $\nu$ and $\gamma$ into the perceptron algorithm update rule $$w_{t+1} = \gamma w_t + \eta y_ix_i.$$The scalar $\eta>0$ is called the [[Curve fitting#^c983b3| learning rate]] and $\gamma\in [0,1]$ is called the _forgetting rate_. 

As the perceptron algorithm selects a index to operate on at random at each step, analysis of the algorithm using version of the optimization method [[Curve fitting#Gradient steepest descent|gradient descent]] called [[Overview of machine learning#^d6a173|stochastic gradient decent]] is a natural connection.

Recall, in stochastic gradient decent the local improvement the method makes at each step is given by a local linear approximation of the loss function based on the current function parameters. Using the notation of the current problem, that is $$w_{t+1} = w_t -\eta\nabla_{w_t}L(f_{w_t}(x_i),y_i).$$Where $(x_i,y_i)$ is randomly chosen and the expression $\nabla_{w_t}L(f_{w_t}(x_i),y_i)$ is the gradient of the loss function with respect to the model parameters $w_t$. 

By taking $L(\langle w,x\rangle, y) = \max\{1-y\langle w,x \rangle, 0\}$, known as _hinge loss_, the above update rule becomes _roughly_$$w_{t+1} = \begin{cases}w_t+\eta y_ix_i & \text{ if }y\langle w,x_i\rangle<1\\w_t & \text{ otherwise,}\end{cases}$$as $\nabla L(f_{w_t}(x_i),y_i) = -y_ix_i$ when $y\langle w_t,x_i\rangle < 1$ and $0$ when $y\langle w_t,x_i\rangle > 1$ with the gradient being undefined for $y\langle w_t,x_i\rangle = 1$; this is what is meant by roughly above, the justification comes from further analysis by subgradients. This, is almost of the desired form of the generalized update rule given at the start of the section.

The $\gamma$ parameter in the update rule can be recovered by adding a additional weight penalty to the loss function in order to bias the weights from growing to large. This is known as [[Curve fitting#Regularization|regularization]], and helps prevent [[Curve fitting#^024b32|overfitting]] and promote generalization. In particular, the $l_2$-regularized empirical risk minimization problem takes $$L(\langle w,x\rangle, y) = \max\{1-y\langle w,x \rangle, 0\} + \frac{\lambda}{2}\|w \|^2,$$with the risk being minimized equal to $$R[L(\langle w,x\rangle, y)] = \frac{1}{N}\sum_{i=1}^N\max\{1-y\langle w,x \rangle, 0\} + \frac{\lambda}{2}\|w \|^2.$$Where for the given update rule $\gamma = (1-\eta\lambda)$. 

