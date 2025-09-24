(GFD:Diffusion)=
# The diffusion equation

The diffusion equation describes a molecular mixing process that, with time, distributes a parameter (e.g., salt, temperature, momentum) towards a state with smaller spatial gradients. If you wait long enough, the parameter is evenly distributed.

The diffusion equation for momentum $u(x,t)$ is expressed:

```{math}
:label: eq:Diffusion
\frac{\partial u}{\partial t}=\gamma\frac{\partial^2u}{\partial x^2},
```

where $\gamma>0$ represents a diffusion coefficient, referred to as viscosity. 