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

**Solution: **

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



