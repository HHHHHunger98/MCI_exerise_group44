# 11 – Flow Visualization


**Flow Properties**

Compressibility:
- Compressible: gas, air .. use {velocity vector field, scalar density field,
    scalar pressure field, temperature field..}
- incompressible: e.g. liquid, velocity vector field, scalar temperature field.. is **divergence free**, constant density and viscosity (internal fraction)

Time dependence:
- steady/stationary flow: velocity vector field does not change over time.
- unsteady/dynamic flow: velocity vector field changes..

Point Properties:
- vector: length + direction for vis.

Local Properties:
- convergence/ divergence
- Rotation (curl)



## MATH

**Nabla Operator**

$$\vac{\nabla} = (\frac {\partial}{\partial x_1}, \cdots,
\frac{\partial}{\partial x_n})$$

**Divergence**: scalar measure of volume expansion:

$$div \vec{u} = \vec{\nabla}^T \vec{u} = 
\frac{\partial{u_x}}{\partial x}+
\frac{\partial{u_y}}{\partial y}+
\frac{\partial{u_z}}{\partial z}
$$

**Rotation**: vector: describing axis and streath of rotation:

$$
rot \vec{u} = \vec{\nabla} \times \vec{u}
$$


![m](img/mat.png)

**EigenValues of Jacobian matrix**
- 1 real eigen value
- optionally 2 dual eigen values.

27 Configurations:
{x,y,z} x {left, right, no rotation} x {inflow, outflow, saddle}


**Reynolds number Re**  
![rn](img/rn.png)

## Vis Methods
- elementary: use only th evector field, not its derivatives
- local: analyze local env using derivatives..
- global: dense representation of the vector field (not showing length, maybe)
- Topological: anaylyze critical points, flow regions and separation lines.
    Reduce amount of data..

## LINE FEATURES

- Stream lines, tangent to vector field at fixed time.
- Path lines, tracing moving particles in time evolving flow
- Streak lines, tracing color outflow ouver time from fixed position (tracing
    multiple particles w. different color at once)
- Time Line: time evolution of a massless line

**Fundamentally: find a paramiterized curve that follows a certain differential equation**

![de](img/de.png)

**Numerical Integration (stream line)**

(explicit) Euler Method:
```
x_i+1 = x_i + h*u(xi,ti)
```

**Problem: not precise, error accumulation fast.**
- reduce step length. (increased computation)
- implicit euler: first evolve the vector field. More work in single step but
    can increast step width. One order smaller error
```
x_i+1 = x_i + h*u(xi+1,ti+1)
```
- implicit euler Extends to Runge Kutta 4 O(h^5) error
- Step width adaption: use RK4 twice, each with half stepwidth. So that the
    error can be estimated. Adjust stepwidth on the fly according to error size.

**Life Features Rendering**
- Lines as (very thin) tubes for lighting
- Line thickness could also match to a value. Also possible for texturing.

**Line Freatures SEEDING strategies**
- Simplest: distribute on regular grid. Arrow glyphs do not show what parts of
    space are connected by flow
- Stream lines should not intersect.
- APPROACHES
    - Randomly chose seeds, stop intergration while closer than threshold to other lines 
    - focus seeding in beginning around critical points
    - chose next sample at point farthest apart from previous lines

## Texture Based Methods

**Integrate and Draw**:
- randomly choose seeds
- integrade stream line back and forth (i.e. in both directions)
- draw stream line with random color into image. (i.e. each steam line with a
    color)

![iad](img/iad.png)
- high contrast image without boundary defects
- non uniform brightness, no information about vector length and orientation

**Extend to show velocity strength and orientations**

**Line Integral Convolution LIC**
- Generate noise texture
- randomly choose seeds
- integrate steam line back and forth
- Set seed pixel color to convolution of noise texture along stream line

**Image based**
- advect noise texture in flow
- works also for unsteady flow

## QUESTIONS

176. Shortly name and describe the types of local properties that exist in flow
     data? (1+2 Pt)
- Convergence/Divergence, Rotation (curl), (harmonic if none), flux.

177. What is a common mathematical approach to analyze the local environment of
     critical points? (2 Pt)
- Calculate the Eigenvalue of the jacobian matrix for the point, the point can
    be categorized by the eigenvalue's range (wrt. imaginary parts and real
    parts.).

178. Given a picture of flow field with marked spots... Describe properties of
     the critical points marked in the given picture with the following
     attributes: divergent, convergent, saddle, left/right turning spiral (1Pt
     each)
![prop](img/prop.png)
![prop2](img/prop2.png)

179. Name 3 types of characteristic lines in vector field visualization. (1.5
     Pt)
180. Characteristic lines are a common approach to visualize vector fields.
     Shortly describe the following types of lines: stream lines, path lines,
     streak lines, time lines (4 Pt)

- Stream lines: trace tangents of the vector field at a fixed time.
- Path lines: trace particle movement (evolving in time)
- Streak lines: trace color outflow, multiple path lines with different colors.
- Time lines: time evolving of a "string".



181. Given pictures of a simulated discrete vector field (see slide 14)...
     Depicted is the progressive flow field in successive time steps t0 . . t 3
     Draw the following characteristic lines in the sketches below: streak line,
     path line, stream line for t 2 (3 Pt)

182. Streamlines can be computed by numerical integration. What is a general
     issue in low order polygonal approximation techniques like the explicit
     Euler method? (1 Pt)
- Issue: error accumulation is fast.
- Possible Solutions: smaller steps, implicit euler, RK .. 

183. Shortly describe the technique Integrate and Draw. (3 Pt)
- See above

184. How can you extend Integrate and Draw methods to visualize the strength and
     orientation of the vector field at a given sample position? (1 Pt)
- strength: length of stream lines
- orientation: use asymmetric line integratral functions to color the line


185. Shortly describe the technique Line Integral Convolution. (3 Pt)
- See above.


186. Compare the approaches Integrate and Draw and Line Integral Convolution.
     What are the similarities and what are the differences? (4 Pt)
- TODo
