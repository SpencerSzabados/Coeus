_Noise Worms_ are composed of joined line segments that are iteratively constructed by orientating new segments in the direction given by a noise function evaluated at the endpoint of the prior segment.

A key difference between defining a "worm" volume based on a select range of values from volumetric noise (e.g., [[Lattice gradient noises#Perlin noise|perlin noise]]) and noise worms, is that worms are guaranteed to be contiguous due to the construction process.

Nose worms have been used to create tunnels (or paths) in procedurally generated games.

# Methods of construction 
One specific method of construction, is to draw a _reference_ line segment within the noise domain and used it to perform directional lookups at points along its length corresponding to segments on the noise worm; this is the method used by http://libnoise.sourceforge.net/examples/worms/. Using this method the worms can be animated by translating the reference segment within the noise domain and then updating the directions of the worms segments accordingly. Provided the noise function used is [[Noise functions#^f341a0|coherent]] (smooth) each worm segment will move in a smooth fashion.

I implemented this method in JavaScript, see [[Perlin worms]].

