Absorbing [[Markov chains]] are a specific form of (discrete) markov chain that include states that are impossible to transition out of once entered (absorbing states). This form of markov chains admit analysis using the _first step method_. 


# Overview 
**Definition: (Absorbing Markov chain)** A Markov chain $\{X_i\}_{i\geq 1}$ is said to be absorbing if the associated transition matrix $P$ contains a entry $P_{jj}=1$ for a state $s_j$, which is said to be absorbing, and for any initial state $X_0=s_i$ there exists a finite sequence of states $X_1=s_{i_1},X_2=s_{i_2},\dots,X=s_{j}$ with $P_{i,i_1}P_{i_1,i_2}\cdots P_{i_{n},j}>0$; that is, there exists a possible path from any state to at least one absorbing state. States that are not absorbing are called _transient_.

Let $\{X_i\}_{i\geq 1}$ be a finite state absorbing Markov chain with states $s_0,s_1,\dots,s_N$. Suppose states $s_0,\dots,s_{r-1}$ are transient, meaning $P_{ij}^n\to 0$ as $n\to \infty$ for $0\leq i,j< r$, while states $s_r,\dots,s_N$ are absorbing, meaning $p_{ii}=1$ for $r\leq i\leq N$. The transition matrix of this form of Markov chain can be decomposed into $$P=\begin{bmatrix}Q& R\\ 0&I\end{bmatrix}$$where $0$ is a $(N-r+1)\times r$ matrix of zeros, $I$ the $(N-r+1)\times(N-r+1)$ identity matrix, $Q$ a $r\times r$ transition matrix for transient states with $Q_{ij}=P_{ij}$ for $0\leq i,j<r$, and $R$ the transition matrix for transitioning from a transient state to an absorbing state. See (p83)[[@Taylor_1998]].

