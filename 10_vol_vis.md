# 10 - VOLUME

## OUTLINE / TERMS

- indirect vol. vis. falls back to surface rendering
    - slicing
    - contouring (iso-surface)
- direct vol. rendering. Volume rendering
    - Compositing
    - transfer function design
    - rendering approaches

![overview](img/vol_overview.png)

**Data Specs**:
- Grids: most regular (voxel) / unstructured grids / curvi-linear grids ..etc.
- Feature space: scalar (1D)
- Optional segmentation/ labeling: voxel labeled to different group IDs (e.g.
    for different anatomic structures)

**Voxel**: **vol**ume **el**ement grid
- corresponds to observation point with feature value (vertices of voxel grid)
- e.g. sampling points...
- edge connects 2 voxels
- cell: cube/tetrahedron spanned by 8/4 voxels
- face: separates two cells

**Dual grid**
- dual cell: one per vertex, corresponding to **voronoi cell**
- dual vertex: one per cell.
- dual edge: one per face: connects dual vertices


**Interpolation schemes**: nearest neighbor / trilinear

**Segmentation / Labeling**
- Goal: determine for each voxel a group index(which structure it belongs)

## Indirect Vol. Vis.

**Orthogonal Slicing** (s.14)
- Mostly for medical imaging
- Slices are in 3 orthogonal (x,y,z) directions

**Oblique Slicing**
- An oblique slicing is defined by a plane
- The plane is defined by 1) 3 points 2) plane normal and signed distance from
    origin.
- interpolation (typically trilinear) needed if slicing a voxel grid. Also can
    be solved by using 3D texturing.
- Rendering: CPU and GPU approach (see quests)

**Contouring**
- iso-surfaces: from an iso-value S0
- iso-bands from two values S0 and S1
- Volume Segment on labeled data: all grid faces where two adjacent
    voxel belong to different segments
- Cuberille and Dual contouring

**Cuberille**
- Classify all voxels [inside,outside]
- fill dual cell of interior voxels
- for all edges connecting interior with exterior, add dual face to the
    cuberille-surface.
- cuberille surface is a pure quadrilateral mesh.

**Dual Contouring**
- move dual vertices onto iso-surface.  
- This is more smooth!
![dual](img/dual.png)


**Marching Cubes**  

The algorithm: fast with lookup table.
- iterate all voxel cells (can be shortcoming)
- classfy 8 knots inside/outside and create 8-bit index. (the indexing manner
    can be any, but must be **consistent**)
- lookup cut edges (edges that connects inside and outside vertices) and compute
    edge points (do a linear interpolation) with normals of interpolated voxel
    gradients
- lookup triangulation

remarks:
- doesn't not necessarily need to look up cut edges, since this can be done with
    simple boolean computations
- ambiguities are not resolved according to trilinear interpolation (???)
- potential number of triangles: huge, hard for realtime rendering
    - caching/ reusing
    - compute triangles in (geometry) shader pipeline on GPU
    - simplify triangle mesh in smooth reigions of iso-surfave or extract from
        **octree** instead of grid
    - **Grid sanpping**: elimite very short edged triangles: if edge point "very
        close" to grid vertex then move it to grid vertex..

**Marching Tetrahedra**  
- only 2 cases for classfication (considering symmetries) in tetrahedra meshes.
- NO ambiguous cases
- pitfall: tessellation is not cool: one cube splits into 5 or 6 tetrahedral.

##Direct VolViz##


**Compositing**  
- need to show a **COMBINATION** of values along a ray from eye through the
    pixel
- sample the locations along the ray.
- **Compositing techniques: aggregate the samples's scalar values into a final
    pixel**

Such compositing can be: first, max, blending, average, first ... e.g.  
- blending
    - for blending transfer functions are needed. (for both color and opacity)
    - blending allows depth perception. (ording matters in opacity maxing!)
    - Emission-absorption model: I = E1 + T1(E2 + T2(E3 + T3(...)))
    - (optional if the ray encounters a point above a threashold, the remaining
        points are not considered)
- the first: first point value along the ray above a threashold.(basically
    iso-surface)
- averaging: is indepent of depth ordering: no depth perception, not even
    rotating. (similar to x-ray image)
- max: often used in MRT/CT. Independent of depth ordering but depth
    perception is better during rotation..

**Transfer Function Design (for blending)..**

Houndsfield Scale

**Rendering Approaches** (slide 42.)
- Texture-Slicing (slicing in the eye-coord domain)
- Shear Warp (slicing in volume domain, then transfer to eye domain) not quite
    used nowadays..
- Raycasting (typical approach today, for regular grids)
- Projection 

**Forward/ Backward** Slide 43.

## QUEST.
158. Compare direct and indirect volume visualization. What are the basic
     approaches? What are the general differences? (2+2 Pt)
- direct vol. vis. vis renders the volume in a transparent fashion, the whole
    volume is shown. Approaches: compositing, transfer function design,
    dendering approaches.
    - Compositing
    - (transfer function design for blending)
    - rendering approaches
- indirect vol. vis. is oblique, i.e. only the front most element along the view
    direcion is visible. Basic approaches are contouring and slicing.

159. **What is Oblique Slicing? Describe a CPU and a GPU approach for rendering
     oblique slices via 3D texture. (2+1+1 Pt)**
- cuts the volume with a plane and shows the cross section.
- The trilinear interpolation is automatically solved by using 3D texture.
- CPU: compute intersection polygon of plane with volume box, then use 3D
    texturing.
- GPU: define a clipping plane along the cutting plaing and use the GPU clipping
    functionality (thefore the "outside" part is no longer visible.)


160. Describe the technique Dual Contouring. (3 Pt)
- classify all voxels in [inside,outside], fill dual cell of interior
    voxels. For all edges connecting interior with exterior, add dual face to
    the cuberille-surface.
- Dual Contoring: further move the dual vertices onto the iso-surface (so that
    the iso-surface could match the iso-value). This could be done by moving the
    dual vertices in the (+-) gradient directions (think about projection).


161. Describe the Marching Cubes algorithm with the help of a sketch. (3 Pt)
- Fast impl. with lookup table.
-

162. Given a picture of a 3D grid cell and an iso-value v... Classify the voxel
     of the cell based on the iso-value v and draw the resulting iso-surface
     intersection points onto the edges. (1+1 Pt)

163. Regarding the Marching Cubes algorithm, how many cases exist (without
     exploiting symmetries)? (1 Pt)
- 2^8 = 256.

164. A common problem with marching cubes is that because of the creation of
     triangles with very short edges, an extremely high number of triangles can
     be produced. Describe a solution for that issue. (1 Pt)
-  grid snapping: if a point is considered "close enough" (e.g. closer than a
    percent threashold) to the grid vertex.
    then it can be snapped to the grid.

165. Describe another technique to reduce the number of generated triangles
     produced by Marching Cubes. (1 Pt)
- short edge collapsing.

166. Describe the basic procedure for direct volume visualization. Consider the
     terms ray, sampling and compositing. (3 Pt)
- 


167. Given pictures of different compositing methods for direct volume
     rendering... Assign the following compositing methods for direct volume
     rendering to the pictures: max, average, first (2 Pt)
- slide 31.

168. Shortly describe the following compositing methods for direct volume
     rendering: max, average, first (1+1+1 Pt)
- max: use the max value of the sample points. average: literal. first: use the
    value of the sample that the ray first encounters a threshold
    value(effectively iso-surface)

169. What is the emission-absorption model and how does the compositing mode
     blending generally works? (1+1 Pt)

170. What are the two basic parameters controlled by a transfer function?
     (0.5+0.5 Pt)

171. What are the typical tools of a transfer function editor? (3 Pt)
- is this seriously a question?

172. What is the purpose of a histogram when designing a transfer function? (1
     Pt)

173. Given a table direct vs. indirect volume rendering methods... Assign the
     following techniques to either direct or indirect volume rendering: e.g.
     texture slicing, shear warp, raycasting, dual contouring, marching cubes,
     cuberille (0.5 Pt each)

174. How can you utilize the shader units on a GPU for raycasting? (3 Pt)

175. Name and shortly describe two acceleration techniques for raycasting. (1+2
     Pt)
