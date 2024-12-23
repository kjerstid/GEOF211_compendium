(LinearAdvectionEquation:analyticSolution)=
# The exact equation

```{margin} Euler's formula:
$$
e^{i\theta}=\cos \theta + i\sin \theta
$$

is widely used to represent simple oscillatory behaviour. 
```
The linear advection equation (eq. {eq}`eq:Advection`) is given by:

$$
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} = 0, c>0
$$

We will assume an initial condition in the form of a simple wave:

$$
	u(x,0)=A e^{i k x},
$$ (eq:initialCond)

where $k = 2\pi/\lambda$ is the wave number ($\lambda$ is the wavelength). 

We can find the analytic (exact) solution of {eq}`eq:Advection` using the method *separation of variables*.
Let the solution to {eq}`eq:Advection` with initial condition {eq}`eq:initialCond` be given by:

$$
u(x,t)=G(t)H(x)
$$ (eq:sepVar)

We substitute $u(x,t)=G(t)H(x)$ in {eq}`eq:Advection`, and separate the x- and t-dependent terms on wither side of the equal sign:

\begin{align} 
   \frac{\partial }{\partial t} (G(t)H(x))=& -c \frac{\partial }{\partial x} (G(t)H(x)) \\
   H(x)\frac{\partial G(t)}{\partial t} =& -c G(t) \frac{\partial H(x)}{\partial x} \\
   \frac{1}{G(t)} \frac{\partial G(t)}{\partial t} =& -c \frac{1}{H(x)} \frac{\partial H(x)}{\partial x}, 
\end{align}

The equal sign can only hold for all $(x,t)$ if both side are equal to a constant value, $-\alpha$. We can now integrate each side of the equation, yielding

\begin{align} 
      \frac{1}{G(t)} \frac{\partial G(t)}{\partial t} =& -\alpha \Leftrightarrow G(t)=A_1e^{-\alpha t} \\
      -c \frac{1}{H(x)} \frac{\partial H(x)}{\partial x}=& -\alpha \Leftrightarrow H(x)=A_2e^{\alpha x/c},
\end{align}

We can now subsitute the expressions for $G(t)$ and $H(x)$ into {eq}`eq:sepVar` and find $u(x,t)=G(t)H(x)=A_1A_2e^{-\alpha t}e^{\alpha x/c}$. 

Using the initial conditions {eq}`eq:Advection` at $t=0$ we have $u(x,0)=A_1A_2e^{\alpha x/c}$, so we know that $A=A_1A_2$ and $ik = \alpha/c$ and so $\alpha=ikc$. Finally, we can write:

$$
	u(x,t)=Ae^{-ikct}e^{ikcx/c}=Ae^{ik(x-ct)},
$$ (eq:anaSolution)

which is the solution of {eq}`eq:Advection` given the initial condition {eq}`eq:initialCond`. This solution represents the initial condition moving along the positive $x$-direction with translation velocity $c$.
