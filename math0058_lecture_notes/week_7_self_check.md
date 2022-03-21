# Week 7 Self check questions and solutions

**Question 1:**

Let $A\in\mathbb{C}^{n\times n}$ be diagonalizable and $\lambda$ an eigenvalue of $A$ with associated right eigenvector $x$ and left eigenvector $y$. Consider the perturbed eigenvalue equation 

$$
(A + \delta A)(x+ \delta x) = (\lambda + \delta \lambda)(x + \delta x).
$$

To first order show that $|\delta\lambda| \leq \frac{\|x\| \|y\|}{|y^H\delta Ax|}  \|\delta A\|$.

**Solution:**

We multiply out the perturbed eigenvalue equations and ignore higher order terms to obtain

$$
A\delta x + \delta A x = \lambda \delta x + \delta\lambda x.
$$

We now multiply from the left with $y^H$ and use that $y^HA = \lambda y^H$, resulting in

$$
y^H\delta A x = \delta\lambda y^Hx,
$$

from which we get

$$
\delta\lambda = \frac{y^H\delta A x}{y^Hx}.
$$

Taking norms we obtain the bound

$$
|\delta\lambda|\leq \frac{\|x\| \|y\|}{|y^Hx|} \|\delta A\|.
$$

This motivates the definition of the eigenvalue condition number $\kappa(\lambda)$ as

$$
\kappa(\lambda) = \frac{\|x\| \|y\|}{|y^Hx|}.
$$

**Question 2:**

Let $A = \begin{bmatrix}a & c\\0 & b\end{bmatrix}$ for real numbers $a, b, c$ and $a\neq b$. 
Show that the condition numbers of the eigenvalues of $A$ asymptotically 
grow like $|\frac{c}{b-a}|$ as $b\rightarrow a$.

**Solution:**

The eigenvalues are $\lambda_1 = a$ and $\lambda_2=b$ with corresponding right/left eigenvectors $x_1 = \begin{bmatrix}1 & 0\end{bmatrix}^T$, $y_1 = \begin{bmatrix}-1 & \frac{c}{b-a}\end{bmatrix}^T$, $x_2 = \begin{bmatrix}\frac{c}{a-b} & -1\end{bmatrix}^T$, $y_2 = \begin{bmatrix}0 & 1\end{bmatrix}^T$.

The condition number of an eigenvalue is given as $\kappa = \frac{\|x\|_2\|y\|_2}{|x^Hy|}$. We hence obtain for both eigenpairs that

$$
\kappa = \left(1 + \frac{c^2}{(b-a)^2}\right)^{1/2}.
$$

It follows that $\kappa\sim \left|\frac{c}{b-a}\right|$.

**Question 3:**

Show that the eigenvalues $\lambda$ of a Hermitian matrix are all real.

**Solution:**

Let $Ax= \lambda x$ for some eigenvalue $\lambda\in\mathbb{C}$ and $x\neq 0$ with $\|x\|_2=1$. 
Multiplying from the left with $x^H$ gives

$$
x^HAx = \lambda.
$$

Taking the Hermitian transpose on both sides we obtain (taking into account that a Hermitian trans
pose of a scalar is just its complex conjugate)

$$
x^HA^Hx = \overline{\lambda}.
$$

Since $A=A^H$ it follows that $\lambda = \overline{\lambda}$ and therefore that $\lambda$ is real.

We can also proceed directly through the Schur decomposition. The Schur decomposition is
$$
A = QR Q^T.
$$

Since $A=A^H$ it follows that $R=R^H$. Since $R$ is upper triangular it must be therefore diagonal.
Moreover, all the diagonal elements must be real since $R=R^H$. Since the eigenvalues are the diagonal
elements it follows that the eigenvalues are real. The Schur decomposition is therefore identical to the
eigenvalue decomposition $A= X\Lambda X^{-1}$ with $X=Q$ the matrix of eigenvectors.

**Question 4:**

Show that for a Hermitian matrix $A\in\mathbb{C}^{n\times n}$ we have

$$
x^HAx \in\mathbb{R}
$$

for all $x\in\mathbb{C}^{n}$. A Hermitian matrix is called positive definite if in addition
  $x^HAx> 0$ for all $x\in\mathbb{C}^{n}\backslash\{0\}$. Show that this is equivalent to the
  condition that all eigenvalues of $A$ are positive. Finally, conclude that for a Hermitian positive
  definite matrix it holds that $\det(A) > 0$.

**Solution:**

$A$ is Hermitian, hence $A=A^H$ and therefore for the complex conjugate $\overline{x^HAx}$ of $x^HAx$ we have

$$
\overline{x^HAx} = \left(x^HAx\right)^H  = x^HA^Hx = x^HAx.
$$

Hence, $\overline{x^HAx} = x^HAx$ and therefore $x^HAx$ must be real for any complex vector $x\in\mathbb{C}^n$.
It follows easily that if $A$ is Hermitian positive definite (that is $x^HAx>0$ for all $x\neq 0$)
all eigenvalues are positive. Let $\lambda_j$ be an eigenvalue with associated eigenvector $x_j$
and $\|x_j\|_2 = 1$. We have that

$$
\lambda_j = x_j^HAx_j > 0
$$

since the condition that $x^HAx$ is positive holds for all nonzero vectors, and therefore in particular also eigenvectors.

Now assume that all eigenvalues $\lambda_j$ are larger than zero. Let $x\in\mathbb{C}$. We expand $x$ in the basis of
eigenvectors and obtain $x = \sum_j \alpha_jx_j$. Assuming without loss of generality that
$\|x_j\|_2=1$ for all $j$ we have from the orthogonality of eigenvectors for Hermitian matrices that

$$
x^HAx = \sum_j\lambda_j|\alpha_j|^2 > 0.
$$

Finally, the determinant of a matrix is just the product of its
eigenvalues. We hence obtain that $\det(A) > 0$ if $A$ is Hermitian positive definite.

