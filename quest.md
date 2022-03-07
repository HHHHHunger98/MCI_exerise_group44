**Define the term (data) visualization**

is to transform data into visual forms such that the viewers can observe the
information and perceive the features without needing to dig into the raw data.

**SciVis vs. InfoVis**  
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

**Modes of vis.**
Static, Animation, Interactive visual analysis, In-Situ(data streamed into vis),
Interactive Steering(change of simulation parameters/ control cyber-physical
systems), Visual Analytics

**Simulation/Vis coupling**
![coupling](img/coupling.png)
- Weak coupling: all data yields from simulation are transmited to
    visualization.
- Hyprid: transmit data in compact representation
- Strong: Simulation and Vis. are done together, the rendered images are
    transmited to display client.

**Scenario where weak coupling is not feasible**
- the simulation is on a very large scale
- limited bandwidth
- visualization requires high computing power and can't be done on client devices

**General interation tasks**  
Overview: entire information space, global patterns  
Zoom: interesting information objs, smaller subset  
Filter: select subset based on attributes  
Details-on-demand: Select objs to get details  
Relate: relationships between objs, compare values  
History: recording actions to undo  
Extract: extraction of subsets of the information space and request parameters.  

**Advanced interaction techniques**  
Basic: selection(e.g. mouseover, click, touch), rearrange(e.g. move, sort, delete)
Advanced: Filtering, Overview+Detail, Zooming and panning, Focus+Contect, Brushing and
linking, probing, 3d Navi, Slicing etc.

**Basic diagrams**
![diagrams](img/diagrams.png)

**Visualization Methods** (15) what ? 

**Dimensionality of observation space and feature space (17-19)**  
![dim](img/dim.png)


**3 types of area influence that a specific data value can have: reference point
local reference and global reference**  
**How the references from above should be generally visualized**  

**Reference Point**:
- The data values refer only to individual observation points(e.g. fractals,
    chaotic phenomena) (therefore can't apply interpolation)
- Vis. Rule: The data balues may only be assigned to individual points in the
    graphical representation.

**Local refreence**
- The data value refer to local region of the observation space (e.g.
    temperature value as a function of position)
- Vis. Rule: values at points where no value is given can be estimated from neighboring
    observations w. suitable interpolation methods

**Global reference**
- the data values apply to the entire observation space (e.g. background
    radiation, total energy)
- Vis. Rule: value assigned to global area in the graphical representation.


**types of data grids/meshes** (22-25)
![grid](img/grid.png)

Regular vs unstructured meshes:
- unstructured meshes can locally adapt to data
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

**value ranges and examples, norminal, ordinal, metric**

**data type and examples, scalar, vectorial, tensorial... **
- Scalar: 1D values
- Vectorial nD values,  can represent direction
- tensorial: kth-order tensor with n^k dimension. scalars/vectors are 0th/1st
    order tensors

**Taxonomy by shneiderman?**

