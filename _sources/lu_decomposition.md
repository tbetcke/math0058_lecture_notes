# Solving linear system with the LU Decomposition

Solving linear systems of equations is among the most fundamental operations in a computer. Many problems (even nonlinear ones) evenutally reduce to sequences of linear system solves.

Most students learn about Gaussian elimination in their first Calculus modules. The LU decomposition is simply a more organised way to perform Gaussian elimination.

## Basic idea

We consider the linear system of equations

$$
Ax = b
$$

with $A\in\mathbb{R}^{n\times n}$. LU Decomposition works in the same way for complex matrices. So this is not a restriction. We also have $x, b\in\mathbb{R}^n$. Throughout we assume that $A$ is nonsingular.

Many techniques in Numerical Linear Algebra are based on finding suitable decompositions of matrices into products of simpler matrices. The same applies to the LU Decomposition.

Let

$$
A = LU
$$

be a decomposition of $A$ into the product of two matrices $L$ and $U$.

We obtain the new system

$$
LUx = b
$$

To solve this system we now have to solve two matrix problems,
namely

$$
Ly = b
$$

and 

$$
Ux = y.
$$

This seems cumbersome. Instead of one linear system. We now have two. However, the trick is to choose a decomposition that makes solving linear systems with $L$ and $U$ particularly easy.

In the LU decomposition $L$ will be a lower triangular matrix, that is nonzero elements are only on the diagonal and below the diagonal. $U$ will correspondingly be an upper triangular matrix.

## Solving an upper triangular system of equations

Assume we have upper triangular $U$. We want to solve $Ux = y$.

The equations are

$$
\begin{aligned}
u_{n,n}x_n &= y_n\\
u_{n-1,n-1}x_{n-1} + u_{n-1, x}x_n &= y_{n-1}\\
\dots &= \dots\\
\sum_{j=i}^n u_{i, j}x_j &= y_i.
\end{aligned}
$$

Hence, we start by solving for $x_n$ to obtain $x_n = y_n / u_{n, n}$ and then work our way up so that for $x_i$ we have

$$
x_i = \frac{y_i - \sum_{j=i + 1}^n u_{i, j}x_j}{u_{i, i}}.
$$

What is the cost of this triangular solve? We are counting the number of additions, subtractions, multiplications, and divisions.

In step $i$ we have $n-i$ multiplications, one subtraction (apart from the first step) and one division. Hence, the overall number $ops$ of operations is

$$
ops = 2n - 1 + \sum_{i=1}^n n-i,
$$

where $2n-1$ is the number of subtractions and divisions and in the sum we have the number of multiplications.

We can easily compute this to obtain

$$
ops = 2n-1 + n^2 - \frac{n(n+1)}{2} = \frac{n^2}{2}+\frac{3}{2}n - 1.
$$

## Deriving the LU Decomposition

We still don't know how to compute the LU decomposition itself. This will be done in the following.

### A review of Gaussian elimination

Consider the following $3\times 3$ linear system of equations

$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13}\\
a_{21} & a_{22} & a_{23}\\
a_{31} & a_{32} & a_{33}
\end{bmatrix}
\begin{bmatrix}
x_1\\ x_2 \\ x_3
\end{bmatrix}
= \begin{bmatrix}b_1 \\ b_2 \\ b_3\end{bmatrix}.
$$

We want to transform this system into an upper triangular system.
In the first step we multiply the first row with $\ell_{21} = \frac{a_{21}}{a_{11}}$ and subtract from the second row to obtain the
modified system

$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13}\\
0 & \tilde{a}_{22} & \tilde{a}_{23}\\
a_{31} & a_{32} & a_{33}
\end{bmatrix}
\begin{bmatrix}
x_1\\ x_2 \\ x_3
\end{bmatrix}
= \begin{bmatrix}b_1 \\ \tilde{b}_2 \\ b_3\end{bmatrix}
$$

with

$$
\tilde{a}_{22} = a_{22} - l_{21}a_{12}, \quad \tilde{a}_{23} = a_{23} - \ell_{21}a_{13}
$$

and $b_2$ modified correspondingly. We then define $\ell_{31} = \frac{a_{31}}{a_{11}}$ and proceed in a similar way with the third row to obtaiin

$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13}\\
0 & \tilde{a}_{22} & \tilde{a}_{23}\\
0 & \tilde{a}_{32} & \tilde{a}_{33}
\end{bmatrix}
\begin{bmatrix}
x_1\\ x_2 \\ x_3
\end{bmatrix}
= \begin{bmatrix}b_1 \\ \tilde{b}_2 \\ \tilde{b}_3\end{bmatrix}.
$$

We now continue in the same way with the bottom right matrix. Define the element $\ell_{32} = \frac{\tilde{a}_{32}}{\tilde{a}_{22}}$, multiply the second row with it and subtract from the third row, giving at the end an upper triangular system of the form

$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13}\\
0 & \tilde{a}_{22} & \tilde{a}_{23}\\
0 & 0 & \hat{a}_{33}
\end{bmatrix}
\begin{bmatrix}
x_1\\ x_2 \\ x_3
\end{bmatrix}
= \begin{bmatrix}b_1 \\ \tilde{b}_2 \\ \hat{b}_3\end{bmatrix}.
$$

We can now easily solve this system by backward substitution to compute first $x_3$, then $x_2$, and finally $x_1$.

## Formalising Gaussian elimination

We now introduce a different way of writing Gaussian elimination
that will directly lead us to the LU decomposition.

The key to Gaussian elimination is the subtraction of the multiple of one row from another row. Define

$$
L_{21} := I - \ell_{21}e_2e_1^T,
$$

Here, the vector $e_j$ is the $j$-th unit vector, which has a $1$ at position $j$ and zeros otherwise.

If we form the product $L_{21}A$ it is straight forward to see that the result is a matrix, where $\ell_{21}$ times the first row is subtracted from the second row. The reason is that $e_1^TA$ picks out the first row of $A$, and then the multiplication $e_2e_1^TA$ creates a new matrix whose second row is the first row of $A$, and zeros otherwise.

We can now write the continued subtraction of multiples of one row from another to achieve at an upper triangular matrix as

$$
U = L_{n, n-1}\dots L_{32}\dots L_{n1}\dots L_{31}L_{21}A.
$$

Define

$$
L := L_{21}^{-1}L_{31}^{-1}\dots
$$

to obtain

$$
A = LU.
$$

We know by construction that $U$ is upper triangular. But what
is the structure of $L$? First of all, we have that

$$
L_{i, j}^{-1} = I + \ell_{i, j}e_ie_j^T.
$$

This follows from 

$$
(I + \ell_{i, j}e_ie_j^T)(I - \ell_{i, j}e_ie_j^T) = I.
$$

We can now simplify $L$ to

$$
\begin{aligned}
L &= (I + \ell_{21}e_2e_1^T)(I + \ell_{31}e_3e_1^T)\dots\\
  &= I + \ell_{21}e_2e_1^T + \ell_{31} e_3e_1^T\dots
\end{aligned}
$$

Hence, $L$ is a lower triangular matrix whose diagonal is just
the identity matrix and where at position $(i, j)$ we have the
entry $\ell_{i, j}$, a remarkably simple structure, and exactly
what we need.

## The complete algorithm

Consider we want to solve the linear system

$$
Ax = b
$$

In the first step we compute the LU decomposition

$$
A = LU
$$

by Gaussian elimination and storing the $\ell_{ij}$ multipliers for each row in the corresponding position of the $L$ matrix.

We then solve $Ly=b$ by forward substitution, that is first we
solve for $y_1$, then for $y_2$, etc. The algorithm is very similar to the triangular solve that we discussed earlier. We
just have to proceed from the first entry to the last entry of
$y$ since the matrix is now lower triangular. Moreover, since all diagonal entries are $1$ we do not need to divide by $L_{ii}$.

We then solve $Ux=b$ by backward substitution.

## Cost of the LU Decomposition

We have already established that a triangular solve
costs $\mathcal{O}(n^2)$ operations. For the computation of the decomposition $A=LU$ an operation count gives a cost of $\frac{2}{3}n^3 + O(n^2)$ operations. Hence, by far the dominating cost
is the LU decomposition itself. Once we have computed it the forward and backward solves are relatively much cheaper. If we want to solve many linear systems where the matrix $A$ never changes but the right-hand side $b$ changes, we only need to
compute the $LU$ decomposition once and can then forward and backward solve easily in each step.



