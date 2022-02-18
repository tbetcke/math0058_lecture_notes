# Week 6 Self check questions and solutions

**Question 1:**

Let $A\in\mathbb{R}^{m\times n}$ with $m\geq n$ and $\text{rank}(A)=n$ and $b\in\mathbb{R}^m$. We define the following least-squares problem: 

Find $\hat{x}\in\mathbb{R}^n$, such that

$$
\|A\hat{x}-b\|_2 = \min_{x\in\mathbb{R}^n}\|Ax-b\|_2.
$$

**Solution:**

The SVD of $A$ is given as $A=U\Sigma V^T$, where $U\in\mathbb{R}^{m\times m}$ and $V\in\mathbb{R}^{n\times n}$ are orthogonal
matrices and $\Sigma \in\mathbb{R}^{m\times n}$ is a diagonal matrix with the nonzero singular values $\sigma_1\geq\sigma_2\geq\dots\geq\sigma_r$ in decreasing order on the diagonal of the matrix.

Let $A = U\Sigma V^T$. Substituting into the least-squares problem we have

$$
\|Ax-b\|_2 = \|U\Sigma V^Tx - b\|_2 = \|\Sigma y - \hat{b}\|_2
$$
        
for $y=V^Tx$ and $\hat{b} = U^Tb$. By minimizing the above expression we find $y_j$ as $y_j = \hat{b}_j/\sigma_j$. If $\sigma_j=0$ then we set $y_j=0$. This is equivalent to $y = \Sigma^{\dagger}\hat{b}$.
Substituting back in for $\hat{b}$ and $y$ we obtain $x = V\Sigma^{\dagger}U^Tb = A^{\dagger}b$.

**Question 2:**
    
We now consider the modified least-squares problem
$$\min_{x\in\mathbb{R}^n} \|Ax-b\|_2^2+\|L x\|_2^2$$
with $L\in\mathbb{R}^{n\times n}$ nonsingular.
Show that the solution of this least-squares problem is identical to the solution of
$$
(A^TA+L^TL)x = A^Tb.
$$

**Solution:**

The modified least-squares problem is identical to

$$
\min_{x\in\mathbb{R}^n}\left\|\begin{bmatrix}A\\L\end{bmatrix}x-\begin{bmatrix}b\\ 0\end{bmatrix}\right\|_2.
$$

Applying the normal equation to this problem we arrive at

$$
(A^TA+L^TL)x = A^Tb.
$$    

**Question 3:**

Let $A\in\mathbb{R}^{m\times n}$ with $m\geq n$. Show that the smallest singular value $\sigma_n$ of $A$ satisfies

$$
\sigma_n = \min_{x\in\mathbb{R}^n} \frac{\|Ax\|_2}{\|x\|_2}.
$$

**Solution:**
    
Using the SVD $A = U\Sigma V^T$ we can replace $A$ by the diagonal matrix $\Sigma$ since the 2-norm is invariant under orthogonal transformations. Let now $y$ be given with $\|y\|_2=1$. We have

$$
\|\Sigma y\|_2^2 = \sum_{j}\sigma_j^2y_j^2 \geq \sigma_n\sum_jy_j^2 = \sigma_n.
$$

This inequality becomes an equality for $y$ chosen to be the unit vector $e_n$. Hence, for $\Sigma$ diagonal the result follows and therefore for arbitrary $A\in\mathbb{R}^{m\times n}$ through the invariance of the norm under orthogonal transformations.

Notice the symmetry between smallest and largest singular value. By maximizing we obtain the largest singular value and by minimizing the smallest.

**Question 4:**

Let $A = QR$ be the QR decomposition of a matrix $A\in\mathbb{R}^{m\times n}$ with
$R\in\mathbb{R}^{n\times n}$. Show that the singular values of $A$ are identical to the singular values
of $R$.

**Solution:**

We use the full QR decomposition, that is let 

$$
A = \begin{bmatrix}Q & Q^{\bot}\end{bmatrix}\begin{bmatrix}R\\ 0\end{bmatrix}.
$$

Let $R = U\Sigma V^T$ be the SVD of $R$. Plugging into the above equation gives

$$
A = \begin{bmatrix}Q & Q^{\bot}\end{bmatrix}\begin{bmatrix}U & 0 \\ 0 & I\end{bmatrix}\begin{bmatrix}\Sigma \\ 0\end{bmatrix}V^T.
$$

We see that this is the singular value decomposition of $A$ with singular values contained in $\Sigma$.



