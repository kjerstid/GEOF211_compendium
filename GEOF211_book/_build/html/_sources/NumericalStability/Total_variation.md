(NumericalStability:Total_variation)=
# Total Variation (TV) and Total Variation Diminishing (TVD) schemes

## Total variation (TV)
The total variation is a measure of the amount of oscillation in the field:

(definition:Total Variation)=
:::{admonition} Definition
:class: important
$$
TV(q^n)=\sum_{m=2}^J|(q_m^n-q_{m-1}^n)|
$$ (eq:TotalVariation)
:::

## Total Variation Diminishing (TVD) schemes

(definition:Total Variation DIminishing schemes)=
:::{admonition} Definition
:class: important
A numerical scheme is total variation diminishing if:
$$
$TV(q^{n+1})\leq TV(q^n)$
$$ (eq:TotalVariation)
:::

For TVD schemes, the amount of oscillation does not increase with time.

A TVD scheme preserves *monotonicity*. If the initial field is monotone, a TVD scheme cannot give oscillations like
overshoots.

 If $ q_m^n=\geq q_{m+1}^n\,\, \forall\, m $, then $ q_m^{n+1}=\geq q_{m+1}^{n+1}\,\, \forall\, m $.

However, discontinuities may still be smoothed in TVD schemes.

## Harten's theorem

Consider a general method of the form:

$$
q_m^{n+1}=q_m^n-C_{m-1}^n(q_m^n-q_{m-1}^n)+D_m^n(q_{m+1}^n-q_m^n)
$$ (eq:HartenGeneral)

where the coefficients $C$ and $D$ are arbitrary values that may depend on $q$. (Note that
these coefficients are displaced half a grid length to the right, so that e.g. $D_m^n$ is valid
at $j+\frac{1}{2}$. Then it has been shown {cite:p}`Harten1983` that 

(theorem:HartenTheorem)=
:::{admonition} Harten's Theorem
:class: important
Consider a method on the general form (`eq:HartenGeneral`). Then
$$
TV(q^{n+1})\leq TV(q^n)
$$
if $C_m^n+D_m^n\leq 1$ and $C_m^n\geq 0$, $D_m^n \geq 0\,\, \forall\,m$
:::

These TVD conditions are called Harten’s theorem.

