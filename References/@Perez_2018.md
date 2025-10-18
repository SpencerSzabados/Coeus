---
doc type: Research paper summary
title: "FiLM: visual reasoning with a general conditioning layer"
authors: Ethan Perez, Florian Strub, Harm de Vries, Vincent Dumoulin, Aaron Courville
year: 2018
date: 2025-10-16
references:
---
---

# Overview
This paper proposes a method of affinely modulating the neuron values of a [[Artificial neural networks|neural network]], such as a CNN, using some scalar values output from a (possibly) learned function that is conditioned on the input to the network and some secondary task; e.g., the CNN might generate features from an image that are feed into a classifier head, but features and first modulated based on a text encoding to highlight specific objects. Note, this paper was published before the meteoric rise in the use of [[Layer attention]] in text/vision models.

# Primary results
The goal of this paper is adapt a backbone architecture, such as a feature encoder for computer vision, into one that is task conditioned with some global feature correlations.

## Method
This paper proposes a network block called FiLM takes the following form: Let $x\in \mathbb{R}^d$ be some network input and $c\in \mathbb{R}^T$ be some condition that should correlate with the desired output (whatever that is) of the network $F_\theta(x)$. For simplicity of setup, suppose the network can be decomposed in terms of some feature encoder $f$ and a output head $h$, like $$F_\theta(x)=h_\phi\circ f_\psi(x)$$and denote the network blocks of $f_\psi$ by $b_{\psi_i}^{(i)}:\mathbb{R}^{c_i}\to\mathbb{R}^{c_{i+1}}$ so that $$f_\psi=b_{\psi_n}^{(n)}\circ \cdots \circ b_{\psi_0}^{(0)}.$$To incorporate FiLM into this network we modify the block as follows given some parameters $\gamma$,$\beta$ $$FiLM(b_{\psi_i}^{(i)},\gamma,\beta) = \gamma\odot b_{\psi_i}^{(i)}+\beta$$where $\gamma,\beta \in \mathbb{R}^{c_{i+1}}$ and are applied before the final activation function of the block (if you want to allow gating the network output with negative values). These parameter are predicted by separate network $g_\eta$ which maps the condition variable to the concatenated vector $$\begin{align}&g_\eta:\mathbb{R}^T\to \otimes_{i=0}^n(\mathbb{R}^{c_{i+1}}\times\mathbb{R}^{c_{i+1}})\\ &g_\eta(c)=((\gamma^{(0)},\beta^{(0)}),\dots,(\gamma^{(n)},\beta^{(n)}))\end{align}$$the final model is then of the form $$F_\theta(x,c) = h_\phi\circ FiLM(b_{\psi_n}^{(n)},g_\eta(c)_n)\circ \dots \circ FiLM(b_{\psi_0}^{(0)},g_\eta(c)_0)(x).$$
Of course you don't need to apply FiLM to every block.

# Experimental results
The proposed method, at time of publication, performed well on a set of image question answer tasks for object counting and reasoning using an architecture similar to that I described above. 

The authors provide a very detailed ablation study for the method. Critically, it seems that clamping (using clip or sigmoid, etc.) the individual values of $\gamma$ and $\beta$ can drastically reduce performance; the given reason is that restricting these values makes it more challenging to gate neurons off as the FiLM blocks can not multiply outputs by very negative values.