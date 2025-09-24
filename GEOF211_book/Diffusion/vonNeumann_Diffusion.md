# von Neumann stability analysis for the diffusion equation

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

Substituting a solution like {eq}`eq:vonNeumannSolution` in {eq}`eq:FTCSDiffusion`, we have

```{math}
B^{n+1}e^{ikm\Delta x}=B^ne^{ikm\Delta x}+ D\frac{\Delta t}{\Delta x^2}B^{n} e^{ik(m+1)\Delta x}\\
    -2B^{n} e^{ikm\Delta x}+B^{n} e^{ik(m-1)\Delta x}
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