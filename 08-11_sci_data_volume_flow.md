# SciVis Intro

104. Describe all the parts of a typical scene required for 3D rendering on a graphics card. (4 Pt)  ???

Vertex attri of 3D model in context of meshes:
- Position: the 3D location of a vertex.
- Color: namely, the color..
- Normal: the (averaged) normal vector of the vertex's neighbouring faces.
- Texture Coordinates: the coordinates in texture space that the vertex
    corresponds to.

Surface difinitions, and their advanteges/disadvantages:
- Triangle Mesh: a mesh of triangles to approximate the surface. is discrete,
    perfect for storing and triversal algorithm. Not Smooth, loss of accuracy.
    differential geometry doesn't apply.
- Parametric Suface: is a 2D mapping from R2 to R3, good for texturing,
    differential analysis, accurate computation for i.e. curves, surface,
    volume. Hard to find explicit (analytical) parametrization for irregular
    surfaces, limited to simple geometry: e.g. torrus.
- Height Map: is a special form of parametrization: e.g. let x = u, y = v, z =
    h(u,v). Easy differential calculations, easy texturing, intuitive. Limited
    usage (only for terrain-like surfaces).
- Iso-surface: implicite surface function: f(x,y,z)=0, defines the boundary.
    Easy to identify inside/outside/on boundary. No explicite def of the surface
    therefore hard to reconstruct. (test all xyz combinations).. 

**Light Sources**
- Directional light source: parallel rays = point light source from infinitely
    far away. Light direction constant.
- Point light source: rays rediation from a point. Light direction depends on
    relative positions from object to light source.


**Define simple model of pinhole camera**, name the required internal and
external parameters.
- Internal parameters: Pixel resolution w and h of sensors, Opening angle,
    distance znear and zfar (near and far clipping planes)
- External: camera location, view-direction

**View Frustum**
is a frustum, defined by the near and far clipping plane and for edges. It
bounds "what can be seen"

**Math structures for 3d model transformation, how are they used**  
Transform matrix. The 3d can be viewed as a matrix, each column vector
represents one vertex position. By applying (multiplying) the transformation
matrix to the model matrix, the product matrix will be the result of
transformation.

What is the advantage of using homogenous vector and matrix representations
regarding 3D transformations. (2 Pt)

by adding addition w-component to the vectors/matrix, the operations are
extended to affine space. Vector and points are treated differently. The most
trivial advatage: Matrix products can not produce translation (i.e. shifting)
without the additional component. 

Given is the sequence of steps in the rendering process from a scene object
with its vertex positions in object coordinates to the rendering-ready
positions in window coordinates. Fill out the remaining fields. (5 Pt)

```
Object Coords --->  Eye Coords  ----> Clip Coords ---> Window Coords
            Model View         Projection        Viewport
3D                  3D                2D               2D
```

Main shader units in modern OpenGL pipeline?  
Vertex shader, geometry shader and fragment shader.

Shortly describe how the data is transferred from the CPU to the GPU and how the data is processed afterwards. (2+4 Pt)

Data trasferred from CPU to GPU: vertex data to vertex buffers, pixel data to texture objects.
![GL](img/GPU.png)

**Basic lighting calculatons** (slide 21)  
Q116-117 


**z-Buffer approach for depth testing**  
storing depth per pixel, keep only the front most fragment.

**regarding transparency, how visibility sorting can be done on fragment level**  

**Back-to-front rendering and the over operator**  

![trans](img/trans.png)

**Halo:** A small boundary around semi-transparent objects. Describe and
advantages: 121-122
- adding uni-colored less transparent boundary to 3D element.
- defined by halo color, opacity and width.
- improves the perception of visibility order (more clear who's front who's back)

---
**Scalar field** 

Regarding the visualization of 2D scalar fields as pixel images, there are
different approaches to optimally map the value range of the data onto the
maximum range of the color model values. One of those techniques is called
**window transfer function**. Describe this method with the help of a typical
application scenario. (3 Pt)
- It is used to linearly transfer a range to normlized one e.g. [0,1]

    $$f_{ij}^{window} = \frac{f_{ij} - f_{min}}{f_{max} - f_{min}}$$
- e.g. for medical image, interactively setting the fmin and fmax can bring
    contrast to interesting parts.

Regarding the visualization of 2D scalar fields as pixel images, there are
different approaches to adapt the value range of the color space to the human
visual perception. In this context, describe the technique **gamma correction.**

![gamma](img/gamma.png)

**Histogram equalization** 125
![histo](img/histo.png)

**Color Mapping**

**Produce color bands for given 2D scalar data**

**Scalar: contour lines and color bands**

**3D occlusion: selection, projection, slicing, clipping** 128
- Selection
- Projection
- Slicing
- Clipping

**Contouring** slide 42

**Extract iso-lines and iso-surfaces**

**Compute normals in iso-surface** : vector of partial derivitives.

**Marching squares** input, output and steps?

**Grid cell: Ambiguity im marching squares** ..






# 10 - VOLUME

## OUTLINE

- indirect vol. vis.
    - slicing
    - contouring
- direct vol. rendering
    - Compositing
    - transfer function design
    - rendering approaches

![overview](img/vol_overview.png)


**Voxel**: volume element grid
- corresponds to observation point with feature value (vertices of voxel grid)
- e.g. sampling points...
- edge connects 2 voxels
- cell: cube/tetrahedron spanned by 8/4 voxels
- face: separates two cells

**Dual grid**
- dual cell: one per vertex, corresponding to voronoi cell
- dual vertex: one per cell.
- dual edge: one per face: connects dual vertices


**Interpolation schemes**: nearest neighbor / trilinear

**Segmentation / Labeling**
- Goal: determine for each voxel a group index(which structure it belongs)

## Indirect Vol. Vis.

**Slicing - Oblique**
- An oblique slicing is defined by a plane
- The plane is defined by 1) 3 points 2) plane normal and signed distance from
    origin.
- interpolation needed if slicing a voxel grid
- Rendering: CPU and GPU approach

**Contouring**
- iso-surfaces: from an iso-value S0
- iso-bands from two values S0 and S1
- Volume Segment on labeled data: all grid faces where two adjacent
    voxel belong to different segments
- Cuberille and Dual contouring


**Marching Cubes**

##Direct VolViz: compositing##



## QUEST.

**Compare direct/indirect vol vis, basic approaches? general diffs?**

- indirect: slicing, contouring
- direct: compositing, transfer function design, rendering approaches.
- DIFF //TODO
    - indirect vol. vis. is oblique, only the boundary surface can be seen
    - direct vol vis. can show both the surface and the inside.

**Oblique Slicing?, CPU and GPU approach for rendering oblique slices via 3D
texture**

**Dual Contouring**

**Marching Cubes Algorithm**

**162,163,164,165**

**Direct vol. vis. , ray, sampling and compositing**

**167,168: max, average, first**

169. What is the emission-absorption model and how does the compositing mode blending generally works?  
170. What are the two basic parameters controlled by a transfer function? (0.5+0.5 Pt)  
171. What are the typical tools of a transfer function editor? (3 Pt)  
172. What is the purpose of a histogram when designing a transfer function? (1 Pt)  
173. Given a table direct vs. indirect volume rendering methods... Assign the following techniques to either
direct or indirect volume rendering: e.g. texture slicing, shear warp, raycasting, dual contouring, marching
cubes, cuberille (0.5 Pt each)  
174. How can you utilize the shader units on a GPU for raycasting? (3 Pt)  
175. Name and shortly describe two acceleration techniques for raycasting. (1+2 Pt)  











