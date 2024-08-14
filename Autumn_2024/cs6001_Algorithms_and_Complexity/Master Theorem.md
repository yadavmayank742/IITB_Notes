#master_theorem 
> Reference Book : [Proof Without Words](https://www.amazon.in/Proofs-without-Words-Exercises-Classroom/dp/0883857006)



For a general form , $T(n) = aT(n/b) + cn^d$

**THINK** by drawing the recursive tree :

$T(n) = n^d \times (1 + (\frac{a}{b^d}) + (\frac{a}{b^d})^2 + \dots +(\frac{a}{b^d})^k)$

$\approx n^d \cdot (\frac{a}{b^d})^k$         *{using geometric progression}*

$\approx n ^{\log_b a}$ 


$$
T(n)=\begin{cases*}
\Theta(n^d) & if $\frac{a}{b^d} < 1$,\\
\Theta(n^d \cdot \log_2 n) & if $\frac{a}{b^d} == 1$,\\
\Theta(n^{\log_b a}) & if $\frac{a}{b^d} > 1$,\\
\end{cases*}
$$



