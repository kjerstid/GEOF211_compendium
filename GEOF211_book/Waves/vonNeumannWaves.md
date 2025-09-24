# von Neumann analysis of the wave equation

The one-dimensional wave equation (equation {eq}`eq:Waves`), repeated here is :

```{math}
\frac{\partial^2 \eta}{\partial t^2}=c^2\frac{\partial^2 \eta}{\partial x^2}
```
, where $\eta$ is the fluid surface, $c=\sqrt{gH}$, $g\sim9.81\text{ms}^-1$ is the gravitational constant and $H$ is the depth of the fluid.

The CTCS scheme for the wave equation can be found using the centered formula (Eq. {eq}`eq:Centered2derivative`) for the second derivative on either side of the equation and reordering the expression:

```{margin}
```{note}
$r^2=\frac{c^2\Delta t^2}{\Delta x^2}$
```

```{math}
:label: eq:Waves_CTCS
\eta_m^{n+1}=2\eta_m^{n}-\eta_m^{n-1}+r^2(n_{m+1}^n-2n_{m}^n+n_{m-1}^n)
```

Substituting a solution like {eq}`eq:vonNeumannSolution`,$\eta_m^n\sim B^ne^{ikm\Delta x}$, in {eq}`eq:Waves_CTCS`, we have:

```{math}
\begin{aligned}
B^{n+1} e^{ikm\Delta 𝑥}&=2𝐵^𝑛 e^{ikm\Delta 𝑥} −B^{n−1} 𝑒^{ikm\Delta x}+𝑟^2 (B^n e^{ik(m+1)\Delta x}−2B^n e^{ikm\Delta x}+B^n e^{ik(m−1)\Delta x}) \quad \text{:Divide by }$e^{ikm\Delta x}\\ 
B^{n+1}&=2B^𝑛−B^{n−1}+r^2 B^n e^{ik\Delta 𝑥}−2r^2 B^n+r^2 B^n 𝑒^{−ik\Delta x} \qquad \text{:Factorize} \\
B^{n+1}&=2(1−r^2)B^n−B^{n−1}+r^2 B^n \underbrace{(e^{ik\Delta x}+e^{−ik\Delta x})}_{2cos(k\Delta x)}\\
B^{n+1}&=2(1−𝑟^2)B^n−B^{n−1}+2r^2 B^n cos(k\Delta x) \qquad \text{:Factorize}\\
B^{n+1}&=2\left (1−2𝑟^2 \left (\frac{1−cos⁡(𝑘Δ𝑥)}{2}\right )\right )B^n−B^{n−1}
\qquad \text{Use: } sin^2\frac{\theta}{2}=\frac{1-cos\theta}{2}\\
B^{n+1}&=2(\underbrace{1−2𝑟^2sin^2\frac{k\Delta x}{2}}_{\gamma})B^n−B^{n−1} \\
B^{n+1}&=2\gamma B^n−B^{n−1}             
\end{aligned}
```

This expression contains three timesteps of $B$. To solve from here, we could use a recurrence matrix, or we can check for specific timesteps. The condition $|\frac{B^{n+1}}{B^n}|<1$ only holds if it holds for any three concurrent timesteps. We can test the conditions with, e.g., inserting $n=1$, which yields:

```{math}
\begin{aligned}
B^2&=2\gamma B-B^0

B^2-2\gamma B+1&=0

B_{1,2}&=\gamma\pm\sqrt{\gamma^2-1}
\end{aligned}
```

We must have $|B_{1,2}|<1$. If $\gamma >1$, $B_1$ willl also be $>1$. We must, therefore, require $|\gamma|\le1$.

```{math}
\begin{aligned}
|\gamma|&=\left|1−2𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\right|\le1\\
-1&\le1−2𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\le1 \qquad:\text{Subtract 1 everywhere}\\
-2&\le−2𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\le0
\end{aligned}
```

The right inequality always holds. We must look more closely at the left inequality. Dividing by $-2$ and flipping the inequality, we have:

```{math}
\begin{aligned}
1&\ge𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}\\
𝑟^2𝑠𝑖𝑛^2\frac{𝑘Δ𝑥}{2}&\le1
\end{aligned}
```

Since the sine squared is always positive and $\le1$, we must have $𝑟^2≤1$:

```{math}
r^2=\frac{c^2\Delta t^2}{\Delta x^2}\le1
```

which yields $r=\frac{c\Delta t}{\Delta x}\le1$. We, therefore, end up with the same CFL criterion as for the advection equation. 