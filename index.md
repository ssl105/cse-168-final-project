# Rendering Gems by Scott Lee
![gems](images/gems.jpeg)

# Project Overview

I was first interested in implementing the interaction between gems and aurora borealis, but after doing some preliminary research it would have been too much to handle alone given the timespan. I tried to  focus on rendering gems and implementing the research from this [paper](https://dl.acm.org/doi/10.1145/1015706.1015708), but ultimately thought that implementing [photon mapping](https://graphics.stanford.edu/courses/cs348b-00/course8.pdf) would be more interesting.

## Implementation

### objloader
I was able to find a free diamond model on [cgtrader](https://www.cgtrader.com/free-3d-models/scripts-plugins/modelling/low-poly-diamond-6899deeb-29ce-4d74-aa69-cc5d6418a390). From there I incorporated [tinyobjloader](https://github.com/tinyobjloader/tinyobjloader) into my code to work together with the parser used in previous assignments. I added a new command for the test scenes: 

`obj pathToObjFile`

This allows me to utilize previous scenes and reuse transformation and material command formats. This also makes it easier to add multiple obj files to one scene.

### Photon mapping

I started the process by creating a new ray generation program and closest hit integrator on optix. Some pseudocode was given for ray generation in the photon mapping paper. I used stratified sampling to evenly sample the origin for each photon ray on a quadlight. I also used cosine sampling for the direction of the photon since they are more likely to travel in aligment with the normal of the light.

For the integrator, I followed the russian roullete method outlined in the paper. Given $$K_{d}$$ for diffuse and $$K_{s}$$ for specular, the probability of reflection is calculated as such: 

$$P_{r} = max(K_{d}.x + K_{s}.x, K_{d}.y + K_{s}.y, K_{d}.z + K_{s}.z)$$

The probability of absorbtion would be $$P_{a} = 1 - P_{r}$$. 
Furthermore the probability of diffuse reflection:

$$P_{d} = \frac{K_{d}.x + K_{d}.y + K_{d}.z}{K_{d}.x + K_{d}.y + K_{d}.z + K_{s}.x + K_{s}.y + K_{s}.z}P_{r}$$

Probability of specular reflection:

$$P_{s} = \frac{K_{s}.x + K_{s}.y + K_{s}.z}{K_{d}.x + K_{d}.y + K_{d}.z + K_{s}.x + K_{s}.y + K_{s}.z}P_{r}$$

$$\xi\in[0, P_{d}] \rightarrow$$ diffuse reflection

$$\xi\in[P_{d}, P_{r}] \rightarrow$$ specular reflection

$$\xi\in[P_{r}, 1] \rightarrow$$ absorbance

Given the power of an incoming photon $$P_{inc}$$, the power of the specular reflected photon is calculated as such:

$$P_{refl}.x = P_{inc}.x K_{s}.x / P_{s}$$

$$P_{refl}.y = P_{inc}.x K_{s}.y / P_{s}$$

$$P_{refl}.z = P_{inc}.x K_{s}.z / P_{s}$$

The diffuse reflect power can be calculated in the same ways as above. 

To determine whether a ray is transmitted or reflected I use Sh
ven absorbance coefficient $$K_{a}$$, which is an rgb value, the color that is transmitted with each photon would be calculated by subtracting the coefficient by 1: $1 -K_{a}$$

### Images





# Resources
 - [Photon Mapping](https://graphics.stanford.edu/courses/cs348b-00/course8.pdf)
 - [Reflection and Refraction](https://graphics.stanford.edu/courses/cs148-10-summer/docs/2006--degreve--reflection_refraction.pdf)
 - [tinyobjloader](https://github.com/tinyobjloader/tinyobjloader)
 - [median of medians algorithm](https://www.youtube.com/watch?v=RItfXpx3SD4)
 - [heap implementation](https://algorithmtutor.com/Data-Structures/Tree/Binary-Heaps/)
 - [Slides found online for KNN algorithms](https://www.colorado.edu/amath/sites/default/files/attached-files/k-d_trees_and_knn_searches.pdf)
 - [Video on KD Trees](https://www.youtube.com/watch?v=Glp7THUpGow&ab_channel=StableSort)
 - [SIGGRAPH 04: Graphics gems revisited](https://dl.acm.org/doi/10.1145/1015706.1015708)

{% include lib/mathjax.html %}
