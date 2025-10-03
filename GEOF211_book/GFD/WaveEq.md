# The wave equation

## The classical wave equation

The classical wave equation in 1D can be written:

definition:Wave)=
:::{admonition} The wave equation
:class: important
```{math}
:label: eq:Waves
\frac{\partial^2 \eta}{\partial t^2}=c^2\frac{\partial^2 \eta}{\partial x^2}
```
:::

, where $\eta$ represents the vertical displacement of the wave surface. In the ocean this would mean the deviation from the mean sea surface heigh.

The general solution to the wave equation {eq}`eq:Waves` can be expressed as:

```{math}
:label: eq:WavesSolution
\eta(x,t)=f(x+ct)+g(x-ct)
```

The solution represents one wave moving eastward ($f(x+ct)$) and one wave moving westward (g(x-ct)). If a surface is initially disturbed, such as from depressing the surface, waves will spread in all directions. If you throw a pebble in a puddle, you will see waves spreading like rings from the center of where you threw the pebble. For the 1D case, you can think of it as a transect cutting across the 2D case, or alternatively as 
throwing a pebble in a very narrow and long puddle. Here, the waves spread in only 2 directions, as is indicated in the solution to the wave equation {eq}`eq:WavesSolution`. 

## Inertia-Gravity waves

Inertia-gravity waves describes the relation between the surface elevation and velocity. We have a set of coupled equations where one equation describes the change in surface elevtion with time caused by a horizontal velocity shear. Additionally, we have one equation (or 2, if northward velocity $v\ne0$) describing the acceleration of water parcels associated with horizontal gradients in surface elevation and coriolis. 

definition:InertiaGravity)=
:::{admonition} Inertial Gravity waves
:class: important
```{math}
:label: eq:InertiaGravity
\begin{aligned}
\frac{\partial \eta}{\partial t}+H\frac{\partial u}{\partial x}&=0\\
\frac{\partial u}{\partial t}-fv&=-g\frac{\partial p}{\partial x}\\
\frac{\partial v}{\partial t}+fu&=0
\end{aligned}
```
:::

You may see the resemblance between the two latter equations in {eq}`eq:InertiaGravity`and the inertial oscillations from {eq}`eq:InertialOscillations`. The only term separating them is the right hand side of {eq}`eq:InertiaGravity`, which is nonzero, and contains a term linking the oscillatory motion to gravity and horizontal pressure differences caused by the surface elevation $\eta$. Here, the surface elevation is only varying in one dimension, representing a wave moving in the east/west dimension (i.e., $\frac{\partial \eta}{\partial y}=0$).

{eq}`eq:InertiaGravity` are a set of coupled equations. The velocity and surface elevation terms are connected, and you have to solve the equations jointly.
