(BoundaryCondtitions:Physical_BC)=
# Physical descriptions of boundary conditions

Physical descriptions of bounary conditions means that we design the type of boundary conditions (the mathematical ones described in section {ref}'BoundaryCondtitions:Mathematical_BC') to match a desired physical behavior at the boundary.

## Wall boundary conditions
In geophysical fluid dynamic models, we sometimes encounter boundaries that should act like walls. In ocean models, we typically have coastlines, or in low-altitude atmospheric models we may tall mountain ranges. When we have a wall boundary condition, we must ensure that the fluid velocity normal to the boundary is zero. This means that we have a homogenous Dirichlet condition for flow normal to the wall. 

Let us consider an example with a 1D model for advection and a forward in time, centered in space (FTCS) scheme, on a model domain $x\in[0,L]$:

$$
u_{m}^{n+1} = u_{m}^{n-1} - c\frac{\Delta t}{\Delta x}(u_{m+1}^{n}-u_{m-1}^{n}).
$$ (eq:Leapfrog)

Here, we will define the homogenous wall Dirichlet conditions as:

$$
\begin{align}
u_{0}^{n+1} = 0\\
u_{L}^{n+1} = 0
\end{align}
$$ (eq:BC_wall)


In 2 dimensions, we must also consifer flow tangential to the boundary. here, we typically choose from no-slip or slip boundary conditions.

**No-slip boundary conditions**

A no-slip boundary condition is valid for viscous fluids and fixes the fluid velocity to zero on the walls. It implies that the fluid sticks to the boundary/wall with no relative movement between the fluid and the wall.

If you, for example, consider flow along a channel or a river, the flow will be slower near the walls, and in a thin layer next to the walls, it will be zero. The no-slip conditions is therefore typically a homogenous Dirichlet boundary condition for flow both normal to, an parallell with the boundary.

For a 2D vextension of the advection equation ({ref}'eq:NonLinAdvection_u_3d'), we get that both u and v are zero in all grid cells touching the boundaries.

**Slip boundary condition**

A slip boundary condition is also a type of wall boundary condition, but here you allow flow parallell to the boundary. This means that there is no frictional effects that decelelate the flow to zero near the wall. The slip condition is valid for non-viscous fluids. In slip conditions, you set a homegenous Dirichlet condition for flow normal to the wall (no flow through the wall) and a homogenous von Neumann boundary condition for flow paralell to the wall (no changes in velocity). 

If you consider the same example as for no-slip boundaries, it means that the river flows with the same velocity in all grid cells, including the grid cell closest to the boundaries.

Fo a 2D advection example as above, $u=0$ at the eastern and western boundaries, but are non-zero at the northern and southern boundaries, meaning there is flow along the boundnary. Similarly, $v=0$ at the norhtern and southern boundary, but is non-zero along the eastern and western boundaries. For the flow along the boundaries, we must ensure a homogenous von Neuman condition.

## Periodic boundary conditions

Consider a 1D domain for a simple 1D advection model. Imagine that the domain is a strip of paper that you bend into a circle and tape the two ends together. This will give you a circular domain, where the signal is smoothly flowing around and around. When you view as 1D plot, it will appear as the signal is leaving the domain at one end/boundary and re-enter at the end. You can use periodic boundary conditions for 2D and 3D models as well, but is becomes harder to imagine how the doian looks like if you tape it together at the boundaries.

Periodic boundaries are often used in regional models, where the topography and properties of the flow does not change much while passing the model domain. One of the biggest advangates of this boundary condition, is that you effectively avoid boundaries. You do not need to make any physical decisions for what happens at the boundaries. Instead, you use the same numerical scheme as for the iternal gri points, and make sure that the indices wrap around the periodic boundary.

Let us consider an example with a 1D model for advection and a forward in time, centered in space (FTCS) scheme:

$$
u_{m}^{n+1} = u_{m}^{n-1} - c\frac{\Delta t}{\Delta x}(u_{m+1}^{n}-u_{m-1}^{n}),
$$ (eq:Leapfrog)

We now, use the same scheme for each of the two boundaries, $x=0$ an $x=L$ and adjust the index $m$ to match a boundary taped together. Here you can think of the coninuos indices at the border to be $(\ldots, L-2,L-2,L,0,1,2,\ldots)$

$$
\begin{align}
u_{0}^{n+1} = u_{0}^{n-1} - c\frac{\Delta t}{\Delta x}(u_{1}^{n}-u_{L}^{n}),\\
u_{L}^{n+1} = u_{L}^{n-1} - c\frac{\Delta t}{\Delta x}(u_{0}^{n}-u_{L-1}^{n})
\end{align}
$$ (eq:BC_periodic)

```{note}
Python has periodic boundary conditions build-in at the left hand side (lower end) of your domain. If you provide a python array with a negative index, it will start counting backward from the right hand side. Make sure that you always check how you define your boundaries, and make a comment in your code if you are deliberately taking advantage of this feature. There is no periodic boundary built-in at the right boundary. If you try to parse and index that is larger than $L$, you will get an error message.
```
