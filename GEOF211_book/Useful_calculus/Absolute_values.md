(Useful_calculus:Absolute_values)=
# Absolute values

The absolute value is denoted by vertical bars and indicate the positive number corresponding to the numeric value of an expression.

Let $a$ be a positive number, $a>0$

Then we have:

```{math}
:label: eq:Absolute_def
\begin{aligned}
|a|=a\\
|-a|=a
\end{aligned}
```

For inequalities, we have two notations that mean the same:

```{math}
:label: eq:Absolute_inequality
\begin{aligned}
|a|\leq1\\
-1\leq a\leq 1
\end{aligned}
```

Inequalities of sums and differences:

```{math}
:label: eq:Absolute_sum
\begin{aligned}
|a+b|&=\sqrt{a^2+b^2}\\
|a-b|&=\sqrt{a^2+(-b)^2}\\
\end{aligned}
```

```{math}
:label: eq:Absolute_fraction
\left|\frac{a}{b}\right|=\frac{|a|}{|b|}
```

Combining the equations above gives the following:

```{math}
:label: eq:Absolute_fraction2
\begin{aligned}
\left|\frac{a+b}{a-b}\right|&=\frac{|a+b|}{|a-b|}\\
&=\frac{\sqrt{a^2+b^2}}{\sqrt{a^2+(-b)^2}}\\
&=1
\end{aligned}
```

The triangle inequality can be useful in some stabilty analyses:

```{math}
:label: eq:Triangle_identity
|x+y|\leq|x|+|y|
```


