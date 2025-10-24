(Calculus:DiffEq)=
# Differential equations

Equations that contains derivatives of a variable, are called differential equations. An example could be the hydrostatic balance {eq}`eq:Hydrostatic`, where $\frac{\partial p}{\partial z}+\rho g=0$. Here you find two variables: pressure, $p$, and density, $\rho$. The pressure is differentiated with respect to vertical space, $z$.

The order of the differential equation is following the order of the highest derivatives in the equation. The hysdrostatic equaton is, therefore, a first order differential equation, whereas the wave equation ({eq}`eq:Waves`) is a second order differential equation

## Ordinary differential equations, ODE
(definition:errorApproximation)=
:::{admonition} Definition
:class: important
**Ordinary differential equations, ODEs** have derivatives with respect to only independent variable. 
:::

The hydrostatic equation above, and the inertial oscillations ({eq}`eq:InertialOscillations`) are examples of ordinary differential equations. 


## Partial differential equations, PDE
(definition:errorApproximation)=
:::{admonition} Definition
:class: important
**Partial differential equations, PDEs** have derivatives with respect to more than one independant variable. 
:::

The Navier-Stokes equation ({eq}`eq:NavierStokes`), the wave equation ({eq}`eq:Waves`) and the continuity equation ({eq}`eq:Continuity_main`) are examples of partial differential equations.

For second order partial differential equations with two dependant variables, we have an additional classification depending on the terms included. This classification comes from the resemblance to the equations describing ellipses, hyperbolas, and parabolas.

* Elliptic equatons are of the type $\frac{\partial^2 u}{\partial x^2}+\frac{\partial^2 u}{\partial y^2}+\ldots=0$.

* Hyperbolic equatons are of the type $\frac{\partial^2 u}{\partial x^2}-\frac{\partial^2 u}{\partial y^2}+\ldots=0$.

* Parabolic equatons are of the type $\frac{\partial^2 u}{\partial x^2}+\ldots=0$.

Can you identify any equations on either of these categories?



