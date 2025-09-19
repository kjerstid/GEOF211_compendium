(finite-differences:formulas-2stderivative)=
# Finite difference formulas for the 2nd derivative

One way of establishing schemses for the 2nd derivative, such as the term $\frac{\partial^2 u}{\partial x^2}$ in the Diffusion equation {eq}`eq:Diffusion`, is to manipulate Taylor series in varous ways. This method for finding the schemes, also provides us with the error terms that indicate the scheme order. We typically start with Taylor series for $u^{n+1}$ and $u^{n-1}$, but you can invoke $u$ at other time steps (or space steps). 

We start from the Taylor expansion in Equation {eq}`eq:taylorSeries_v1`, repeated here with Leibnitz difference notation: 

```{math}
u(t)=u^n+\frac{(t-t^n)}{1!}\frac{\partial u}{\partial t}+\frac{(t-t^n)^2}{2!}\frac{\partial^2 u}{\partial t^2}+\sum_{p=3}^{\infty}\frac{(t-t^n)^p}{p!}\frac{\partial^p u}{\partial t^p}
```

We now insert $t=n+1$ to achieve the Taylor expansion for $u^{n+1}$ and insert $t=n-1$ to get the expansion for $u^{n-1}$. 

```{math}
:label: eq:Taylor_n_pm1
\begin{aligned}
u^{n+1} & =u^n+\Delta t\frac{\partial u}{\partial t}|_{t^n}+\frac{\Delta t^2}{2!}\frac{\partial^2 u}{\partial t^2}|_{t^n}+\frac{\Delta t^2}{3!}\frac{\partial^3 u}{\partial t^3}|_{t^n}+\frac{\Delta t^4}{4!}\frac{\partial^4 u}{\partial t^4}|_{t^n} & +h.o.t\\
u^{n-1} & =u^n+\Delta t\frac{\partial u}{\partial t}|_{t^n}-\frac{\Delta t^2}{2!}\frac{\partial^2 u}{\partial t^2}|_{t^n}+\frac{\Delta t^2}{3!}\frac{\partial^3 u}{\partial t^3}|_{t^n}-\frac{\Delta t^4}{4!}\frac{\partial^4 u}{\partial t^4}|_{t^n} & +h.o.t
\end{aligned}
```

It is also possible to invoke more values of $u$ at earlier or later time step.


(finite-differences:formulas-2ndderivative)=
## Centered formula

If you compare the two expressions in Equation {eq}`eq:tTaylor_n_pm1`, you may. notice that all the terms are the same. The only thing that separates the two expressions, are the signs in front of every second term. We are interested in finding a scheme for the second order derivative, which we find in the third term on the right hand side. We would also like to get rid of the term with the first derivative (second term on the right hand side). The trick now is to add these two equations together. Then we cancel out the first derivative terms, and keep the second derivative. We can collect the remaining terms on either side of the equals sign.

```{math}
:label: eq:Taylor_n_pm1_b
u^{n+1}+u^{n-1}=2u^n+2\frac{\Delta t^2}{2!}\frac{\partial^2 u}{\partial t^2}|_{t^n}+2\frac{\Delta t^4}{4!}\frac{\partial^4 u}{\partial t^4}|_{t^n}+h.o.t
```

Solving Equation {eq}`eq:tTaylor_n_pm1_b` for the second derivative, we get:

(definition:Centered2derivative)=
:::{admonition} Centered scheme for the 2nd derivative:
:class: definition

```{math} 
:label: eq:Centered2derivative
\frac{\partial^2 u}{\partial t^2}|_{t^n}=\frac{u^{n+1}-2u^n+u^{n-1}}{\Delta t^2} + \frac{\Delta t^4}{12}\frac{\partial^4 u}{\partial t^4} + h.o.t
```
:::

This is a second order three-point centered formula for the second derivative.

## Forward formula

You can obtain a forward formula using the same procedure as for the centered formula. To do so, we must start with the Taylor expansions for $u^{n+1}$ and $u^{n+2}$:

```{margin} 
```{note}
The factors 2, 4, 8, 16, comes from the term $(t^{n+2}-t^n)$ which equals $2\Delta t$.
```
```

```{math}
:label: eq:Taylor_n_p12
\begin{aligned}
u^{n+1} & =u^n+\Delta t\frac{\partial u}{\partial t}|_{t^n}+\frac{\Delta t^2}{2!}\frac{\partial^2 u}{\partial t^2}|_{t^n}+\frac{\Delta t^2}{3!}\frac{\partial^3 u}{\partial t^3}|_{t^n}+\frac{\Delta t^4}{4!}\frac{\partial^4 u}{\partial t^4}|_{t^n} & +h.o.t\\
u^{n+2}&=u^n+2\Delta t\frac{\partial u}{\partial t}|_{t^n}+4\frac{\Delta t^2}{2!}\frac{\partial^2 u}{\partial t^2}|_{t^n}+8\frac{\Delta t^2}{3!}\frac{\partial^3 u}{\partial t^3}|_{t^n}+16\frac{\Delta t^4}{4!}\frac{\partial^4 u}{\partial t^4}|_{t^n} & +h.o.t
\end{aligned}
```

To end up with an expression that cancels out the first derivatives, we can take the expression for $u^{n+2}$ and subract 2 times the expression for $u^{n+1}$. Solving for the second derivative, we obtain:

(definition:Forward2derivative)=
:::{admonition} Forward scheme for the 2nd derivative:
:class: definition

```{math} 
:label: eq:Forward2derivative
\frac{\partial^2 u}{\partial t^2}|_{t^n}=\frac{u^{n+2}-2u^{n+1}+u^{n}}{\Delta t^2} -\Delta t\frac{\partial^3 u}{\partial t^3}- \frac{14\Delta t^4}{24}\frac{\partial^4 u}{\partial t^4} + h.o.t
```

This is a forst order three-point forward formula for the second derivative. It is less used than the centered formula, since the error is typically higher for a first order formula.
:::

