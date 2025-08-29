https://mrl.cs.nyu.edu/~perlin/doc/oscar.html

# Volumetric textures
## Hypertextures
Existing between shape (surface models) and textures _hypertextures_ extend the idea of solid textures (as defined in [[@Perlin_1985]]) to generate both an objects texture and form/geometry. Unlike solid texturing, where a modeled object _slices_ a solid texture along its surface, hypertextures procedurally generate both an objects texture and form. 

Procedural volumetric textures created using space filling curves were proposed in [[@Perlin_1989]], working by modifying a controllable stochastic noise function using a set of _shaping functions_. Instead of modeling objects as connected surfaces, they are modeled as distributions of densities, divided into _hard_ and _soft_ regions acting as the spine and deformable parts of the model respectively. Rendering is then done by sampling throughout the described volume.

### Modeling hypertextures
To describe a hypertexture Perlin defined two types of functions: 

**Object Density Function:** An _object density function_ $D(x)$ with range $[0,1]$ which describes the density of a $3D$ shape (solid) for all point. The _soft region_ (deformable) of an object consists of all $x$ such that $0<D(x)<1$.

**Density Modulation Function:** A _density modulation function_ $f_i$, which is used to modulate (deform) an object's density within its soft region. 

A hypertexture is created by successively applying DMFs $f_i$ to an objects ODF $D(x)$: $$H(D(x),x) = f_n(\dots f_1(f_0(D(x))).$$ 
### Boolean operations of hypertextures
In order to create more complex geometries we need to combine a set of primitives, as is done using traditional shape modeling methods. 

**Boolean operations** for soft objects $A$ and $B$ are implemented through their density functions $a(x)$ and $b(x)$:
  - Intersection: $A\cap B = a(x)b(x)$;
  - Complement: $\overline A = 1 - a(x)$;
  - Difference: $A-B = A\cap \overline B = a(x)-a(x)b(x)$;
  - Union: $A\cup B = \overline{\overline A \cap \overline B} = a(x)+b(x)-a(x)b(x)$.
These operations however don't full a complete Boolean algebra since $A\cap A = a(x)a(x) \neq A$.


### Base density modulation functions
Here are a sample of DMFs that can be used to build upon and combined using functions, e.g., $abs$, $\sin$, etc.

**Bias:** _Bias functions_, $bias_b$ is a power curve defined over the unit interval such that $bias_b(0)=0$, $bias_b(1/2)=b$, and $bias_b(1)=1$, can be used to push up or pull down an objects density. Thus, by increasing or decreasing $b$ the density values in an objects soft regions can be biased up or down; e.g., $$bias_b(t) = t^{\frac{\ln(b)}{\ln(1/2)}}.$$
**Gain:** An objects density gradient can be made flatter or steeper (sharper) by controlling variance; specifically, a gain function $gain_g$ is defined over the unit interval such that $gain_g(0)=0$, $gain_g(1/4)=(1-g)/2$, $gain_g(1/2)=1/2$, $gain_g(3/4)=(1+g)/2$, and $gain_g(1)=1$. By increasing or decreasing the value of $g$, we can increase or decrease the rate at which the midrange of an object's soft region goes from $0$ to $1$; e.g., Gain can be defined as a spline of two bias curves $$gain_g(t) = \begin{cases}bias_g(2t)/2 &\text{ if } t<1/2\\ 1-bias_{1-g}(2-2t)/2 & \text{ otherwise.} \end{cases}$$
**Noise:** An approximation of white noise band-limited to a single [[Noise functions#^5ca82c|octave]], such as [[Noise functions]], allows us to introduce randomness into the digital single.

**Turbulence:** An approximation for the appearance of turbulent activity can be used to build higher level DMFs; e.g., $$turbulence = \sum_i \left|\frac{1}{2^i}noise(2^i x)\right|.$$

### Hypertexture primitives
**Sphere:** A sphere centered on the point $c$ of radius $r$ and softness $s$ can be defined by the density function $$\begin{align} D_{[c,r,s]}(q):\;& r_1^2 = (r-s/2)^2;\\ &r_0^2 = (r+s/2)^2;\\ &r_q^2 = (q_x-c_x)^2+(q_y-c_y)^2+(q_z-c_z)^2;\\ &D = \begin{cases}1 & \text{ if } r_q^2\leq r_1^2\\ (r_0^2-r_q^2)/(r_0^2-r_1^2) & \text{ if } r_q^2\geq r_0^2 \end{cases}  \end{align}$$where $r_0$ is the outer boundary (radius) with $D=0$, $r_1$ is the inner boundary of the soft region, and $r_q$ is the radius of the sphere center at the point $q$.


### Rendering hypertextures
By (the given definition) hypertextures have no well defined surfaces, at least in general, so volume rendering techniques are a well suited method to use; e.g., [[Ray tracing and light transport]]. As DMF evaluation is pointwise independent, as with most [[Procedural textures|procedural texturing methods]] and [[Noise functions|noise function]] approaches, hypertexture rendering is well suited for parallel and distributed rendering. 

#### Ray marching algorithm 
The algorithm given by Perlin is the following.

