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
(scheme:crank-nicolson-diffusion)=
# The Crank-Nicholson Scheme for diffusion

The Crank-Nicolson scheme was originally made for diffusion. The scheme is a modification of the FTCS (Forward in time, centered in space) scheme. It uses the forward approximation to the time derivative at $t^n$ and the average of the centred approximations of the spatial second derivative at $t^n$ and $t^{n+1}$.

```{math}
:label: eq:schemeCrankNicolsonDiffusion
  \frac{u_m^{n+1}-u_m^n}{\Delta t} = -\frac{\gamma}{2\Delta x^2}\left(\frac{u_{m+1}^{n+1}-2u_{m}^{n+1}+u_{m-1}^{n+1}}{2} + \frac{u_{m+1}^{n}-2u_{m}^{n}+u_{m-1}^{n}}{2}\right) 
```

Another way of looking at {eq}`eq:schemeCrankNicolson` is that the left hand side (LHS) is a centred approximation of the time derivative at $t^{n+1/2}$ and the averaging of the spatial derivatives provides an estimate of the spatial derivative at $t^{n+1/2}$.

The use of the terms at $t^{n+1}$ poses a complication because these are not known at time $t^n$. Therefore, the scheme is not an explicit time marching scheme as we have seen so far, but one where the solution is implicit in the scheme itself, hence the designation of *implicit* scheme. To obtain the unknown values at $t^{n+1}$, a linear system of equations must be solved. 

We can expand {eq}`eq:schemeCrankNicolsonDiffusion` to obtain 

```{margin} 
$C=\gamma\frac{\Delta t}{\Delta x^2}$ <br>
$r=C/2$

```

```{math}
:label: eq:schemeCrankNicolsonDiffusion_sorted
  -ru_{m-1}^{n+1}+(1+2r)u_m^{n+1}-ru_{m+1}^{n+1}=ru_{m-1}^n+(1-2r)u_m^n+ru_{m+1}^n
```

that is a linear system of equations 

```{math}
:label: eq:schemeAB_diff
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
            0               &              \cdots           &            0             & -r{4} & 1+2r                         & -r \\
         0               &              \cdots           &        0                 & 0                 &-r & 1+2r                        \\
\end{pmatrix}
```

```{math}
B = 
\begin{pmatrix}
  1-2r                        & r   & 0                             &         0                & \cdots & 0\\
  \frac{\sigma}{4} & 1                         & -\frac{\sigma}{4}       &         0                & \cdots & 0\\
                          0 & r & 1 -2r                             & r & \cdots & 0\\
            \vdots       &          \vdots        &   \vdots                     & \ddots               & \vdots  & \vdots\\
            0               &              \cdots           &            0             & r & 1-2r                         & r \\
         0               &              \cdots           &        0                 & 0                 &r & 1-2r                         \\
\end{pmatrix}
```

In the case $A$ and $B$ are tridiagonal, as above, the solution of the linear system {eq}`eq:schemeAB_diff` is expedite. In other cases, iterative methods must be used.

## Consistency, stability and convergence

The stability of the scheme can be determined by the von Neumann stability analysis assuming a solution of the form $B^n e^{ikm\Delta x}$.


we arrive at the following amplification factor:

```{math}
:label: eq:ampFactorCN
   |G| = \left|\frac{u_{m}^{n+1}}{u_{m}^{n}}\right| = \left|\frac{1-2Csin^2(\frac{k\Delta x}{2})}{1+2Csin^2\frac{k\Delta x}{2}}\right|,
```
, since the denominator will always be larger than the numerator

The scheme is, therefore, *unconditionally stable* and doesn't suffer from CFL limitations, unlike the previous explicit schemes.