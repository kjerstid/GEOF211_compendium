(GFD:Waves)=
# Wave equation

## The classical wave equation

The classical wave equation in 1D can be written:

```{math}
:label: eq:Waves
\frac{\partial^2 \eta}{\partial t^2}=c^2\frac{\partial^2 \eta}{\partial x^2}
```

, where $\eta$ represents the vertical displacement of the wave surface. In the ocean this would mean the deviation from the mean sea surface heigh.

The general solution to the wave equation {eq}`eq:Waves` can be expressed as:

```{math}
:label: eq:WavesSolution
\eta(x,t)=f(x+ct)+g(x-ct)
```

The solution represents one wave moving eastward ($f(x+ct)$) and one wave moving westward (g(x-ct)). If a surface is initially disturbed, such as from depressing the surface, waves will spread in all directions. If you throw a pebble in a puddle, you will see waves spreading like rings from the center of where you threw the pebble. For the 1D case, you can think of it as a transect cutting across the 2D case, or alternatively as 
throwing a pebble in a very narrow and long puddle. Here, the waves spread in only 2 directions, as is indicated in the solution to the wave equation {eq}`eq:WavesSolution`. 

We can prove that this solution is correct, by differentiating the solution twice using the chain rule and inserting the expressions into the equation. To make the calculations tidier, we can introduce $u=x+ct$ and $v=x-ct$. Our general solution now looks like $\eta(x,t)=f(u)+g(v)$. When differentiating $u$ and $v$ with respect to $x$, they are bot zero, while differentiating them with respect to $t$, gives either $+c$ or $-c$. 

```{margin}
```{note}
Here, $u,v$ are names of the variable transformations, and does not indicate velocity in the east/north direction as in other sections of this material.
```
```

```{math}
:label: eq:WavesSolution_proof_a
\begin{aligned}

\frac{\partial \eta}{\partial x} & =\frac{\partial f}{\partial u}\frac{\partial u}{\partial x}+\frac{\partial g}{\partial x}\frac{\partial v}{\partial x} & =\frac{\partial f}{\partial u}+\frac{\partial g}{\partial x} \\

\frac{\partial^2 \eta}{\partial x^2} & =\frac{\partial^2 f}{\partial u^2}\frac{\partial u}{\partial x}+\frac{\partial^2 g}{\partial v^2}\frac{\partial v}{\partial x} & =\frac{\partial^2 f}{\partial u^2}+\frac{\partial^2 g}{\partial x^2} \\


\frac{\partial \eta}{\partial t} & =\frac{\partial f}{\partial u}\frac{\partial u}{\partial t}+\frac{\partial g}{\partial t}\frac{\partial v}{\partial t} & =\frac{\partial f}{\partial u}c+\frac{\partial g}{\partial t}(-c) \\

\frac{\partial^2 \eta}{\partial t^2} & =c\frac{\partial^2 f}{\partial u^2}\frac{\partial u}{\partial x}-c\frac{\partial^2 g}{\partial t^2}\frac{\partial v}{\partial t} & =c^2\frac{\partial^2 f}{\partial u^2}+(-c)^2\frac{\partial^2 g}{\partial v^2}\\

\eta(x,t) & =f(x+ct)+g(x-ct) &
\end{aligned}
```

Inserting these expressions into the wave equation yields:
```{math}
:label: eq:WavesSolution_proof

\frac{\partial^2 eta}{\partial t^2} =c^2\frac{\partial^2 f}{\partial u^2}+(-c)^2\frac{\partial^2 g}{\partial v^2}=c^2(\frac{\partial^2 f}{\partial u^2}+\frac{\partial^2 g}{\partial v^2})=c^2\frac{\partial^2 eta}{\partial x^2}

```

