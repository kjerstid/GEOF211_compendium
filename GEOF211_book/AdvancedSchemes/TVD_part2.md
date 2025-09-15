(AdvancedSchemes:TVD2)=
# Total Variation Diminishing (TVD) schemes (part 2)
We know that FTBS has severe dnumerical diffusion, and that Lax-Wendroff can give solutions where oscillations grow near strong gradients. Making a flux limiter that just switch between these two schemes is not necessarily sufficient to provide a good numerical model for the advection equation.

To improve our numerical scheme even further, we can try to ensure that the scheme does not introdue oscillations. Chapter {ref}`sec:TVD1` introduced the concept of Total Variation and Total Variation Diminishing (TVD) schemes. We will expand on this concept here, to design improved numerical schemes for advection based on the Godunov approach with flux limiters. This boils down to finding clever values of $\phi(\theta)$.

We will make a short recap of TVD part 1 from chapter {ref}`sec:TVD1`. The total variation is a measure of the amount of oscillation in the field:

(definition:Total Variation)=
:::{admonition} Definition
:class: important
```{math}
:label: eq:TotalVariation
TV(q^n)=\sum_{m=2}^J|(q_m^n-q_{m-1}^n)|
```
:::

A numerical scheme is Total Variation Diminishing if:

(definition:Total Variation Diminishing schemes)=
:::{admonition} Definition
:class: important
A numerical scheme is total variation diminishing if:
```{math}
:label: eq:TotalVariation_b
TV(q^{n+1})\leq TV(q^n)
```
:::

So - how can we ensure that the Godunov scheme on flux form is TVD? 

Do you remember the Harten theorem fro Equation {eq}`eq:Harten`?

Consider a general method of the form:

```{math}
q_k^{n+1}=q_k^n-A_{k-1}^n(q_k^n-q_{k-1}^n)+B_k^n(q_{k+1}^n-q_k^n)
```

where the coefficients $A$ and $B$ are arbitrary values that may depend on $q$. (Note that
these coefficients are displaced half a grid length to the right, so that, e.g., $B_k^n$ is valid at $j+\frac{1}{2}$.) Then it has been shown {cite:p}`Harten1983` that 

(theorem:HartenTheorem)=
:::{admonition} Harten's Theorem
:class: important
Consider a method on the general form (Equation {eq}`eq:HartenGeneral`). Then
```{math}
TV(q^{n+1})\leq TV(q^n)
```
if $A_k^n+B_k^n\leq 1$ and $A_k^n\geq 0$, $B_k^n \geq 0\,\, \forall\,k$
:::

We can now verify that the Godunov scheme with flux limiters for linear advection is TVD. To do so, requires a nit of math. We must first find an expression for the scheme on the general for (Equation {eq}`eq:HartenGeneral`), and then find restrictions for $A$ and $B$.

**Step 1: Inserting the fluxes into the equation fo $q_k^{n+1}$ from Equation {eq}`eq:Godunov_fluxform_downwind_massaged` to find the General form**

```{math}
\begin{aligned}
q_k^{n+1}& =q_k^n+\frac{\Delta t}{\Delta x}\left[ {\color{salmon}{aq_{k-1}^n}+\frac{a}{2}(1-C)}{\color{teal}{(q_k^n-q_{k-1}^n)\phi(\theta_{k-1/2}^n)}}- {\color{salmon}{aq_k^n}}+\frac{a}{2}(1-C){\color{ForestGreen}{(q_{k+1}^n-q_k^n)\phi(\theta_{k+1/2}^n)}}  \right]\\
& =q_k^n- {\color{salmon}{C(q_{k-1}^n-q_{k-1}^n)}} -\frac{C}{2}(1-C)\left[ {\color{ForestGreen}{\phi(\theta_{k+1/2}^n)(q_{k+1}^n-q_k^n)}} - {\color{teal}{\phi(\theta_{k-1/2}^n)(q_k^n-q_{k-1}^n)}} \right]
\end{aligned}
```

This is not yet on the general form. To get there, we must factorize the scheme in terms of ${\color{violet}{(q_k^n-q_{k-1}^n)}}$. This is not straighforward to guess (it is indeed tempting to leave the term with $(q_{k+1}^n-q_k^n)$ separately), but we will see how it works out:

```{math}
:label: eq:Godunov_pregeneral
q_k^{n+1}=q_k^n-C {\color{violet}{(s_{k-1}^n-q_{k-1}^n)}} -\frac{C}{2}(1-C)\left[ \phi(\theta_{k+1/2}^n)\frac{(q_{k+1}^n-q_k^n)}{{\color{violet}{(q_{k-1}^n-q_{k-1}^n)}}} - \phi(\theta_{k-1/2}^n){\color{violet}{(q_k^n-q_{k-1}^n)}} \right]
```

Noting that the term $\frac{(q_{k+1}^n-q_k^n)}{{\color{violet}{(q_{k-1}^n-q_{k-1}^n)}}}$ is the same as ${1}/{\theta_{k+1/2}^n}$, we can replace this in equation {eq}`eq:Godunov_pregeneral`, and complete the factorizing of ${\color{violet}{(q_k^n-q_{k-1}^n)}}$ to get the scheme on the general form:

(definition:Total Variation)=
:::{admonition} Godunov on the general form
:class: important
```{math}
\begin{aligned}
q_k^{n+1} & =q_k^n - A_{k-1/2}{\color{violet}{(q_k^n-q_{k-1}^n)}}   \\
A_{k-1/2} & =\left(C+\frac{C}{2}(1-C)\left[ \frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n}-\phi(\theta_{k-1/2}^n) \right]\right)\\
B_{k+1/2} & =0
\end{aligned}
```
:::

We can now check what conditions yield $A\ge0$ and $A+B\le1\,\,\rightarrow\,\,0\le A \le 1$. The calculations are not straightforward, since the expression for $A$ is more coplicated than for, e.g., the FTBS scheme we looked at before. It is usefulto start by summarizing some properties of $\theta_{k+1/2}^n$:
* If q varies linearly, then $\theta_{k+1/2}^1$ (the same slope between neighboring grid points)
* If there is a local extrema $\theta_{k+1/2}^n\le$ (opposite signs of the slope at either side of a grid point $k$)
* To avoid problems at a local extrema, we can require $\theta$ to be zero in these extrema. This means that we require  $\phi(\theta_{k+1/2}^n\le)<0$ whenever $\theta_{k+1/2}^n<0$

We can first insert  $\phi(\theta_{k+1/2}^n\le)=0$ to find one criteria for $A$. Then we can insert  $\phi(\theta_{k-1/2}^n\le)=0$ to find a second criteria for $A$. Both of these criteria must hold to ensure a TVD scheme. Since we have $B=0$, we must have $0\le A\le B$:

If $\phi(\theta_{k+1/2}^n\le)=0$, we have:

```{math}
:label: eq:A_right
\begin{aligned}
0 & \le C-\frac{C}{2}(1-C)\phi(\theta_{k-1/2}^n) && \le 1 & \: & ,\text{subtract } C\\
-C & \le -\frac{C}{2}(1-C)\phi(\theta_{k-1/2}^n) && \le 1-C & \: &,\text{mulitply by } \frac{2}{C(1-C)}\\
-C(\frac{2}{C(1-C)}) & \le -\phi(\theta_{k-1/2}^n) && \le (1-C)\frac{2}{C(1-C)} & \: &,\text{cancel terms } \\
-\frac{2}{(1-C)} & \le -\phi(\theta_{k-1/2}^n)  && \le \frac{2}{C} & \: &,\text{mulitply by }-1 \text{ and swap sides, ensuring correct signs} \\
-\frac{2}{C} & \le \phi(\theta_{k-1/2}^n) && \le \frac{2}{(1-C)} & \: &
\end{aligned}
```



Similarly, if $\phi(\theta_{k-1/2}^n\le)=0$, we have:
```{math}
:label: eq:A_left
\begin{aligned}
0 & \le C-\frac{C}{2}(1-C)\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} && \le 1\\
-C & \le \frac{C}{2}(1-C)\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} && \le 1-C\\
-C(\frac{2}{C(1-C)}) & \le \frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} && \le (1-C)\frac{2}{C(1-C)}\\
-\frac{2}{(1-C)} & \le \frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} && \le \frac{2}{C}\\
\end{aligned}
```

We must have $0\le A \le 1$ for all grid cells to ensure TVD. The left hand side inequalities of Equations {eq}`eq:A_right` and {eq}`eq:A_left` are not problematic, since these only give lower bounds that are easy to fulfill. Instead, we much pay attention to the right hand sides of the inequalitites, which give the upper bound and the strictest constraints for $\phi(\theta_{k-1/2}^n)$.

From Equation {eq}`eq:A_right`, we must have: $\phi(\theta_{k-1/2}^n) \le \frac{2}{(1-C)}$ and from Equation {eq}`eq:A_left`, we must have $\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} \le \frac{2}{C}$. From here, let us consider a classical CFL constraint where $C<1$. The two expressions take on their smallest (strictest) values when $\phi(\theta_{k-1/2}^n) \le 2$ (for $C=0$) and $\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} \le 2$ for $C=1$. To ensure TVD, we must, therefore, require that $\phi(\theta_{k-1/2}^n)\le2$ and also $\phi(\theta_{k-1/2}^n)\le2\theta$. We can express this double requirement as a minmod:

(definition:TVD criteria)=
:::{admonition} The Godunov scheme is TVD if:
:class: important
```{math}
:label: eq:TVD_crit
\phi(\theta) 
\begin{cases} 
\leq \text{minmod}(2,2\theta) & \forall \theta \ge 0\\
=0 & \forall \theta \le 0
\end{cases} 
```
:::

```{figure} ./TVD2.png
---
:name: `fig:TVD_theta_phi_TVDcrit`
:width: 40%
:align: center
---
$\theta$-$\phi$ space for visualizing flux limieters. Two simple flux limiters,$\phi\equiv0$ (blue) and $\phi\equiv1$ (red) are sketched. These corresond with the FTBS and the Lax-Wendroff scheme. The hatched area shows the area where the TVD criteria from Equation {eq}`eq:TVD_crit` holds.  
```

Figure {ref}`fig:TVD_theta_phi_TVDcrit` shows the $\theta$-$\phi$ space, where the area that ensures TVD is hatched. The area is bounded by the lines $\phi(\theta)= 2$ and $\phi(\theta)= 2\theta$.  

We can now better understand where the oscillations in the Lax-Wendroff scheme comes from. As long as the slope $\theta \ge\frac{1}{2}$, the scheme is inside the TVD regime. However, for negative or small values of $\theta$ ($\theta\le \frac{1}{2}$), the red line, representing Lax Wendroff, is outside the hatched area that ensures TVD. It is for these small $\theta$ that the oscillations start to grow.