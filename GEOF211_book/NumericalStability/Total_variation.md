(NumericalStability:Total_variation)=
# Total Variation (TV) and Total Variation Diminishing (TVD) schemes

## Total variation (TV)
The total variation is a measure of the amount of oscillation in the field:

(definition:Total Variation)=
:::{admonition} Definition
:class: important
```{math}
:label: eq:TotalVariation
TV(q^n)=\sum_{m=2}^J|(q_m^n-q_{m-1}^n)|
```
:::

The change in total variation with time, can tell you much about the behaviour of the numerical solution. Schemes that give unwanted oscillations will typically have large variation in Total variation, although the Total Variation may still vary within bounds.

(important:stabilityPDE)=
:::{important}
When you calculate the Total Variation, you must carefully consider your boundary conditions to make sure you treat the boudnary points correctly.
:::


## Total Variation Diminishing (TVD) schemes

(definition:Total Variation DIminishing schemes)=
:::{admonition} Definition
:class: important
A numerical scheme is total variation diminishing if:
```{math}
:label: eq:TotalVariation_b
TV(q^{n+1})\leq TV(q^n)
```
:::

For TVD schemes, the amount of oscillation does not increase with time. The FTBS scheme for linear advection is an example of a TVD scheme, as long as we don't break the CFL criterion. The scheme smoothes out the original signal and reduce the Total Variation with time. 

A TVD scheme preserves *monotonicity*. If the initial field is monotone, a TVD scheme cannot give oscillations like
overshoots.

 If $ q_m^n=\geq q_{m+1}^n\,\, \forall\, m $, then $ q_m^{n+1}=\geq q_{m+1}^{n+1}\,\, \forall\, m $.

However, discontinuities may still be smoothed in TVD schemes, as is the case for  the FTBS for linear advection.

## Harten's theorem

Consider a general method of the form:

```{math}
:label: eq:HartenGeneral
q_m^{n+1}=q_m^n-C_{m-1}^n(q_m^n-q_{m-1}^n)+D_m^n(q_{m+1}^n-q_m^n)
```

where the coefficients $C$ and $D$ are arbitrary values that may depend on $q$. (Note that
these coefficients are displaced half a grid length to the right, so that, e.g., $D_m^n$ is valid
at $j+\frac{1}{2}$.) Then it has been shown {cite:p}`Harten1983` that 

(theorem:HartenTheorem)=
:::{admonition} Harten's Theorem
:class: important
Consider a method on the general form (`eq:HartenGeneral`). Then
```{math}
TV(q^{n+1})\leq TV(q^n)
```
if $A_m^n+B_m^n\leq 1$ and $A_m^n\geq 0$, $B_m^n \geq 0\,\, \forall\,m$
:::

We can now verify that the FTBS scheme for linear advection is TVD.
The FTBS scheme for linear advection is written:
```{math}
q_m^{n+1}=q_m^n-a\frac{\Delta t}{\Delta x}(q_m^n-q_{m-1}^n)
```

If we compare this scheme with the general form (eq. `eq:HartenGeneral`), we find that $A_{m-1}^n=a\frac{\Delta t}{\Delta x}$ and $B_m^n=0$. The coefficient $A_{m-1}$ is positive as long as the advection speed $a$ is positive. We also find that the requirement $A_{m-1}+B_m^n<1$ holds as long as $A=a\frac{\Delta t}{\Delta x}\leq 1$, which is the same requirement as the CFL criterion. The FTBS scheme for linear advection is, therefore, TVD as along as $A=a\frac{\Delta t}{\Delta x}\leq 1$.

Try for yourself to write the CTCS schgeme for linear advection on the general form, and check if the scheme is TVD.
