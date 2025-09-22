(GFD:Primitive Equations)=
# The Primitive equations

## The continuity equation

```{math}
:label: eq:Continuity_main
\frac{\partial \rho}{\partial t}+\frac{\partial}{\partial x}(\rho u)+\frac{\partial}{\partial y}(\rho v)+\frac{\partial}{\partial z}(\rho w)=0
```

For incompressible fluids, we can eliminitate $\rho$ and get the following version:

```{math}
:label: eq:Continuity
\frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}+\frac{\partial w}{\partial z}=0
```

## The Navier-stokes equation
The Navier-Stokes equation, also known as the equation of motion, describes how velocity change with time as a result of external forces such as gravity, pressure, friction, and Coriolis. Using the Boussinesq approximation, the equation can be expressed:

```{math}
:label: eq:NavierStokes
\begin{aligned}
x:&\overbrace{\frac{\partial u}{\partial t}}^{\text{Local change}}
+\overbrace{u\frac{\partial u}{\partial x}+v\frac{\partial u}{\partial y}+w\frac{\partial u}{\partial z}}^{\text{Advection}}
-\overbrace{fv}^{\text{Coriolis}}
&=\overbrace{-\frac{1}{\rho_0}\frac{\partial p}{\partial x}}^{\text{Pressure gradient}}
+\overbrace{0}^{\text{gravity}}
+\overbrace{\frac{\partial}{\partial x}(\mathscr{A}_H\frac{\partial u}{\partial x})z+\frac{\partial}{\partial y}(\mathscr{A}_H\frac{\partial u}{\partial y})+\frac{\partial}{\partial z}(\mathscr{A}_v\frac{\partial u}{\partial z})}^{\text{Friction}}\\

y:&\quad\frac{\partial v}{\partial t}
+u\frac{\partial v}{\partial x}+v\frac{\partial v}{\partial y}+w\frac{\partial v}{\partial z}
+fu
&=-\frac{1}{\rho_0}\frac{\partial p}{\partial y}
+0
+\frac{\partial}{\partial x}(\mathscr{A}_H\frac{\partial v}{\partial x})+\frac{\partial}{\partial y}(\mathscr{A}_H\frac{\partial v}{\partial y})+\frac{\partial}{\partial z}(\mathscr{A}_v\frac{\partial v}{\partial z})\\

z:& 0&=-\frac{\partial p}{\partial z}&-\rho g
\end{aligned} 
```

,$\rho_0$ is a reference density, $g$ is the gravitational acceleration, $f=2\Omega sin\phi$ is the Coriolis parameter, $\phi$ is the latitude, and $\mathscr{A}_H$ and $\mathscr{A}_V$ are the horizontal viscosity and vertical eddy diffusivities, respectively. Here, we assume incompressibility, which yields a hydrostatic balance in the the vertical direction.



## The density equation (energy equation)
```{math}
:label: eq:Density
\frac{\partial \rho}{\partial t}+u\frac{\partial \rho}{\partial x}+v\frac{\partial \rho}{\partial y}+w\frac{\partial \rho}{\partial z}=\frac{\partial}{\partial x}(\mathscr{A}_H\frac{\partial \rho}{\partial x})+\frac{\partial}{\partial y}(\mathscr{A}_H\frac{\partial \rho}{\partial y})+\frac{\partial}{\partial z}(\mathscr{A}_V\frac{\partial \rho}{\partial z})
```

If the right hand side of the density equation is zero, we have conservation of mass.

You can read more about these equations in {cite:ts}`Cushman-RoisinBeckers2011`, chapter 3.1 and 4.4

## References:

```{bibliography}
```



