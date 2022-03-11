# Perturbation results for eigenvalue problems

In this section we are discussing some classical eigenvalue perturbation bounds.
We start with condition numbers of eigenvalues and then provide eigenvalue perturbation
results for symmetric and nonsymmetric systems.



## Eigenvalue Condition numbers

Let $A\in\mathbb{C}^{n\times n}$ and $(\lambda, x)$ an eigenpair of $A$. Denote the associated left-eigenvector as $y$.
A left eigenvector satisfies $y^HA = \lambda y^H$.

Let $\lambda + \delta\lambda$ be an eigenvalue of the perturbed matrix $A+\Delta A$. Then to first order

$$
\delta\lambda = \frac{y^H\Delta Ax}{y^Hx}
$$

(see exercises for proof).

It follows that to first order

$$
|\delta\lambda| \leq \frac{\|x\| \|y\|}{|x^Hy|} \|\Delta A\|
$$

and we can define the absolute condition number $\kappa(\lambda) = \frac{\|x\| \|y\|}{|x^Hy|}$. 

Hence, if $x$ and $y$ are orthogonal then the condition number tends to infinity. Let us now investigate what
happens if $\lambda$ is a multiple eigenvalue. For simplicity assume that its algebraic multiplicity is the
same as its geometric multiplicity. Then we have two right eigenvectors $x_1$, and $x_2$, but also two left
eigenvectors $y_1$ and $y_2$. Moreover, any nonzero linear combination $\alpha_1 x_1 + \alpha_2 x_2$ is a
right eigenvector, and similarly any linear combination of $y_1$ and $y_2$ is a left eigenvector.

Assume that $y_1$ is not orthogonal to $x_2$ (otherwise, we already have an orthogonal pair of left and right
eigenvector). We can then solve

$$
y_1^H(x_1 - \alpha x_2) = 0,
$$

from which it follows that $y_1 \bot (x_1 - \frac{y_1^H x_1}{y_1^H x_2}x_2)$. As conclusion whenever we have
a multiple eigenvalue we can find a combination of left and right eigenvector that is orthogonal, demonstrating
that multiple eigenvalues are unstable to perturbations. This is intuitively clear. If we have a polynomial with
a multiple root then a small arbitrary perturbation in the coefficients will turn a multiple root into several simple
roots. If we have a Jordan form (that is the geometric multiplicity is smaller than the algebraic multiplicity) we can
do similar considerations.

## Eigenvalue perturbations and the resolvent

We define the resolvent fuction as $z\rightarrow (zI - A)^{-1}$ for $A\in\mathbb{C}^{n\times n}$. If $z$ is an eigenvalue
then the resolvent function is unbounded since $zI - A$ is not invertible in that case. It is interesting to
consider what happens with the resolvent function if $z$ is not an eigenvalue but close to an eigenvalue.

### Theorem 

The followin statements are equivalent.

1. $z$ is an eigenvalue of $A+\Delta A$ for some $\Delta A$ with $\|\Delta A\|_2\leq \epsilon$.
2. There exists a vector $u\in\mathbb{C}^n$ with $\|(A-zI)u\|_2 \leq \epsilon$ and $\|u\|_2=1$.
3. For the smallest singular value $\sigma_n$ of $(zI - A)$ we have that $\sigma_n\leq\epsilon$.
4. $\|(zI - A)^{-1}\|_2\geq \epsilon^{-1}$.

Statement 1 is about the existence of a nearby matrix with a slightly perturbed eigenvalue. Statement
2 is about the existence of a vector $u$ that satisfies $Au\approx \lambda u$ with only a small error. Statement 3 
is about the size of the smallest singluar value of $zI - A$ and statement 4 gives a lower bound on the size
of the resolvent function close to an eigenvalue.

This theorem shows that all these concepts are equivalent to each other. Let us give a proof.

Assume that statement 1 is true. We hence have

$$
(A + \Delta A) u = zu 
$$

for some $u$ with $\|u\|_2=1$ and $\|\Delta A\|_2\leq \epsilon$. Reordering gives 

$$
\|(A - zI)u\|_2 = \|\Delta A u\|_2 \leq \|\Delta A\|_2 \leq \epsilon
$$

showing statement 2. Now let us show that 3 follows from 2. From the exercises we know that

$$
\sigma_n = \min_{u\in\mathbb{C}^n, \|u\|_2=1} \|(zI - A)u\|_2
$$

Using Statement 2 it follows immediately that $\sigma_n \leq \epsilon$.

4 now follows from 3 since 

$$
\|(zI - A)^{-1}\|_2 = \sigma_n^{-1} \geq \sigma_n^{-1}.
$$

Finally, we need to prove that 1 follows from 4 to establish equivalence of all statements.

We have from statement 4 that there exist $u$, $v$ with $\|u\|_2=\|v\|_2=1$ and $\hat{\epsilon}\leq \epsilon$
such that

$$
(zI-A)^{-1}v = \hat{\epsilon}^{-1}u.
$$

It follows that $\epsilon v = (zI-A)u$ and therefore 

$$
(A + \hat{\epsilon}vu^H)u = zu.
$$

Statement 1 therefore follows with $\Delta A = \hat{\epsilon}vu^H$.

## The Bauer-Fike Theorem

Let $A\in\mathbb{C}^{n\times n}$ be diagonalizable with $AX = X\Lambda$, $\Lambda\in\mathbb{C}^{n\times n}$ diagonal,
and $\Delta A$ a perturbation of $A$. For every eigenvalue $z$ of $A+\Delta A$
there exists an eigenvalue $\lambda$ of $A$ such that

$$
|z-\lambda| \leq \|X\|_2 \|X^{-1}\|_2 \|\Delta A\|_2.
$$

Before we prove this statement let us briefly reflect on it. The statement shows that the condition number of the
eigenvector matrix $X$ determines by how much we can expect arbitrary eigenvalues to be perturbed under perturbations of $A$.

This result is related to the eigenvalue condition number. From $AX = X\Lambda$ it follows that $X^{-1}A = X^{-1}\Lambda$. Hence, the rows of $X^{-1}$ are the left eigenvectors
of the matrix $A$. The Bauer-Fike theorem therefore gives a sharp bound for the maximum perturbation of any eigenvalue
based on the norm of the matrix of right eigenvectors and the matrix of left eigenvectors.

The eigenvalue condition number in contrast uses the angle between left and right eigenvector to give a first order bound for each
individual eigenvalue.

The proof of the Bauer-Fike theorem is straight forward using our previous perturbation bounds. From $z$ being an
eigenvalue of $A+\Delta A$ it follows that

$$
\begin{aligned}
\|\Delta A\|_2^{-1}&\leq \|(zI - A)^{-1}\|_2\\ 
                &\leq \|(zI - X\Lambda X^{-1})^{-1}\|_2\\
                &\leq \|X\|_2\|X^{-1}\|_2 \|(zI - \Lambda)^{-1}\|_2\\
                &= \|X\|_2\|X^{-1}\|_2 |z-\lambda|^{-1} 
\end{aligned} 
$$ 

for an eigenvalue $\lambda$ of $A$. Reordering gives the desired statement.

## Perturbation bounds for Hermitian eigenvalue problems

If a matrix $A$ is Hermitian (that is $A^H=A$) then from the Schur decomposition it follows that

$$
A = Q\Lambda Q^H
$$

with $Q^HQ = I$. Moreover, the left eigenvectors are identical to the right eigenvectors.
Hence, if $\lambda$ is a not a multiple eigenvalue of $A$ then we have that $\kappa(\lambda)=1$.
Similarly, the Bauer-Fike theorem simplifies to $|z-\lambda| \leq \|\Delta A\|_2$, showing that
eigenvalues of symmetric matrices are at most perturbed by the size of the input perturbation.

### Rayleigh-Quotient for Hermitian eigenvalue problems

Let $A\in\mathbb{R}^{n\times n}$ be a symmetric matrix (that is $A=A^T$). Define the Rayleigh quotient

$$
r(x) = \frac{x^TAx}{x^Tx}.
$$
 
The Rayleigh quotient has a powerful property. First of all it is straight forward to see that if $x$ is an 
eigenvector then $r(x) = \lambda$. What happens if instead of $x$ we apply a small perturbation $\tilde{x} = x + \epsilon$?
We then obtain

$$
r(\tilde{x}) = \lambda + \mathcal{O}(\epsilon^2).
$$

It follows that if we know the eigenvector only up to an accuracy of $\epsilon$ we can still extract the
eigenvalue up to an accuracy of $\mathcal{O}(\epsilon^2)$. This is exploited in
numerical algorithms to compute eigenvalues with high accuracy for Hermitian problems.

The proof of this statement is rather simple. All it says is that $\nabla r(x) = 0$ if $x$ is an eigenvector. The
rest follows from Taylor's theorem. So let's compute the derivative of $r(x)$.

We have that

$$
(x + \epsilon)^HA(x + \epsilon) = x^HAx + 2x^HA\epsilon + \epsilon^HA\epsilon.
$$

Hence, $(x^TAx)' = 2x^TA$ for a symmetric matrix $A$ (convince yourself that we needed to use the
property that $A$ is symmetric for this derivation).

Applying the quotient rule we now get that

$$
\nabla r(x) =  \frac{2}{\|x\|_2^2}\left[Ax - r(x)x\right].
$$

Hence, if $x$ is an eigenvector, using that then $r(x) = \lambda$ we obtain $\nabla r(x) = 0$.




