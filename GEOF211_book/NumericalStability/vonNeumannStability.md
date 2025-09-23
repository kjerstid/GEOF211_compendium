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

### The wave equation

The one-dimensional wave equation (equation {eq}`eq:Waves`), repeated here is :

```{math}
\frac{\partial^2 \eta}{\partial t^2}=c^2\frac{\partial^2 \eta}{\partial x^2}
```
,where $\eta$ is the fluid surface, $c=\sqrt{gH}$, $g\sim9.81\text{ms}^-1$ is the gravitational constant and $H$ is the depth of the fluid.

The CTCS scheme for the wave equation can be found using the centered formula (Eq. {eq}`eq:Centered2derivative`) for the second derivative on either side of the equation and reordering the expression:

```{margin}
```{note}
$r^2=\frac{c^2\Delta t^2}{\Delta x^2}$
```

```{math}
:label: eq:Waves_CTCS
\eta_m^{n+1}=2\eta_m^{n}-\eta_m^{n-1}+r^2(n_{m+1}^n-2n_{m}^n+n_{m-1}^n)
```

Substituting a solution like {eq}`eq:vonNeumannSolution`,$\eta_m^n\sim B^ne^{ikm\Delta x}$, in {eq}`eq:Waves_CTCS`, we have:

```{math}
\begin{aligned}

B^{n+1} e^{ikm\Delta 𝑥}&=2𝐵^𝑛 e^{ikm\Delta 𝑥} −B^{n−1} 𝑒^{ikm\Delta x}+𝑟^2 (B^n e^{ik(m+1)\Delta x}−2B^n e^{ikm\Delta x}+B^n e^{ik(m−1)\Delta x}) \quad \text{:Divide by }$e^{ikm\Delta x}\\ 
B^{n+1}&=2B^𝑛−B^{n−1}+r^2 B^n e^{ik\Delta 𝑥}−2r^2 B^n+r^2 B^n 𝑒^{−ik\Delta x} \qquad Factorize \\
B^{n+1}&=2(1−r^2)B^n−B^{n−1}+r^2 B^n \underbrace{(e^{ik\Delta x}+e^{−ik\Delta x})}_{2cos(k\Delta x)}\\
B^{n+1}&=2(1−𝑟^2)B^n−B^{n−1}+2r^2 B^n cos(k\Delta x) \qquad :Factorize\\
B^{n+1}&=2\left (1−2𝑟^2 \left (\frac{1−cos⁡(𝑘Δ𝑥)}{2}\right )\right )B^n−B^{n−1}
\qquad :Use $sin^2\frac{\theta}{2}=\frac{1-cos\theta}{2}$\\
B^{n+1}&=2(\underbrace{1−2𝑟^2sin^2\frac{k\Deltam x}{2}}_{\gamma})B^n−B^{n−1} \\
B^{n+1}&=2\gamma B^n−B^{n−1}             
\end{aligned}
```

This expression contains three timesteps of $B$. To solve from here, we could use a recurrence matrix, or we can check for specific timesteps. The condition $|\frac{B^{n+1}}{B^n}|<1$ only holds if it holds for any three concurrent timesteps. We can test the conditions with, e.g., inserting $n=1$, which yields:

```{math}
\begin{aligned}
B^2&=2\gamma B-B^0

B^2-2\gamma B+1&=0

B_{1,2}&=\gamma\pm\sqrt{\gamma^2-1}
\end{aligned}
```

We must have $|B_{1,2}|<1$. If $\gamma >1$, $B_1$ willl also be $>1$. We must, therefore, require $|\gamma|\le1$.

```{math}
\begin{aligned}
|\gamma|&=\left|1−2𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\right|\le1\\
-1&\le1−2𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\le1 \qquad:\text{Subtract 1 everywhere}\\
-2&\le−2𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\le0
\end{aligned}
```

The right inequality always holds. We must look more closely at the left inequality. Dividing by $-2$ and flipping the inequality, we have:

```{math}
\begin{aligned}
1&\ge𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\\
𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}&\le1
\end{aligned}
```

Since the sine squared is always positive and $\le1$, we must have $𝑟^2≤1$:

```{math}
r^2=\frac{c^2\Delta t^2}{\Delta x^2}\le1
```

which yields $r=\frac{c\Delta t}{\Delta x}\le1$. We, therefore, end up with the same CFL criterion as for the advection equation. 