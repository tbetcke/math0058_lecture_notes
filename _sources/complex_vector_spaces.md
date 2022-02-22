# Complex vector spaces

Eigenvalues are often complex. It therefore makes sense in many
cases to pose problems in the context of complex vector spaces.

In this short section we want to highlight a few differences when dealing
with complex spaces.

## Inner products and norms

The complex equivalent of the usual Euclidian inner product is given as

$$
\langle x, y\rangle = \overline{y}^Tx = \sum_j x_j\overline{y_j}.
$$

Hence, we have to take the complex conjugate of $y$ when computing the
inner product.

Correspondingly, the $2$-norm of a vector is given by

$$
\|x\|_2 = \left(\sum_{j}x_j\overline{x_j}\right)^{1/2}
=\langle x, x\rangle^{1/2}.
$$

## Hermitian matrices

The equivalent of transposed matrices in complex vector spaces is 
the Conjugate Transpose of a matrix.
We have

$$
A^{H} := \overline{A}^T.
$$

With this definition it holds that

$$
\langle Ax, y\rangle = \langle x, A^Hy\rangle.
$$

We call a matrix Hermitian (or self-adjoint) if it holds that

$$
A^H = A.
$$

From this it follows that the diagonal elements of a Hermitian matrix must
be purely real.

## Orthogonal matrices

Since we have changed the definition of inner product the definition of
orthogonal matrices also changes. In complex vector spaces we call a matrix
$Q\in\mathbb{C}^{n\times n}$ *unitary* if

$$
Q^HQ = I.
$$

Hence, a unitary matrix is the complex equivalent of an orthogonal matrix.
