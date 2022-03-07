# Data Preparation

## Goals / Overview
**Reconstruction**  
- interpolation: exact fit for observation points.
- approximation: best fit for observation points.
- signal reconstruction (using sinc function)
- derivative exsimation 

**Point Queries**
- probing: display feature vector for individual point. (on demand)
- raycasting: find first point along ray where feathre threshold is reached.
    (like iso-surfaces)
- resampling: compute all feature values for points on grid. easier computation
    than unstructured ones.

**Application: Trends**  
- local trends from derivatives

**Noise cancelation**  
**Feature Extraction**  



## Cell-based interpolation
- (typical) find which cell the query point (which is not a sample point) falls in. Use
    floor function for regular grids. find its relative positions $\lambda$ wrt.
    its cell.
- Some grids may not be regular, need other query methods. [slide 12]



**1D linear interpolation**: define a hat function of height 1 per sample point.  
![intp](img/intp1.png).  
e.g. sample point i with value vi and hat function fi  
$$E(p) = \sum_{i}^{n}{v_if_i(p)}$$

- This is global and doesn't need to consider the intervals (e.g. are they
regular?). 
- The sample points needs to be sorted in order to construct the hat functions.
- Alternatively do the interval based interpolation: find relative positions
  wrt. the cell (adjacent sample points): 
$$\vec{f}(x) = (1-\lambda)\vec{f_0}
+ \lambda \vec{f_1}$$
$$\lambda = (x-x_0)/(x_1-x_0), \lambda \in [0,1]$$


**2D Bllinear Interpolation**
![2d](img/2d.png)

- You need to define a direction anyways..
- The chosen direction doesn't change the result .think about the geometric meaning.
- **Applying twice linear doesn't make the result linear. ($\alpha\beta$ is not a
    linear component). Inside of rectangle, bilinear interpolation is mixed
    quadratic.**

**3D Trilinear interpolation**: basically the samething as Bilinear, with one
more parameter $\gamma$
- Trilinear is linear along edges and bilinear on faces.
- **Bilinear / Trilinear** are only $C^0$ continuity across cells (i.e. first
derivatives not continuous across cells.)


**Affine Combination** of points $\underline{x_i}$ is a 
- linear combination $\underline{x} = \sum_{i=0}^{d}{\sigma_i\underline{x}_i}$
- where the weights $\sigma_i$ are in [0,1] and sums up to 1.
- The coefficients $\sigma_i$ are called barycentric coordinates.
- Affine independent: think about linear independent. Max number of affine
    independent points in $R^d$ is d+1. e.g. (point for 0D, segment for 1d,
    triangle for 2d). INSIGHT: there are at most n linear independent nD vectors
    in $R^n$ therefore requiring at least (and only necessarily) n+1 points to
    construct the basis vectors.
- A set of d+1 affine independet point is called **simplex**

**Unstructured Grids: barycentric interpolation** 
- is linear!
- input: unstructured grid with data points; query point
- output: linearly interpolated value.
- 1.determine simplex that contains x.
- 2.compute the barycentric coordinates from (with lienar equation system):

    $\underline{x} = \sigma_1\underline{x_1} + \sigma_2\underline{x_2}  +
    \sigma_3\underline{x_3}$

    $1 = \sigma_1 + \sigma_2 + \sigma_3$
- 3. mix feature values with barycentric coordinates: $\underline{x} = \sum_{i=0}^{d}{\sigma_i\underline{x}_i}$

**INSIGHT**: the idea is to find a linear(affine) combination $\sigma =
(\sigma_1 \cdots \sigma_n)$ for simplex $x=(x_1 \cdots x_n)^T$ such that 
$\underline{x}^T = \sigma x$ .. Then apply the same coefficients to the feature
space to get the linear combination of $f_i$ as the value for the interpolation.

**INSIGHT**: by limiting the value to [0,1] and the sum of coefficients to 1,
the affine combination of simplex could only produce points **inside** of the
primitive (e.g. triangle)

**A BIG QUESTION**: what's the simplex? (e.g. in which triangle does this point
fall?)

**point localization**: find which triangle a poitn falls in:

The algorithm:
- boundary case is treated otherwise
- 1. start from random triangle
- 2. check for each edge whether target point is on the **outside**
- 3. if all checks fall, target triangle is found
- 4. otherwise move to triangle adjacent to edge where point was outside first
     or in case of boundary edge terminate and output boundary edge.

![outside](img/outside.png)

- Generalize to convex polyhedra
- acceleration: use of a hierarchy.

## Estimation of Derivatives 
- problem: in linear interpolation deriatives not continuous at sample
    locations.

**1D differences:**
- forward, backward and central(equaldistance / general).
- Error analysis: central difference better.

**Finite Differences on regular grids**:
- Partial derivatives from gradient vector.
- approx. with central difference: **NOT rotational invariant**
- sobel operator:

    $$
    \frac{\partial{f}}{\partial{x}} (x_0,y_0)  = \frac{1}{8} \sum_{i,j=-1}^{1}
    s_{ij}^{x} \cdot f(x_i,y_j)
    $$

    $$
    s^x = [-1,0,1; -2,0,2; -1,0,1]
    $$
    
    $$
    s^y = [1,2,1; 0,0,0;-1,-2,-1]
    $$
- 3D different weights but same idea.


## Voronoi / Delaunay
- Problem: How to interpolate the points when you don't have a grid?

**Delaunay triangulation and voronoi diagram**
- Delaunay Triangulation: minimizes largest circum circle and maximizes smallest
    interior angle of triangles
- Voronoi diagram: split space into regions (each containing a point) of "cloest
    distance to point" : i.e. all the points in a voronoi reigion is no closer to
    other sample points than to its own.
- Voronoi diagram is constructed via perpendicular bisector.
- Delaunay graph (of voronoi diagram)
    - The sample points are vertices
    - Two vertices are connected by an edge, iff the voronoi cells share an
        edge.

- Delaunay graph is a triangulation if no 4 points conincide on a circle.
- Typically delaunay triangulation is NOT produced from voronoi
    diagram.(complexity)

**Use determinant** to check whether a forth point is in the circumcircle of a
triangle.

![de](img/dela.png)

**threorem** a triangulation is delaunay triangulation if:
- all points are covered
- convex hull of points covered
- local delaunay condition full filled for each edge

**Edge-flipping algorithm**  
- is quite conceptional
- start with any trianglulation of the **convex ull**
- put edges that are not locally delaunay ont ostack
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


**Problem** numerical problem when four points lay on circle or on a straight
line (happens all the time on regular grid)
- can add small random jitter to points
- use numerically stable math
- handle all special cases separately

**Problem** point localization dominates runtime: can be improved with
hierarchical data structure.. O(nlogn)


## Scatter Data Interpolation
overview:  
![int](img/intapp.png)

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


## QUESTIONS:


**135. What is the difference between interpolation and approximation? (1 Pt)**

- Both are looking for a function that takes an point and outputs an feature
    vector.
- Interpolation requires the function's value at observation points to
    be exactly the same as given.
- Approximation requires the sum of value deviation for each observation points
    to be minimal.

![in](img/intp.png)


136. Given a picture of an interpolated and an approximated 1D signal... Name
     the two different techniques with which the signal was reconstructed.
     Shortly describe them. (1+2 Pt)

137. Given a grid with grid size Δx and a query point x... Determine the cell (j
     x jy) and the relative position within the cell for the query point x. (2
     Pt)


138. Explain 1D linear interpolation. Why is the interpolation problem solved
     “automatically”? (2+1 Pt)
- Define a "hat" function of height 1 for each sample point. To interpolate a
    point x, sum up all the hat functions' value at point x.
- "Automatically": hat functions are 0 for all other sample points. And a interpolated point's
    value are only determined linearly by its two neighbouring sample points.


139. Given one cell of a grid (with grid size Δx) and a query point x...
     Determine the value of x via bilinear interpolation. (2 Pt)

140. Describe the term **affine combination**. Which mathematical properties are
     required? (1+2 Pt)
- Is a linear combination of points with coefficients that has value in [0,1] and sum up
    to 1.

141. What is affine independency? (1 Pt)
- a set of points are affine independent iff no points can be a affine
    combination of the others. (think about linear independency)

142. What is the maximum number of independent points in Rd ? (1 Pt)
- d + 1

143. What is a simplex? (2 Pt)  
- a set of d + 1 affine independent points (think about basis in vector space)

144. What are barycentric coordinates? (1 Pt)
- barycentric coordinates of point p, are the coefficients, with which the affine combination of simplex produce the
    position of p.

145. Given a picture of a triangle mesh, a target point and a triangle as
     starting point... Describe an algorithm how to find the triangle that
     contains the given target point x starting with the marked triangle. Please
     mark the other triangles in the sketch that get visited by the algorithm in
     the correct order. (2+1 Pt)
- see above.

146. Regarding a triangle (x1 x2 x3), describe a method to check whether a point
     x is outside (or inside) of a triangle edge. (2 Pt)
- use determinant, see above.

147. How can you estimate derivatives in cell-based data? Describe the two
     techniques forward difference and central difference. (2 Pt)
- trivial

148. Describe a case where the results of the central differences deviate
     strongly from those of the forward differences. (2 Pt)
- TODO

149. In contrast to finite differences what is special about the Sobel Operator
     regarding the quality of the derivatives. (2 Pt)
- It considers the diagonal elements and is rotational invariant.

150. Given pictures of the same data where different approaches for the
     computation of the surface normal were used... The images were rendered
     using different methods for normal estimation. Assign the following
     techniques: forward differences, central differences, Sobel Operator (2 Pt)
- see the slides...

151. Given a set of points... Draw the Voronoi Diagram for the given set of
     points. (2 Pt)
- see above.

152. Describe how a Voronoi Diagram is defined mathematically. (2 Pt)  
![vo](img/vo.png)


153. How is the Delaunay Graph generated from a Voronoi Diagram? (2 Pt)
- each sample point is a vertex.
- connects the vertices iff two corresponding voronoi reigions share an edge.

154. Given a Voronoi Diagram... Draw the corresponding Delaunay Graph for the
     given Voronoi Diagram.
- trivial

155. Regarding Delaunay Triangulation, describe the Edge-Flipping algorithm. (4
     Pt)
- see above.

156. Given different interpolation approaches... Shortly describe the following
     interpolation approaches in one sentence and make a statement about the
     continuity of the functions: e.g. constant on Voronoi Cells, Shepard
     interpolation, Delaunay triangulation, Natural Neighbour Interpolation (2 Pt each)
- see above

157. To solve the interpolation problem via Shepard Interpolation, radial basis
     functions are used. What is a radial basis function? What are advantages
     and disadvantages of this approach? (1+2 Pt)
- Analog to the hat functions defined in 1D linear interpolation: define a
    function for each sample points. Such that for a point x, f(x) is an affine
    combination of all the basis function fi. The definition sees above.










