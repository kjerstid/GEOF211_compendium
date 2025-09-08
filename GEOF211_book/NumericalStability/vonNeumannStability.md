(NumericalStability:vonNeumannStability)=
# Von Neumann Stability Analysis

The von Neumann stability analysis method is simple to apply but it cannot handle boundary conditions.

It consists of replacing the spatial variation by a single Fourier component. The method is sufficient for linear equations with constant coefficients.

We shall illustrate the Von Neumann stability method with the FTCS scheme.

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

Substituing in {eq}`eqFTCSAdvection`, we get

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

### The diffusion equation

The one-dimensional diffusion equation is 

```{math}
:label: eq:diffusion
\frac{\partial u}{\partial t} = D \frac{\partial^2 u}{\partial x^2},
```

where $D$ is the diffusivity. 

The FTCS scheme applied to {eq}`eq:diffusion` is:

```{math}
:label: eq:FTCSDiffusion
u_m^{n+1} = u_m^{n} + D\frac{\Delta t}{\Delta x^2}(u_{m+1}^n-2u_{m}^n+u_{m-1}^n)
```

Substituting a solution like {eq}`eq:vonNeumanSolution` in {eq}`eq:FTCSDiffusion`, we have

```{math}
B^{n+1}e^{ikm\Delta x}=B^ne^{ikm\Delta x}+ D\frac{\Delta t}{\Delta x^2}(B^{n} e^{ik(m+1)\Delta x}\\
    -2B^{n} e^{ikm\Delta x}+(B^{n} e^{ik(m-1)\Delta x})
```

which, after some manipulation, allows to obtain the following expression for the amplification factor:

```{math}
\frac{B^{n+1}}{B^n} = 1-2\tau+2\tau\cos k\Delta x = 1-4\tau \sin^2 \frac{k \Delta x}{2}, \quad \tau=D\frac{\Delta t}{\Delta x^2}.
```

The Von Neumann stability condition is:

```{math}
:label: eq:vonNeumannCOnditionDiffusion
\left|\frac{B^{n+1}}{B^n}\right|\leq 1 \Leftrightarrow \left|1-4\tau \sin^2 \frac{k \Delta x}{2}\right| \leq 1, \quad \text{for all } k.
```

For $\tau > 0$, the worst case occurs when $\sin^2 \frac{k \Delta x}{2}=1$, which leads to 

$$
\tau \leq \frac{1}{2}. 
$$

Therefore, the FTCS scheme apllied to the linear diffusion equation {eq}`eq:diffusion` is *conditionally stable*, with the stability condition

```{math}
:label: eq:cflLiomitDiffusion
D\frac{\Delta t}{\Delta x^2} \leq \frac{1}{2}.
```


