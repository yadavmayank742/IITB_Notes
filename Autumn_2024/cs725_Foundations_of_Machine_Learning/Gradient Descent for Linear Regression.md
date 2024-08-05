#gradient_descent #linear_regression 

*It is a first order iterative algorithm used to find local optima (maxima or minima) of a differentiable function.*

**Gradient** ==  $\nabla_wL$   $\text{complete formula later}$

**Descent** == since we are interested in *minimizing the loss function*, thus we update $w$ in the ***reverse direction of the gradient***.

Thus we apply **GD** to estimate $w$ which parametrizes a loss function.


Template for GD Algo :
```
1. Intialize w
2. Repeat
	1. Choose a descent direction
	2. Choose a step size
	3. Update w using an update rule
3. Exit, repeat if stopping criteria is met
```

NOTEs:
- Step size is determined by $\eta > 0$ ; $\eta$ is called "***Learning Rate***" 
- Example : $w_{t+h} \leftarrow w_t - \eta\nabla_hL$  where $- \eta\nabla_hL$ is *Descent Direction*.
----
>What happens with GD when the step size is too small ?

*too many iterations needed to reach the final solution*

>What happens with GD when the step size is too large ?

*Delayed arrival at solution, in worst case, the loss could diverge*
