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

We can prove that this solution is correct, by differentiating the solution twice using the chain rule and inserting the expressions into the equation. To make the calculations tidier, we can introduce a variable transform set $\phi=x+ct$ and $\psi=x-ct$. Our general solution now becomes $\eta(x,t)=f(\phi)+g(\psi)$. 

```{margin}
```{note}
When differentiating $\phi$ and $\psi$ with respect to $x$, they are bot zero, while differentiating them with respect to $t$, gives either $+c$ or $-c$. 
````
```


```{math}
:label: eq:WavesSolution_proof_a
\begin{aligned}

\frac{\partial \eta}{\partial x} & =\frac{\partial f}{\partial \phi}\frac{\partial \phi}{\partial x}+\frac{\partial g}{\partial \psi}\frac{\partial \psi}{\partial x}  =\frac{\partial f}{\partial \phi}+\frac{\partial g}{\partial \psi}\\

\frac{\partial^2 \eta}{\partial x^2} & =\frac{\partial^2 f}{\partial \phi^2}\frac{\partial \phi}{\partial x}+\frac{\partial^2 g}{\partial \psi^2}\frac{\partial \psi}{\partial x}  =\frac{\partial^2 f}{\partial \phi^2}+\frac{\partial^2 g}{\partial \psi^2}\\

\frac{\partial \eta}{\partial t} & =\frac{\partial f}{\partial \phi}\frac{\partial \phi}{\partial t}+\frac{\partial g}{\partial \psi}\frac{\partial \psi}{\partial t}  =\frac{\partial f}{\partial \phi}c+\frac{\partial g}{\partial \psi}(-c)\\

\frac{\partial^2 \eta}{\partial t^2} & =c\frac{\partial^2 f}{\partial \phi^2}\frac{\partial \phi}{\partial x}-c\frac{\partial^2 g}{\partial \psi^2}\frac{\partial \psi}{\partial t} &=c^2\frac{\partial^2 f}{\partial \phi^2}+(-c)^2\frac{\partial^2 g}{\partial \psi^2}\\

\eta(x,t) & =f(x+ct)+g(x-ct) 
\end{aligned}
```


```{math}
:label: eq:WavesSolution_proof_a
\begin{aligned}
\frac{\partial \eta}{\partial x} &= \frac{\partial f}{\partial \phi}\frac{\partial \phi}{\partial x} + \frac{\partial g}{\partial \psi}\frac{\partial \psi}{\partial x} = \frac{\partial f}{\partial \phi} + \frac{\partial g}{\partial \psi} \\
\frac{\partial^2 \eta}{\partial x^2} &= \frac{\partial^2 f}{\partial \phi^2}\frac{\partial \phi}{\partial x} + \frac{\partial^2 g}{\partial \psi^2}\frac{\partial \psi}{\partial x} = \frac{\partial^2 f}{\partial \phi^2} + \frac{\partial^2 g}{\partial \psi^2} \\
\frac{\partial \eta}{\partial t} &= \frac{\partial f}{\partial \phi}\frac{\partial \phi}{\partial t} + \frac{\partial g}{\partial \psi}\frac{\partial \psi}{\partial t} = \frac{\partial f}{\partial \phi}c + \frac{\partial g}{\partial \psi}(-c) \\
\frac{\partial^2 \eta}{\partial t^2} &= c^2\frac{\partial^2 f}{\partial \phi^2} + (-c)^2\frac{\partial^2 g}{\partial \psi^2} \\
\eta(x,t) &= f(x+ct) + g(x-ct)
\end{aligned}


Inserting these expressions into the wave equation yields:
```{math}
:label: eq:WavesSolution_proof

\frac{\partial^2 eta}{\partial t^2} =c^2\frac{\partial^2 f}{\partial u^2}+(-c)^2\frac{\partial^2 g}{\partial v^2}=c^2(\frac{\partial^2 f}{\partial u^2}+\frac{\partial^2 g}{\partial v^2})=c^2\frac{\partial^2 eta}{\partial x^2}

```

