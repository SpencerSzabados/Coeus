---
doc type: Note
authors: Spencer Szabados
date: 2023-09-20
tags:
  - random_sampling
  - approximation
  - signal_processing
---
___

Fourier's theorem (series) is a fundamental result in approximation theory (and therefore [[numerical analysis]]) which gives a way to encode any function (data) as a linear combination of primitive (meaning easy to evaluate) functions.


# Overview

## Approximating the Fourier transformation 
There are many different ways of approximating the Fourier transformation itself depending on the kind of function being analysed (data); in particular, if the domain of interest varies continuous in all parameters or not, if not then we can utilize the so called discrete Fourier transformation. If the function of interest is univariate then all the following methods are equivalent.


### Discrete (space) Fourier transformation

### Discrete (time) Fourier transformation


### Discrete Fourier transformation 
TODO - correct notation, the function can be continuous in range as the function represents the grey level of each pixel and is indexed by two values.

**Definition: (DFT)** The discrete (space and time) Fourier transformation of a discrete function $f_{xy}$ (e.g., image) of $M\times N$ values is defined coordinate wise as $$F(f)_{mn} = \sum_{x=0}^{M-1}\sum_{y=0}^{N-1}f_{xy}\exp{\left(-i2\pi\left(\frac{mx}{M}+\frac{ny}{N}\right)\right)}$$and results in a discrete function of the same dimension (a latus of the same size). See [github-vincmazet](https://vincmazet.github.io/bip/filtering/fourier.html).

**Definition: (Inverse DFT)** The inverse discrete Fourier transformation restores the origin (discrete function or an approximation of a continuous function) by computing the element wise values $$F^{-1}(h)_{xy}=\frac{1}{MN}\sum_{m=0}^{M-1}\sum_{n=0}^{N-1}F(f)_{mn}\exp{\left(i2\pi\left(\frac{mx}{M}+\frac{ny}{N}\right)\right)}.$$

As the Fourier transformation makes use of complex values, the amplitude, $|F(m,n)\exp(\cdot)|$, and phase, $(xm/M+yn/N)$, are commonly displayed or operated on separately.
 

# Denoising data using Fourier transformation 



## Energy spectra filter denoising 
Analysing the energy spectral density of a signals Fourier transformation can be used to (quickly) denoise data by designing and applying simple frequency filters that remove unwanted (noisy) spectra which are applied before inverting and recovering the signal. See [Medium-Chen](https://kinder-chen.medium.com/denoising-data-with-fast-fourier-transform-a81d9f38cc4c).

https://github.com/Bharati2301/Image-Denoising-using-Fast-Fourier-Transform