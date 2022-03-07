# 01 - INTRO
**Define the term (data) visualization. (1 Pt.)**

- is to transform data into visual forms such that the viewers can observe the
information and perceive the features without needing to dig into the raw data.

**Describe 2 differences between SciVis and InfoVis. (2 Pt.)**  

SciVis: 
- used for physical data (e.g. medical, volume, flow)
- spatialzation is given (realworld data with entities)

InfoVis:
- used for Abstract data (conceptual). e.g. hierarchy or software metrics
- Spatialzation is chosen


**Vis pipeline**  
- Collecting data
- transforming data: data is reduced by filtering, analysis, statical methods,
    focus on important parts
- Visualizing data: resulting data mapped to visual model, translated into
    geometric and graphical information, displayed.
- gaining insights and knowledge

![pipeline](img/pipeline.png)

**Vis. Phases**
- Exploration Phase: Visualize all data, search for hypotheses
- Validation Phase: Validate hypotheses
- Presentation Phase

**Vis. Goals**
- Explore/ Calculate (analyze, reason about information)
- Communicate (explain, make decisions, reason about information)
- Control(interactive ctrl, gain knowledge for decision making asap)


**Describe the differences between Weak Coupling and Strong Coupling in the
simulation-visualization process. (2 Pt.)**

- Weak coupling: all data yields from simulation are transmited to
  visualization.
- Hyprid: transmit data in compact representation
- Strong: Simulation and Vis. are done together, the rendered images are
  transmited to display client.

**Describe a scenario where weak coupling is not feasible. (2 Pt.)**
- the simulation is on a very large scale
- limited bandwidth
- visualization requires high computing power and can't be done on client devices

**General interation tasks**  
- Overview: entire information space, global patterns  
- Zoom: interesting information objs, smaller subset  
- Filter: select subset based on attributes  
- Details-on-demand: Select objs to get details  
- Relate: relationships between objs, compare values  
- History: recording actions to undo  
- Extract: extraction of subsets of the information space and request parameters.  


**describe an advanced interaction technique (Overview + Detail, Zooming and
Panning, Focus + Context, Brushing and Linking) (2 Pt.)**
- todo


**Dimensionality of data**

![dim](img/dim.png)


**Area influences**

- Reference Point: points, not to be interpolated, vis. as individual points.
- Local refreence: continuous in space/time. interpolation needed.
- Global reference: global/constant across the samples. vis. as maybe background
  colors..

**grids/meshes (3 Pt.)**  

![grid](img/grid.png)

**Describe 2 differences between regular and unstructured grids. (2 Pt.)**
- unstructured meshes can locally adapt to data. regular grids keeps global
    constant metrics.
- unstructured shows explicit connectivity and geometry while regular shows
    both implicitly

**values properties: has metric, has order, discrete, continuous .. eg.**
- Qualitative: no metric defined
    - Nominal: no order characteristics (e.g. names, class elements). only
        equality test possible
    - Ordinal: order relation defined (first, second, third..). equality test
        and trend analysis possible
- Quantitative: metric available, inherently ordinal.
    - range can be discrete or continuous
    - quantization converts to ordinal data

**data type and examples, scalar, vectorial, tensorial...**
- Scalar: 1D values
- Vectorial nD values,  can represent direction
- tensorial: kth-order tensor with n^k dimension. scalars/vectors are 0th/1st
    order tensors

**taxonomy by Shneiderman (slide 50)**

# 02 - Perception

**What does preattentive perception mean? In what period of time does it
typically occur?**

- some visual properties can be perceived without forcusing attention. i.e. they
  pop out. or so to speak, some "obvious" things that people notice without
  thinking. **200 - 250 ms**  qualifies as pre-attentive (pop-up
  effects/attentional tuning)  


**Which visual characteristics can be perceived well preattentively, which less?
Give examples of multiple attributes that hinder preattentive perception.**
- good for: contrast
- bad for: conjunction of features (e.g. "the red triangle")


**Name and explain essential design principles.** Establish references to known
visualization techniques and explain why observance of the principles is
essential. Study well-designed advertising brochures and name the design
principles used.


- Figure and Ground (Figur-Grund-Trennung)
- Similarity (Ähnlichkeit): Similar objects perceived as belonging together
- Proximity (Nähe): Close objects perveived as belonging together, stronger than
    similarity
- Symmetry: similar objects along symmetric axis
- Closure (Geschlossenheit)
- Continuity: Smooth gradient, visual entities tend to be smooth andcontinuous.
- Relative Size
- ADDITION: 
    - Connectedness: explicit links, stronger than Proximity and Similarity. Can
        override others
    - Common Fate: in dynamic animations, grouping by tendency of motion.
    - Simplicity: multiple thinkable elements, choose the simplest (also think
        about closure)

It provides a scheme for vis. disign that follow people's perception/intuitions..

# 03 - Visual Variables
**todo , 41,42,43,45**


**Which visual variables** can be distinguished in general, and which of them can be assigned to intrinsic codes?

- **POSITION**, size, shape, value (light to dark), orientation, color, texture,
  size, value orientation
- I'm not sure about the {general, intrinsic codes..}

**If you want to visualize quantitative data as exact values or only as tendencies, which visual attributes do you typically use? Justify your decision.**
- exact values: positions and maybe size.
- only tendencies: colors, orientation, value .. 
- the second group are good for comparision, but not easy to get an exact value
  with human eye/brain..

**Bertin identified four basic perceptual questions and a number of visual
variables. Which variables are best suited for which type of perception?**

**Describe the two design goals of visual mapping, expressiveness and effectiveness.**
- Effectiveness: observer can perceive and comprehend information fast
- Expressiveness: visualization shows exactly the data and nothing more (less
    redundant)

**Monosemic encoding means. Why is that an important goal for graphical symbols?**
- Monosemic encoding: each symbol has a single meaning, as opposed to polysemic
encodings.
- To: be certain, eliminate ambiguity.

**Perceptual Properties/Types of vis. Vars (43)**

- Associative: different symbols perceived similarly -> show marks on grid
    structure / check whether variation of vis vars does not influence
    perception of grid
- Selective: different symbols perceived differently -> e.g. letter ZVQ test
- order: different values perceived in order
- quantitative: changes can be read numerically
- (length): how many perceptible distinctions
![visvar](img/visvar.png)

**Most effective vis. variable for data types (45,46)**  
![visvar2](img/visvar2.png)


**Capabilities for the use of color**
- Distinction and grouping of elements
- Emphasis and marking of elements or areas
- Replica of phenomena (e.g. red->hot, blue->code)
- Expression of mood

**Problem/Attentions using colors**
- Cultural diff.
- Color blindness
- Not good for small size objects

**Linear separation regarding the selection of colors**  
- Linear Separation: Preattentive selective perception for 3 colors is given,
  only if third color is not on linear connection between two other colors in
  perceptual color space(think about linear independence in linear algebra)
- To select: select the third color away from the two others' connection. Don't
  be like interpolated color.

**Test the above with experimental scenario**  
- image with solid objects e.g. squares with two existing colors, add one object
  with the third color and measure time to find target of third color.


Regarding the design of a color palette that is considered to visualize nominal
data we need to ensure equal lightness between each of the colors. In this
context, depict the differences between **lightness and brightness.** (2 Pt)

**Color Properties**
- Radiance, the light power transported along rays. can be specialized per
  wavelength (spectral radiance). is **physical**
- Luminace, (percepted radiance) incorporates the sensitivity of the human eyes,
  is measureable
- Brightness, **absolute** visual perception of luminance incorporating all
  perceptual effects of the human visual system. 
- Lightness (value, tone), **relative brightness** in a scene, doesn't change with
  an increase of the overall illumination, 

**Describe a method that can be utilized to produce a color palette of equal lightness.**
- two color images of face (are negative/inverted color), show side by side,
- choose grey value with reference lightness and show it on image background
- for each color in palette, map it to foreground and adjust lightness to point
    where perceived face jumps from left side to right side.

**Regarding color palette design for nominal data, which color space is usually
used to maximize linear separation?**
- I would say sRGB...  method see above..

**Describe 3 important design criteria regarding color palette design for
quantitative and ordinal data.**
- Preserve order and for quantitative attributes value difference in perceived
  colors
- Obvious start and end colors (no cycles)
- Obvious changes of the hue should be reserved for critical areas (e.g. change
  of the sign)
- Colorblind safe.


**Shortly describe a method how the perception of ordering in a color map can be
improved/achieved. (1 Pt)**
- do a gamma correction ... so that the perceptual color gradient is linear..

**Name 3 texture attributes and data type**
- Norminal Data: collection of textures.. can be nested e.g. w. category
  (leather, favric, stone..)
- **Ordinal Data**: grain size, contrast, density, regularity, orientation
- Quantitative Data: grain size, contrast, orientation

**Name 2 visual attributes (except position) that textures based on Gabor
functions can utilize. (2 Pt)**
- contrast frequency and orientation..

**Given example picture of textons... Describe the 3 visual variables that the
given Texton Mapping utilizes.**
- contrast, size, orientation..

**To synthesize a complete texture, the observed data is sampled and the resulting
textons are blended additively. Name 2 sampling approaches and describe each of
them shortly. (2+2 Pt)**
- Uniform sampling: simple, not preserving contrast
- inverse area sampling: simple, irregular
- poisson disk sampling: nice, complicated

**The last 2 may watch video for details.**

# 04 - Attribute Visualization / Multivariate Data

**Select examples of data objects with 1-n attributes and consider which
visualization forms are suitable for comparison, analysis or search tasks. For
multivariate data, try to identify primary or dominant attributes.**

**In which of the visualization forms discussed in the lecture can correlations in
a) static state and b) dynamic (i.e. through interaction) be identified?**
- ?

**Why are scatterplots such a frequently used visualization form? For which data
types and visualization tasks are they suitable? Which extension possibilities
do you know?**

**Name, describe, and compare visualization techniques for trivariate data.**

- Linked histograms  
- Scatterplot w. visual attributes  
- 3D scatterplot  

**How can visualization techniques for multivariate data be categorized in
principle? Name examples.**

**What is the core idea of the Parallel Coordinates technique, and which inherent
problem is elegantly solved with it? Say something about the complexity of this
technique.**

**Distinguish attribute and object visibility for multivariate data visualizations
and give examples for each group.**

**Why do parallel coordinates hardly support object visibility, but attribute
visibility?**


# 05 - Relations
**Why do lines play an important role in many forms of representation of
relations? Name key techniques that make effective use of lines.**
- simple and effective, easy exteinsions (e.g. width/color of lines)
- intuitively perceived as "connection"
- e.g. railways connection map


Explain and contrast the **quantity-oriented diagram** visualization types Venn
diagram, InfoCrystal and ClusterMaps with a self-chosen example.

- Venn: Objects represented as dots, each circle represents a certain
    (boolean) property. Objects sharing the same property locates in the same
    corresponding circle.
    - Quickly finding objects with desired properties
    - With logics/ set/ collections in mind.
    - Limited number of attributes.
- InfoCrystal: is a mutation of 3-attribute venn diagram.
    - Categorical
    - Simple in form
    - only 3 attr.
- ClusterMap
    - Basically the same thing as venn diagram
    - each cluster is marked by a inner node
    - more clear than venn
    - do not consider property intersection that has no element in it.


**Which essential aspects and challenges for graph visualizations are known to you?**
- Scalability

**Explain at least 5 guidelines for drawing graphs. How can we group the
rules?**

**Select sample diagrams and check the extent to which Moody's rules have been
taken into account.**

**Name and describe basic graph layout techniques and explain which aspects have
been well solved and which problems exist.**
- not sure..
- Node-Link diagrams: Force-Directed, multilevel Networks, Radical
- Adjacency Matrix
- Enclosure

**Also discuss 3D solutions or hyperbolic representations and their potential.**

**Set up an overview of all tree visualizations you learned in the lecture.
Select three sufficiently different ones and explain these techniques in
detail.**





**How can tree visualizations basically be grouped and structured?**

**Tree Vis.** approaches
- Simple Identations 
    - Shows parent-child relation
    - mostly for text (clear indentation reference for monospace text)
    - frequent scrolling required
- Node-Link Diagrams: hierarchies, scaling problem, tree breadth.
    - Clear hierarchies,scaling problem (tree breadth)
    - **Reingold- and Tilford Algorithm**
    - Variants, Reingold-Tilford Layout, Radial Layout, Cone Trees & Ballon
        Trees, Hyperbolic Trees, Dendrograms
- Space Filling Approaches(known as treemaps) (enclosure):
    - Entire tree shown at once, easy to recognize one major attribute of nodes
        (e.g. size)
    - Difficult to estimate depth in hiearchy.
    - Variants: TreeMaps, Voronoi TreeMaps, jigsaw maps
- Layered Approaches
    - tree stucture depicted by means of:
        - Layers, adjacency, direction
        - often: recursive subdivision of tree
        - Parent nodes occupy larger area
        - Child levels follow depending on parent size
    - Variants:, Icicle Trees, FacetZoom, Sunburst Diagrams, Cascaded Lists


**What is the main difference between Node-Link Diagrams and Enclosure Diagrams?
Give examples from each category and explain advantages and disadvantages in
terms of usability.**

- Enclosure could encode trees but not networks. i.e. It can't show
    cross-subtree relations

**Use examples to explain where the limits of using 3D graphics lie and why
metaphors taken too literally do not necessarily have to be advantageous.**

**Think about the role of the visual repertoire or the grammar of visual diagram
elements using self-chosen examples. For example, pick out some of the tree
visualization techniques presented and consider how they could be improved
visually.**

# 06 - Time
Which temporal aspects of data can be distinguished?

Name several example techniques for each time visualization group and explain
one representative in detail.

How well can periodic relationships of events be read with a Gantt or
Pert-diagram?

Explain examples for the use of axes for time and other variables and describe
possibilities how such axes can be combined. What are the advantages and
disadvantages?

Give an example and the advantages and disadvantages of radial time
visualizations.

Choose possible dimensions for a taxonomy of time visualization techniques that
you consider important (why?) and develop your own classification scheme.

# 07 - Presentation / Interaction

**Name one possible classification for data analysis tasks. Why do tasks play a
crucial rule?**
- overview, zoom, filter ... etc. as before
- WHY? it a guideline..

**What are multiple coordinated views? Explain the concept and discuss advantages
for data exploration.**
- Slide 10

**Name examples for the combination of different presentation techniques that
allow displaying large data amounts on small displays and keeping an overview in
detail views.**

**Define and characterize zooming & panning.**

- Zomming is: constant, continuously increasing (de)magnification of display
    details. (scroll)
- Panning is: constant, continuously movement of viewport over a larger
    information space. (drag)
- Multiscale information spaces/ user interfaces
- Scale is changed for entire View
- Temporary loss of contextual information

Explain the concepts of geometric zoom and semantic zoom.
- TODO

When using zooming and panning in combination, which issues can occur?
- There can be unexpected shifting of pans while zooming. (slide 21)

**Space-Scale diagrams**: fundation of zooming and panning  
It's basically storing information on different level of scales (magnification).
And a (linear) mapping among the levels.

**SSD trajectories**
**Space-Scale diagrams**: fundation of zooming and panning  
It's basically storing information on different level of scales (magnification).
And a (linear) mapping among the levels.

Explain different possible **zoom effects** by using a space-scale diagram.
- Geometric Zomming
- Bounded-geometric zomming: max level of magnification
- fade-bounded geometric zooming:
- fixed-shape/size zomming
- Anti-Zomming: no zooming for some elements (e.g. text on maps)
- Compound fixed-shape Zomming
- Piecewise fixed-shape zooming, semantic zooming

**What is Speed-Dependent Automatic Zooming? For what is it used and what are
advantages?**
- zooming level depends on the speed that viewers going through the information.
- Faster = quick glimpse, need overview, less details, zoom out.
- Slower = read details, zoom in
- E.g. for text reader: zoom out for quick structual overview, zoom in for
    detail readings.
- Advantages? less operation required, intuitive for some tasks, e.g. reading



**Explain the mathematical functions that allow to describe distortion-oriented
focus+context techniques. Name specific examples that were discussed in the
lecture.**

**Select two distortion-oriented techniques and explain them in detail. Also
discuss advantages and disadvantages.**

**What is the main difference between Bifocal Display and Perspective Wall?**

- Bifocal: a gate function, either in or out. Constant mag. 
- Perspective Wall: smooth transisition outside of the gate, varying mag.

**Provide the transformation function and the magnification function for Bifocal
Display and Graphical Fisheye Views.**

![disto](img/distoFunction.png)
![disto2](img/disto2.png)

**Explain a possible classification of distortion-oriented techniques based on the
magnificatio**

![sort](img/sort.png)
# 08 - SciVis Intro

**104. Describe all the parts of a typical scene required for 3D rendering on a
graphics card. (4 Pt)**

**105. In 3D scenes, meshes are often used to describe shape and visual
appearance. In this context, please shortly describe the following attributes
that a vertex of a 3D model can have: position, color, normal, texture
coordinates (4 Pt)**

**106. Describe the following surface definitions (+advantages/disadvantages?):
triangle mesh, parametric surface, height field, iso-surface (8 Pt)**

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


**107. How can one compute the normal of an iso-surface? (2 Pt)**
- take a vector of partial derivatives..

**108. Describe 2 different types of light sources and draw a sketch for each in
     the given field.**
- point and directional..

**109. What is needed to define a simple model of a pinhole camera? Name the
required internal and external parameters/variables. (1+1 Pt)**

- Internal parameters: Pixel resolution w and h of sensors, Opening angle,
    distance znear and zfar (near and far clipping planes)
- External: camera location, view-direction

**Describe the term view frustum. (2 Pt)**
- is a frustum, defined by the near and far clipping plane and for edges. It
bounds "what can be seen"

**Which mathematical structures are used to provide 3D model transformations?
How are they used? (2 Pt)**
- Transform matrix. The 3d can be viewed as a matrix, each column vector
  represents one vertex position. By applying (multiplying) the transformation
  matrix to the model matrix, the product matrix will be the result of
  transformation.

**What is the advantage of using homogenous vector and matrix representations
regarding 3D transformations. (2 Pt)**

- by adding addition w-component to the vectors/matrix, the operations are
  extended to affine space. Vector and points are treated differently. The most
  trivial advatage: Matrix products can not produce translation (i.e. shifting)
  without the additional component. 

**113. Given the picture from slide 19... Given is the sequence of steps in the
rendering process from a scene object with its vertex positions in object
coordinates to the rendering-ready positions in window coordinates. Fill out the
remaining fields. (5 Pt)**

```
Object Coords --->  Eye Coords  ----> Clip Coords ---> Window Coords
            Model View         Projection        Viewport
3D                  3D                2D               2D
```

**114. What are the main shader units in a modern OpenGL pipeline? (1.5 Pt)**
- vertex, geometry and fragment shader.

**Shortly describe how the data is transferred from the CPU to the GPU and
     how the data is processed afterwards. (2+4 Pt)**
- REFER TO CG1
![GL](img/GPU.png)

**116. Given a picture as on slide 21 (eye, light source, surface point, surface
normal)... Depict the variables and parameters that are required for basic
lighting calculations. (2 Pt)**
- ambient, BlinPhon, Diffuse, etc..


**118. In the rendering process, the primitives are processed in the order of
their occurrence. Usually they are not sorted by visibility. To establish the
right depth order one could utilize the z-buffer method. Please describe this
approach. (4 Pt)**
- storing depth per pixel, keep only the front most fragment.


**119. Regarding transparency, describe how visibility sorting can be done on
fragment level. (3 Pt)**

**120. Shortly describe back-to-front rendering and, in this context, the over
operator. (1+2 Pt)**

![trans](img/trans.png)

**Halo**
- adding uni-colored less transparent boundary to 3D element.
- defined by halo color, opacity and width.
- improves the perception of visibility order (more clear who's front who's back)

**123. Regarding the visualization of 2D scalar fields as pixel images, there
are different approaches to optimally map the value range of the data onto the
maximum range of the color model values. One of those techniques is called
window transfer function. Describe this method with the help of a typical
application scenario. (3 Pt)**

- It is used to linearly transfer a range to normlized one e.g. [0,1]

    $$f_{ij}^{window} = \frac{f_{ij} - f_{min}}{f_{max} - f_{min}}$$
- e.g. for medical image, interactively setting the fmin and fmax can bring
    contrast to interesting parts.

**Gamma Correction**
- refer to CG1

**125. Describe the technique Histogram Equalization. What type of the human
visual perception does it utilize? (1+1 Pt)**

![histo](img/histo.png)

**How can one produce color bands for given 2D scalar data? (1 Pt)**

**Regarding 2D scalar data, describe the different approaches contour lines and
color bands. (2 Pt)**

**In 3D domains, there usually is a lot of occlusion. Describe each of the
following techniques that counteract this problem: selection, projection,
slicing, clipping (4 Pt)**


**Describe the technique contouring. How can contouring enrich the
representation of a height field? (2+1 Pt)**

**Name the techniques that extract iso-lines (2D domain) and iso-surfaces (3D
domain). (1+1 Pt)**

**Given a picture of a grid cell... Describe the technique Marching Squares.
What is the input, the output and the steps that are processed? Complete the
sketch. (5+1 Pt)**

**Given a grid cell processed by Marching Squares that has an ambiguous case...
Describe why there is an ambiguous case here and how the ambiguity can be
resolved. Use the sketch to support your explanations. (1+2+1 Pt)**


# 09 - Data Prep

**135. What is the difference between interpolation and approximation? (1 Pt)**
- Both are looking for a function that takes an point and outputs an feature
    vector.
- Interpolation requires the function's value at observation points to
    be exactly the same as given.
- Approximation requires the sum of value deviation for each observation points
    to be minimal.

**136. Given a picture of an interpolated and an approximated 1D signal... Name
the two different techniques with which the signal was reconstructed. Shortly
describe them. (1+2 Pt)**


**138. Explain 1D linear interpolation. Why is the interpolation problem solved
“automatically”? (2+1 Pt)**

- Define a "hat" function of height 1 for each sample point. To interpolate a
  point x, sum up all the hat functions' value at point x.
- "Automatically": hat functions are 0 for all other sample points. And a
  interpolated point's value are only determined linearly by its two
  neighbouring sample points.

**139.bilinear interpolation. (2 Pt)**

**140. Describe the term affine combination. Which mathematical properties are
required? (1+2 Pt)**
- Is a linear combination of points with coefficients that has value in [0,1]
  and sum up to 1.

**141. What is affine independency? (1 Pt)**
- a set of points are affine independent iff no points can be a affine
    combination of the others. (think about linear independency)

**142. What is the maximum number of independent points in Rd ? (1 Pt) **
- d + 1

**143. What is a simplex? (2 Pt)**
- a set of d + 1 affine independent points (think about basis in vector space)

144. What are barycentric coordinates? (1 Pt)
- barycentric coordinates of point p, are the coefficients, with which the
  affine combination of simplex produce the position of p.

**145. Given a picture of a triangle mesh, a target point and a triangle as
starting point... Describe an algorithm how to find the triangle that contains
the given target point x starting with the marked triangle. Please mark the
other triangles in the sketch that get visited by the algorithm in the correct
order. (2+1 Pt)**

**146. Regarding a triangle (x1 x2 x3), describe a method to check whether a
point x is outside (or inside) of a triangle edge. (2 Pt)**

**147. How can you estimate derivatives in cell-based data? Describe the two
techniques forward difference and central difference. (2 Pt)**

     
**148. Describe a case where the results of the central differences deviate
strongly from those of the forward differences. (2 Pt)**

**149. In contrast to finite differences what is special about the Sobel
Operator regarding the quality of the derivatives. (2 Pt)**

Given pictures of the same data where different approaches for the
computation of the surface normal were used... The images were rendered using
different methods for normal estimation. Assign the following techniques:
forward differences, central differences, Sobel Operator (2 Pt)

**Voronoi diagram:**
- construct with perpendicular bisectors..

**Describe how a Voronoi Diagram is defined mathematically. (2 Pt)**

**How is the Delaunay Graph generated from a Voronoi Diagram? (2 Pt)**
- create dual mesh of the voronoi diagram.

**155. Regarding Delaunay Triangulation, describe the Edge-Flipping algorithm**
- is quite conceptional
- start with any trianglulation of the **convex hull**
- put edges that are not locally delaunay onto stack
- while stack not empty
    - take top edge from stack
    - if it is still not locally delaunay
        - flip edge
        - check for the non boundary edges for the four neighbour edges the
            local delaunay property and push the edges not having it onto stack.

**Insertion-algorithm**
- Bring points into random permutaion
- construct triangle from first 3 points
- insert remaining points one after the other
    - perfom point location algorithm
    - if point is outside of convex hull, find all boundary edges relative to
        which point is outside and connect point to these edges with newly
        created triangles. do local flips until all affected edges are locally
        delaunay.
    - if point is inside triangle, split triangle into three triangles; and do
        local flips until all affected edges are locally delaunay.


**157. To solve the interpolation problem via Shepard Interpolation, radial
basis functions are used. What is a radial basis function? What are advantages
and disadvantages of this approach? (1+2 Pt)**

- Analog to the hat functions defined in 1D linear interpolation: define a
  function for each sample points. Such that for a point x, f(x) is an affine
  combination of all the basis function fi. The definition sees above.

**Scatter Data Interpolation**

**156. Given different interpolation approaches... Shortly describe the
following interpolation approaches in one sentence and make a statement about
the continuity of the functions: e.g. constant on Voronoi Cells, Shepard
interpolation, Delaunay triangulation, Natural Neighbour Interpolation (2 Pt
each)**
overview:  

- constant on voronoi cells: nearest neighbor intepolation, not continous
- shepard intepolation: defines radial basis functions. Cinf continous
- Delaunay triangulation + barycentric intepolation. C0 continous.
- Natural Neighbour intepolation

**Shepard interpolation**: similar to 1d hat functions..
- Define per observation point one basis function 
$$\Phi_i(x) = \frac {\lambda_i(\underline{x})}{\sum_j{\lambda_j{\underline(x)}}}$$
$$\lambda_i(x) = 1/||\underline{x} - \underline{x}_i||^\rho$$  
- interpolation problem is automatically solved by summing up the function
    values.
- infinite order continuity for p>1 but will have flat data (zero gradiant)
- fx is affine combination of fi (therefore all points lays in convex hulll of data
    points)

**Natural Neighbor / Sibson interpolation**
- same general form for f(x) and $\Phi_i(x)$, but only sum up local neighbors
    N(x) such that interpolation becomes local.
- Construct voronoi cell for the point x and find the natural neighbors.
- Lambda function has variants: //TODO
- IMPL: // TODO from slide 41.


# 10 - Vol. Vis.

**158. Compare direct and indirect volume visualization. What are the basic
approaches? What are the general differences? (2+2 Pt)**
- direct vol. vis. vis renders the volume in a transparent fashion, the whole
    volume is shown. Approaches: compositing, transfer function design,
    dendering approaches.
    - Compositing
    - (transfer function design for blending)
    - rendering approaches
- indirect vol. vis. is oblique, i.e. only the front most element along the view
    direcion is visible. Basic approaches are contouring and slicing.

**159. What is Oblique Slicing? Describe a CPU and a GPU approach for rendering
oblique slices via 3D texture. (2+1+1 Pt)**
- cuts the volume with a plane and shows the cross section.
- The trilinear interpolation is automatically solved by using 3D texture.
- CPU: compute intersection polygon of plane with volume box, then use 3D
    texturing.
- GPU: define a clipping plane along the cutting plaing and use the GPU clipping
    functionality (thefore the "outside" part is no longer visible.)


**160. Describe the technique Dual Contouring. (3 Pt)**
- classify all voxels in [inside,outside], fill dual cell of interior
    voxels. For all edges connecting interior with exterior, add dual face to
    the cuberille-surface.
- Dual Contoring: further move the dual vertices onto the iso-surface (so that
    the iso-surface could match the iso-value). This could be done by moving the
    dual vertices in the (+-) gradient directions (think about projection).


**161. Describe the Marching Cubes algorithm with the help of a sketch. (3 Pt)**
- Fast impl. with lookup table.

**162. Given a picture of a 3D grid cell and an iso-value v... Classify the
voxel of the cell based on the iso-value v and draw the resulting iso-surface
intersection points onto the edges. (1+1 Pt)**

**163. Regarding the Marching Cubes algorithm, how many cases exist (without
exploiting symmetries)? (1 Pt)**
- 2^8 = 256.

**164. A common problem with marching cubes is that because of the creation of
triangles with very short edges, an extremely high number of triangles can be
produced. Describe a solution for that issue. (1 Pt)**
-  grid snapping: if a point is considered "close enough" (e.g. closer than a
    percent threashold) to the grid vertex.
    then it can be snapped to the grid.

**165. Describe another technique to reduce the number of generated triangles
produced by Marching Cubes. (1 Pt)**
- short edge collapsing.

**166. Describe the basic procedure for direct volume visualization. Consider
the terms ray, sampling and compositing. (3 Pt)**


**167. Given pictures of different compositing methods for direct volume
rendering... Assign the following compositing methods for direct volume
rendering to the pictures: max, average, first (2 Pt)**
- slide 31.

**168. Shortly describe the following compositing methods for direct volume
rendering: max, average, first (1+1+1 Pt)**
- max: use the max value of the sample points. average: literal. first: use the
    value of the sample that the ray first encounters a threshold
    value(effectively iso-surface)

**169. What is the emission-absorption model and how does the compositing mode
blending generally works? (1+1 Pt)**
- define 2 transfer functions to convert the scalar value of a point into
  opacity and color. the colors are mixed alone the ray..

**170. What are the two basic parameters controlled by a transfer function?**
- opacity(absorption)/ color(emission)


**172. What is the purpose of a histogram when designing a transfer function?**
- maximizing brightness and contrast.

**174. How can you utilize the shader units on a GPU for raycasting? (3 Pt)**

**175. Name and shortly describe two acceleration techniques for raycasting.**



# 11 - Flow Vis.

**176. Shortly name and describe the types of local properties that exist in
flow data? (1+2 Pt)**
- Convergence/Divergence, Rotation (curl), (harmonic if none), flux.

**177. What is a common mathematical approach to analyze the local environment
of critical points? (2 Pt)**
- Calculate the Eigenvalue of the jacobian matrix for the point, the point can
    be categorized by the eigenvalue's range (wrt. imaginary parts and real
    parts.).

**178. Given a picture of flow field with marked spots... Describe properties of
the critical points marked in the given picture with the following attributes:
divergent, convergent, saddle, left/right turning spiral (1Pt each)**
![prop](img/prop.png)
![prop2](img/prop2.png)

**179. Name 3 types of characteristic lines in vector field visualization. (1.5
     Pt)**

**180. Characteristic lines are a common approach to visualize vector fields.
Shortly describe the following types of lines: stream lines, path lines, streak
lines, time lines (4 Pt)**

- Stream lines: trace tangents of the vector field at a fixed time.
- Path lines: trace particle movement (evolving in time)
- Streak lines: trace color outflow, multiple path lines with different colors.
- Time lines: time evolving of a "string".


**182. Streamlines can be computed by numerical integration. What is a general
issue in low order polygonal approximation techniques like the explicit Euler
method? (1 Pt)**
- Issue: error accumulation is fast.
- Possible Solutions: smaller steps, implicit euler, RK .. 


**Integrate and Draw**:
- randomly choose seeds
- integrade stream line back and forth (i.e. in both directions)
- draw stream line with random color into image. (i.e. each steam line with a
    color)

![iad](img/iad.png)
- high contrast image without boundary defects
- non uniform brightness, no information about vector length and orientation

**184. How can you extend Integrate and Draw methods to visualize the strength
and orientation of the vector field at a given sample position? (1 Pt)**
- strength: length of stream lines
- orientation: use asymmetric line integratral functions to color the line


**185. Shortly describe the technique Line Integral Convolution. (3 Pt)**
- Generate noise texture
- randomly choose seeds
- integrate steam line back and forth
- Set seed pixel color to convolution of noise texture along stream line

**186. Compare the approaches Integrate and Draw and Line Integral Convolution.
What are the similarities and what are the differences? (4 Pt)**
- both are steam line vis.
- later feels more "smooth..."
- not showing stength..



