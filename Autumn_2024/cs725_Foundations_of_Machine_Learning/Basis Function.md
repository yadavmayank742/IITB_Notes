
#basis_function #linear_regression 

Define $\phi$ : $\chi \rightarrow \mathbb{R}^m$, 
$$
\phi(x) =\begin{bmatrix}
			1 \\
           \phi_{1}(x) \\
           \phi_{2}(x) \\
           \vdots \\
           \phi_{m}(x) \\
         \end{bmatrix}

$$
typically, $m >>d$ , but $d >m$ as well if there're correlated/spurious features that we want to eliminate.

# Common Type of Basis Functions:
1. **Polynomial Basis** - for 1-D points, $\phi_j(x) = x^j$.
2. **Radial Basis Function (RBF)** - for 1-D Points, $\phi_j(x) = e^{-\frac{(x - \mu_j)^2}{\sigma_j^2}}$  where $\mu_j$ and $\sigma_j$ are predefined.
	This is also called **Gaussian Basis**
3. 