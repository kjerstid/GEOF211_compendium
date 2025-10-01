(Useful_calculus:Formal_def_derivative)=
# The Formal definition of the derivative

Let us consider a function $u(t)$ that depends continuously on $t$. 

```{figure} ./Differentiate.png
---
name: fig:Differentiate
width: 75%
align: center
---
A continuous function $u(t)$. Two points $t$ and $t+\Delta t$ are indicated alont the horizontal axis, and their functional values are indicated on the vertical axis. The slope between the two points is an approximation for the derivative at the point $t$.
```

The slope between the two point $t$ and $t+\Delta t$ is an approximation of the derivative of $u(t)$ in the point $t$. The distance between $t$ and $\Delta t$ determines how good the approximation is. If we reducing the time step $\Delta t$, i.e., shift the rightmost point closer to the point $t$,  we get an improved approximation for the derivatice. The exact derivative, is found by letting $\Delta t$ approah zero:

```{math}
:label: eq:exactDerivative
\frac{du}{dt} = \lim_{\Delta t \to 0} \frac{u(t+\Delta t)-u(t)}{\Delta t}.
```