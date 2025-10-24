(LinearAdvectionEquation:schemeStabiliz)=
# Schemes with stabilizing terms
Some schemes that are unstable, can be modified using stabilizing term. A common method for stabilizing schemes, is to replace one or more terms with the spatial or time averages of neighboring grid points. The Lax-Fiedrich scheme is an example of this.

## The Lax-Friedrich Scheme

The FTCS scheme for linear advection is unstable, as shown through the von Neumann analysis ({numref}`NumericalStability:vonNeumannStabilityFTCS`). The Lax Friedrich scheme is a simple modification of the FTCS scheme aiming to make the scheme stable. The main advantage of having a centered scheme in space, is that the signal can move in both direction, as seen fro the domain of dependence.

The FTCS scheme ({eq}`eq:FTCSAdvection`) is:

```{math}
u_m^{n+1} = u_m^{n} - c\frac{\Delta t}{2\Delta x}(u_{m+1}^n-u_{m-1}^n)
```

The Lax-Friedrich modification uses a **stabilizing term**, and replaces the first term on the right hand side with the average value of the two neighboring grid points in space:

```{math}
:label: eq:LaxFriedrich
u_m^{n+1} = \frac{1}{2}(u_{m+1}^{n}+u_{m-1}^{n}) - c\frac{\Delta t}{2\Delta x}(u_{m+1}^n-u_{m-1}^n)
```

```{note}
Try to do a von Neumann analysis of the Lax-Friedrich scheme. It is very similar to the analysis in {numref}`NumericalStability:vonNeumannStabilityFTCS` and is a great exercise to test your understanding of the stability analysis and the necessary mathematical manipulations.
```