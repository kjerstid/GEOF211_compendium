(LinearAdvectionEquation:schemePredCorr)=
# Predictor-corrector schemes 

To improve the stability of numerical schemes it is possible is to incorporate a scheme with more than one step of calculations. The predictor-corrector schemes typically uses two steps, a predictor-step, where we predict a solution, and a corrector-step where we refine the final solution/estimate. These schemes also typically includes ""fictional time steps in between the regular time steps, such as a solution at time step $n+1/2$. The method, therefore, also fit into the category of half-step schemes described in {numref}`LinearAdvectionEquation:schemeHalfstep`.

The McCormack scheme for linear advection is a good example of how this works.

(LinearAdvectionEquation:schemeMacCormack)=
## The MacCormack Scheme

The MacCormack scheme is composed of a *predictor* step and a *corrector* step. It is one of the simplest of the *predictor-corrector* class of numerical schemes. 

**Step 1: The Predictor step**
The predictor step is used to obtain an estimate $\tilde{u}$ of the unknown function $u$ at timstep $t^{n+1}$. Here, we use the FTFS scheme (Forward in time, forward in space):

```{math}
   \tilde{u}_m^{n+1}=u_m^n - a\frac{\Delta t}{\Delta x}\left( u_{m+1}^n - u_m^n \right)
```

We will also need the same FTFS step for the grid point to the left of $u_m^{n+1}$, which is $\tilde{u}_{m-1}^{n+1}$:

```{math}
   \tilde{u}_{m-1}^{n+1}=u_{m-1}^n - a\frac{\Delta t}{\Delta x}\left( u_{m}^n - u_{m-1}^n \right).
```

Note the use of a **forward** formula to approximate the spatial derivative. 

**Step 2: the corrector step**

The corrector step uses a FTBS (forward in time and backward in space) scheme with a half-step in time from $u_m^{n+1/2}$ to $u_m^{n+1}$ and the estimates $ \tilde{u}_m^{n+1}$ and $ \tilde{u}_{m-1}^{n+1}$ to approximate the **backward** spatial derivative :

```{math}
   u_m^{n+1}=u_m^{n+\frac{1}{2}} - a\frac{\Delta t}{2\Delta x}\left( \tilde{u}_{m}^{n+1} - \tilde{u}_{m-1}^{n+1} \right)
```

To obtain the solution at the half-step in time, $t^{n+\frac{1}{2}}$, we simply average the function at $t^n$ and the estimate at $t^{n+1}$: 

```{math}
   u_m^{n+\frac{1}{2}} = \frac{u_m^{n} + \tilde{u}_m^{n+1}}{2}
```

The final scheme is:

```{math}
u_m^{n+1} = \frac{u_m^{n} + \tilde{u}_m^{n+1}}{2} - a\frac{\Delta t}{2\Delta x}\left( \tilde{u}_{m}^{n+1} - \tilde{u}_{m-1}^{n+1} \right)
```

For the linear advection equation, you can insert the expressions for $\tilde{u}_m^{n+1}$, $\tilde{u}_k^{n}$ and $\tilde{u}_{m-1}^{n}$ into the final scheme to get a 1-step solution, which gives the same result as the Lax-Wendroff approach:

```{math}
u_m^{n+1}=u_m^n-\frac{C}{2}(u_{m+1}^n-u_{m-1}^n)+\frac{C^2}{2}(u_{m+1}^n-2u_m^n+u_{m-1}^n),
```

where $C=\frac{a\Delta t}{\Delta x}$ is the Courant number.

For the linear advection equation, the MacCormack scheme is equivalent to the Lax-Wendroff scheme, so its properties are the same as those of the latter. 






