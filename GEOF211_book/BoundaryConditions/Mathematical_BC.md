(BoundaryCondtitions:Mathematical_BC)=
# Mathematical descriptions of boundary conditions


There are many types of boundary conditions. The most common boundary conditions for geophysical fluid dynamics are Dirichlet, von Neumann, and Robin boundary conditions.

## Dirichlet boundary conditions
Dirichlet boundary conditions describes a boundary where you set a fixed value at the boundary. If you, for example, think about a 1D model for momentum $u(x,t)$ defined in the range $x\in[0,L]$ we can express this as:

$$
\begin{align}
u(x_{0},t)=f_1(t),\\
u(x_{L},t)=f_2(t),
\end{align}
$$ (eq:BV_Dirichlet)

where $x_{0,L}$ denotes the boundaries at $x=0$ and $x=L$, and $f_{1,2}(t)$ is a function of time or a constant value. 

```{note}
If $f_{1,2}(t)\equiv 0$, we call it a homogenous boundary condition.
```


## von Neuman boundary conditions
von Neumann boundary conditions describe a boundary where you define a fixed gradient, $\frac{\partial u}{\partial x}$, at the boundary. For the same type of probem as above, this will be expressed as:

$$
\begin{align}
\frac{\partial u(x_{0},t)}{\partial x}=f_1(t),\\
\frac{\partial u(x_{L},t)}{\partial x}=f_2(t)
\end{align}
$$ (eq:BV_Neumann)

## Robin boundary conditions
Robin boundary conditions is a mix of von Neuman and Dirichlet boundary conditions, where you decide a linear combination of $u(x,t)$ and the gradient $\frac{\partial u}{\partial x}$ at the boundaries:

$$
\begin{align}
\frac{\partial u(x_{0},t)}{\partial x}+a u(x_{0},t)=f1(t),\\
\frac{\partial u(x_{L},t)}{\partial x}+u(x_{L},t)=f_2(t)
\end{align}
$$ (eq:BV_Robin)