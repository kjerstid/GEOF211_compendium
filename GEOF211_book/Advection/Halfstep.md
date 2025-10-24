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
(LinearAdvectionEquation:schemeHalfstep)=
# Half-step schemes 

When we derived the McCormarck scheme in {numref}`LinearAdvectionEquation:schemeMacCormack`, we referred to the scheme as a *predictor-corrector scheme*. However, we also ended up using half time steps ($t^{n+1/2}$) to get to the final numerical solution. Schemes that incorporate half-steps in time or space, may also be referred to as *half-step* schemes. The Lax-Wendroff scheme is an interesting example to look into. We can derive the scheme in multiple ways, and one of them uses half-steps in both time and space. This two-step approach, is also referred to as the Richtmayer scheme. Below, you will see how this derivation looks like for the linear advection equation. However, the method can be extended also to other non-linear hyperbolic partial differential equations.

## The Lax-Wendroff 2-step scheme

When deriving the Lax-Wendroff scheme using the 2-step approach, we compute $u_k^{n+1}$ using not the time derivative at $t=n\Delta t$, but that at the *half-step*, $t=n\Delta t + \Delta t/2=(n+1/2)\Delta t$, using a forward in time approach. 

```{math}
	u_m^{n+1}=u_m^n+\frac{\Delta t}{2}\left(-a\frac{\partial u}{\partial x}\mid_{m,n+1/2}\right)
```

To obtain the spatial derivative at the half-time step, we must have the function values at $t^{n+1/2}$, which we derive in the same way

```{math}
	u_m^{n+1/2}=u_m^n+\frac{\Delta t}{2}\left(-a\frac{\partial u}{\partial x}\mid_{m,n}\right).
```

The Lax-Wendroff method thus involves two steps:

 **Step 1: Calculting $u$ at the half-steps in time and space** 
 
 First, compute $\frac{\partial u}{\partial x}\mid_{m,n+1/2}$ using central differences, that involve the *mid-points* $m+1/2$ and $m-1/2$:

```{math}
:label: eq:LW_Step1
\begin{aligned}
	u_{m-1/2}^{n+1/2}&=\frac{1}{2}(u_m^n+u_{m-1}^n)-a\frac{\Delta t}{2\Delta x}(u_m^n-u_{m-1}^n)\\
	u_{m+1/2}^{n+1/2}&=\frac{1}{2}(u_{m+1}^n+u_{m}^n)-a\frac{\Delta t}{2\Delta x}(u_{m+1}^n-u_{m}^n)
\end{aligned}
```
 **Step 2: Calculate $u_m^{n+1}$ using the half-step solutions from step 1** 
 
 Compute $u_m^{n+1}$ using the spatial derivative at $n+1/2$:

```{math}
:label: eq:LW_Step2
	u_{m}^{n+1}=u_m^n-a\frac{\Delta t}{2\Delta x}(u_{m+1/2}^{n+1/2}-u_{m-1/2}^{n+1/2})
```
For the linear advection equation, it is possible to merge step 1 and step 2, by inserting the expressions for $u_{m-1/2}^{n\pm 1/2}$ from {eq}`eq:LW_Step1` into step 2 ({eq}`eq:LW_Step2`). After some massaging of the expression, you will end up with the same Lax-Wendroff scheme as we find in other derivations:

```{math}
:label: eq:LW_2step_merged
	u_{m}^{n+1}=\frac{C}{2}(1+C)u_{m-1}^n+(1-C^2)u_m^n-\frac{C}{2}u_{m+1}^n
```

### Application: propagation of top hat function using the Lax-Wendroww 2-step approach

We apply the Lax-Wendroff scheme to the top hat initial condition.

```{code-cell} ipython3
:tags: ["hide-cell"]

def topHat(x):
   f0=np.zeros(x.shape)
   f0[(x>0.45) & (x<0.55)]=1

   return f0
```

The Lax-Wendroff scheme is implemented in the following Python function:

```{code-cell} ipython3
:tags: ["hide-cell"]

def LaxWendroff(u0,a,dt,dx,N,M):
    
    # Initial condition
    u=u0.copy()
    
    # Initialize arrays for step 1 solution
    um2=np.zeros((M-1,))
    up2=np.zeros((M-1,))

    # CFL number
    C = a*dt/dx
    
    for l in range(N):
        
        # Western B.C. no change in time
        u[0]  = u[0]

        # Step 1: compute u at mid-points k +/- 1/2 and half-step n+1/2
        
        um2=0.5*(u[1:-1]+u[0:-2])-C/2*(u[1:-1]-u[0:-2])
        up2=0.5*(u[2:]+u[1:-1])-C/2*(u[2:]-u[1:-1])
        
        # Step 2
        u[1 : M-1] = u[1 : M-1] - C*(up2-um2)
        
        # eastern B.C. no change in time
        u[M-1]  = u[M-1]
    
    return u
```

In the next code snippet, we set the discretization parameters and integrate the initial condition with the Lax-Wendroff scheme:

```{code-cell} ipython3
:tags: ["hide-input"]

import numpy as np
import matplotlib.pyplot as plt

N     = 30       # Number of time steps
M     = 100      # Number of grid points
a     = 0.75     # Propagation speed

dt = 0.01
dx = 1/M

print("Number of time steps = {:d}".format(N))
print("Number of grid points = {:d}".format(M))
print("Time step = {:f}".format(dt))
print("Grid size = {:f}".format(dx))
print("CFL number = {:f}".format(a*dt/dx))

# Grid points
X=np.linspace(0,1,M)

# Integrate the initial condition N time steps
U=LaxWendroff(topHat(X),a,dt,dx,N,M)

```

The solution at the end of the integration is shown below:

```{code-cell} ipython3
:tags: ["hide-input"]

# Shift the exact solution a distance equivalent to a*N*dt
newX = np.mod(X-a*N*dt,1)

fig, ax0 = plt.subplots()

ax0.plot(X, U, lw = 2, color = "b",  label='Lax-Wendroff')
ax0.plot(X, topHat(newX), lw = 1, color = "m",  label='Exact')

ax0.set_title("Lax-Wendroff Solution at t={:5.2f}".format(N*dt))
ax0.set_xlabel('$x$')
ax0.set_xlim([0, 1])
ax0.set_ylabel('$u$')
ax0.legend()

plt.show()

```
The Lex-Wendroff scheme avoids the excessive numerical diffusion of the Upwind scheme, but oscillations are still visible at the sharp transitions of the top hat function. These oscillations are known as the Gibbs phenomenon.
