(AdvancedSchemes:FluxLimiters)=
# Flux Limiters


*This chapter is co-written with Sigrid Christine Pedersen (student in GEOF211 spring 2025)*

The minmod limiter, described in chapter {ref}`chap:minmod` is useful to avoid strong slopes for the reconstructed signal. Using flux limiters, is another approach to gain controll over the model behaviour near strong gradients. To understand the flux limiters, we must first look into how numerical schemes can be written in a flux form:

(definition:Flux form)=
:::{admonition} The flux form of the advection scheme can be written:
:class: important
```{math}
:label: eq:fluxform
q_k^{n+1}=q_k^n+\frac{\Delta t}{\Delta x}[F_{k-1/2}^n-F_{k+1/2}^n]
```
:::

The flux form means that we split up what is entering the grid cell $k$ from the left, $F_{k-1/2}^n$ (entering from grid cell $k-1$), and what is leaving the grid cell towards the right $F_{k+1/2}^n$ (leaving from grid cell $k$).

```{note}
The Advection equation on the flux form looks very similar to the simple schemes, such as the FTBS, FTBS, or FTCS. But, note that the sign in front of $\frac{\Delta t}{\Delta x}$ is positive and that the advection speed $a$ is included in the fluxes. The sign is positive, since we do the flux from the left minus the flux from the right inside the paranthesis.
```

## Godunov on Flux form

We can write the Godunov scheme on Flux form by identifying terms related to grid cell $k-1$ and grid cell $k$. If we repeat the Godunov step 2 equation with colors to help us separate the terms, we get:

```{math}
:label: eq:Godunov_color
q_k^{n+1} = {\color{Cerulean}{q_k^n}} - a {\color{Cerulean}{\frac{\Delta t}{\Delta x}}} \left( {\color{teal}{q_k^n}} - {\color{salmon}{q_{k-1}^n}} \right) - \frac{a \Delta t}{2} \left( 1 - \frac{a \Delta t}{\Delta x} \right) \left( {\color{teal}{\sigma_k^n}} - {\color{salmon}{\sigma_{k-1}^n}} \right)
```

```{math}
:label: eq:Godunov_fluxform
{\color{Cerulean}{q_k^{n+1}}}={\color{Cerulean}{q_k^n}}+\frac{\Delta t}{\Delta x}[F_{k-1/2}^n-F_{k+1/2}^n],
```
where

```{math}
:label: eq:Godunov_fluxes
\begin{aligned}
{\color{salmon}{F_{k-1/2}^n}}&=a{\color{salmon}{q_{k-1}^n}}+\left(\frac{\Delta x}{2}-a\frac{\Delta t}{2}\right)a{\color{salmon}{\sigma_{k-1}^n}}\\
{\color{teal}{F_{k+1/2}^n}}&=a{\color{teal}{q_{k+1}^n}}+\left(\frac{\Delta x}{2}-a\frac{\Delta t}{2}\right)a{\color{teal}{\sigma_{k+1}^n}}
\end{aligned}
```

Now that we have the advection equation on the flux form, we can define a flux limiter $\phi(\theta)$ to avid overshoots and undershoots near strong gradients or local maxima and minima of the signal $q(x,t)$. Here, $\theta$ is a smoothness indicator, defined as 

where
```{math}
:label: eq:smoothness_theta
\theta_{k+1/2}^n=\frac{q_k^n-q_{k-1}^n}{q_{k+1}^n-q_k^n}
```

From equation {eq}`eq:smoothness_theta`, we can note a few details:
* $\theta$ is defined at the grid cell edge $k+1/2$. 
* The nominator and denominator contains a backward (upwind) and a forward (downwind) difference of $q_k^n$, respectively. 
* If $\theta$ is positive, the upwind and the downwind slopes have the same sign and $q_k^n$ is not a local extremum. 
* If $\theta\sim+1$, the upwind and downwind slopes are similar, indicating similar behavior of the signal for the neighboring points 
* If $\theta$ is negative, the upwind and downwind slopes have different signs and $q_k^n$ is a local extremum that may require action to avoid overshoots and undershoots

The flux limiter $\phi(\theta)$ takes on a value for each grid cell, based on the value of $\theta$. 

```{note}
You can think of the flux limiter as some kind of switch, or an *if* statement in coding. When you code up a flux limiter, you check the value of $\theta$ for each grid cell, and then define a value $\phi(\theta)$ for each grid cell.
```

The Godunov fluxes from {eq}`eq:Godunov_fluxes` with limiters, will now look like:

```{math}
:label: eq:Godunov_fluxes
\begin{aligned}
F_{k-1/2}^n&=aq_{k-1}^n+\left(\frac{\Delta x}{2}-a\frac{\Delta t}{2}\right)a\sigma_{k-1}^n\phi(\theta_{k-1/2}^n)\\
F_{k+1/2}^n&=aq_{k+1}^n+\left(\frac{\Delta x}{2}-a\frac{\Delta t}{2}\right)a\sigma_{k+1}^n\phi(\theta_{k+1/2}^n)
\end{aligned}
```

If we, as an example, choose the downwind slope $\sigma_k^n = \frac{q_{k+1}^n - q_k^n}{\Delta x}$, the full set of equtions for the Godunov advection scheme on flux form with limiters become:

```{math}
:label: eq:Godunov_fluxform_downwind
\begin{aligned}
q_k^{n+1} & =q_k^n+\frac{\Delta t}{\Delta x}[F_{k-1/2}^n-F_{k+1/2}^n]\\
F_{k-1/2}^n & =aq_{k-1}^n+\left(\frac{\Delta x}{2}-a\frac{\Delta t}{2}\right)a\frac{q_{k}^n - q_{k-1}^n}{\Delta x}\phi(\theta_{k-1/2}^n)\\
F_{k+1/2}^n & =aq_{k+1}^n+\left(\frac{\Delta x}{2}-a\frac{\Delta t}{2}\right)a\frac{q_{k+1}^n - q_k^n}{\Delta x}\phi(\theta_{k+1/2}^n)
\end{aligned}
```

```{margin} 
$C=a\frac{\Delta t}{\Delta x}$ <br>
$\theta_{k+1/2}^n=\frac{q_k^n-q_{k-1}^n}{q_{k+1}^n-q_k^n}$

```

If we insert $C=a\frac{\Delta t}{\Delta x}$, and massage the expression, we end up with:

(definition:Godunov Flux form)=
:::{admonition} Godunov Flux form with downwind slope and limiters:
:class: important

```{math} 
:label: eq:Godunov_fluxform_downwind_massaged
\begin{aligned}
q_k^{n+1}& =q_k^n+\frac{\Delta t}{\Delta x}[F_{k-1/2}^n-F_{k+1/2}^n]\\
F_{k-1/2}^n& =aq_{k-1}^n+\frac{a}{2}(1-C)(q_{k}^n - q_{k-1}^n)\phi(\theta_{k-1/2}^n)\\
F_{k+1/2}^n& =aq_{k}^n+\frac{a}{2}(1-C)(q_{k+1}^n - q_{k}^n)\phi(\theta_{k+1/2}^n)
\end{aligned}
```
:::



Figure {numref}`fig:TVD_theta_phi` illustrates what this means. The figure is showing the $\theta$-$\phi$ space, with the smoothness indicator on the x-axis and our choice of flux limiter value on the y-axis. If we define $\phi(\theta)\equiv0$ for all values of $\theta$ we are only left with the first terms on the right hand sides of the fluxes $F_{k\pm1/2}$. You can try yourself to insert these fluxces into equation {eq}`eq:Godunov_fluxform` and see if you recognize that this is is the FTBS scheme. 

```{figure} ./TVD1.png
---
:name: fig:TVD_theta_phi
:width: 40%
:align: center
---
$\theta$-$\phi$ space for visualizing flux limieters. Two simple flux limiters,$\phi\equiv0$ (blue) and $\phi\equiv1$ (red) are sketched. These corresond with the FTBS and the Lax-Wendroff scheme. You can confirm this by inserting the fluxes into the Godunov equation on flux form, and massage the mathematical expression.
```

## Total Variation Diminishing (TVD) schemes (part 2)
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
q_k^{n+1}=q_k^n-C {\color{violet}{(q_{k-1}^n-q_{k-1}^n)}} -\frac{C}{2}(1-C)\left[ \phi(\theta_{k+1/2}^n)\frac{(q_{k+1}^n-q_k^n)}{{\color{violet}{(q_{k-1}^n-q_{k-1}^n)}}} - \phi(\theta_{k-1/2}^n){\color{violet}{(q_k^n-q_{k-1}^n)}} \right]
```

Noting that the term $\frac{(q_{k+1}^n-q_k^n)}{{\color{violet}{(q_{k-1}^n-q_{k-1}^n)}}}$ is the same as ${1}/{\theta_{k+1/2}^n}$, we can replace this in equation {eq}`eq:Godunov_pregeneral`, and complete the factorizing of ${\color{violet}{(q_k^n-q_{k-1}^n)}}$ to get the scheme on the general form:

(definition:Total Variation)=
:::{admonition} Godunov on the general form
:class: important
```{math}
\begin{aligned}
q_k^{n+1} & =q_k^n- \left(C+\frac{C}{2}(1-C)\left[ \frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n}-\phi(\theta_{k-1/2}^n) \right]\right){\color{violet}{(q_k^n-q_{k-1}^n)}}   \\
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
0 & \le C-\frac{C}{2}(1-C)\phi(\theta_{k-1/2}^n) & \le 1 & \quad & ,\text{subtract } C\\
-C & \le -\frac{C}{2}(1-C)\phi(\theta_{k-1/2}^n) & \le 1-C & \quad &,\text{mulitply by } \frac{2}{C(1-C)}\\
-C(\frac{2}{C(1-C)}) & \le -\phi(\theta_{k-1/2}^n) & \le (1-C)\frac{2}{C(1-C)} & \quad &,\text{cancel terms } \\
-\frac{2}{(1-C)} & \le -\phi(\theta_{k-1/2}^n)  & \le \frac{2}{C} & \quad &,\text{mulitply by }-1 \text{and swap sides, ensuring correct signs} \\
-\frac{2}{C} & \le \phi(\theta_{k-1/2}^n) & \le \frac{2}{(1-C)} & \quad &
\end{aligned}
```



```{math} :label: eq:A_right
\begin{alignat}{3}
0 &\le C-\frac{C}{2}(1-C)\phi(\theta_{k-1/2}^n) & \le 1 &\quad &,\text{subtract } C \\
-C &\le -\frac{C}{2}(1-C)\phi(\theta_{k-1/2}^n) & \le 1-C &\quad &,\text{multiply by } \frac{2}{C(1-C)} \\
-C\left(\frac{2}{C(1-C)}\right) &\le -\phi(\theta_{k-1/2}^n) &\le (1-C)\frac{2}{C(1-C)} &\quad &,\text{cancel terms} \\
-\frac{2}{(1-C)} &\le -\phi(\theta_{k-1/2}^n) &\le \frac{2}{C} &\quad &,\text{multiply by } -1 \text{ and swap sides} \\
-\frac{2}{C} &\le \phi(\theta_{k-1/2}^n) &\le \frac{2}{(1-C)} & 
\end{alignat}
```

Similarly, if $\phi(\theta_{k-1/2}^n\le)=0$, we have:
```{math}
:label: eq:A_left
\begin{aligned}
0 & \le C-\frac{C}{2}(1-C)\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} & \le 1\\
-C & \le \frac{C}{2}(1-C)\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} & \le 1-C\\
-C(\frac{2}{C(1-C)}) & \le \frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} & \le (1-C)\frac{2}{C(1-C)}\\
-\frac{2}{(1-C)} & \le \frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} & \le \frac{2}{C}\\
\end{aligned}
```

We must have $0\le A \le 1$ for all grid cells to ensure TVD. The maximum value of $A$ gives the strictest constraint. We, therefore, continue looking only at the right hand sides of the inequalities. From Equation {eq}`eq:A_right`, we must have: $\phi(\theta_{k-1/2}^n) \le \frac{2}{(1-C)}$ and from Equation {eq}`eq:A_left`, we must have $\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} \le \frac{2}{C}$. From CFL considerations, we can assume we must have $C<1$. Our conditions must therefore take on their strictest (smallest)  values when $\phi(\theta_{k-1/2}^n) \le 2$ (for $C=0$) and $\frac{\phi(\theta_{k+1/2}^n)}{\theta_{k+1/2}^n} \le 2$ for $C=1$.

(definition:TVD criteria)=
:::{admonition} The Godunov scheme is TVD if:
:class: important
```{math}
:label: eq:TVD_crit
\begin{aligned}
\phi(\theta) & \le \text{minmod}(2,2\theta)\,\,\,\,\, & \forall \theta \ge 0\\
\phi(\theta) & =0\,\,\,\,\, & \forall \theta \le 0\\
\end{aligned}
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

Figure {ref}`fig:TVD_theta_phi_TVDcrit` shows the $\theta$-$\phi$ space, where the area that ensures TVD is hatched. The area is bounded by the lines $\phi(\theta)\le 2$ and $\phi(\theta)\le 2\theta$.  We can now better understand where the oscillations in the Lax-Wendroff scheme comes from. As long as the slope $\theta \ge\frac{1}{2}$, the scheme is inside the TVD regime. However, for negative or small values of $\theta$ ($\theta\le \frac{1}{2}$), the red line, representing Lax Wendroff, is outside the hatched area that ensures TVD. It is for these small $\theta$ that the oscillations start to grow.