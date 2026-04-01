(GFD:Shallow Water)=
# The Shallow water equations

The shallow water equations describe waves that have long wave lengths compared to the water depth. The name suggests that these waves occur over shallow water. When surface gravity waves arise in the open ocean, they does not follow the shallow water equations. However, when the waves reach a sloping beach, they will start to behave like shallow water waves when the water column thickness becomes small relative to the wave lengths.

Shallow water waves an also occur in deep waters, when the wave lengths are sufficently long. See {numref}`fig:SWwave` for a sketch of the shallow water wave.

```{figure} ./SWwave.png
---
name: fig:SWwave
width: 75%
align: center
---
Sketch of a shallow water wave. The bottom depth is given by $h(x,y)$ and the surface elevation is given by $\eta(x,y,t)$.
```

To derive the shallow water equations, we start with the continuity equation for incompressible fluids (Eq. {eq}`eq:Continuity`), the Navier stokes equation (Eq. {eq}`eq:NavierStokes`), neglecting friction, and vertical shear in velocity ($\frac{\partial u}{\partial z}=\frac{\partial v}{\partial z}=0$), and the hydrostatic equation (Eq. {eq}`eq:Hydrostatic`): 

```{math}
:label: eq:SW_start
\begin{aligned}
\frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}+\frac{\partial w}{\partial z}&=0\\
\frac{\partial u}{\partial t}+u\frac{\partial u}{\partial x}+v\frac{\partial u}{\partial y}-fv&=-\frac{1}{\rho_0}\frac{\partial p}{\partial x}\\
\frac{\partial v}{\partial t}+u\frac{\partial v}{\partial x}+v\frac{\partial v}{\partial y}+fu&=-\frac{1}{\rho_0}\frac{\partial p}{\partial y}\\
g\rho&=-\frac{\partial p}{\partial z}
\end{aligned}
```

The vertical boundary conditions can be expressed as:

```{math}
:label: eq:SW_vert_bound
\begin{aligned}
\frac{D\eta}{Dt}&&=\frac{\partial \eta}{\partial t}+u\frac{\partial \eta}{\partial x}+v\frac{\partial \eta}{\partial y}=w(z=\eta)\qquad \text{Surface boundary conditions}\\
\bar{u}\cdot\nabla(z+h(x,y))&&=0\qquad \text{at} z=-h(x,y)\qquad\qquad \text{Bottom boundary conditions}
\end{aligned}
```
We can start by integrating the Hydrostatic balance Eq. {eq}`eq:Hydrostatic` from a chosen level $z$ to the free surface:

```{math}
:label: eq:hydrostatic_integral
\begin{aligned}
\int_z^\eta g\rho\,dz=-\int_z^\eta\frac{\partial p}{\partial z}\,dz\\
p(\eta)-p(z)=-g\rho_0(\eta-z)\\
p(z)=p(\eta)+g\rho_0(\eta-z)
\end{aligned}
```

We can now differentiate {eq}`eq:hydrostatic_integral`with respect to $x$ and $y$ to find the right hand sides of the horizontal Navier-Stokes equation. Note that $p(\eta)$ is a constant, typically set as a reference pressure of zero ($p_0$).

```{math}
:label: eq:hydrostatic_integral2
\begin{aligned}
\frac{\partial p}{\partial x}=\frac{\partial}{\partial x}(p_0+g\rho_0(\eta-z))=g\rho_0\frac{\partial \eta}{\partial x}\\
\frac{\partial p}{\partial y}=\frac{\partial}{\partial y}(p_0+g\rho_0(\eta-z))=g\rho_0\frac{\partial \eta}{\partial y}
\end{aligned}
```

By replacing the pressure in Eq. {eq}`eq:NavierStokes` with the expressions in Eq. {eq}`eq:hydrostatic_integral2`, we are done with the Navier-Stokes derivations.

We can now integrate the continuity equation over the water column depth:

```{margin}
```{note}
$$
w(\eta)=\frac{\partial \eta}{\partial t}
$$

$$
w(-h)=0
$$

For a continuous function, the integral and derivation order can be swapped.

```

```{math}
:label: eq:continuity:integral
\begin{aligned}
\int_{-h}^\eta\frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}+\frac{\partial w}{\partial z}dz=0\\
w(\eta)-w(-h)+\int_{-h}^\eta\frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}dz=0\\
\frac{\partial\eta}{\partial t}+\int_{-h}^\eta\frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}dz=0\\
\frac{\partial\eta}{\partial t}+\frac{\partial}{\partial x}\int_{-h}^\eta u\, dz+\frac{\partial}{\partial y}\int_{-h}^\eta v\, dz=0\\
\frac{\partial\eta}{\partial t}+\frac{\partial}{\partial x}u(\eta+h)+\frac{\partial}{\partial y}v(\eta+h)=0
\end{aligned}
```

We now arrive at the shallow-water equation:

(definition:SW)=
:::{admonition} The Shallow Water Equations
:class: important

```{math}
:label: eq:SWEq
\begin{aligned}

\frac{\partial u}{\partial t}+u\frac{\partial u}{\partial x}+v\frac{\partial u}{\partial y}-fv=-g\frac{\partial \eta}{\partial x}\\

\frac{\partial v}{\partial t}+u\frac{\partial v}{\partial x}+v\frac{\partial v}{\partial y}+fu=-g\frac{\partial \eta}{\partial y}\\

\frac{\partial\eta}{\partial t}+\frac{\partial}{\partial x}u(\eta+h)+\frac{\partial}{\partial y}v(\eta+h)=0

\end{aligned}
```
:::

