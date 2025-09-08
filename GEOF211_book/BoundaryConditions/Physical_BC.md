(BoundaryCondtitions:Physical_BC)=
# Physical descriptions of boundary conditions

Physical descriptions of boundary conditions means that we design the type of boundary conditions (the mathematical ones described in section {ref}'BoundaryCondtitions:Mathematical_BC') to match a desired physical behavior at the boundary. Most of the considerations discussed below, relates to boundary conditions of momentum, $\bar u(x,y,t)=\begin{bmatrix} u(x,y,z,t) \\ v(x,y,z,t)\\w(x,y,z,t)\end{bmatrix}$, where viscous forces may become important close to wall boundary conditions, or where you must consider how the flow may pass through an open boundary. For other parameters, such as temperature, salinity, moisture, etc., you are more free to set the boundary conditions in various ways, depending on your types of boundaries.

## Closed boundary conditions
In geophysical fluid dynamic models, we sometimes encounter boundaries that should be closed and act like walls. In ocean models, we typically have coastlines, or in low-altitude atmospheric models we may tall mountain ranges. When we have a wall boundary condition, we must ensure that the fluid velocity normal to the boundary is zero. This means that we have a homogenous Dirichlet condition for flow normal to the wall. 

Let us consider an example with a 1D model for advection and a forward in time, centered in space (FTCS) scheme, on a model domain $x\in[0,L]$:

$$
u_{m}^{n+1} = u_{m}^{n-1} - c\frac{\Delta t}{\Delta x}(u_{m+1}^{n}-u_{m-1}^{n}).
$$ (eq:Leapfrog)

Here, we will define the homogenous wall Dirichlet conditions as:

```{math}
:label: eq:BC_wall
u_0^{n+1} = 0
```

se equation {@eq:BC_wall}.

$$
\begin{align}
u_0^{n+1} = 0\\
u_{L}^{n+1} = 0
\end{align}
$$ (eq:BC_wall)


In 2 dimensions, we must also consifer flow tangential to the boundary. here, we typically choose from no-slip or slip boundary conditions.

**No-slip boundary conditions**

A no-slip boundary condition is valid for viscous fluids, where the flow is not too strong and the viscosity is more important than kinetic effects. Non-slip conditions fixes the fluid velocity to zero on the walls. It implies that the fluid sticks to the boundary/wall with no relative movement between the fluid and the wall.

If you, for example, consider flow along a channel or a river, the flow will be slower near the walls, and in a thin layer next to the walls, it will be zero. The no-slip conditions is therefore typically a homogenous Dirichlet boundary condition for flow both normal to, an parallell with the boundary.

For a 2D extension of the advection equation ({ref}'eq:NonLinAdvection_u_3d'), we get that both u and v are zero in all grid cells touching the boundaries. Let our model domain be defined in the region $x\in[0_x,L_x]$ and $y\in[0_y,L_y]$. Then

$$
\begin{equation}
\begin{aligned}
u_{0_x,\perp}^{n+1} = 0\\
u_{L_x,\perp}^{n+1} = 0\\
u_{\parallel,0_y}^{n+1} = 0\\
u_{\parallel,L_y}^{n+1} = 0\\
\\
v_{0_x,\parallel}^{n+1} = 0\\
v_{L_x,\parallel}^{n+1} = 0\\
v_{\perp,0_y}^{n+1} = 0\\
v_{\perp,L_y}^{n+1} = 0\\
\end{aligned}
\end{equation}
$$ (eq:BC_no_slip)

, where $\parallel$ and $\perp$ refer to flow parallel to and perpendicular to the boundary, respectively.

**Slip boundary condition**

A slip boundary condition is also a type of wall boundary condition, but here you allow flow parallell to the boundary. This means that there is no frictional effects that decelelate the flow to zero near the wall. The slip condition is valid for non-viscous fluids. In slip conditions, you set a homegenous Dirichlet condition for flow normal to the wall (no flow through the wall) and a homogenous von Neumann boundary condition for flow paralell to the wall (no changes in velocity). 

If you consider the same example as for no-slip boundaries, it means that the river flows with the same velocity in all grid cells, including the grid cell closest to the boundaries.

Fo a 2D advection example as above, $u=0$ at the eastern and western boundaries, but are non-zero at the northern and southern boundaries, meaning there is flow along the boundary. Similarly, $v=0$ at the norhtern and southern boundary, but is non-zero along the eastern and western boundaries. For the flow along the boundaries, we must ensure a homogenous von Neuman condition. This gives Dirchlet boundary conditions for flow normal to the boundaries:

$$
\begin{equation}
\begin{aligned}
u_{0_x,\perp}^{n+1} = 0\\
u_{L_x,\perp}^{n+1} = 0\\
v_{\perp,0_y}^{n+1} = 0\\
v_{\perp,L_y}^{n+1} = 0\\
\end{aligned}
\end{equation}
$$ (eq:BC_no_slip_normal)

and homogenous Neumann boundary conditions for flow parallel to the boundaries

$$
\begin{equation}
\begin{aligned}
\frac{\partial u_{\parallel,0_y}^{n+1}}{\partial y} = 0\\
\frac{\partial u_{\parallel,L_y}^{n+1}}{\partial y} = 0\\
\frac{\partial v_{0_x,\parallel}^{n+1}}{\partial x} = 0\\
\frac{\partial v_{L_x,\parallel}^{n+1}}{\partial x} = 0\\
\end{aligned}
\end{equation}
$$ (eq:BC_no_slip_parallel)

## Open boundary conditions

Let's say you run a regional model for the west coast of Norway. The model will naturally have a coastline (or a wall) along the eastern boundary, but the other boundaries will cut through open water to keep the model restricted and exclude the rest of the world. This means that you much make decisions on what happens along the open boundaries. The NorKyst800, a regional 800 m model for the Norwegian coast is a great example of a model with three open boundaries.

```{note}
Ideally, we want the currents to pass smoothly across the open boundary. Although this may sound simple, open boundaries are hard to get right. Sometimes we must make compromises and accept a solution that is not fully desireable. And sometimes, we even set up model domains that are much larger than we need, just to avoid using output data from the area close to the boundaries ...
```

### Periodic boundary conditions

Periodic boundaries are often used in regional models, where the topography and properties of the flow does not change much while passing the model domain. One of the biggest advangates of this boundary condition, is that you effectively avoid boundaries.

Consider a 1D domain for a simple 1D advection model. Imagine that the domain is a strip of paper that you bend into a circle and tape the two ends together. This will give you a circular domain, where the signal is smoothly flowing around and around.  You, therefore, do not need to make any physical decisions for what happens at the open boundaries. Instead, you use the same numerical scheme as for the internal grid points, and make sure that the indices wrap around the periodic boundary.

When you view the model as 1D plots, it will appear as the signal is leaving the domain at one end/boundary and re-enter at the end. You can use periodic boundary conditions for 2D and 3D models as well, but is becomes harder to imagine how the doian looks like if you tape it together at the boundaries.

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

### Gradient boundary conditions (Neumann)

One simple approach for transporting fluids smoothly out (let the signal radiate out) of an open boundary, is to use the Neuman condition, and require that flow rate normal to the open boundary, e.g., $\partial u /\partial x$ along an open western boundary is zero. The flow rate could be derived from the two grid points closest to the boundary, or over a region close to the boundary. For flow parallell to the open boundary, you will typically use Dirichlet conditions, such as, for example $v=0$.

For paramters like temperature, salinity, moisture, etc., you can use Dirichlet or Neumann conditions, depending on the physics you are trying to replicate.

### Radiation boundary conditions

A slightly more advanced version of the gradient condition, is to let the flow radiate out of the model with a calculated flow speed. There are various choices for the flow speed. Excamples include, using the shallow-water wave speed $\sqrt{gH}$, where $g$ is the gravitational constant and $H$ is the fluid hight/depth (*Chapman* condition), the external gravity wave speed (*Flather* condition), or the local phase speed normal to the boundary (*Orlanski* conditions).

### Nudging conditions

Above, we explained how you can use the radiation condition to allow flow to leave your model domain. However, we said nothing about how flow can enter the model domain. A common way to do this, is to apply nudging, also called restoring. This means that you set a Dirichlet condition along the boundary, which may include a positive velocity into your model domain. If you, for example have a regional Norwegian coastal model, you may want to ensure that the relatively fixed northward-flowing coastal current is represented in your model. Here, you may force the current to enter through the southern boundary, and you can make decisions for how the current varies with times, or stays fixed. 

Wehen using nudging conditions, it is common to modify a region close to the boundary to avoid abrupt property changes within the model, and allow the model a region to adjust to the fixed values provided at the boundaries.

### Clamped conditions

This is a Dirichlet conditions, similar to the nudging condition, but without including adjustment over a region. This can lead to strong gradients in the vicinity of the boundary.

### Combined conditions

It is possible to combine open boundary conditions, either by using different types for different parameters, or by adjusting the outgoing/incoming fluid velocity. You can, for example, use radiation conditions for flow leaving the model, and nudging conditions for flow entereing the model.




