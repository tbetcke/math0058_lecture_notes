# Least Squares Problems

Let $A\in\mathbb{R}^{m\times n}$ with $m\geq n$ and $b\in\mathbb{R}^m$.
In the following we assume that $\text{rank}(A) = n$.

We define the following leasts-squares problem

$$
\hat{x} = \text{arg}\min_{x\in\mathbb{R}^n} \|Ax-b\|_2.
$$

## The normal equation

Assume that $\hat{x}$ is a minimizer. Let $\epsilon\in\mathbb{R}^n$ be a small
perturbation. Then

$$
\begin{aligned}
\|A(\hat{x} + \epsilon) - b\|_2^2 &= \left[A(\hat{x} + \epsilon) - b\right]^T\left[A(\hat{x} + \epsilon) - b\right]\\
                                  &= \|A\hat{x} -b \|_2^2+2 \epsilon^T(A^TA\hat{x} - A^Tb) + \epsilon^TA^TA\epsilon
\end{aligned}
$$

It follows that a necessary condition for $\hat{x}$ to be a minimum is that

$$
A^TA\hat{x} - A^Tb = 0.
$$

Since $\epsilon^TA^TA\epsilon = \|A\epsilon\|_2^2 > 0 \forall \epsilon\neq 0$
the necessary condition is also sufficient.

The system

$$
A^TA\hat{x} = A^Tb
$$

is called the normal equation for the least-squares problem.

## Properties of the normal equation


Let $A = U\Sigma V^T$ be the SVD of $A$. As generalization of 
the relative condition number of a square matrix we can define the relative
condition number for a rectangular matrix as $\kappa_{rel}(A):=\sigma_1/\sigma_n$.


We have 

$$
A^TA = V\Sigma^T\Sigma V^T
$$

as SVD of $A$. Hence, $\kappa_{rel}(A^TA) = \sigma_1^2 / \sigma_n^2 = \kappa_{rel}(A)^2$.

It follows that the linear system in the normal equation has a squared condition number
compared to the original matrix $A$. In the following, we discuss orthogonalization methods that
avoid this squaring of condition number.

## Solving least-squares problems with the QR decomposition

Let the full QR decomposition of $A$ be given as

$$
A = \begin{bmatrix} Q_1 & Q_2 \end{bmatrix}\begin{bmatrix}R\\ 0\end{bmatrix}
$$

Substitute into the least-squares problem to obtain

$$
\|Ax - b\| = \|Q\begin{bmatrix}R\\ 0\end{bmatrix}x - b\|_2 = \|\begin{bmatrix}R \\ 0\end{bmatrix}x - Q^Tb\|_2.
$$

The last term gives

$$
\|\begin{bmatrix}R\\ 0\end{bmatrix}x - Q^Tb\|_2 = \|\begin{bmatrix}R\\ 0\end{bmatrix}x - \begin{bmatrix}Q_1^Tb\\ Q_2^Tb\end{bmatrix}\|_2.
$$

We see that we can only influence the first block-line with $x$. In the second line $x$ is multiplied with zero and therefore no choice of $x$
would reduce the contribution from there. Hence, the minimizer is the solution of the problem

$$
Rx = Q_1^Tb.
$$

It is possible to show (see exercises) that $R$ has the same condition number as $A$. Hence, we avoid the squaring of 
condition number from the normal equation.

## Solving least-squares problems with the SVD

The SVD can also be used to solve least-squares problems. This will lead us to an important concept, namely
the *pseudo-inverse* of a matrix.

Let $A = U\Sigma V^T$ be the SVD of $A$. Substitute into the least-squares problem to obtain

$$
\|Ax-b\|_2 = \|U\Sigma V^Tx - b\|_2.
$$

Let $y=V^Tx$ and factorise out $U$ to obtain

$$
\|Ax - b\|_2 = \left\|\begin{bmatrix}\tilde{\Sigma}\\ 0\end{bmatrix}y - \begin{bmatrix}U_1^Tb\\ U_2^Tb\end{bmatrix}\right\|_2.
$$

Hence, $y = \tilde{\Sigma}^{-1}U_1^Tb$ and therefore 

$$
x = V\tilde{\Sigma}^{-1}U_1^Tb = V\begin{bmatrix}\tilde{\Sigma}^{-1} & 0\end{bmatrix}U^Tb.
$$

We define the pseudo-inverse of $A$ as 

$$
A^{\dagger} := V\begin{bmatrix}\tilde{\Sigma}^{-1} & 0\end{bmatrix}U^T.
$$

The pseudo-inverse of $A$ is a generalization of the inverse of $A$.
In the same way that $A^{-1}b$ solves the linear system $Ax=b$ for a square
matrix $A$, the pseudo-inverse $A^{\dagger}$ applied to $b$ solves the least-squares minimisation problem 
$\|Ax-b\|_2$ for rectangular $A$.








