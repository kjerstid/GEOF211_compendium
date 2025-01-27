(NumericalStability:CFL)=
# Courant-Friedrich-Lewy, CFL criterion

The CFL criterion is named after the mathematicians Richard Courant, Kurt Otto Friederichs and Hans Lewy who published a piece "On the partial difference equations of mathematical physics" in 1928, where they discuss the factor and how it relates to stability. 

To understand where the CFL criterion comes from, we can, for example, look at the FTBS scheme for the linear advection equation:

$$
q_m^{n+1}=q_m^n-a\frac{\Delta t}{\Delta x}(q_m^n-q_{m-1}^n)
$$

(definition:CFL)=
:::{admonition} Definition
:class: important
The factor $C=a\frac{\Delta t}{\Delta x}$ is typically called the *Courant number* or simply the *CFL* number
:::

When examining the CFL number, we compare  the size of the displacement during one time step ($a\Delta t$) to the grid cell size $\Delta x$. For most numerical schemes, $C\leq 1$ is a necessary (but not sufficient!) condition for stability. If the displacement is much larger than the grid cell size, $C>>1$, the signal travels many grid cells in just one time step. This means that we cannot calculate the next time step based on the few neighboring grid points like we do in the simple Finite Difference schemes. 

## Characteristics of the linear advection equation

The analytical solution to the linear advection equation (eq {eq}`eq:Advection`) is given by $q(x,t)=q_0(x-at)$, or we can write it as $q(x-at,0)$. For this to be true, the solution must be constant along the charachteristics $x-at$. We can sketch this in the $x-t$ space:

```{figure} ../Figures/Test1.png
The charactheristics for linear advection with different values of $a$ in different colors. The solution starting at any of these characteristics will stay at the charachteristics as they translate in time and space.
```

Alternatively, we can translate the charactheristics to find how they look while passing through the grid point $(m,n)$. The domain of dependence for the exact solution, will lie along the charachteristics.

```{figure} ../Figures/Lin_adv_charachteristic_2.png
The charactheristics for linear advection with different values of $a$ in different colors. The solution starting at any of these characteristics will stay at the charachteristics as they translate in time and space.
```

If we now combine the figures showing the numerical domain of dependence for the FTBS scheme and the exact domain of dependence from the charactheristics, we obtain:

```{figure} ../Figures/Lin_adv_charachteristic_3.png
Domain of dependence for the exact (analytical) solution of the linear advection equation (colors) and for the FTBS scheme (shaded triangles).
```

If the analytical domain of dependence lies within the numerical domain of dependence of a given scheme, then the scheme fullfills a necessary (but not sufficient) requirement for stability. 

The slope of the charachteristic (i.e., physical DoD) is $1/a$. The slope of the nuemrical DoD is $\Delta t/\Delta x$. The physical DoD is within the numerical DoD if $\frac{\Delta t}{\Delta x}\leq \frac{1}{a}$.

This is true if  $a\frac{\Delta t}{\Delta x}\leq 1$. We recognize this as the CFL conditions, where $C=a\frac{\Delta t}{\Delta x}$




