In machine learning, the subfield of using statistical tools to direct actions  
in dynamic environments (not static training data) is called reinforcement learning (RL). Reinforcement learning can be thought of as a hybrid approach between [[Supervised learning]] and [[Unsupervised learning]] techniques.

Reinforcement learning methods can be thought of as approximation schemes for dynamic programming problems; Consequently, [[Artificial neural networks]] and function approximations can be used to yield _simplified_ (generalizable) approaches to approximate solutions of dynamic programming problems. [[@Hardt_2022]]


# Sequential decision making problems
The ideas of sequential decision making (and predictive analytics and optimal control) are central to the boarder view of Reinforcement learning, and understanding the learning problem of of how to best local sequential decisions when the underlying mechanisms and costs are not known ahead of time. 

Sequential decision making differs from static prediction (e.g., [[Supervised learning]]), essentially, in that the later makes decisions based directly on the data rather than an underlying probabilistic model.

_Action_ variables $U$ are incorporated into sequential models, which direct the procedure towards a goal, subject to a reward mechanisms $R$. Where the intended process, that when analysing data $X$ and action variable $U$ is selected that maximized the possible reward $R$. In reinforcement learning, which could be thought of as a empirical version of sequential decision making, the feasible space for $U$ is taken to be a subset of previously observed data rather than the probabilistic models continuum.


## Dynamical systems 
Alongside action variables, another key feature of sequential decision making that sets it apart from static prediction (e.g., [[Supervised learning]]) is the notion of time in the production of data (sequential). Data is assumed to be collected from an evolving process, where current actions (decisions) influence future rewards.

**Definition: (Structured dynamical system)** A _dynamical system model_ has a state $X_t$, exogenous input $U_t$ modeling the current control cation, and reward $R_t$. the state of the system evolves in discrete time steps according to an equation of the from $$X_{t+1} = f_t(X_t,U_t,W_t)$$where $W_t$ is a random variable. The reward is assumed to be a function of these variables, with $R_t = g_t(X_t,U_t,W_t)$, also denoted $R_t(X_t,U_t,W_t)$.

Dynamical systems can be thought of in terms of [[Causal modeling#Structural causal models|structural causal models]], where the model may or may not model causal relationships.


### Markov decision processes 
Structural equations (as used above) is not the only dynamical model commonly used. [[Markov decision process|Markov process]] is a method favored for working directly with probabilistic transitions. Almost all RL problems can be formulated in terms of MDPs.

In a Markov decision process, there is a state to the system $X_t$ and input $U_t$ that are linked by a probabilistic model $P(X_{t+1}|X_t,U_t)$.


## Optimal sequential decision making 
The class of optimization problems that underline much of sequential decision making (SDM) problems is to find a sequence of decision _polices_ that maximize the cumulative reward subject to the uncertain stochastic element of the dynamic system.

**Problem: (SDM police optimization)** Given a dynamical system, the goal of SDM police optimization is to find a set of polices $\pi_1(X_0),\dots,\pi_T(X_T,\dots,X_0)$ that produce a sequence of actions, $U_t = \pi_t(X_t,X_{t-1},\dots,X_0)$, that satisfy the following maximization problem: $$\begin{align*}\text{maximize} &\quad E_{W_t}\left[\sum_{t=0}^T R_t(X_t,U_t,W_t)\right]\text{ wrt decisions } U_1,\dots,U_T\\ \text{subject to} &\quad X_{t+1} = f_t(X_t,U_t,W_t). &&\text{($x_0$ being given.)}\end{align*}$$^d3d55b

Polices are allowed to inspect the current state (typically) before rendering a decision, in addition to inspecting the past history of observed states. In this way, a decision strategy can continually try to mitigate uncertainty through feedback. 


### Dynamic programming approach to SDM
In applying dynamic programming to SDM we require a underlying model of the environment being operated in, so all the following can be considered model-based approaches. 

The [[dynamic programming]] solution to SDM is based on the following principle: If you have found an optimal control policy up to time $T$, $\pi_1,\dots,\pi_T$, and you want to know the optimal strategy starting at sate $x$ at time $t<T$, then you just take the optimal policy starting at time $t$, $\pi_t,\dots,\pi_T$. This allows for the optimal policy to be recursively determined starting from the final time going backwards. 

Proceeding, define the OPT-imal function $$OPT_{[a,b]}(x,u) = \max_{u_t} E_{W_t}\left[\sum_{t=a}^b R_t(X_t,u_t,W_t)\right]$$where $X_{t+1} = f_t(X_t,u_t,W_t)$ with $(X_a,u_a)=(x,u)$, which determines the best achievable value of SDM over the interval $[a,b]$ with action $u$ at time $a$ and initial condition $x$. Thus, the optimal value of SDM over the entire interval $[0,T]$ is $\max_u OPT_{[0,T]}(x_0,u)$ with optimal policy $\pi(x_0) = \arg\max_u OPT_{[0,T]}(x_0,u)$.

Thus, we want to use dynamic programming to compute this optimal function starting with the base case $$OPT_{[T,T]}(x,u) = E_{W_T}[R_t(x,u,W_t)],$$and the recursive calculation $$OPT_{[t,T]}(x,u) = E_{W_t}\left[R_t(x,u,W_t)+\max_{u'}OPT_{[t+1,T]}(f_t(x,u,W_t),u')\right].$$This is known as _Bellman's expectation equation_.


#### Limiting behaviour and stationary policies
The above problem setup assumed finite time horizons, where different polices are applied at each step. On long, limiting, time horizons with invariant dynamics, simpler formulas might be derived. That is, now consider the problem:

**Problem: (SDM average cost policy optimization)**  Given a dynamical system, the goal of SDM average cost police optimization is to find a limiting police $\pi_T$ that produces a sequence of actions, $U_t = \pi_t(X_t,X_{t-1},\dots,X_0)$, that satisfy the following maximization problem: $$\begin{align*}\text{maximize} &\quad \lim_{T\to\infty}E_{W_t}\left[\frac{1}{T}\sum_{t=0}^T R(X_t,U_t,W_t)\right]\text{ wrt decisions } U_1,\dots,U_T\\ \text{subject to} &\quad X_{t+1} = f(X_t,U_t,W_t). \quad\qquad\qquad\text{($x_0$ being given.)}\end{align*}.$$ Note the lack of subscripts on the reward and state transition functions.

SDM average cost policy optimization does not readily admit standard dynamic programming techniques except in special cases, a the most notable being known as _discounted dynamic programming_, which yields approximations of the average reward problem.

**Problem: (SDM discounted cost policy optimization)**  Given a dynamical system, the goal of SDM discounted cost police optimization is to find a limiting police $\pi_T$ that produces a sequence of actions, $U_t = \pi_t(X_t,X_{t-1},\dots,X_0)$, that satisfy the following maximization problem: $$\begin{align*}\text{maximize} &\quad (1-\gamma)E_{W_t}\left[\lim_{T\to\infty}\sum_{t=0}^T\gamma^t R(X_t,U_t,W_t)\right]\text{ wrt decisions } U_1,\dots,U_T\\ \text{subject to} &\quad X_{t+1} = f(X_t,U_t,W_t). \quad\text{($x_0$ being given.)}\end{align*}.$$where $\gamma\in[0,1]$ is a fixed scalar called the _discount factor_. 

For $\gamma$ close to $1$, the discounted reward is approximately equal to the SDM average cost policy reward; can be thought of as an agent making decisions based on long forecast time. When $\gamma$ is close to $0$ the reward is the result of local greediness and might not be close to the optimal result.

Beneficially, the discounted problem admits easy to deal with optimality conditions for Bellman's equation which takes the form $$OPT_\gamma(x,u) = E_{W}\left[R(x,u,W) + \gamma\max_{u'}OPT_{\gamma}(f(x,u,W),u')\right]$$with invariant optimal policy (fixed for all $t$) $$u_t = \arg\max_{u}OPT_{\gamma}(x_t,u).$$That is, at each stage all that is needed to derive the optimal policy is maximize the above optimality function, which can be done using dynamic programming. This also suggests, for reinforcement learning, the amount that needs to be learned in order to make a _near_ optimal decision is not very large for infinite time horizon problems.


#### Computing policies 
There exists a number of different methods for computing special cases of the outlined dynamic programming problem.

There are two primary types of methods used, model-based and model-free methods. The fist requires knowledge of a representative MDP, where the second does not require full knowledge of the MDP instead attempts to solve the SDM problem using previous empiric state-transition values. See [github](https://dudeperf3ct.github.io/rl/2019/12/29/Tabular-Solution/#terminologies).

##### Tabular MDPs
Tabular MDPs refer to a Markov Decision Processes model (typically with a small number of states and actions) represented by entries of a table. [[@Hardt_2022]]. 

Let $S$ denote the set of possible states and $A$ be the set of actions. The state transitions rules are then encoded into a $|S|-by-|S|$ table of conditional probabilities $P(X_{t+1}|X_t,U_t)$, with another similar table for state-action rules.  The optimality equation for the tabular case are thus also tabular in form, enumerating all cost-to-go state action pairs, with $\max_{u'}OPT_{[a,b]}(x,u')$ given by choosing the action associated with the largest entry in the table. Bellman's equations simplifies here to $$OPT_{[t,T]}(x,u) = R_t(x,u)+\sum_{x'}P(X_{t+1}=x'|X_t=x,U_t=u)\max_{u'}OPT_{[t+1,T]}(x',u'),$$which can be computed via matrix-vector operations.



##### Policy and value iteration
Two of the most studies methods for solving discounted infinite time horizon problems are _policy iteration_ and _value iteration_. 

**Algorithm: (Policy iteration)** Policy iteration is a two step procedure consisting of a _policy evaluation_ stage followed by a _policy improvement_ stage. Given a policy $\pi_t$, the policy evaluation step calculates $$OPT_{t+1}(x,u) = E_{W}\left[R(x,u,W) + \gamma OPT_{t}(f(x,\pi_t(x),W),\pi_t(x))\right].$$The policy is then updated by the rule $$\pi_{t+1}(x) = \arg\max_{u}OPT_{t+1}(x,u).$$

**Algorithm: (Value iteration)** Value iteration proceeds stepwise by repeatedly calculating $$OPT_{t+1}(x,u) = E_{W}\left[R(x,u,W)+\gamma\max_{u'}OPT_{t}(f(x,u,W),u')\right].$$Thereby trying to solve Bellman's equation using fixed point iteration principles. Consequently, this method is bound to work well when the iteration is a contraction mapping, which happens to be the case for many problems.


For both it is important to be able to compute expectations efficiently and be able to update all values of $x$ and $u$ in the associated $OPT$ function.


##### Linear quadratic regulator
### Partial observation SDM
A subproblem of SDM is instead of being able to observe the current state directly, we only have access to the partial information given by the outputs $Y_t$ (e.g., action taken) of previous steps, with $$Y_t = h_t(X_t,U_t,W_t).$$This form of SDM problem is considerably more difficult, as we can no longer directly influence (feedback) the action variables $U_t$ as done previously through policy choices.

General partially observed Markov decision processes [(POMDPs)](https://en.wikipedia.org/wiki/Partially_observable_Markov_decision_process) are $PSPACE-hard$, with static output feedback being known to be $NP-hard$, even for small states spaces in likelihood.


#### Separation heuristic 
A common approach to solving approximately output feedback problems is a two stage strategy of _filtering_, which is the name of the process of estimating the state of a dynamical system, and estimator based actions.

**Filtering:** Using all the past partial observations $(y_t,y_{t-1},\dots,y_0)$ build an estimate $\hat{x}_t$ of the current state $X_t$. More specifically, the goal of filtering is to estimate the function $f$ which generates $X_t$ using the previous partial observation data $(y_t,\dots,y_1,u_{t-1},\dots,u_1)$.

**Action:** The action taken is then based on assumed certainty of equivalence between the state estimator and true state. That is, we solve the desired SDM problem as if you have prefect observation of state $X_t$ by taking $\hat{x}_t$ in place of $X_t$ wherever appropriate (i.g., in equations featuring $X_t$). 


##### Optimal filtering
Given an estimator $\hat{f}$ of the state transition function and the observation function $h$, a [[Maximum posterior]] estimate of the state based on current data can be formulated; that is, we want to compute $P(x_t|y_t,\dots,y_0,u_{t-1},\dots,u_1)$ and use it to estimate the mode (most common discrete value) of the density function. The formula for this estimate takes on a simple recursive form but is not always computationally feasible in all cases.

Specifically, due to the conditional independence assumed to be present in the underlying dynamical system model, we can breakdown calculations like $$P(y_t,x_t,x_{t-1},u_{t-1}|\tau_{t-1}) = P(y_t|x_t)P(x_t|x_{t-1},u_{t-1})P(x_{t-1}|\tau_{t-1})P(u_{t-1}|\tau_{t-1})$$where $\tau_t = (y_{t},\dots,y_0,u_{t-1},\dots,u_1)$, which puts call calculations in terms of known (or past) quantities, except for $P(x_{t-1}|\tau_{t-1})$. In the above formula $P(u_{t-1}|\tau_{t-1})$ represents the policy used to determine $u_{t-1}$.

Continuing in this recursive manner, we can apply Bayes rule to compute (TODO - (p233)[[@Hardt_2022]] integral notation is incomplete and I need to review to compute it correctly.) $$\begin{align}P(x_t|\tau_t) = \frac{\int_{x_{t-1}}P(x_t,y_t,x_{t-1},u_{t-1}|\tau_{t-1})\,}{} \end{align}$$

##### Feedforward prediction
For cases where we cannot compute optimal filtering feedforwards prediction remains feasible, working to estimate the sate function $f$ using prediction methods ([[Supervised learning]] in particular). 

In more concrete terms, we aim to construct a function $X_{t+1}\approx h(y_t,\dots,y_0,u_{t-1},\dots,u_1)$ using _time lags_ from historical data.


# Reinforcement learning 
When the probabilistic mechanisms underlying sequential decision making problems are unknown we must use empirical methods to probe for this information. This is the class of problems considered as reinforcement learning.

A central strategy for reinforcement learning problems is to estimate a predictive model for the underlying dynamical system and use this as if it were the true model. This is an application of _principle of certainty equivalence_.

## Exploration-exploitation tradeoffs 
In order to compare different approaches to reinforcement learning, we require some method of summary comparison. 

The two predominant conventions used to compare reinforcement learning methods are [[PAC-learning#PAC-error and PAC-regret|PAC-error and PAC-regrete]].


