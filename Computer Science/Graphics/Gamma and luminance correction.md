---
doc type: Note
authors: Spencer Szabados
tags:
  - graphics
  - image_processing
date: 2022-01-01
references:
---
---

Gamma (filters) defines the relationship between a pixels numerical colour value and its luminance value, and is an important consideration as the response curve of the human eye is (is almost guaranteed to be) different from whatever method used to captured the image in question; in particular the sensitivity of the human eye to changes in brightness is best modelled using a logarithmic scale while CMOS cameras follow a linear response curve, which can only capture a narrow portion of a scenes brightness range (Dynamic range). Beyond this, the luminance apparent to the human eye for certain colours is higher than some colours of equal numerical (RGB average value) luminance. See [Wiki](https://en.wikipedia.org/wiki/Gamma_correction).

In the simplest cases, gamma correction can be done using the following equation.

**Gamma power-law:** Given an input image $I$ with luminance $Y(I)$, with values normalized to within the range $[0,1]$, define the gamma-corrected output $I_F$ as $$I_F = AI^{1/\gamma},$$for constants $A$ and $\gamma$, with $A=\mathbb{I}$ and $-1\leq\gamma\leq 1$ typically chosen.

Using a gamma value of $\gamma < 1$ in the power-law is called _gamma compression_, while a value of $\gamma > 1$ is referred to as _gamma expansion_. 