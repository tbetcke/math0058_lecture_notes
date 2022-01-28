# Week 3 Self check questions and solutions

**Question 1:**

Let $A\in\mathbb{R}^{n\times n}$. Proof that the LU decomposition exists with nonsingular $L$ and $U$ if and only if the determinant of all minors is nonzero.
(Note: The minors are the submatrices $A[:m, :m]$).

Does the LU decomposition exist for the following matrix? Justify your answer. 

$$
\begin{bmatrix}
0.5 &   -2 &   2 \\
-1 & 4 & -5\\
9&  -5& 8 
\end{bmatrix}
$$

**Solution:**

First assume that the LU Decomposition exists. We then have $A = LU$ with nonsingular $L$ and $U$ and hence, for each minor $A[:m, :m] = L[:m, :m]\times U[:m, :m]$.
Since $L$ and $U$ are nonsingular it follows that also the minors are nonsingular and therefore have nonzero determinant.

Now assume that all minors have nonzero determinant. We proceed by induction. Let the statement be true for all matrices have dimension $n-1$. We now partition $A\in\mathbb{R}^{n\times n}$ as

$$
A = \begin{bmatrix}\hat{A} & b\\
                   c^T & \gamma
    \end{bmatrix}
=
\begin{bmatrix}\hat{L} & 0\\
               \ell^T & 1
\end{bmatrix}
\begin{bmatrix}\hat{U} & r\\
               0   & \delta
\end{bmatrix}
$$

with $b,c, \ell, r\in\mathbb{R}^{n-1}$, $\gamma, \delta\in\mathbb{R}$, $\hat{L}, \hat{U}\in\mathbb{R}^{n-1\times n-1}$. Here $\hat{A} = \hat{L}\times\hat{U}$ is a nonsingular LU decomposition of
$\hat{A}$, which exists by induction hypothesis. To construct an LU decomposition of dimension $n$ we need to find $\ell$, $r$ and a nonzero $\delta$ such that the above decomposition is valid.

By inspection we obtain $r=\hat{L}^{-1}\hat{b}$ and $\ell^T = c^T\hat{U}^{-1}$, which exists since $\hat{L}$ and $\hat{U}$ are nonsingular. For $\delta$ we have the expression

$$
\delta = \gamma - l^Tr = \gamma - c^T\hat{A}^{-1}b.
$$

Since $\hat{A}$ is nonsingular $\delta$ exists. It is left to show that $\delta\neq 0$. However, this follows from

$$
\det A = \delta \det\hat{L}\det{\hat{U}} = \delta\det\hat{A}
$$

and that $\det A$ and $\det\hat{A}$ are nonzero by induction hypothesis.


For the matrix 

$$
\begin{bmatrix}
0.5 &   -2 &   2 \\
-1 & 4 & -5\\
9&  -5& 8 
\end{bmatrix}
$$

the first $2\times 2$ subblock is singular. Hence, its determinant is zero and therefore the LU decomposition does not exist.

**Question 2:**

Let $A\in\mathbb{R}^{n\times n}$ be tridiagonal, that is only the main diagonal and the first upper and lower off-diagonals can be nonzero.
    Assume that an LU decomposition exists. Show that it can be computed in $\mathcal{O}(n)$ operations.
    
**Solution**

In each outer loop of the Gaussian elimination only one off-diagonal element needs to be reduced. Hence, the cost for each outer loop is constant and independent of $n$, leading to a total cost of $\mathcal{O}(n)$.

**Question 3:**

Proof the Sherman-Morrison formula

$$
(A+uv^T)^{-1} = A^{-1} - \frac{A^{-1}uv^TA^{-1}}{1+v^TA^{-1}u}
$$

if $1+v^TA^{-1}u\neq 0$.

**Solution:**

We have

$$
\begin{aligned}
    (A+uv^T) \left[A^{-1} - \frac{A^{-1}uv^TA^{-1}}{1+v^TA^{-1}u}\right] &= \\
    I - \frac{uv^TA^{-1}}{1+v^TA^{-1}u} + uv^TA^{-1} - uv^T\frac{A^{-1}uv^TA^{-1}}{1+v^TA^{-1}u} &=\\
    I - \left[\frac{uv^TA^{-1} + uv^TA^{-1}uv^TA^{-1}}{1+v^TA^{-1}u} - uv^TA^{-1}\right] &= \\
    I - u\left[\frac{1+v^TA^{-1}u}{1+v^TA^{-1}u} -1\right]v^TA^{-1}&=\\
    I
\end{aligned}
$$


Similarly, we show that


$$
\begin{aligned}
    \left[A^{-1} - \frac{A^{-1}uv^TA^{-1}}{1+v^TA^{-1}u}\right](A+uv^T) &= \\
    I - A^{-1}u\left[\frac{1 + v^TA^{-1}u}{1+v^TA^{-1}u} - 1\right]v^T &= \\
    I
\end{aligned}
$$

Hence, the formula holds.

