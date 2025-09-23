(linearadvection:Introduction)=
# The advection equation

*Advection* is a process where a parameter like, e.g., salt, temperature, moisture, momentum, oxygen... is transported by the velocity field in a given direction. 

## Non-linear advection

From the Navier Stokes equation {eq}`eq:NavierStokes` we can look at a simplified case for advection of momentum, where changes in the local time derivative $\frac{\partial u}{\partial t}$ is only depending on the velocity field.

```{math}
:label: eq:NonLinAdvection_u_3d
\frac{\partial u}{\partial t}+u(t,x,y,z)\frac{\partial u}{\partial x}+v(t,x,y,z)\frac{\partial u}{\partial y}+w(t,x,y,z)\frac{\partial u}{\partial z}=0
```

If we disregard motion in the y, and z-direction ($v=0$ and $w=0$), we obtain the one-dimensional non-linear advection equation for momentum:

```{math}
:label: eq:NonLinAdvection_u_1d
\frac{\partial u}{\partial t}+u(t,x)\frac{\partial u}{\partial x}=0
```

For other parameters, like, e.g., temperature ($\theta$) the non-linear advection equation is written:

```{math}
:label: eq:NonLinAdvection_t_1d
\frac{\partial \theta}{\partial t}+u(t,x)\frac{\partial \theta}{\partial x}=0
```

The first term of {eq}`eq:NonLinAdvection_t_1d` is the local change with time. If we consider, e.g. temperature, we can use an example of changing the temperature in a room. If you turn on a heater, the temperature will rise, but the air inside the room stays the same. The heater is a heat source and represent a local change in temperature with time. If you instead open the window, air will flow through the window and change the temperature by replacing some of the air (as air flow in through the window, air will also leave the room through the window). This is the temperature change following advection (second term of {eq}`eq:NonLinAdvection_t_1d`) .

## Linear advection

To obtain the *linear advection equation*, you can simply replace the velocity $u(t)$, with a constant velocity $a$. The linear, 1D equation for temperature, $\theta$ then becomes:

```{math}
:label: eq:LinAdvection_theta_1d
\frac{\partial \theta}{\partial t}+a\frac{\partial \theta}{\partial x}=0
```

This is a first order partial differential equation that represents, in a simple form, the process of advection in the atmosphere and ocean. Linear advection of momentum $u$, can similarly be expressed 

```{math}
:label: eq:Advection
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} = 0, a>0
```

Here we have an expression that models the transport of a signal $u(x,t)$ in 1-d space with velocity $a$. The velocity $a$ may also be interpreted as a phase speed of a wave that propagates in the positive $x$-direction. 

The simplicity of Equation {eq}`eq:Advection` and its closeness to the Navier-Stokes equation that govern fluid flow make it an attractive model for studying the solution of partial differential equations with numerical methods. The analytical solution to {eq}`eq:Advection` is known, so we can solve the associated numerical difference equations and compar the analytic and numerical solutions directly.
 
```{tableofcontents}
```
