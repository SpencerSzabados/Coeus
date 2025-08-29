Lattice gradient noises (particularly procedural [[Noise functions]]) generate noise by interpolating or convolving between random gradient values defined on an integer (discrete) lattice. [[@Lagae_2010]] 

# Perlin noise 
Perlin noise is a procedural noise function defined as a mixture of primitive stochastic functions, see [[@Perlin_1985]],[standford](http://physbam.stanford.edu/cs448x/old/Procedural_Noise(2f)Perlin_Noise.html). These functions, per the original paper, are classed broadly into the function categories:

$Noise()$ a scalar valued function which takes a three dimensional vector as argument (or whatever vector is appropriate to the space you are operating in) and satisfies: (1) Statistical invariance under rotation and translation (no matter how the domain is rotated or translated it has the same statistical character); and (2) has narrow bandpass limit in frequency; that is, it has no visible features larger or smaller than within a certain narrow size range.

$Dnoise()$ a vector valued differential of the $Noise()$ signal, defined by the instantaneous rate of change of $Noise()$ along the $x$,$y$, and $z$ directions. This primitive, provides a simple way of specifying perturbations to surface normals.

The most known technique for generating a $Noise()$ function is that given in the original paper (also see [[@Perlin_2001]]), namely: 
  1. Consider the set of all points in space whose $x$,$y$, and $z$ coordinates are all integer valued; i.e., the integer lattice. Associate with each point on the integer lattice a pseudo-random value and $x$,$y$, and $z$ gradient values; more precisely, map each ordered sequence of three integers $(x,y,z)$ into an uncorrelated sequence of four real numbers: $H(x,y,z)=(a,b,c,d)$ where $(a,b,c,d)$ define a linear equation with gradient $(a,b,c)$ and value $d$ at $(x,y,z)$. $H()$ is best implemented as a hash function based on (seeded) pseudo-random values. 
  2. If $(x,y,z)$ is not on the integer lattice compute a smooth interpolation (e.g., spline interpolation using a weighted sum of cubic polynomial ease weights) between the surrounding eight lattice equation coefficients (values associated with each vertex of the lattice).
In a later follow up paper, [[@Perlin_2002]] [source code](https://cs.nyu.edu/~perlin/noise/), a improved algorithm was given that corrected discontinuous derivative based artifacts that appear on the boundaries of lattice cells, by using a specific 5th order interpolation polynomial.

## Texturing surfaces
Surface textures may be simulated by using $Noise()$ to control the amount of $Dnoise()$ perturbation. Using noise to create surface (or volumetric) textures is a form of [[Procedural textures|procedural texturing]].

http://devmag.org.za/2009/04/25/perlin-noise/

## Complexity 
Perlin noise scales with $O(2^d)$ time complexity for lookups in a $d$-dimensional space, and requires $O(d)$ many arithmetic operations per query. Hence, the total computational complexity of Perlin noise is $O(d\cdot 2^d)$. 

## Implementations
### Reference 
The following is the improved reference implementation of Perlin noise given by Perlin in his follow up paper.

```Java
// JAVA REFERENCE IMPLEMENTATION OF IMPROVED NOISE - COPYRIGHT 2002 KEN PERLIN.

public final class ImprovedNoise {
   static public double noise(double x, double y, double z) {
      int X = (int)Math.floor(x) & 255,                  // FIND UNIT CUBE THAT
          Y = (int)Math.floor(y) & 255,                  // CONTAINS POINT.
          Z = (int)Math.floor(z) & 255;
      x -= Math.floor(x);                                // FIND RELATIVE X,Y,Z
      y -= Math.floor(y);                                // OF POINT IN CUBE.
      z -= Math.floor(z);
      double u = fade(x),                                // COMPUTE FADE CURVES
             v = fade(y),                                // FOR EACH OF X,Y,Z.
             w = fade(z);
      int A = p[X  ]+Y, AA = p[A]+Z, AB = p[A+1]+Z,      // HASH COORDINATES OF
          B = p[X+1]+Y, BA = p[B]+Z, BB = p[B+1]+Z;      // THE 8 CUBE CORNERS,

      return lerp(w, lerp(v, lerp(u, grad(p[AA  ], x  , y  , z   ),  // AND ADD
                                     grad(p[BA  ], x-1, y  , z   )), // BLENDED
                             lerp(u, grad(p[AB  ], x  , y-1, z   ),  // RESULTS
                                     grad(p[BB  ], x-1, y-1, z   ))),// FROM  8
                     lerp(v, lerp(u, grad(p[AA+1], x  , y  , z-1 ),  // CORNERS
                                     grad(p[BA+1], x-1, y  , z-1 )), // OF CUBE
                             lerp(u, grad(p[AB+1], x  , y-1, z-1 ),
                                     grad(p[BB+1], x-1, y-1, z-1 ))));
   }
   static double fade(double t) { return t * t * t * (t * (t * 6 - 15) + 10); }
   static double lerp(double t, double a, double b) { return a + t * (b - a); }
   static double grad(int hash, double x, double y, double z) {
      int h = hash & 15;                      // CONVERT LO 4 BITS OF HASH CODE
      double u = h<8 ? x : y,                 // INTO 12 GRADIENT DIRECTIONS.
             v = h<4 ? y : h==12||h==14 ? x : z;
      return ((h&1) == 0 ? u : -u) + ((h&2) == 0 ? v : -v);
   }
   static final int p[] = new int[512], permutation[] = { 151,160,137,91,90,15,
   131,13,201,95,96,53,194,233,7,225,140,36,103,30,69,142,8,99,37,240,21,10,23,
   190, 6,148,247,120,234,75,0,26,197,62,94,252,219,203,117,35,11,32,57,177,33,
   88,237,149,56,87,174,20,125,136,171,168, 68,175,74,165,71,134,139,48,27,166,
   77,146,158,231,83,111,229,122,60,211,133,230,220,105,92,41,55,46,245,40,244,
   102,143,54, 65,25,63,161, 1,216,80,73,209,76,132,187,208, 89,18,169,200,196,
   135,130,116,188,159,86,164,100,109,198,173,186, 3,64,52,217,226,250,124,123,
   5,202,38,147,118,126,255,82,85,212,207,206,59,227,47,16,58,17,182,189,28,42,
   223,183,170,213,119,248,152, 2,44,154,163, 70,221,153,101,155,167, 43,172,9,
   129,22,39,253, 19,98,108,110,79,113,224,232,178,185, 112,104,218,246,97,228,
   251,34,242,193,238,210,144,12,191,179,162,241, 81,51,145,235,249,14,239,107,
   49,192,214, 31,181,199,106,157,184, 84,204,176,115,121,50,45,127, 4,150,254,
   138,236,205,93,222,114,67,29,24,72,243,141,128,195,78,66,215,61,156,180
   };
   static { for (int i=0; i < 256 ; i++) p[256+i] = p[i] = permutation[i]; }
}
```

This algorithm uses a fixed permutation matrix, and is therefore a [[Noise functions#^f341a0|coherent noise function]], the matrix can be randomized to produce more varied results. See [nividia](https://developer.nvidia.com/sites/all/modules/custom/gpugems/books/GPUGems/gpugems_ch05.html) for more implementation details.


# Simplex noise
Simplex noise, [[@Perlin_2001]], was made to correct some of the directional artifacts present in the original version of [[Lattice gradient noises#Perlin noise|perlin noise]], simplex noise is _visually isotropic_, while also obtaining lower computational overhead in higher dimensions (as well as being simpler to implement at the hardware level). 

Rather than using a table lookup scheme to compute the index of a pseudo-random gradient at each sounding vertex of a lattice grid, like in the original implementation of Perlin noise, Simplex noise can be implemented directly using uses bit-manipulation. Additionally, Simplex noise uses a simplicial grid, which requires only four component evaluations (in 3D) for any query point with a spherically symmetric kernel multiplied by a linear gradient. See the following sections for more detail.

**Computing index of pseudorandom gradient:** Given an integer lattice point $(X,Y,Z)$, the lower six bits of the sum $$\begin{align}i=\,&b(X,Y,Z,0)+b(Y,Z,X,1)+b(Z,X,Y,2)+b(X,Y,Z,3)+\\ &b(Y,Z,X,4)+b(Z,X,Y,5)+b(X,Y,Z,6)+b(Y,Z,X,7),\end{align}$$where $b(\cdot)$ uses its last argument as a bit index into a very small table of predefined bit patterns, is used to generate a gradient direction. And example of the bit pattern table is $$bitPatterns[\,] = \{ 0x15,0x38,0x32,0x2c,0x0d,0x13,0x07,0x2a \}$$
**Using the index to derive pseudorandom gradient:** The six bit pseudo-random index, $i$, is then converted into a _visually uniform gradient vector_, which is easy to include into a derivative calculation (while requiring no multiplication operations to compute). In particular, the lower three bits of $i$ are used to compute a (discrete) magnitude vector $(p,q,r)$ with either zero or one valued entries based on each of $x,y$, and $z$; with the upper three bits used to determine an octant for the resulting gradient (positive or negative sign in each of $x,y$, and $z$).

**Point in Simplex Location:** A query point $(x,y,z)$ is located within a simplex $\triangle$ by the following method: 
  1. The coordinates of the query point are skewed; $(x',y',z')=(x+s,y+s,z+s)$ where $s=(x+y+z)/3$.
  2. The integer portion of the skewed coordinates identify a surrounding unit cube with lowest coordinates values of $(X',Y',Z') = (\lfloor x' \rfloor, \lfloor y'\rfloor, \lfloor z\rfloor)$.
  3. The coordinates of the located corner vertex are then unskewed; $(X,Y,Z) = (X'-s,Y'-s,Z'-s)$.
  4. The simplex that contains the query point $(x,y,z)$ relative to $(X,Y,Z)$ 

(TODO - finish and rephrase)

**Simplicial kernel:** If a query point is located in the direction $(u,v,w)$ from a given (neighbouring) simplex vertex, then this vertex contributes $$\begin{cases}8[0.6 - 2(u + v + w)]^4 & \text{if }\;\; 0.6 - 2(u + v + w)>0\\
0 & \text{otherwise.}\end{cases}$$to the final result.

## Complexity 
Simplex noise scales on the order of $O(d)$ for $d$-dimensions, with $O(d)$ arithmetic operations per query. Thus, Simplex noise has total computational complexity of $O(d^2)$.

## Implementations
### Reference 
The following is the reference implementation given by Perlin in [[@Perlin_2001]].

```Java
// JAVA REFERENCE IMPLEMENTATION OF SIMPLEX NOISE - COPYRIGHT 2001 KEN PERLIN.
public final class Noise3 {
  static int i,j,k, A[] = {0,0,0};
  static double u,v,w;
  static double noise(double x, double y, double z) {
    double s = (x+y+z)/3;
    i=(int)Math.floor(x+s); j=(int)Math.floor(y+s); k=(int)Math.floor(z+s);
    s = (i+j+k)/6.; u = x-i+s; v = y-j+s; w = z-k+s;
    A[0]=A[1]=A[2]=0;
    int hi = u>=w ? u>=v ? 0 : 1 : v>=w ? 1 : 2;
    int lo = u< w ? u< v ? 0 : 1 : v< w ? 1 : 2;
    return K(hi) + K(3-hi-lo) + K(lo) + K(0);
  }
  static double K(int a) {
    double s = (A[0]+A[1]+A[2])/6.;
    double x = u-A[0]+s, y = v-A[1]+s, z = w-A[2]+s, t = .6-x*x-y*y-z*z;
    int h = shuffle(i+A[0],j+A[1],k+A[2]);
    A[a]++;
    if (t < 0)
      return 0;
    int b5 = h>>5 & 1, b4 = h>>4 & 1, b3 = h>>3 & 1, b2= h>>2 & 1, b = h & 3;
    double p = b==1?x:b==2?y:z, q = b==1?y:b==2?z:x, r = b==1?z:b==2?x:y;
    p = (b5==b3 ? -p : p); q = (b5==b4 ? -q : q); r = (b5!=(b4^b3) ? -r : r);
    t *= t;
    return 8 * t * t * (p + (b==0 ? q+r : b2==0 ? q : r));
  }
  static int shuffle(int i, int j, int k) {
    return b(i,j,k,0) + b(j,k,i,1) + b(k,i,j,2) + b(i,j,k,3) +
           b(j,k,i,4) + b(k,i,j,5) + b(i,j,k,6) + b(j,k,i,7) ;
  }
  static int b(int i, int j, int k, int B) { return T[b(i,B)<<2 | b(j,B)<<1 | b(k,B)]; }
  static int b(int N, int B) { return N>>B & 1; }
  static int T[] = {0x15,0x38,0x32,0x2c,0x0d,0x13,0x07,0x2a};
}
```
