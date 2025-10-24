(scheme:lax-wendroff)=
# The Lax-Wendroff 1-step approach from Taylor expansions

The Lax-Wendroff 1-step approach start with the equation of interest (here, the linear advection equation) and the Taylor expansion for $u_m^{n+1}$:

```{math}
:label: eq:LinAdv
\frac{\partial u}{\partial t}=-a\frac{\partial u}{\partial x}
```

```{math}
:label: eq:TaylorExp
u_m^{n+1}=u_m^n+\Delta t\frac{\partial u}{\partial t}\mid_m^n+\Delta t^2\frac{\partial^2 u}{\partial t^2}\mid_m^n+\Delta t^3\frac{\partial^3 u}{\partial t^3}\mid_m^n+h.o.t
```

To get a higher order scheme, we can replace both the first and second derivatives of $u$ by first expressing them in terms of spatial derivatives, which we can get from {eq} ´eq:LinAdv´. 


To obtain an expression for the first derivative, we can simply use {eq} ´eq:LinAdv´ and insert a central space scheme for the spatial derivative:

```{math}
:label: eq:Taylor1diff
\frac{\partial u}{\partial t}\mid_m^n=-a\frac{u_{m+1}^n-u_{m-1}^n}{2\Delta x}
```

To obtain an expression for the second derivative, we can differentiate {eq} ´eq:LinAdv´ once with respect to time and once with respect to space and then combine the two results:

```{math}
:label: eq:advectiondiff
\begin{aligned}
\frac{\partial^2 u}{\partial t^2}&=-a{\color{salmon}{\frac{\partial^2 u}{\partial x\partial t}}}\\
{\color{salmon}{\frac{\partial^2 u}{\partial t\partial x}}}&=-a\frac{\partial^2 u}{\partial x^2}
\end{aligned}
```

The second equation of {eq}`eq:advectiondiff` gives us an expression of ${\color{salmon}{\frac{\partial^2 u}{\partial t\partial x}}}$ which we can insert into the forst equation of {eq}`eq:advectiondiff` to obtain:

```{math}
:label: eq:advection2diff
\frac{\partial^2 u}{\partial t^2}=-a^2\frac{\partial^2 u}{\partial x^2}\\
```

If we now insert a central in time scheme for the right hand side of eq:advection2diff, we obtain;

```{math}
:label: eq:Taylor2diff
\frac{\partial^2 u}{\partial t^2}\mid_m^n \sim a^2\frac{u_{m+1}^n-2u_m^n+u_{m-1}^n}{\Delta x^2}
```

We can now insert {eq}`eq:Taylor1diff` and {eq}`eq:Taylor2diff` into {eq}`eq:TaylorExp` to get the 1-step scheme:

```{math}
u_m^{n+1}=u_m^n-\frac{a \Delta t}{2\Delta x}\left( u_{m+1}^n-u_{m-1}^n\right)+\frac{a^2\Delta t^2}{2\Delta x^2}\left( u_{m+1}^n-2u_m^2+u_{m-1}^n \right)+h.o.t
```

By further massaging an incorporating the $C=\frac{a\Delta t}{\Delta x}$, we get:

```{math}
u_m^{n+1}=\frac{C}{2}(1+C)u_{m-1}^n+(1-C^2)u_m^n-\frac{C}{2}(1-C)u_{m+1}^n+h.o.t
```

## Consistency, stability and convergence for the Lax-Wendroff scheme

The scheme is 2nd order in time and space. To determine its stability we can express the scheme as:

$$
	u_m^{n+1} = \alpha u_{m-1}^n + \beta u_m^n + \gamma u_{m+1}^n
$$

with 

```{math}
\begin{aligned}
	\alpha &= \frac{\sigma}{2}(\sigma + 1),\\
	\beta &= 1- \sigma^2, \\
	\gamma &= \frac{\sigma}{2}(\sigma - 1)
\end{aligned}
```

Assuming a solution of the type $B^n e^{i\lambda m \Delta x}$, the amplification factor is 

```{math}
	G=(1+\sigma^2(\cos \lambda \Delta x - 1)) - i\sigma \sin \lambda \Delta x
```

which has a norm 

```{math}
	|G|^2 = 1-\sigma^2(1-\sigma^2)(1 - \cos \lambda \Delta x)^2.
```

For the method to be stable, the condition is $|G|^2 \leq 1$ which provides the following stability condition

```{math}
	1-\sigma^2 \ge 0 \Leftrightarrow \sigma = \frac{a\Delta t}{\Delta x} \leq 1.
```

which is the well-known CFL condition.

