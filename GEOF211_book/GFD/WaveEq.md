# The wave equation

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