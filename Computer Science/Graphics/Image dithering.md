Dithering, in the context of image processing, is a method of converting a greyscale image to black and white (or a color image to a reduced color set) by using black dots of varying density to approximate the average gray levels of the original image (where for color images colors that are not available in the palette are approximated by a diffusion of colored pixels from within the available palette). See [Wiki](https://en.wikipedia.org/wiki/Dither), [surma](https://surma.dev/things/ditherpunk/), [visgraf](https://www.visgraf.impa.br/Courses/ip00/proj/Dithering1/algoritmos_desenvolvidos.htm) for a more detailed overview.


# Colour space preliminaries

# Methods of dithering 
## Thresholding
## Random dithering
## Noise based dithering 

### Blue noise dithering 
[[Noise based image dithering]]


## Patterning


## Ordered dithering
Ordered dithering is a commonly used image dithering algorithm that uses set pixel patterns and set thresholds to replicate the apparent grey levels of regions of an image. Consequently, the algorithm(s) result in images with a characteristic crosshatching pattern. See [Wiki](https://en.wikipedia.org/wiki/Ordered_dithering).

(unknown type) https://bisqwit.iki.fi/story/howto/dither/jy/

### Cyclical threshold matrices
(TODO - do more)

Substituting a cyclical matrix, with values not exceeding one, in place of that used in [[Image dithering#Bayer methods|byaer based dithering methods]] results in an image with diagonal striping in the direction corresponding to the row shifts used in the construction of the matrix.


### Bayer methods
See [matematicas](http://matematicas.uam.es/~fernando.chamizo/dark/d_dither.html), [codeproject](https://www.codeproject.com/Articles/5259216/Dither-Ordered-and-Floyd-Steinberg-Monochrome-Colo).
Bayer dithering methods are differentiated from other threshold matrix methods by a set of criteria the matrix values must satisfy.

**Algorithm:** The final image is rendered progressively by thresholding (comparing) each pixels colour value based on a corresponding value from a threshold map (Bayer matrix). 

**Constructing a general Bayer matrix:** Bayer derived, in [[@Bayer_1973]], from furrier analysis certain criteria for producing threshold matrices of orders a power of two, listed below, that result in an _optimal pattern of dispersed dots_ in the final image. The threshold matrix is described reclusively by
(TODO)
with the entries of any matrix in the sequence satisfying  
(TODO)

An arbitrary sized $2^n\times 2^n$ threshold map satisfying these constraints, and the most commonly used variety, can be constructed recursively using the block matrix equation $$M_{n+1} = \frac{1}{(2n)^2}\begin{bmatrix}(2n)^2M_n & (2n)^2M_n+2\\ (2n)^2M_n+3 & (2n)^2M_n+1 \end{bmatrix},$$ with an initial matrix $$M_1 = \frac{1}{4}\begin{bmatrix}0 & 2\\ 3 & 1\end{bmatrix},$$which has entry values ranging from $0,1,\dots,2^{2n}-1$. See [Wiki](https://en.wikipedia.org/wiki/Ordered_dithering#Threshold_map).

(Note, any matrix can be used as a threshold matrix, but the ones generated using the above method are the informal standard, and typically yield good results. Additionally, the effectiveness of the algorithm is not affected by rotation or mirroring of the threshold map)

Threshold maps can be pre-computed and normalized, by subtracting $0.5$, so the sum of the entries is one. The sum normalization step can be skipped resulting a slightly brighter image with almost-white pixels to not be dithered. This is fine for greyscale dithering, but will cause artifacts for color dithering.

**Applying the threshold matrix:** The threshold map controls how a pixels value is quantized to a different color, by comparing the scaled pixel color value to the corresponding threshold map entry. More precisely, the value $c$ of each color channel of $pixel(i,j)$ is transformed to the quantized value $$c' = \text{nearest\_palette\_colour}(c+rM(i \mod n,\,j\mod n)),$$where $M$ is the threshold map and $r$ is the amount of spread in the color space. For a $8-bit$ $RGB$ colour pallet with $2^{3N}$ evenly spaced colours, $r$ is typically chosen as $r=\frac{255}{N}\frac{1}{2}$, where the trailing one-half is a normalization term. Multiplication of the threshold map by $r$ serves to scale the threshold matrix to the same range as the pixel color values. For grey scale images this rule can be simplified by taking $r=1$ and taking the nearest palette colour to be the quantized grey scale value, for a set number of grey levels.

Example of grey scale Bayer ordered dithering, from [[Ordered (Bayer) image dithering]].
![[MIke_c4d8luminance 1.png]]


### Void and clustering methods
[[@Ulichney_1993]]


## Error-diffusion
Error-diffusion based methods attempt to minimize visual artifacts by diffusing error from the quantization process into neighbouring pixels. 

[[@Ostromoukhov_2001]]

### Floyed-Steinberg algorithm
A commonly used, simple error-diffusion based, dithering algorithm, see [Wiki](https://en.wikipedia.org/wiki/Floyd%E2%80%93Steinberg_dithering), [visgraf](https://www.visgraf.impa.br/Courses/ip00/proj/Dithering1/floyd_steinberg_dithering.html), [matematicas](http://matematicas.uam.es/~fernando.chamizo/dark/d_dither.html), [[@Omohundro_1990]].

Lena dithered using Floyed-Steinberg algorithm.
![[lena floyd.jpg]]

## Case studies

# Dithering effects under camera motion
## Stabilizing dithering effects
### Case studies
The game, Return of The Obra Dinn [2018], is a $3D$ game that makes use of $1-bit$ dithering to render the environment. In an attempt to limit motion sickness of players, the developer made significant efforts to limit the change in the dithering pattern applied to objects in the scene as the camera moves and rotates though it. See https://forums.tigsource.com/index.php?topic=40832.msg1363742#msg1363742.