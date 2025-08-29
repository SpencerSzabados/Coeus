There are many different kinds of light _simulation_ rendering techniques that fall under the umbrella of "ray tracing" but differ in their implementations (design goals) sufficiently as to be given a different, more specific, names. 

# Radiosity
https://en.wikipedia.org/wiki/Radiosity_(computer_graphics)

# Light transport 
All physically based ray tracing methods, among others, belong to the class of methods called _light transport algorithms_, as they operate by simulating how light interacts with surfaces (or objects) as it moves through a scene to generate images.

https://www.scratchapixel.com/lessons/3d-basic-rendering/ray-tracing-overview/light-transport-ray-tracing-whitted

# Raycasting
Like in raytracing, rays are cast ([[Line segment intersection#Ray shooting|ray shooting]]) from the eye of the observer  (one per pixel) to sample the light (radiance) value traveling towards the observer from the first object intersected by the ray. The simplicity of raycasting, and distinction from other raytracing methods, is colour and luminance values are computed without recursively tracing additional rays. This cutoff increases the speed of rendering, but eliminates the ability to accurately rendering reflections, refractions, or shadows; however, all of these elements can be approximated to an extent using texture maps. https://en.wikipedia.org/wiki/Ray_casting

There are many possible perspective (view) models for the observer to shoot rays in accordance with. For modeling convenience, a typical coordinate system for the camera has the screen in the $X-Y$ plane, the scene in the $+Z$ half space, and the focal point on the $-Z$ axis.
![[330px-Cameras_local_coordinate_system.jpg]]

## Realistically shaded 3D geometry


## 2D Raycasting for rendering 3D scenes 
Raycasting, as implemented in early video games, is a simplified version of [[Ray tracing and light transport#Raytracing|raytracing]] that is capable of rendering 3D scenes from a limited set of perspectives, by operating on top-down 2D planar slices of the objects being drawn. After a 2D object is hit by a ray, indicating the associated 3D object is visible to the camera and should be drawn, the object is drawn as flat texture (perhaps on more complex geometry) in the location the ray intersected the associated 2D representative, more specifically, projection distortion is applied to the surface texture and an entire vertical column is copied into the frame.


## Volumetric ray casting 
Volumetric ray casting or tracing are techniques to for _volumetric rendering_, which allows for the visualization of 3D solid data, e.g., particle effects, transparent/translucent materials, CT and MIR scan data, etc, without fitting geometric primitives to the data (not just surfaces). Other techniques used volumetric rendering include, voxel based binary space partitions and marching cube algorithms; voxels are sometimes used in conjunction with ray casting to improve performance.

### Methods
#### Hybrid ray-voxel approach
The method outlined in [[@Levoy_1990]] (and https://web.cs.wpi.edu/~matt/courses/cs563/talks/powwie/p1/ray-cast.htm)  is made for visualizing discrete multidimensional data in 3D, where the color and opacity of regions are defined using voxels. 

This method makes use of [[Phong shading]]


# Raytracing 
Raytracing based rendering algorithm operate in _image order_ , iterating over the pixels of the image to be produce rather than iterator over the objects in the scene to be rendered. 

## Distributed ray tracing 
https://en.wikipedia.org/wiki/Distributed_ray_tracing
https://computergraphics.stackexchange.com/questions/6/why-does-monte-carlo-ray-tracing-perform-better-than-distributed-ray-tracing
http://www.cs.cornell.edu/courses/cs4620/2013fa/lectures/22mcrt.pdf

# Path tracing
Path tracing is a sophisticated form of ray tracing that uses Mote-Carlo sampling methods to faithfully recreate global illumination effects, in addition to those effects that have to be specifically implemented in more conventional ray tracing methods (e.g., soft shadows, depth of field, motion blur, etc.), by integrating over the luminance arriving to a single point on a surface from multiple randomly sampled directions (paths). See, (https://en.wikipedia.org/wiki/Path_tracing).

Due to its accuracy, and algorithmic simplicity, path tracing is used to generate reference images when testing the quality of other rendering algorithms. However, the path tracing algorithm is relatively inefficient, as a very large number of rays must be traced to get high-quality images free of noise artifacts. 

https://raytracing.github.io/books/RayTracingInOneWeekend.html

### Direct light sampling along paths

## Volumetric path tracing