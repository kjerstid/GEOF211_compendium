---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
(scheme:crank-nicholson-diffusion)=
# The Crank-Nicholson Scheme for diffusion

The Crank-Nicholson scheme was originally designed to solve the diffusion equation (heat conduction)

```{math}
:label: eq:schemeCrankNicolson_diffusion
  \frac{u_m^{n+1}-u_m^n}{\Delta t} = -\frac{\gamma}{\Delta x^2}\left(\frac{u_{m+1}^{n+1}-2u_{m-1}^{n+1}+u_{m+-}^{n+1}}{2} + \frac{u_{m+1}^{n}-2u_{m-1}^{n}+u_{m-1}^{n}}{2}\right)
```

The scheme is a modification of the FTCS (Forward in time, centered in space) scheme. It uses the forward approximation to the time derivative at $t^n$ and the average of the centred approximations of the space derivative at $t^n$ and $t^{n+1}$.

Another way of looking at {eq}`eq:schemeCrankNicolson` is that the left hand side (LHS) is a centred approximation of the time derivative at $t^{n+1/2}$ and the averaging of the spatial derivatives provides an estimate of the spatial derivative at $t^{n+1/2}$.

The use of the terms at $t^{n+1}$ poses a complication because these are not known at time $t^n$. Therefore, the scheme is not an explicit time marching scheme as we have seen so far, but one where the solution is implicit in the scheme itself, hence the designation of *implicit* scheme. To obtain the unknown values at $t^{n+1}$, a linear system of equations must be solved. 

We can expand {eq}`eq:schemeCrankNicolson` to obtain 

```{math}
  -ru_{m-1}^{n+1}  + (1+2r)u_m^{n+1} -ru_{m+1}^{n+1} =
    ru_{m-1}^{n}  + (1-2r)u_m^{n} +ru_{m+1}^{n},\quad C = \gamma\frac {\Delta t}{\Delta x^2}, \quad r=\frac{C}{2}   
```

that is a linear system of equations 

```{math}
:label: eq:schemeAB
  A\mathbf{u}^{n+1}=B\mathbf{u}^{n}.
```

To find the matrices, you can first insert $m=0$ into the equation. This will give you the first row in $A$ and $B$, respectively. You will find the second row by inserting $m=1$ and so forth until the last row is found by inserting $m=L$. 

The matrices $A$ and $B$ below, represents a case of Dirichlet boundary conditions, $u(0,t)=u_0^n=0$ and $u(L,t)=u_L^n=0$. This is why the matrices do not include a first column for $u_0^{n+1}$ or a last column for $u_L^{n+1}$.

If you choose boundary conditions where $u(0,t)\neq 0$ and $u(L,t)\neq 0$, you will need to consider what value they take, and extend the matrices A and B with one column for $u_0$ and one for $u_L$ at either side of the matrices. 

```{math}
A = 
\begin{pmatrix}
  1+2r                        & -r   & 0                             &         0                & \cdots & 0\\
  -r & 1+2r                         & -r       &         0                & \cdots & 0\\
                          0 & -r & 1+2r                              & -r & \cdots & 0\\
            \vdots       &          \vdots        &   \vdots                     & \ddots               & \vdots  & \vdots\\
            0               &              \cdots           &            0             & -r & 1+2r                        & -r \\
         0               &              \cdots           &        0                 & 0                 &-r & 1+2r                         \\
\end{pmatrix}
´´´

```{math}
B = 
\begin{pmatrix}
  1-2r                        & r   & 0                             &         0                & \cdots & 0\\
  r & 1-2r                         & r       &         0                & \cdots & 0\\
                          0 & r & 1-2r                              & r & \cdots & 0\\
            \vdots       &          \vdots        &   \vdots                     & \ddots               & \vdots  & \vdots\\
            0               &              \cdots           &            0             & r & 1-2r                         & r \\
         0               &              \cdots           &        0                 & 0                 &r & 1-2r                         \\
\end{pmatrix}
```

In the case $A$ and $B$ are tridiagonal, as above, the solution of the linear system {eq}`eq:schemeAB` is expedite. In other cases, iterative methods must be used.

## Consistency, stability and convergence

The scheme has a truncation error $O(\Delta t^2,\Delta x^2)$, since the spatial derivatives are approximated by a centred formula and the time derivative also, at $t^{n+1/2}$.
The stability of the scheme can be determined by the usual method of assuming a solution of the form $B^n e^{ikm\Delta x}$ and noting that

```{math}
    u_{m+1}^{n}+u_{m-1}^{n} = (2\cos k\Delta x)u_{m}^{n}
```

and 

```{math}
2\sin^2(\frac{k\Delta x}{2})=1-\cos(k\Delta x),
```

we arrive at the following amplification factor:

```{math}
:label: eq:ampFactorCN
   G = \frac{u_{m}^{n+1}}{u_{m}^{n}} =\frac{B^{n+1}}{B^n}= \frac{1-2C\sin^2 (\frac{k\Delta x}{2})}{1+2C\sin^2(\frac{k \Delta x}{2})},
```

whose norm $|G|$ is

```{math}
 |G| = \left| \frac{1-2C\sin^2 (\frac{k\Delta x}{2})}{1+2C\sin^2(\frac{k \Delta x}{2})}\right| = 
    \frac{ \left|1-2C\sin^2 (\frac{k\Delta x}{2})\right|}{ \left|1+2C\sin^2(\frac{k \Delta x}{2})\right|} = 1.
```

The scheme is, therefore, *unconditionally stable* and doesn't suffer from CFL limitations, unlike the previous explicit schemes.

