#master_theorem 

For a general form , $T(n) = aT(n/b) + cn^d$

$$
T(n)=\begin{cases*}
\Theta(n^d) & if $\frac{a}{b^d} < 1$,\\
\Theta(n^d \cdot \log_2 n) & if $\frac{a}{b^d} == 1$,\\
\Theta(n^{\log_b a}) & if $\frac{a}{b^d} > 1$,\\
\end{cases*}
$$

