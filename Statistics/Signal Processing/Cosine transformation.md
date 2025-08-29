---
doc type: Note
authors: Spencer Szabados
date: 2023-09-25
tags:
  - random_sampling
  - approximation
  - signal_processing
  - compression
---
___

The (discrete) Cosine transformation is a special case of the [[Statistics/Signal Processing/Fourier transformation|Fourier transformation]] that does not make use of complex values, which simplifying its application and analysis in certain cases.


# Overview 
There are many different variants (definitions) of the discrete cosine transformation. 

**Definition: (Discrete cosine transformation)** Consider a discrete function $f_{xy}$ (a indexed set of function values) of size $M\times N$ the discrete cosine transformation of this is $$F(f)_{mn} = \frac{2c(m)c(n)}{\sqrt{MN}}\sum_{x=0}^{M-1}\sum_{y=0}^{N-1}f_{xy}\cos\left(\frac{(2x+1)m\pi}{2M}\right)\cos\left(\frac{(2y+1)n\pi}{2N}\right)$$where $$c(i) = \begin{cases}\frac{1}{\sqrt{2}} & \text{ if } i=0\\ 1 &\text{ if }i\neq 0.\end{cases}$$See [[@Nacer_2001]]

**Definition: (Inverse discrete cosine transformation)** The inverse discrete cosine transformation of a function $f_{xy}$ is $$F^{-1}(h)_{xy} = \sum_{m=0}^{M-1}\sum_{n=0}^{N-1}\frac{2c(m)c(n)}{\sqrt{MN}}F(f)_{mn}\cos\left(\frac{(2x-1)m\pi}{2M}\right)\cos\left(\frac{(2y-1)n\pi}{2N}\right).$$See [[@Nacer_2001]] (formula as stated in paper is incorrect, the above is corrected).


# Image denoising using DCT


# Image compression using DCT
Following the simple compression scheme outlined in [[@Nacer_2001]] and [Cabeen](https://www.math.cuhk.edu.hk/~lmlui/dct.pdf), data after transformation is truncated using high and low pass filters, which remove parts of the image that are not easily detected by the human eye, the resulting data is then encoded using a run-length encoder.

## Data truncation


## Entropy encoding 


