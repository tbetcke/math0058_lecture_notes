# Week 1 Self check questions and solutions

**Question 1:**

Let $A\in\mathbb{R}^{m\times n}$. Proof that

* $\|A\|_1 = \max_j \sum_i|a_{ij}|$.
* $\|A\|_{\infty} = \max_i \sum_j|a_{ij}|$.

Note: It follows that $\|A\|_1 = \|A^T\|_{\infty}$.

**Solution:**

From the definition of a vector induced matrix norm we have that

$$
\begin{aligned}
\|A\|_1 &= \max_{\|x\|_1 = 1} \sum_i |\left[Ax\right]_i|\\
        &\leq \max_{\|x\|_1 = 1} \sum_{i} \sum_j |a_{ij}| |x_j|\\
        &= \max_{\|x\|_1 = 1}  \sum_j |x_j|\sum_i |a_{ij}|\\
        &\leq \max_j\sum_i |a_{ij}| \max_{\|x\|_1 = 1} \sum_j|x_j|\\
        &=\max_j\sum_i |a_{ij}|.
\end{aligned}
$$

It is left to show that this upper bound is attainable. But this can be easily accomplished. Let $\hat{j} = \text{argmax}_j \sum_i |a_{ij}|$ be the index $\hat{j}$ associated with the largest column sum. We then set $x_j = 0$ for $j\neq \hat{j}$ and $x_{\hat{j}} = 1$.

For $\|A\|_{\infty}$ we obtain

$$
\|A\|_{\infty} = \max_{\|x\|_{\infty} = 1} \max_i |\left[Ax\right]_i| \leq \max_i \sum_{j}|a_{ij}|.
$$

Let $\hat{i}$ be the row index for which the upper bound is attained. By choosing $x_j = \text{sign}~a_{\hat{i}j}$ we have that $\|Ax\|_{\infty} = \max_i \sum_{j}|a_{ij}|$, which confirms that the upper bound can be attained.

**Question 2:**

For the matrix $A = \begin{bmatrix} 2 & 3 \\ 0 & 1\end{bmatrix}$ compute $\|A|_p$ for $p=1, 2, \infty, F$.

**Solution:**

We have $\|A|_1 = 4$, $\|A|_{\infty} = 5$, $\|A|_F = \sqrt{14}$. For $\|A\|_2$ we compute the eigenvalues of

$$
A^TA = \begin{bmatrix}4 & 6\\ 6 & 10\end{bmatrix},
$$

giving us $\lambda_{1, 2} = 7 \pm 3\sqrt{5}$. Hence, $\|A\|_2 = \sqrt{7 + 3\sqrt{5}}$.

**Question 3:**

Show that $\|x\|_{\infty} = \lim_{p\rightarrow\infty} \|x\|_p$ for $x\in\mathbb{R}^n$.

**Solution:**

Let $\hat{j}$ be the index of the largest element by magnitude in $x$. We have that

$$
\lim_{p\rightarrow\infty} \|x\|_p = \lim_{p\rightarrow\infty} \left[ \sum_{j}|x_j|^p\right]^{1/p} = |x_{\hat{j}}|\lim_{p\rightarrow\infty} \left[1 +  \sum_{j\neq \hat{j}}|x/\hat{x}|^p\right]^{1/p} = |x_{\hat{j}}|.
$$

**Question 4:**

Explain the meaning of $\epsilon_{mach}$.

**Solution:**

$\epsilon_{mach}$ is defined as $\epsilon{mach} = \frac{1}{2}b^{1-p}$, which is half the distance of $1$ to the next floating point number. It is the maximum relative error of a real number $x$ and its closest floating point representation $x'$, that is

$$
|x - x'| \leq |x|\epsilon_{mach}.
$$

**Question 5:**

Why do double precision numbers  give you around 15 digits of accuracy? 

**Solution:**

We have $\epsilon_{mach} = 2^{-53}\approx 1.11E-16$ in double precision. Hence, the relative error of mapping a real number to its floating point representation is correct to around 15 digits.