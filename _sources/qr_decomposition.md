# The QR Decomposition

## Orthogonal matrices

Let $Q\in\mathbb{R}^{n\times n}$. $Q$ is called *orthogonal* if $Q^TQ=I$. Hence, all rows and columns of $Q$ have unit length,
and the columns of $Q$ are mutually orthogonal. Orthogonal transformations are angle and 2-norm preserving. We can see this as follows. Denote by $\langle x, y\rangle := y^Tx$ the
usual Euclidian inner product. We have

$$
\langle Qx, Qy\rangle = \langle x, Q^TQy\langle = \langle x, y\rangle.
$$

Preservation of norm follows from $\|Qx\|_2^2 = \langle Qx, Qx\rangle = \langle x, x\rangle = \|x\|_2^2$.

## The QR Decomposition

Consider $A\in\mathbb{R}^{m\times n}$, $m\geq n$. We want to orthogonalise the colunmns of $A$. The following algorithm is called *Gram-Schmidt* orthogonalisation.

Let $\tilde{q}_1 :=a_1$ be the fst column of $A$.

- Define $q_1 := \frac{\tilde{q}_1}{\|\tilde{q}_1\|_2}$
- The column $q_2$ is computed by orthogonalizing $a_2$ against $q_1$.
    $$
    \begin{aligned}
    \tilde{q}_2 &:= a_2 - \langle a_2, q_1\rangle q_1\\
    q_2 &:= \frac{\tilde{q}_2}{\|\tilde{q}_2\|_2}.
    \end{aligned}
    $$
- For the column $q_3$ we need to orthogonalize against $a_3$ against $q_1$ and $q_2$, that is
    $$
    \begin{aligned}
    \tilde{q}_3 &:= a_3 - \langle a_3, q_1\rangle q_1 - \langle a_3, q_2\rangle q_2\\
    q_3 &:= \frac{\tilde{q}_3}{\|\tilde{q}_3\|_2}.
    \end{aligned}
    $$
- For column $q_k$ we correspondingly obtain
    $$
    \begin{aligned}
    \tilde{q}_k &:= a_k - \sum_{j=1}^{k-1}\langle a_k, q_j\rangle q_j\\
    q_3 &:= \frac{\tilde{q}_3}{\|\tilde{q}_3\|_2}.
    \end{aligned}
    $$

We can write this procedure as a matrix decomposition. From the above we have that

$$
\begin{aligned}
a_1 &= \|\tilde{q}_1\|_2q_1\\
a_2 &= \|\tilde{q}_2\|_2q_2 + \langle a_2, q_1\rangle q_1\\
a_k &= \|\tilde{q}_k\|_2q_k + \sum_{j=1}^{k-1}\langle a_k, q_j\rangle q_j
\end{aligned}
$$

It follows that 

$$
A = QR
$$

with 

$$
Q = \begin{bmatrix}q_1, \dots, q_n\end{bmatrix}
$$
having orthogonal columns and

$$
R = \begin{bmatrix}
\|\tilde{q}_1\|_2 & \langle a_2, q_1\rangle & \dots & \langle a_n, q_1\rangle\\
                  &  \|\tilde{q}_2\|_2 & \ddots & \vdots\\
                  &                    & \ddots & \\
                  &                    &        & \|\tilde{q}_n\|_2
\end{bmatrix}
$$

is an upper triangular matrix.

### Theorem (QR Decomposition)

Let $A\in\mathbb{R}^{m\times n}$, $m\geq n$. Then the QR decomposition $A=QR$ with
$Q\in\mathbb{R}^{m\times n}$, $Q^TQ = I$, $R\in\mathbb{R}^{n\times n}$ upper triangular, exists and is unique up to the choice of signs in the diagonal elements $r_{i,i}$.


## Solving linear systems of equations with the QR decomposition

Consider the linear system of equations $Ax = b$ with $A\in\mathbb{R}^{n\times n}$.
Let

$$
A = QR
$$

be the QR decomposition of $A$. We can use it as follows to solve the linear system of equations.

$$
\begin{aligned}
Ax &= b,\\
QRx &= b,\\
Rx &= Q^Tb.\\
\end{aligned}
$$
The last equation is a simple upper triangular system that can be solved by backward substitution.

**It can be shown that the solution of a linear system of equations via QR decomposition is always backward stable. But it is rarely done in practice as it is around twice as expensive as the LU decomosition.**

## Reduced vs full QR decomposition

Consider the QR decomposition $A = QR$ with $Q\in\mathbb{R}^{m\times n}$ and $R\in\mathbb{R}^{n\times n}$. We call this QR decomposition a reduced QR decomposition. To define the full QR decomposition let $Q^{\bot}\in\mathbb{R}^{m\times m-n}$ be a matrix whose columns are orthornomal and satisfy $\hat{Q}^TQ = 0$ (i.e. they are a basis of the orthogonal complement of the range of $A$). We can reformulate the QR decomposition as

$$
A = \begin{bmatrix}Q & Q^{\bot}\end{bmatrix}\begin{bmatrix}R\\ 0\end{bmatrix} =: \tilde{R}\tilde{Q}.
$$

The QR decomposition $A = \tilde{Q}\tilde{R}$ is called full QR decomposition. It is rarely used in practical computation as the columns of $Q^{\bot}$ are usually not required. But it is important theoretically, as $Q^{\bot}$ forms a square orthogonal (and therefore invertible) matrix and contains information about the range of $A$ and its orthogonal complement.

