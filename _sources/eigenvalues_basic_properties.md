# Basic properties of eigenvalue problems

## Definition and motivation

Let $A\in\mathbb{C}^{n\times n}$. An eigenvalue problem takes the form
to find $x\in\mathbb{C}^n$, $x\neq 0$ and $\lambda\in\mathbb{C}$ such that

$$
Ax = \lambda x.
$$

Eigenvalue problems arise naturally in the study of initial value problems.
Consider the problem of solving the ODE

$$
y' = Ay
$$

for $A\in\mathbb{C}^{n\times n}$ with $y(0) = y_0$.

By writing $y(t) = y_0e^{\lambda t}$ and substituting we obtain the
eigenvalue problem

$$
Ay_0 = \lambda y_0.
$$

When reasoning about eigenvalues it therefore makes sense to think of
eigenvalues not just as properties of matrices but as properties of
dynamical systems driven by the matrix $A$. This contrasts singular values,
which describe the mapping properties of a matrix $A$ and are therefore
intuitively quite distinct from eigenvalues.

# Characteristic polynomials, algebraic and geometric multiplicities

We can rewrite an eigenvalue problem in the form

$$
(\lambda I - A)x = 0.
$$

This has nontrivial solutions $x$ if and only if $\lambda I - A$ is singular, or
equivalently

$$
\det(\lambda I - A) = 0.
$$

We define the characteristic polynomial

$$
p(\lambda) := \det(\lambda I - A).
$$

By expanding the determinant we can see that $p$ is a polynomial of maximum
degree $n$. Denote the $j$the zero of $p$ as $\lambda_j$. We have that

$$
P(\lambda) = \prod_j (\lambda -\lambda_j)^\alpha_j,
$$

where $\alpha_j$ denotes the algebraic multiplicity of the $j$th root.
From the fundamental theorem of algebra we know that $n = \sum_j \alpha_j$.
Hence, if we count by multiplicities an $n\times n$ matrix has $n$ eigenvalues.

For eigenvalue problems also of relevance is the geometrix multicity $\beta_j$
of an eigenvalue $\lambda_j$. $\beta_j$ is defined as the dimension of the
nullspace of 

$$
\lambda_j I - A.
$$

If $\lambda_j$ is a single eigenvalue then this dimension is $1$.
If $\alpha_j >1$ we have that $\beta_j \leq \alpha_j$. More about this
relationship is obtained by discussing the Jordan normal form of a matrix,
which is not topic of this module.

## The eigenvalue decomposition

If $\alpha_j=\beta_j$ for all $j$ the following eigenvalue decomposition exists

$$
A = X\Lambda X^{-1},
$$

where $X\in\mathbb{C}^{n\times n}$ is a nonsingular matrix whose columns $x_j$ are
the eigenvectors of $A$ and $\Lambda$ is a diagonal matrix whose diagonal entries
are the associated eigenvalues $\lambda_j$.


