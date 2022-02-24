# The Schur decomposition

The eigenvalue decomposition $A = X\Lambda X^{-1}$ is often not useful for computational purposes.
First of all, it may not exist at all but rather only a Jordan normal form. 
While in floating point arithmetic the small machine perturbations tend to ensure that the actual matrix
is diagonalizable, the effects of a nearby Jordan form nevertheless lead to instabilities. Furthermore,
the matrix $X$ of eigenvectors may be ill-conditioned and therefore the inverse not well determined
computationally.

A more practical decomposition for computations is the Schur decomposition of $A$.

## Formulation and properties of the Schur decomposition

Let $A\in\mathbb{C}^{n\times n}$. The Schur decomposition of $A$ is given as

$$
A = QRQ^H
$$

with $Q\in\mathbb{C}^{n\times n}$ unitary and $R\in\mathbb{C}^{n\times n}$ upper triangular.

Before we prove the Schur decomposition let us discuss some of its properties.

- The diagonal values of $R$ are the eigenvalues of $A$. This follows from 
$\det (\lambda I - A) = \det Q \det Q^H \det (\lambda I-R)$ and expanding the last determinant along the
diagonal.
- If $A$ is Hermitian then the Schur decomposition is an eigenvalue decomposition since from $A=A^H$
it follows that $R=R^H$, which for upper triangular matrices is only possible if they are diagonal.
The first column of $Q$ is the eigenvector associated with the upper diagonal element $r_{11}$ of $R$.
- Let $R_k$ be the upper left $k\times k$ principal submatrix of $R$ and $Q_k\in\mathbb{C}^{n\times k}$ the
matrix of the first $k$ columns of $Q$. We have that $AQ_k = Q_kR_k$. Hence, for every $v\in \text{span}\{q_1, \dots, q_k\}$
we have that $Av\subset \text{span}\{q_1, \dots, q_k\}$. We also say that this subspace is invariant under $A$.
It follows that the Schur decomposition defines a sequence of growing invariant subspaces.

## Existence proof for the Schur decomposition

Proving the existence of the Schur decomposition is astonishingly easy. Consider an eigenvalue $\lambda$
with associated eigenvector $x$ such that $\|x\|_2=1$. We define the matrix $Q$ as

$$
Q = \begin{bmatrix}x & \hat{Q}\end{bmatrix}
$$

with $\hat{Q}$ formed of orthogonal columns that are a basis of $\text{span}\{x\}^\bot$. Computing
$Q^HAQ$ gives

$$
Q^HAQ = \begin{bmatrix}\lambda &w\\
                        0      & \tilde{A}
        \end{bmatrix}
$$

The matrix $\tilde{A}$ is of dimension $n-1$. We can hence use an induction argument and assume that the
Schur decomposition of $\tilde{A}$ exists with $\tilde{A} = \tilde{Q}\tilde{R}\tilde{Q}^H$.

We obtain

$$
A = Q\begin{bmatrix}1 & \\  & \tilde{Q}\end{bmatrix}\begin{bmatrix}\lambda & w \\  & \tilde{R}\end{bmatrix}
    \begin{bmatrix}1 & \\ & \tilde{Q}^H\end{bmatrix}Q^H
$$

as Schur decomposition of $A$. We still need to fix the induction start. But if $A$ is a scalar $\alpha$ then
the Schur decomposition is simply $\alpha = 1 \cdot \alpha \cdot 1$.



