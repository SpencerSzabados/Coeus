---
doc type: Note
authors: Spencer Szabados
date: 2023-09-13
tags:
  - stochastic_processes
  - ito_calculus
  - statistics
  - economics
  - diffusion
---
___

Differential stochastic processes are, defined by myself, [[Stochastic Process]] that make use of Ito's calculus or other continuum analysis methods applied to randomized processes to derive representative [[Ordinary differential equations]] or [[Stochastic differential equations]] (SDE) and vise versa. This note is primarily concerned with the derivation and manipulation of SDE's (and their application to [[Diffusion models]]).

Much of the work sounding these differential processes originates from option pricing in stock trading. 

Much of the following is taken from CS335 lecture notes from Waterloo University instructed by Sevyeri, a course that I TA-ed [F2023], and lecture notes [EEC586-Ragisky](https://maxim.ece.illinois.edu/teaching/spring23/index.html) from Illinois University. 

# Overview 
Brownian motion (also called Wiener process) refers to randomised motion (in space) that is drawn/distributed according to a [[Families of distributions#Gaussian (Normal) distribution|Guassian distribution]]; this is a form of continuous time and [[Markov chains#Continuous state Markov chains|continuous state Markov chain process]] (random walk).

**Time series form of SDE:** Suppose $X$ is a [[Random variables|random variable]] that varies with resect to time $t$ and space following the stochastic differential equation $$dX = \mu(X(t),t) dt + \sigma(X(t),t) dW,$$where $\mu dt$ is referred to as the _drift_ term, and $\sigma$ the _shift_ or _volatility_, and $dW$ is a random variable of the form $dW = \phi \sqrt{dt}$ with the random variable $\phi\sim \mathcal{N}(0,1)$. 

If we allow $X$ to evolve over a period of duration $dt$, then the expected deviation from its initial value is $$E[dX] = E[\mu dt]+\sigma E[\phi \sqrt{dt}] = \mu dt$$with variance $$Var[dX] = \sigma^2dt,$$for what ever values $\mu$ and $\sigma$ are within the time step window $dt$.

The infinitesimal change in state from one time to another only depends on the current state. 

As discussed in the later section [[Differential stochastic processes#Numerical computation of SDEs|numerical computation of SDEs]], the paths that are defined by such processes are infinitely jagged and not differentiable anywhere, meaning $dX/dt$ does not exist, so care must be taken to not mistake the meaning for the above SDE form. These equations do not represent derivatives (in the standard way) but are differential forms that express stochastic integral equations of the form: $$\int_0^tdX_s = X_t - X_0 =\int_0^t\mu(X(s),s) ds + \int_0^t\sigma(X(s),s) dW,$$where $X(0)=x_0$ is an initial condition with probability one, i.e., $X(0)\sim \delta_{x_0}(t)$.
See [StackEchange-Gono](https://math.stackexchange.com/a/3659688).

Hence, we cannot discuss $E[dX/dt]$ but we may analyse $E[dX]/dt$.


# Stochastic calculus 

**Theorem: (Stochastic integral)** The stochastic integral of a noisy process (random variable) is $$\int_0^tW(t)dW(t) = \frac{1}{2}W^2(t)-\frac{1}{2}T.$$This differs from the standard calculus integral of the same form by the constant factor $T/2$.

**Theorem: (Stochastic expectation integral property)** When analysing the expected value (deviation) of a stochastic function $\sigma(X(t),t)$ the following properties hold: $$E\left[\int_0^t\sigma(X(t),t)dW(t)\right] = 0,$$and $$E\left[\left(\int_0^t\sigma(X(t),t)dW(t)\right)^2\right]=\int_0^tE[\sigma^2(X(s),s)]ds.$$


## Ito's lemma 
Suppose we have a stochastic process of the form $$dX = \mu(X,t)dt+\sigma(X,t)dW$$and we want to analyse the behaviour of a function defined in terms of $X$, e.g., $f(X,t)$ or even simpler $Y(t)=X^2(t)$. Ito's lemma allows us to state $df$ in terms of the quantities present in the SDE governing $X$. In particular, using [[Taylor series]] $$\begin{align*}df(x,t) =& \frac{\partial}{\partial x}f(x,t)dx+\frac{1}{2}\frac{\partial^2}{\partial x^2}f(x,t)dx^2+\cdots\\ +&\frac{\partial}{\partial t}f(x,t)dt + \frac{1}{2}\frac{\partial^2}{\partial t^2}f(x,t)dt^2+\cdots\end{align*}$$wherein substitution of $dx$ by the above SDE gives $$\begin{align*}df(x,t) =& \frac{\partial}{\partial x}f(x,t)(\mu dt+\sigma dW)+\frac{1}{2}\frac{\partial^2}{\partial x^2}f(x,t)(\mu dt+\sigma dW)^2+\cdots\\ +&\frac{\partial}{\partial t}f(x,t)dt + \frac{1}{2}\frac{\partial^2}{\partial t^2}f(x,t)dt^2+\cdots\end{align*}$$where in the limit $dt\to 0$ the mixed higher order time depended terms tend to zero (e.g., $dtdW$, $dW^2$, etc.) since $dW\in O(\sqrt{dt})$ it follows that $dW^2\to dt$ when $dt \to 0$, so the above reduces to the following: $$df = \left(\frac{\partial}{\partial t}f+\mu f+\frac{\sigma^2}{2}\frac{\partial^2}{\partial x^2}f\right)+\sigma\frac{\partial}{\partial x}f dW.$$
 
See [Wiki](https://en.wikipedia.org/wiki/It%C3%B4%27s_lemma).

### Solving SDEs using Ito's lemma
Some SDEs can be solved explicitly using Ito's lemma; meaning, we can derive an expression for how $f$ is distributed at any time. 

**Method:** If $\mu$ and $\sigma$ are constants (scalars) then Ito's lemma can be used to solve SDEs of the form $dX = \mu dt + \sigma dW$ by integrating from $0$ to $t$ to give $$X(t)-X(0) = \mu t + \sigma(W(t)-W(0))$$where it can be shown that $W(t)-W(0)\sim N(0,t)$.


# Numerical computation of SDEs
Such processes are typically discretized to enable the use of [[numerical analysis]] techniques to study their behaviour, as analytical computation is often difficult. On the other hand, it is also possible to see from the limiting behaviour of such a discrete Markov chain process the derivation of the foregoing continuous formulation. See the subsection [[Differential stochastic processes#Numerical computation of SDEs|numerical computation of SDEs]] for a more general discussion.

#### Uniform special grid (latus)
For simplicity consider a state space to be a Euclidean (grid) latus with unit size $\Delta h$, so that 
for an initial start point $X_0$ and $W_0$ the value of $X$ evolves as $$X\gets \begin{cases}X_0+\Delta h & \text{ with probability }p\\ X_0-\Delta h &\text{ with probability }q \quad(=1-p),\end{cases}$$with each update occurring over a period of time $\Delta t$ (that is, if we are interested in analysing the behaviour of $X$ over a time period of length $t$, we discretize $t$ into $N$ intervals of length $\Delta t$). 

Observe, when $\mu=0$ and $\sigma=1$, we can observe for $N$ discretized steps of a time interval of length $t$, where $N$ is made sufficiently large (correspondingly $\Delta t$ is made sufficiently small), we have $$W_N-W_0 \approx \int_0^t dW\sim\mathcal{N}(0,t).$$From this, we can fine the total distance traveled after $N=t/\Delta t$ discrete steps of size $|W_i-W_{i-1}|=\Delta h = \sigma\sqrt{\Delta t}$ is $$N\Delta h = \frac{t\sigma}{\sqrt{\Delta t}}$$