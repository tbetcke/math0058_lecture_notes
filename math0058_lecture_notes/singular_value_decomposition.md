# The Singular Value decomposition

### Theorem (Singular Value Decomposition)

Let $A\in\mathbb{R}^{m\times n}$, $m\geq n$. Then $A$ has a singular value decomposition of the form

$$
A = U\sigma V^T.
$$

Here $U\in\mathbb{R}^{m\times m}$ and $V\in\mathbb{R}^{n\times n}$ are orthogonal matrices. The matrix $\Sigma$ has the form

$$
\Sigma = \begin{bmatrix}\tilde{\Sigma}\\ 0 \end{bmatrix}
$$

with $\tilde{\Sigma} = \text{diag}(\sigma_1, \sigma_2, \dots, \sigma_r, 0, \dots, 0)$, with $r$ being the rank of the matrix $A$.

The $\sigma_j$ are called singular values of $A$. The columns $v_j$ of $V$ are called right singular vectors. The columns $u_j$ of $U$ are called left singular vectors.

### Existence Proof

The proof proceeds via induction.

Define $\sigma_1 = \|A\|_2$. In finite dimensions we know that there exists $v_1$, $\|v_1\|_2 = 1$, s.t. $Av_1 = \sigma_1 u_1$ for some $u_1\in\mathbb{R}^m$ with $\|u_1\|_2 = 1$. Now let $U_1$ and $V_1$ be orthogonal matrices of the form

$$
\begin{aligned}
V_1 &= \begin{bmatrix}v_1 & \tilde{V}_1\end{bmatrix}\\
U_1 &= \begin{bmatrix}u_1 & \tilde{U}_1\end{bmatrix}
\end{aligned}
$$

It follows that 

$$
S := U_1^TAV_1 = \begin{bmatrix}\sigma_1 & w^T\\
                            0       & B
            \end{bmatrix}.
$$
$w$ is some vector of dimension $n-1$. $B$ is a matrix of dimension $m-1\times n-1$. In order to proceed we need to show that $w=0$.

We have

$$
\begin{aligned}
\|S\|_2 &= \left\|\begin{bmatrix}\sigma_1 & w^T\\
                            0       & B
            \end{bmatrix}\right\|_2\\ 
        &\geq \frac{\left\|\begin{bmatrix}\sigma_1 & w^T\\
                                    0       & B
                    \end{bmatrix}\begin{bmatrix}
                    \sigma_1\\ w\end{bmatrix}\right\|_2}{\left(\sigma_1^2 + w^Tw\right)^{1/2}}\\
        &\geq \left(\sigma_1^2 + w^Tw\right)^{1/2}.
\end{aligned}
$$

The first inequality follows from the fact that $\|Ax\| / \|x\| \leq \|A\|$ by definition of a vector induced matrix norm.



