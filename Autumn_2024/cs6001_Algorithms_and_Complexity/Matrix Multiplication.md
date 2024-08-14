#matrix_multiplication #strassen_matrix_multiplication


$$
\begin{bmatrix}
    x_{11} & x_{12} & x_{13} & \dots & x_{1n} \\
    x_{21} & x_{22} & x_{23} & \dots & x_{2n} \\
    \vdots & \vdots & \vdots & \ddots & \vdots\\
    x_{n1} & x_{n2} & x_{n3} & \dots & x_{nn}
\end{bmatrix}_{n\times n}
\times
\begin{bmatrix}
    y_{11} & y_{12} & y_{13} & \dots & y_{1n} \\
    y_{21} & y_{22} & y_{23} & \dots & y_{2n} \\
    \vdots & \vdots & \vdots & \ddots & \vdots\\
    y_{n1} & y_{n2} & y_{n3} & \dots & y_{nn}
\end{bmatrix}_{n\times n}
=
\begin{bmatrix}
    z_{11} & z_{12} & z_{13} & \dots & z_{1n} \\
    z_{21} & z_{22} & z_{23} & \dots & z_{2n} \\
    \vdots & \vdots & \vdots & \ddots & \vdots\\
    z_{n1} & z_{n2} & z_{n3} & \dots & z_{nn}
\end{bmatrix}_{n\times n}
$$


$z_{ij} = <X_i, Y_j>$

$==\sum^{n}_{k=1}X_i(k)Y_j(k)$

Therefore,  $T(n) = 8T(\frac{n}{2}) + n^2$

or, $T(n) = \Theta(n^3)$
