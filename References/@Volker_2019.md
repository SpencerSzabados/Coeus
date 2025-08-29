---
title: Legendre memory units: Continuous-time representation in recurrent neural networks
authors: Aaron Voelker, Ivana Kajić, Chris Eliasmith
year: 2019
---

# Overview
The authors propose a new form of recurrent neural network, specifically within the class they call memory units, that can be used for maintaining information for long time frames (long range dependencies) based on a [[Linear dynamical systems]] using [[Orthogonal polynomials]] (specifically Legendre polynomials) projections. 


# Primary results 
The LMU is derived from a linear transfer function for continuous-time delay, which can be expressed in the form $F(s)=e^{-\theta s}$ where $\theta$ is the desired window size, and can be approximated by $d$ coupled [[ordinary differential equations]] which can be expressed as $$\theta\frac{d m(t)}{dt} = Am(t)+bu(t)$$where $m(t)\in\mathbb{R}^d$ is a state-vector. The $A$ and $B$ matrices can be computed explicitly using Pade approximations for a given dimension $d$. Critically, the sate vector $m$ can be related to the value of the input signal $u$ at time $t-\theta'$, for any $o\leq \theta'\leq \theta$, through a Legendre polynomials expansion of upto $d-1$ polynomials. Specifically, $$u(t-\theta') \approx \sum_{i=0}^{d-1}P_i\left(\frac{\theta'}{\theta}\right)m_i(t)$$where $P_i$ is a shifted Legendre polynomial of degree $i$. 

This system is then discretized and mapped into the memory of a recurrent neural network, such that, given a input $u_t\in\mathbb{R}$ $$m_t = \bar{A}m_{t-1}+\bar{B}u_t$$where $\bar{A}$ and $\bar{B}$ are the discretized matrices; e.g., for a sufficiently small $\Delta t$ we may write $$\bar{A}=(\Delta t/\theta)A+I \quad\text{ and }\quad \bar{B} = (\Delta t/\theta)B.$$
When implemented within a neural network, given an input vector, $x_t$, the LMU generates a hidden state, $h_t\in\mathbb{R}^n$, based on the current input, previous hidden state, and current memory state through a non-linear [[Activation functions|activation function]] $f$,  $$h_t = f(W_x x_t+W_hh_{t-1}+W_mm_t)$$where $W_x,W_h$ and $W_m$ are learned weights. Similarly, the input signal $u_t$ is computed using learned vector encodings $e_x,e_h,$ and $e_m$ with $$u_t=e_x^\intercal x_t + e_h^\intercal h_{t-1} +e_m^\intercal m_{t-1}.$$These vector encodings are responsible for projecting the data into memory. The memory parameters, $\bar{A},\bar{B},$ and $\theta$, can be trained in terms of adapting the window size but this not necessary based on the authors experiments (These matrices are also held fixed within [[@Chilkuri_2021]]) as these matrices can be initialized to appropriate values.


# Experimental results 
It is demonstrated that a moderately size LMU can model temporal dependencies across $100,000$ time-steps, well exciding the performance of a comparably sized LSTM network. 