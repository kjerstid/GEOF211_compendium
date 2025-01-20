(NumericalStability:DomainDep)=
# Domain of Dependence (DoD)
The domain of dependence is a measure of which grid points the numerical solution for a given grid point $q_m^{n+1}$ depends on. If we, for example look at the FTBS scheme for the advection equation:

$$
q_m^{n+1}=q_m^n-a\frac{\Delta t}{\Delta x}(q_m^n-q_{m-1}^n)
$$

Here, the solution for $q_m^{n+1}$ depends on the terms $q_m^n$ and $q_{m-1}^n$. We can annotate these dependencies in the discrete time-space domain:

```{figure} ../Figures/Domain_Dep_FTBS.png
The Domain of Dependence (DoD), for the FTBS scheme to the linear advection equation.
```

