(GFD:Waves)=
# The classical wave equation and its solution

The classical wave equation in 1D can be written:

```{math}
:label: eq:Waves
\frac{\partial^2 \eta}{\partial t^2}=c^2\frac{\partial^2 \eta}{\partial x^2}
```

, where $\eta$ represents the vertical displacement of the wave surface. In the ocean this would mean the deviation from the mean sea surface heigh.

The general solution to the wave equation {eq}`eq:Waves` can be expressed as:

```{math}
:label: eq:WavesSolution
\eta(x,t)=f(x+ct)+g(x-ct)
```

The solution represents one wave moving eastward ($f(x+ct)$) and one wave moving westward (g(x-ct)). If a surface is initially disturbed, such as from depressing the surface, waves will spread in all directions. If you throw a pebble in a puddle, you will see waves spreading like rings from the center of where you threw the pebble. For the 1D case, you can think of it as a transect cutting across the 2D case, or alternatively as 
throwing a pebble in a very narrow and long puddle. Here, the waves spread in only 2 directions, as is indicated in the solution to the wave equation {eq}`eq:WavesSolution`. 

## Proving the general solution 
We can prove that this solution is correct, by differentiating the solution twice using the chain rule and inserting the expressions into the equation. To make the calculations tidier, we can introduce a variable transform set $\phi=x+ct$ and $\psi=x-ct$. Our general solution now becomes $\eta(x,t)=f(\phi)+g(\psi)$. 

```{margin}
```{note}
When differentiating $\phi$ and $\psi$ with respect to $x$, they are both zero, while differentiating them with respect to $t$, gives either $+c$ or $-c$. 
```


```{math}
:label: eq:WavesSolution_proof_a
\begin{aligned}

\frac{\partial \eta}{\partial x} & =\frac{\partial f}{\partial \phi}\frac{\partial \phi}{\partial x}+\frac{\partial g}{\partial \psi}\frac{\partial \psi}{\partial x} & =\frac{\partial f}{\partial \phi}+\frac{\partial g}{\partial \psi}\\
\frac{\partial^2 \eta}{\partial x^2} & =\frac{\partial^2 f}{\partial \phi^2}\frac{\partial \phi}{\partial x}+\frac{\partial^2 g}{\partial \psi^2}\frac{\partial \psi}{\partial x} & =\frac{\partial^2 f}{\partial \phi^2}+\frac{\partial^2 g}{\partial \psi^2}\\

\frac{\partial \eta}{\partial t} & =\frac{\partial f}{\partial \phi}\frac{\partial \phi}{\partial t}+\frac{\partial g}{\partial \psi}\frac{\partial \psi}{\partial t} & =\frac{\partial f}{\partial \phi}c+\frac{\partial g}{\partial \psi}(-c)\\

\frac{\partial^2 \eta}{\partial t^2} & =c\frac{\partial^2 f}{\partial \phi^2}\frac{\partial \phi}{\partial x}-c\frac{\partial^2 g}{\partial \psi^2}\frac{\partial \psi}{\partial t} &v=c^2\frac{\partial^2 f}{\partial \phi^2}+(-c)^2\frac{\partial^2 g}{\partial \psi^2}

\end{aligned}
```


Inserting these expressions into the wave equation yields:
```{math}
:label: eq:WavesSolution_proof

\frac{\partial^2 \eta}{\partial t^2} =c^2\frac{\partial^2 f}{\partial \phi^2}+(-c)^2\frac{\partial^2 g}{\partial \psi^2}=c^2(\frac{\partial^2 f}{\partial \phi^2}+\frac{\partial^2 g}{\partial \psi^2})=c^2\frac{\partial^2 \eta}{\partial x^2}

```

## Solving the wave equation numerically

We can use the centered scheme for second deriatives (Equation {eq}`eq:Centered2derivative`) for both the time derivative and the space derivative, yielding a CTCS scheme:

```{margin}
```{note}
$r=\frac{c^2\Delta t^2}{\Delta x^2}$
```


```{math}
:label: eq:CTCS_Waves
\begin{aligned}
\frac{\eta_m^{n+1}-2\eta_m^n+\eta_m^{n-1}}{2\Delta t^2}&=c^2\frac{\eta_{m+1}^n-2\eta_m^n+\eta_{-1}^n}{2\Delta x^2}\qquad\text{:Solving for }\eta_m^{n+1}\\
\eta_m^{n+1}&=2(1-r^2)\eta_m^n+r^2(\eta_{m+1}^n+\eta_{m-1}^n)-\eta_m^{n-1}
\end{aligned}
```

The CTCS scheme for the classical wave equation includes three time steps for $\eta$. To start a time marching algorithm, we need to now both $\eta_m^0$ and $\eta_m^1$. 

A common workaround to make life easy, is to use the same initial condition for both time step $n=0$ and $n=1$.

A more common method, is to assign both a Dirichlet initial condition for $\eta_m^0$ and a von Neumann initial condition for the derivative $\frac{\partial\eta_m^0}{\partial t}$:

```{math}
:label: eq:ini_wave_Dirichlet
\eta_m^0=f(x_m)
````

```{math}
:label: eq:ini_wave_Neumann
\frac{\partial\eta_m^0}{\partial t}=g(x_m)
```

Equation {eq}`eq:ini_wave_Neumann`can be expressed through a second order centered difference scheme:

```{math}
:label: eq:ini_wave_Neumann_C
\begin{aligned}
\frac{\eta_m^1-\eta_m^{-1}}{2\Delta t}&=g(x_m)
\eta_m^1-eta_m^{-1}&=2\Delta t(g(x_m))
\end{aligned}
```

We can rearrange the numerical scheme of our CTSC model and insert $n=0$ (Equation {eq}`eq:CTCS_Waves`) to yield:

```{math}
:label: eq:CTCS_Waves_n0
\eta_m^1+\eta_m^{-1}=2(1-r^2)\eta_m^0+r^2(\eta_{m+1}^0+\eta_{m-1}^0)
```

Now, we can add Equation {eq}`eq:ini_wave_Neumann`   and {eq}`eq:CTCS_Waves_n0` to obtain an equation for $\eta_m^1$. Together with the Dirichlet booundary condition, we now have:

```{margin}
```{note}
Here we use $\eta_m^0$ with $f(x_m)$ from the first equation into the second.
```

```{math}
:label: eq:CTCS_Waves_ini
\begin{aligned}
\eta_m^0&=f(x_m)\\
\eta_m^1&=\frac{r^2(\eta_{m+1}^0+\eta_{m-1}^0)}{2} +(1-r^2)\eta_m^0+\Delta t g(x_m)\\
 &=\frac{r^2(f(x_{m+1})+f(x_{m-1}^0))}{2} +(1-r^2)f(x_m)+\Delta t g(x_m)
\end{aligned}
```

