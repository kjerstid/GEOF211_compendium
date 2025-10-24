(GFD:Primitive Equations)=
# The Primitive equations

## The continuity equation
The continuity equation is very important in geophysical fluid dynamics. It comes from the principle of mass conservation. It states that the total rate of change of mass is zero ({eq}`eq:Continuity_main`). The physical interpretation of the equation, is that a local change of mass with time ($\frac{\partial \rho}{\partial t}$) is caused by advection, i.e., flow in or out of a volume unit.


(definition:Continuity main)=
:::{admonition} The continutiy equation
:class: important
```{math}
:label: eq:Continuity_main
\frac{\partial \rho}{\partial t}+\frac{\partial}{\partial x}(\rho u)+\frac{\partial}{\partial y}(\rho v)+\frac{\partial}{\partial z}(\rho w)=0
```
:::

The continity equation can also be expressed in a more compact vector form:

(definition:Continuity main)=
:::{admonition} The continutiy equation on vector form
:class: important
```{math}
:label: eq:Continuity_main_vector
\frac{\partial \rho}{\partial t}+\nabla\cdot(\rho\bar{u})=0
```
:::

For incompressible fluids, we can eliminitate variations in density ($\rho$) and get the following simplified version of the continuity equation:

(definition:Continuity incompress)=
:::{admonition} The continutiy equation for incompressible fluids
:class: important
```{math}
:label: eq:Continuity
\frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}+\frac{\partial w}{\partial z}=0
```
:::


## The Navier-stokes equation
The Navier-Stokes equation, also known as the **Equation of motion**, describes how velocity change with time as a result of external forces such as gravity, pressure, friction, and Coriolis. If we assume incomporessibility and use the Boussinesq approximation which ignores density variation in all terms except for the term where we multiply density with gravity, the equation can be expressed:

(definition:Navier-Stoke)=
:::{admonition} The Navier-Stokes equation 
:class: important
```{math}
:label: eq:NavierStokes
\begin{aligned}
x:&\overbrace{\frac{\partial u}{\partial t}}^{\text{Local change}}
+\overbrace{u\frac{\partial u}{\partial x}+v\frac{\partial u}{\partial y}+w\frac{\partial u}{\partial z}}^{\text{Advection}}-\overbrace{fv}^{\text{Coriolis}}&&=\overbrace{-\frac{1}{\rho_0}\frac{\partial p}{\partial x}}^{\text{Pressure gradient}}+\overbrace{0}^{\text{gravity}}+\overbrace{\frac{\partial}{\partial x}(\mathscr{A}_H\frac{\partial u}{\partial x})z+\frac{\partial}{\partial y}(\mathscr{A}_H\frac{\partial u}{\partial y})+\frac{\partial}{\partial z}(\mathscr{A}_v\frac{\partial u}{\partial z})}^{\text{Friction}}\\
y:&\quad\frac{\partial v}{\partial t}\quad+ u\frac{\partial v}{\partial x}+v\frac{\partial v}{\partial y}+w\frac{\partial v}{\partial z}\quad+fu&&=\quad-\frac{1}{\rho_0}\frac{\partial p}{\partial y}\quad+\quad0\quad+\frac{\partial}{\partial x}(\mathscr{A}_H\frac{\partial v}{\partial x})+\frac{\partial}{\partial y}(\mathscr{A}_H\frac{\partial v}{\partial y})+\frac{\partial}{\partial z}(\mathscr{A}_v\frac{\partial v}{\partial z})\\
z:& &0\qquad&=\qquad-\frac{\partial p}{\partial z}\quad-\quad\rho g
\end{aligned} 
```
:::

where:

* $u$ and $v$ are the velocity in Estward and Northward direction, respectively,
* $p$ is the pressure,
* $\rho_0$ is the reference density,
* $\rho$ is the density perturbation,
* $\nu$ is the kinematic viscosity,
* $g$ is the gravitational acceleration,
* $f=2\Omega sin\phi$ is the Coriolis parameter,
* $\phi$ is the latitude,
* $\mathscr{A}_H$ and $\mathscr{A}_V$ are the horizontal viscosity and vertical eddy diffusivities, respectively.



,$\rho_0$ is a constant reference density, $g$ is the gravitational acceleration, $f=2\Omega sin\phi$ is the Coriolis parameter, $\phi$ is the latitude, and $\mathscr{A}_H$ and $\mathscr{A}_V$ are the horizontal viscosity and vertical eddy diffusivities, respectively. Since we assumed incompressibility, we get the  hydrostatic balance in the the vertical direction.

The vector form of the Navier-Stokes equation provides a compact notation:

(definition:NS_vector)=
:::{admonition} The Navier-Stokes equation on vector form:
:class: important
```{math}
:label: eq:NS_vector
$\frac{\partial \bar{u}}{\partial t} + (\bar{u} \cdot \nabla)\bar{u}+ 2\bar{\Omega} \times \bar{u}= -\frac{1}{\rho_0} \nabla p + \mathscr{A} \nabla^2 \bar{u} + \bar{g} \frac{\rho}{\rho_0}
```
:::


## The Hydrostatic equation
When the water column is in hydrostatic equilibrium, the vertical component of the Navier-Stokes {eq}`eq:NavierStokes`becomes:

(definition:Hydrostatic)=
:::{admonition} The Hydrostatic equilibrium
:class: important
```{math}
:label: eq:Hydrostatic
0=-\frac{\partial p}{\partial z}\rho g
```
:::

## The density equation (energy equation)

(definition:densityEq)=
:::{admonition} The density equation
:class: important
```{math}
:label: eq:Density
\frac{\partial \rho}{\partial t}+u\frac{\partial \rho}{\partial x}+v\frac{\partial \rho}{\partial y}+w\frac{\partial \rho}{\partial z}=\frac{\partial}{\partial x}(\mathscr{A}_H\frac{\partial \rho}{\partial x})+\frac{\partial}{\partial y}(\mathscr{A}_H\frac{\partial \rho}{\partial y})+\frac{\partial}{\partial z}(\mathscr{A}_V\frac{\partial \rho}{\partial z})
```
:::

If the right hand side of the density equation is zero, we have conservation of mass.

You can read more about these equations in {cite:ts}`Cushman-RoisinBeckers2011`, chapter 3.1 and 4.4




