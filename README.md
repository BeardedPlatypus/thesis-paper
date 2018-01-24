<img src="https://github.com/BeardedPlatypus/thesis-paper/blob/master/teaser.png?raw=true" alt="Teaser image" title="Hashed Shading" align="middle" height="222px" />

# Forward and Deferred Hashed Shading Paper

## About

This repository houses the 
[Forward and Deferred Hashed Shading paper](https://github.com/BeardedPlatypus/thesis-paper/blob/master/paper.pdf) 
and corresponding source files produced as part of my master thesis in computer
science. The paper introduces the Hashed Shading light assignment algorithm 
used to render a large number of lights efficiently. This algorithm is compared
with the popular light assignment algorithms: Tiled Shading and Clustered Shading.

## Abstract

_(as written in [paper](https://github.com/BeardedPlatypus/thesis-paper/blob/master/paper.pdf))_

This paper introduces the Hashed Shading algorithm, a light assignment algorithm
for forward and deferred shading. It uses a subdivision independent from the view
frustum in order to reuse data structures between frames. The scene is subdivided
into cubes of a specified size and represented using a linkless octree to store
the data efficiently in memory and allow for a fast retrieval of relevant lights
during shading.
The performance of Hashed Shading is compared to both Tiled and Clustered Shading.
Forward Hashed Shading reduces the number of light calculations and the execution
time by a factor of two compared to Forward Tiled Shading. It achieves a similar
reduction in the number of light calculations as Clustered Shading. Furthermore 
the Hashed Shading algorithm scales slightly better in regards to resolution than
Tiled and Clustered Shading due to the camera-independent subdivision.
Currently Hashed Shading does not support dynamic lights, and requires significant
memory to store the linkless octree. Solutions for these issues are proposed but
have not been implemented.

## Algorithm

The Hashed Shading algorithm uses an octree to subdivide the scene space. In each
leaf node, the intersecting finite lights are stored. This octree can be queried 
when frames are subsequently rendered, with the scene positions of pixels. Each
query returns the set of lights which intersect with the leaf node the pixel falls
within. Thus reducing the set of lights that needs to be evaluated.  

This octree data structure is independent from the view frustum, and thus the 
creation of the initial octree can executed as a pre-process. 

In order to efficiently access the octree on the GPU, the 
[linkless octree implementation](https://hub.hku.hk/bitstream/10722/134617/2/content.pdf?accept=1) 
is used. This approach utilises spatial hash maps which are saved in textures, 
to represent each layer of the octree. Because each layer is represented by a
texture, it can be efficiently accessed on the GPU. 

## Technique comparisons

Hashed Shading is compared with Tiled Shading, Clustered Shading and runs 
without any light assignment algorithms. The results of these experiments
are visualised in the following videos. On the left the actual rendered 
frame is displayed, on the right the number of light calculations per pixel
is visualised, where a white pixel corresponds with the maximum number of 
light calculations, and black with no light calculations. These experiments
were executed for three demo scenes, which can be found in the 
[data repository](https://github.com/BeardedPlatypus/thesis-data).

### Indoor Spaceship Scene

<iframe width="1280" height="720" src="https://www.youtube.com/embed/u9o_V4ynB_A" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

*Based upon: [3D Render Challenge #18](http://www.3drender.com/challenges/) modelled by Juan Carlos Silva.*

### Piper's Alley Scene

<iframe width="1280" height="720" src="https://www.youtube.com/embed/nIyifYvU9vI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

*Based upon: [CGSociety Lighting Challenge #42](http://forums.cgsociety.org/showthread.php?t=1309021) made by Clint Rodriues.*

### Ziggurat Scene

<iframe width="1280" height="720" src="https://www.youtube.com/embed/HrqiPATdB0Y" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

*Based upon: [Sintel Open Movie Ziggurat Scene](https://durian.blender.org).*


## See also

* [The repository of the software implementing the Hashed Shading algorithm.](https://github.com/BeardedPlatypus/nTiled)
* [The repository of the complete master thesis (in dutch).](https://github.com/BeardedPlatypus/thesis-latex)
* [The repository of all the data gathered presented in this paper.](https://github.com/BeardedPlatypus/thesis-data)


