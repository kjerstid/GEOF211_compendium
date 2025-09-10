(AdvancedSchemes:Introduction)=
# Advanced schemes and approaches

All schemes have pros and cons. If we, for example, look into the linear advection equation {eq}`eq:Advection`, repeated here,

```{math}
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} = 0, a>0,
```

we have found:

* FTCS provides stable solutions as long as we do not violate the CFL condition and $a>0$. There is much numerical diffusivity in this scheme, and a given signal will die out when we run the model over a long time period
* CTCS is unstable!
* Lax-Friedrich, which is a modified version of FTCS, is stable. This scheme is valid for all values ov $a$, but has strong numerical diffusion (even more than the FTCS)
* Lax-Wendroff is stable, but we get oscillations in regions of strong gradients.

There are many approaches to design more advanced schemes than those mentioned above. In this chapter, we will look into some of them.