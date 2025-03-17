(LinearAdvectionEquation:schemeMacCormack)=
# The MacCormack Scheme

The MacCormack scheme is another multi-step scheme. It is composed of a *predictor* step and a *corrector* step. It is one of the simplest of the *predictor-corrector* class of numerical schemes. 

The predictor step is used to obtain an estime $\tilde{u}$ of the unknown function $u$ at $t^{n+1}$:

$$
   \tilde{u}_k^{n+1}=u_k^n - a\frac{\Delta t}{\Delta x}\left( u_{k+1}^n - u_k^n \right)
$$

Note the use of a **forward** formula to approximate the spatial derivative. The corrector step uses the estimates $ \tilde{u}^{n+1}$ to approximate the spatial derivative with a **backward** formula:

$$
   u_k^{n+1}=u_k^{n+\frac{1}{2}} - a\frac{\Delta t}{2\Delta x}\left( \tilde{u}_{k}^{n+1} - \tilde{u}_{k-1}^{n+1} \right)
$$

To obtain the solution at $t^{n+\frac{1}{2}}$, we simply average the function at $t^n$ and the estimate at $t^{n+1}$: 

$$
   u_k^{n+\frac{1}{2}} = \frac{u_k^{n} + \tilde{u}_k^{n+1}}{2}
$$

The final scheme is:

$$
u_k^{n+1} = \frac{u_k^{n} + \tilde{u}_k^{n+1}}{2} - a\frac{\Delta t}{2\Delta x}\left( \tilde{u}_{k}^n - \tilde{u}_{k-1}^n \right)
$$

For the linear advection equation, you can insert the expressions for $\tilde{u}_k^{n+1}$, $\tilde{u}_k^{n}$ and $\tilde{u}_{k-1}^{n}$ into the final scheme to get a 1-step solution, which gives the same result as the Lax-Wendroff approach:

$$
u_k^{n+1}=u_k^n-\frac{C}{2}(u_{k+1}^n-u_{k-1}^n)+\frac{C^2}{2}(u_{k+1}^n-2u_k^n+u_{k-1}^n),
$$

where $C=\frac{a\Delta t}{\Delta x}$ is the Courant number.

## Consistency, stability and convergence

For the linear advection equation, the MacCormack scheme is equivalent to the Lax-Wendroff scheme, so its properties are the same as those of the latter. 

## Application: propagation of top hat function

The MacCormack scheme applied to the top hat initial condition gives the same solution as the Lax-Wendroff scheme.


