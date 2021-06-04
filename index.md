# Rendering Gems by Scott Lee
![gems](images/gems.jpeg)

# Project Overview

I was first interested in implementing the interaction between gems and aurora borealis, but after doing some preliminary research it would have been too much to handle alone given the timespan. So, I decided to simply focus on rendering gems and implementing the research from this [paper](https://dl.acm.org/doi/10.1145/1015706.1015708). 

## Implementation

I was able to find a free diamond model on [cgtrader](https://www.cgtrader.com/free-3d-models/scripts-plugins/modelling/low-poly-diamond-6899deeb-29ce-4d74-aa69-cc5d6418a390). From there I incorporated [tinyobjloader](https://github.com/tinyobjloader/tinyobjloader) into my code to work together with the parser used in previous assignments. I added a new command for the test scenes: 

`obj pathToObjFile`

This allows me to utilize previous scenes and reuse transformation and material command formats. This also makes it easier to add multiple obj files to one scene.

$$\xi_{1}\in[0,1]$$

### Images

## Next Steps



# Resources
 - [SIGGRAPH 04: Graphics gems revisited](https://dl.acm.org/doi/10.1145/1015706.1015708)
 - [Photon Mapping](https://graphics.stanford.edu/courses/cs348b-00/course8.pdf)
 - [tinyobjloader](https://github.com/tinyobjloader/tinyobjloader)
 - [median of medians algorithm](https://www.youtube.com/watch?v=RItfXpx3SD4)

{% include lib/mathjax.html %}
