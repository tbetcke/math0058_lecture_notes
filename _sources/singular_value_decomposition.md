# The Singular Value decomposition

### Theorem (Singular Value Decomposition)

Let $A\in\mathbb{R}^{m\times n}$, $m\geq n$. Then $A$ has a singular value decomposition of the form

$$
A = U\Sigma V^T.
$$

Here $U\in\mathbb{R}^{m\times m}$ and $V\in\mathbb{R}^{n\times n}$ are orthogonal matrices. The matrix $\Sigma$ has the form

$$
\Sigma = \begin{bmatrix}\tilde{\Sigma}\\ 0 \end{bmatrix}
$$

with $\tilde{\Sigma} = \text{diag}(\sigma_1, \sigma_2, \dots, \sigma_r, 0, \dots, 0)$, and $r$ the rank of the matrix $A$.

The $\sigma_j$ are called singular values of $A$. The columns $v_j$ of $V$ are called right singular vectors. The columns $u_j$ of $U$ are called left singular vectors.

### Existence Proof

The proof proceeds via induction. Define $\sigma_1 := \|A\|_2$. In finite dimensions we know that there exists $v_1$, $\|v_1\|_2 = 1$, s.t. $Av_1 = \sigma_1 u_1$ for some $u_1\in\mathbb{R}^m$ with $\|u_1\|_2 = 1$. Now let $U_1$ and $V_1$ be orthogonal matrices of the form

$$
\begin{aligned}
V_1 &= \begin{bmatrix}v_1 & \hat{V}_1\end{bmatrix}\\
U_1 &= \begin{bmatrix}u_1 & \hat{U}_1\end{bmatrix}
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

The first inequality follows from the fact that $\|Ax\| / \|x\| \leq \|A\|$ by definition of a vector induced matrix.norm. The second inequality follows from ignoring the contribution of $Bw$ to the norm.

We therefore have that

$$
\sigma_1 = \|S\|_2 \geq \left(\sigma_1^2 + w^Tw\right)^{1/2}.
$$

It follows that 

$$
U_1^TAV_1 = \begin{bmatrix}\sigma_1 & 0\\
                           0 & B
            \end{bmatrix}.
$$

We now use an induction argument to assume that the SVD of $B$ exists with

$$
B = \hat{U}\hat{\Sigma}\hat{V}^T.
$$

Then

$$
A = U_1\begin{bmatrix}1 & 0 \\
                      0 & \hat{U}
        \end{bmatrix}
        \begin{bmatrix}\sigma_1 & 0\\
                       0        & \hat{\Sigma}
        \end{bmatrix}
        \begin{bmatrix}1 & 0\\
                       0 & \hat{V}^T
        \end{bmatrix}V_1^T.
$$

We now define 

$$U:= U_1\begin{bmatrix}1 & 0 \\
                      0 & \hat{U}
        \end{bmatrix},\quad V:=        \begin{bmatrix}1 & 0\\
                       0 & \hat{V}^T
        \end{bmatrix}V_1^T.
$$

The induction start is given by a single column vector if $m > n$ or a scalar if $m=1$. The theorem is trivially satisfied in both cases.

## Properties of the SVD

- The rank of $A$ is identical to $r$, the number of nonzero singular values.
- The nullspace $\text{null}(A)$ is given by $\text{null}(A):= \text{span}\{v_{r+1}, \dots, v_n\}$.
- The range of $A$ is given by $\text{ran}(A) := \text{span}\{u_1, \dots, u_r\}$.
- We have that $\|A\|_2 = \|U\Sigma V^T\|_2 = \|\Sigma\|_2 = \sigma_1$.
- Using that $\|Q_1AQ_2\|_F = \|A\|_F$ for orthogonal matrices $Q_1$, $Q_2$ it correspondingly follows that $\|A\|_F = \|\Sigma\|_F = \left(\sum_{j=1}^r\sigma_j^2\right)^{1/2}$.
As corollary we have that $\|A\|_2 \leq \|A\|_F \leq \sqrt{r}\|A\|_2$.
- If $A$ is invertible then $A^{-1} = V\Sigma^{-1}U^T$ and therefore $\|A^{-1}\| = \sigma_n^{-1}$. It follows for the matrix condition number $\kappa_{rel}(A)$ that $\kappa_{rel}(A) = \frac{\sigma_1}{\sigma_n}$. Moreover $\Delta A := -\sigma_n u_n v_n^T$ is the smallest possible perturbation such that $A+\Delta A$ is singular. Hence, the condition number is just the inverse of the smallest relative distance to the next singular matrix.

## SVD and low-rank approximation

We can rewrite $A = U\Sigma V^T$ as

$$
A = \sigma_1 u_1 v_1^T + \sigma_2u_2v_2^T + \dots + \sigma_r u_r v_r^T.
$$

Each of the involved terms $\sigma_j u_jv_j^T$ forms a rank-1 matrix. Define $A_\nu := \sum_{j=1}^\nu \sigma_j u_jv_j^T$ for $\nu\leq r$. We have that

$$
\|A - A_{\nu}\|_2 = \sigma_{\nu+1}.
$$

### Theorem

Let $A$ and $A_{\nu}$ be defined as above. Then

$$
\|A - A_{\nu}\|_2 = \min_{B\in\mathbb{R}^{m\times n}, \text{rank}(B)\leq\nu} \|A - B\|_2 = \sigma_{\nu+1}.
$$


## The reduced SVD 

Let $A\in\mathbb{R}^{m\times n}$. Write the full SVD as

$$
A = \begin{bmatrix}U_1 & U_2\end{bmatrix}\begin{bmatrix}\hat{\Sigma} & 0\\
                                                        0            & 0
                                         \end{bmatrix}
                                        \begin{bmatrix}V_1 & V_2\end{bmatrix}^T
$$

with $U := \begin{bmatrix}U_1 & U_2\end{bmatrix}\in\mathbb{R}^{m\times m}$ and $V:=\begin{bmatrix}V_1 & V_2\end{bmatrix}\in\mathbb{R}^{n\times n}$ are the orthogonal matrices from the SVD, and $\Sigma :=\begin{bmatrix}\hat{\Sigma} & 0\\0  & 0\end{bmatrix}$. The columns of $U_2$ form a basis for
the orthogonal complement of the range of $A$ and the columns of $V_2$ form the nullspace of $A$. We have $\hat{\Sigma}\in\mathbb{R}^{r\times r}$ a diagonal matrix with $\sigma_1, \dots, \sigma_r$ being its diagonal elements.

The *reduced SVD* is now defined as

$$
A = U_1\hat{\Sigma}V_1^T.
$$

For computational purposes knowledge of the reduced SVD (or dominant parts of it) is usually sufficient.


