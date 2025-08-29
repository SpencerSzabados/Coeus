---
title: Parallelizing legendre memory unit training
authors: Narsimha Reddy Chilkuri, Chris Eliasmith
year: 2021
---

# Overview
The authors propose a simplified LMU architecture than that proposed in [[@Volker_2019]] (and an older paper by the same authors) that can be trained on multiple inputs in parallel rather than sequentially (can more efficiently be trained using GPUs compared to the original model that was trained sequentially). Consequently, the training time of the proposed LMU architecture is significantly lower than that of the original while, despite the models simplification, it still manages to achieve state-of-the-art performance.

According to the authors, the proposed simplified memory unit is motivated by the success of set-attention based architectures (e.g., transformers).


# Primary results 
The formulation of the LMU given in this text is in terms of a [[delay network]] (a form of a [[Linear shift-invariant systems|linear time-invariant system]]) coupled to a [[Nonlinear dynamical system]]. 

The system equations given in [[@Volker_2019]] are simplified by the removal of the terms $e_h$, and $e_m$ from the input $u_t$ vector computation, the removal of $W_h$ from the computation of the output value. This gives the system $$\begin{align} u_t &= f(U_xx_t+b_u)\\ m_t &= \bar{A}m_{t-1}+\bar{B}u_t\end{align}$$which only has a single recurrent connection to the previous state $m_{t-1}$. This recurrence relation can be evaluated directly (no need for performing iterative network calculations) by $$m_t = \sum_{i=1}^t \bar{A}^{t-i}\bar{B}u_i$$which through the use of HU factorization can be computed in one shot where only the final state is desired. This factorization enables the reduction in computational complexity from $O(nd^2d_x)$ to $O(n\log(n)\cdot dd_x)$, where $n$ is the sequence length, $d$ is the order of approximation, and $d_x$ the dimension of the inputs, through the application of a fast Fourier transform.  


# Experimental results 
