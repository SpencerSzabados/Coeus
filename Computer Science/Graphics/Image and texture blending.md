In all the following it is assumed that color values are LDR and are normalized within the standard range of $[0,1]$, unless otherwise specified.


https://www.youtube.com/watch?v=su-s8QoCiPk
http://www.deepskycolors.com/archivo/2010/04/21/formulas-for-Photoshop-blending-modes.html

## Lighten blend modes
**Color Dodge:** 

## Contrast based effects
**Overlay:** Given a target image $I_T$ and an effects image $I_B$ to be be overlaid (blended into) onto $I_T$, each pixel value in the final image $I_F$ is given $$F_T = \begin{cases}1-2(1-I_T)(1-I_B) & \text{ if } Y(I_T)\geq 0.5\\ 2I_TI_B & \text{ if }Y(I_T)<0.5,\end{cases}$$where $Y(\cdot)$ is the luminance value of the image at any pixel.

A slight modification of the overlay blend mode that has a more linear "response" curve is the soft light blend mode.

**Soft light:** Given a target image $I_T$ and an effects image $I_B$ to be be overlaid (blended into) onto $I_T$, each pixel value in the final image $I_F$ is given $$F_T = \begin{cases}2I_TI_B+I_T^2(1-2I_B) & \text{ if } Y(I_B)\geq 0.5\\ 2I_T(1-I_B)+\sqrt{I_T}(2I_B-1) & \text{ if }Y(I_B)<0.5,\end{cases}$$where $Y(\cdot)$ is the luminance value of the image at any pixel.


# Noise filtering 
## Kuwahara filters 
https://en.wikipedia.org/wiki/Kuwahara_filter