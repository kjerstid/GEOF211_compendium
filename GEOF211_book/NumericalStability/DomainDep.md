(NumericalStability:DomainDep)=
# Domain of dependence
The domain of dependence is a measure of which grid points the numerical solution for a given grid point $q_m^{n+1}$ depends on. If we, for example look at the FTBS scheme for the advection equation:

$$
q_m^{n+1}=q_m^n-a\frac{\Delta t}{\Delta x}(q_m^n-q_{m-1}^n)
$$

Here, the solution for $q_m^{n+1}$ depends on the terms $q_m^n$ and $q_{m-1}^n$. We can annotate these dependencies in the discrete time-space domain:


%load_ext tikzmagic

%%tikz --scale 2 --size 300,300 -f svg
\begin{tikzpicture}
    % Axes
    \draw[->] (0,0) -- (5,0) node[right] {$x$};
    \draw[->] (0,0) -- (0,5) node[above] {$t$};

    % Grid points
    \foreach \x in {1,2,3,4} {
        \foreach \y in {1,2,3,4} {
            \fill (\x,\y) circle (2pt);
        }
    }

    % Domain of dependence
    \draw[thick, dashed] (2,2) -- (1,1) -- (3,1) -- cycle;
    \fill[gray, opacity=0.3] (2,2) -- (1,1) -- (3,1) -- cycle;

    % Labels
    \node at (2,2) [above right] {$(x_i, t_n)$};
    \node at (1,1) [below left] {$(x_{i-1}, t_{n-1})$};
    \node at (3,1) [below right] {$(x_{i+1}, t_{n-1})$};

    % Arrows
    \draw[->, thick] (2,2) -- (1,1);
    \draw[->, thick] (2,2) -- (3,1);

\end{tikzpicture}

