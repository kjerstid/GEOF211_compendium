(Implicit:Introduction)=
# Implicit schemes vs explicit schemes

The Finite Difference schemes we have looked at so far, have all been possible to solve explicitly, This means that we inserted our schemes into the derivatives of the equation we studied and solved for $u_m^{n+1}$. The FTCS scheme for the linear advection equation is a good example:

```{math}
:label: eq:CTCS_lin_adv
   u_m^{n+1}=u_m^n-\frac{a\Delta t}{2\Delta x}(u_{m+1}^n+u_{m-1}^n),
```

One approach to improving the simple Finite Difference schemes, is to include both the current timestep $n$ and the next timestep $n+1$ in the schemes. A general way to do so, is to take a weighted average of the spatial difference at the current and the next timestep:

```{math}
:label: eq:NschemeGeneralImplicit
  u_m^{n+1} =-u_m^n -\frac{a\Delta t}{2\Delta x}\left(\alpha(u_{m+1}^{n+1}-u_{m-1}^{n+1}) + (1-\alpha)(u_{m+1}^{n}-u_{m-1}^{n})\right),
```

wehere $\alpha\in[0,1]$ is the weighting factor.

We shall see that this approach will have hughe benefits for , e.g., the diffusion equation. However, introducing $n+1$ timesteps into the schemes cause the resulting difference equation to contain $n+1$-terms with different grid points in the space direction. We can no longer solve the equation for $u_m^{n+1}$ explicitly, and we therefore call this an implicit scheme.
 
```{tableofcontents}
```
