(Grids:Staggering)=
# Staggered grids

When you design a grid for a numerical model, it may be useful to think aboiut your grids as boxes, as shown in {numref}`fig:Grids`. If your grid is 1D, you will have a row of boxes, if you have a 2D grid, you will have a layer of boxes, and for a 3D grid you will have stacked layers of boxes.

If you are dealing with more than one variables, you need to think about where the grid points for each variable should be located within the boxes. The easiest option is to co-locate all the grid points in the center of each box, as illustrated in {numref}`fig:Grids`. This is called a non-staggered grid. In the illustration, you see the variables *pressure, p* and *velocity, u* positioned in the box centers. Choosing this option makes the coding more care-free, but it turns out that this is not the most suitable placements for these variables.

Think about the physics governing pressure and velocity. Imagine you have a box of water at time step *t=0*, where water is leaving on the right side faster than it is filling from the left side. This means that you are reducing the amount of water in your box, and the pressure should naturally decrease. If you think of this in terms of the shallow water equation (Eq. {eq}`eq:SWEq`), where pressure is replaced by sea surface elevation, this would mean that the surface elevation sinks. However, this physical interpretation relies on our knowledge that the velocity at the two box interfaces are different. If we co-locate pressure and velocity in the box centers, we do not immediately know if the pressure will increase or decrease. Instead we must make some averaging and calculate the pressure at the next time step, and this procedure may alter the precision of our model.

Therefore, a more meaningful placing of the grid points, is to stagger the grids, i.e., to place the pressure grid points in the box centers, and the velocity grid points along the box walls/interfaces, as illustrated in Figure {numref}`fig:Grids`.

```{figure} ./GridStag.png
---
name: fig:GridStag
width: 75%
align: center
---
Placement of grid points for multiple variables in co-located/non-staggered grids (top) and staggered grids (bottom). For the staggered grids, the grid points for velocity, *u* is located at the box walls, while the grid points for pressure, *p*, is located at the box center.
```

In 2D, there are more options for placement of grid points. If we make a 2D extension of the staggered grid above - and also an extension of the physics, we get a grid as illustrated in Figure {numref}`ArakawaC`. This is called an Arakawa C-grid. Arakawa and Lamb published a paper in 1977  ({cite:ts}`Arakawa1977`), describing 5 different grid point configurations. These are commonly referred to as Arakawa grids, and includes:
* Arakawa-A: The non-staggered grid, where all variables are defined in the same points
* Arakawa-B: The pressure and other scalars are defined in the box center, and velocity, *u* and *v*, are located in the box corners
* Arakawa-C: The pressure and other scalars are defined in the box center, the eastward velocity, *u* is defined along east/west box walls, and the northward velocity, *v*, is defined along north/south box walls, as depicted in figure {numref}`ArakawaC`
* Arakawa-D: The same as Arakawa-D, but rotated 90 degrees, so that *u* and *v* swap places
* Arakawa-E: The box is rotated 45 degrees, so that *u* and *v* can be co-located in the corners 

```{figure} ./ArakawaC.png
---
name: fig:ArakawaC
width: 75%
align: center
---
The Arakawa-C grid for 2 dimensions. Pressure and scalar variables are located in the grid centers. The velocity grid points for the eastern direction, *u*, are located on the east/west box boundaries, while the velocity grid cells for the northern direction, *v*, are located along the north/south boundaries.
```

The Arakawa-C grid is one of the most common configurations in geophysical fluid modelling. However, som models use Arakawa-B grids or other configurations. Familiarize yourself with a model's grid, either you will design the model, run model experiences on a common model, or analyze data from model outputs.

