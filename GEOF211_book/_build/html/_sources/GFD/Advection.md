(GFD:Advection)=
# Advection equation

*Advection* is a process where a parameter like, e.g., salt, temperature, moisture, momentum, oxygen... is transported by the velocity field in a given direction. 

From the Navier Stokes equation {eq}`eq:NavierStokes` we can look at a simplified case for advection of momentum, where changes in the local time derivative $\frac{\partial u}{\partial t} is only depending on the velocity field.

$$
\frac{\partial u}{\partial t}+u(t,x,y,z)\frac{\partial u}{\partial x}+v(t,x,y,z)\frac{\partial u}{\partial y}+w(t,x,y,z)\frac{\partial u}{\partial z}=0
$$ (eq:NonLinAdvection_u_3d)

If we disregard motion in the y, and z-direction ($v=0$ and $w=0$), we obtain the one-dimensional non-linear advection equation for momentum:

$$
\frac{\partial u}{\partial t}+u(t,x)\frac{\partial u}{\partial x}=0
$$ (eq:NonLinAdvection_u_1d)

For other parameters, like, e.g., temperature ($\theta$) the non-linear advection equation is written:

$$
\frac{\partial \theta}{\partial t}+u(t,x)\frac{\partial \theta}{\partial x}=0
$$ (eq:NonLinAdvection_t_1d)

The first term of {eq}`eq:NonLinAdvection_t_1d` is the local change with time. If we consider, e.g. temperature, we can use an example of changing the temperature in a room. If you turn on a heater, the temperature will rise, but the air inside the room stays the same. The heater is a heat source and represent a local change in temperature with time. If you instead open the window, air will flow through the window and change the temperature by replacing some of the air (as air flow in through the window, air will also leave the room through the window). This is the temperature change following advection (second term of {eq}`eq:NonLinAdvection_t_1d`) .

To obtain the *linear advection equation*, you can simply replace the velocity $u(t)$, with a constant velocity $a$. The linear, 1D equation for temperature, $\theta$ then becomes:

$$
\frac{\partial \theta}{\partial t}+a\frac{\partial \theta}{\partial x}=0
$$ (eq:LinAdvection_theta_1d)



