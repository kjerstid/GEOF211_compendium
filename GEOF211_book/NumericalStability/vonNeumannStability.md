(NumericalStability:vonNeumannStability)=
# Von Neumann Stability Analysis

The von Neumann stability analysis method is simple to apply but it cannot handle boundary conditions.

It consists of replacing the spatial variation by a single Fourier component. The method is sufficient for linear equations with constant coefficients.

We shall illustrate the Von Neumann stability method with the FTCS scheme.

(NumericalStability:vonNeumannStabilityFTCS)=
## Stability of the FTCS scheme

### The linear advection equation

The FTCS scheme for the linear advection equation is given by:

```{math}
:label: eq:FTCSAdvection
u_m^{n+1} = u_m^{n} - c\frac{\Delta t}{2\Delta x}(u_{m+1}^n-u_{m-1}^n)
```

To apply the Von Neumann stability analysis method we assume a solution of the form:

```{math}
:label: eq:vonNeumannSolution
u_m^n=B^n e^{ikm\Delta x}. 
```

Substituing in {eq}`eq:FTCSAdvection`, we get

```{math}
B^{n+1} e^{ikm\Delta x} &= B^{n} e^{ikm\Delta x} - c\frac{\Delta t}{2\Delta x}(B^{n} e^{ik(m+1)\Delta x}-B^{n} e^{ik(m-1)\Delta x}) \\
B^{n+1} e^{ikm\Delta x} &= B^{n} e^{ikm\Delta x}\left[1 - c\frac{\Delta t}{2\Delta x}(e^{ik\Delta x}-e^{-ik\Delta x})\right].
```

Eliminating the common factor $e^{ikm\Delta x}$ and defining the amplification factor as $|B^{n+1}/B^n|$, we can write:

```{math}
\frac{B^{n+1}}{B^n}=1-c\frac{\Delta t}{\Delta x}i\sin k\Delta x
```

For the scheme to be stable, we require that the amplification factor be $\leq 1$:

```{math}
\left|\frac{B^{n+1}}{B^n}\right|=\left|1-c\frac{\Delta t}{\Delta x}i\sin k\Delta x\right|\leq 1,
```

which is impossible to fulfill, because

```{math}
\left|\frac{B^{n+1}}{B^n}\right|=\sqrt{1+\left(c\frac{\Delta t}{\Delta x}\right)\sin^2 k\Delta x} \ge 1, \quad \text{for all } k.
```

Therefore, the FTCS scheme applied to the linear advection equation is always unstable, i.e., it is *unconditionally unstable*.



