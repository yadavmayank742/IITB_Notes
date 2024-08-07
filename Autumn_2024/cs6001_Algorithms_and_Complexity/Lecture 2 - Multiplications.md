07 Aug, 2024

> The course can give strategies for solving problems, but practice is needed to inculcate the skill of solving problems.

Starting from previous lecture, 
**Question :** Given $x$ and $y$ , two $n$ digit numbers, find the optimum way to multiply them .
--

**[Andrey Nikolaevich Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov)** questioned what is the [best way](https://www.realclearscience.com/articles/2019/04/10/weve_found_a_quicker_way_to_multiply_really_big_numbers_110939.html) to multiply 2 ***large numbers*** ? 

**[Anatoly Alexeyevich Karatsuba](https://en.wikipedia.org/wiki/Anatoly_Karatsuba)** proposed a [solution](https://mathworld.wolfram.com/KaratsubaMultiplication.html).

---
**Example :** Assume $x = 5142$ and $y = 2048$

then, 
$x = 51 \times 100 + 42$ , here we say $x_{high} == 51$ and $x_{low} == 42$ 
	
and 

$y = 20 \times 100 + 48$ , here we say $y_{high} == 20$ and $y_{low} == 48$

Assuming $n$ is $even$, In general,
	 $x = x_h \times 10^{\frac{n}{2}} + x_l$
	and
	$y = y_h \times 10^{\frac{n}{2}} + y_l$

Thus, 
$x\times y = (x_h\cdot 10^{\frac{n}{2}} + x_l) \times (y_h \cdot 10^{\frac{n}{2}} + y_l)$
$= (x_h \cdot y_h \cdot 10^n) + (x_h \cdot y_l + x_l \cdot y_h)\cdot 10^\frac{n}{2} + x_l\cdot y_l$

Hence, the total time spent, $T(n) = 4\cdot T(\frac{n}{2})+ O(n)$

$4\cdot T(\frac{n}{2})$ : for 4 multiplications, and 

$O(n)$ : for 1 addition
 
 This could lead to $T(n) = O(n^2)$
 
 But if instead of the $4$ multiplications, we can reduce them to $3$, then, the total time spent becomes, $T(n) = 3\cdot T(\frac{n}{2})+ O(n)$, which leads to $T(n) = O(n^{1.585})$.

---
# Induction :

 