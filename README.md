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

## See also

* [The repository of the software implementing the Hashed Shading algorithm.](https://github.com/BeardedPlatypus/nTiled)
* [The repository of the complete master thesis (in dutch).](https://github.com/BeardedPlatypus/thesis-latex)


