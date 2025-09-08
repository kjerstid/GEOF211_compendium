(Useful_calculus:Trigonometry)=
# Trigonometry

#### Pythagorean indentity:

```{math}
:label: eq:Trig_pythagoras
\sin^2 x+\cos^2 x=1
```

#### Sine and cosine additive identities
```{math}
:label: eq:Trig_sine_add
\sin(x+y)=\sin x\cos y+\cos x\sin y
```

```{math}
:label: eq:Trig_cos_add
\cos(x+y)=\cos x\cos y-\sin x\sin y
```

#### Double angle formulas:
```{math}
:label: eq:Trig_psine_double
\sin(2x)=2\sin x\cos x
```

```{math}
:label: eq:Trig_cosine_double
\cos(2x)=\cos^2 x-\sin^2 x=2cos^2 x-1=1-2\sin^2x
```

#### Half angle formulas:
```{math}
:label: eq:Trig_sine:half
\sin(\frac{x}{2})=\pm \sqrt{\frac{1-\cos x}{2}}
```

```{math}
:label: eq:Trig_cosine_half
\cos(\frac{x}{2})=\pm \sqrt{\frac{1+\cos x}{2}}
```

## Complex numbers
The imaginary unit, $i$ is defined as:
```{math}
:label: eq:Complex_i
i=\sqrt{-1}
```

A complex number is and expression of the form: 

```{math}
:label: eq:Complex_def
z=x+iy
```

The distance from origo, the the point (x,y) in the complex plane is called the modulus and is defined as:
```{math}
:label: eq:Complex_modulus
|z|=\sqrt{x^2+y^2}
```

The norm of a complex  number (equivalent of the vector length in the complex plane) is:
```{math}
:label: eq:Complex_norm_squared
|z|^2=x^2+y^2
```

The modulus of a product of two complex numbers $z$ and $w$ is:
```{math}
:label: eq:Complex_modulus_product
|zw|=|z||w|
```

The modulus of the sum of two complex numbers, also called "The triangle inequality" is defined:
```{math}
:label: eq:Complex_triangle_identity
|z+w|<|z|+|w|
```


## The Euler formula and modifications

#### Eulers identity
```{math}
:label: eq:Euler_identity
e^{i\pi}+1=0
```

#### Eulers formula
```{math}
:label: eq:Euler
e^{ix}=\cos x+i\sin x
```

#### Cosine exponential form
```{math}
:label: eq:Euler_cos
\frac{e^{ix}+e^{-ix}}{2}=\cos x
```

#### Sine exponential form
```{math}
:label: eq:Euler_sin
\frac{e^{ix}-e^{-ix}}{2i}=\sin x
```

#### Tangent exponential form
```{math}
:label: eq:Euler_tan
\frac{e^{ix}-e^{-ix}}{i(e^{ix}+e^{-1x})}=\tan x
```

#### Complex exponential
```{math}
:label: eq:Euler_complex_exp
e^{x+iy}=e^x(\cos y+i\sin y)
```

#### de Moivre's theorem
```{math}
:label: eq:Euler_sine_add
(\cos x+i\sin x)^n=\cos nx+i\sin nx
```

You can read more about trigonometry in {cite:ts}`Adams2018calculus`, chapter P.6.
