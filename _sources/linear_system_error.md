# Backward error and condition number of linear systems of equations

We consider the linear system of equations $Ay = b$ with $A\in\mathbb{R}^{n\times n}$ and $b\in\mathbb{R}^n$. We assume that $A$ is nonsingular.

## Backward error

For this linear system of equations the definition of the backward error is given as

$$
\eta(y) = \min \{\epsilon: A(y + \Delta y) = b + \Delta b, \|\Delta A\| \leq \epsilon \|A\|, \|\Delta b\|\leq \epsilon\|b\|\}.
$$

The backward error can be explicitly computed. The result goes back to Rigal and Gaches (1961). We do not show the full derivation here.

$$
\eta(\tilde{y}) = \frac{\|b - A\tilde{y}\|}{\|A\|\cdot \|\tilde{y}\| + \|b\|}
$$

The beauty of this result is that it only has computable quantities. The expression $r := b - A\tilde{y}$ is called the residual of the linear system. It measures how close the left- and right-hand side are. Residual expressions are typical in backward error results. 

## Condition Number

To derive a precise expression for the condition number of the linear system we need a little helper Lemma

### Lemma

Let $\|\cdot\|$ be a submultiplicative matrix norm and $X\in\mathbb{R}^{n\times n}$. Then $\|X\| < 1$ implies that $I - X$ is invertible, $(I-X)^{-1} = \sum_{i=0}^{\infty}X^i$ and $\|(I-X)^{-1}\| \leq \frac{1}{1-\|X\|}$.

**Proof**

We consider the partial sums

$$
S_n  = \sum_{i=0}^{n}X^{i}
$$

By norm equivalence and submultiplicativity we have that
$$
|(S_n)_{i, j}| \leq \sum_{i=0}^{n}\left|\left(X^n\right)_{i, j}\right|\leq \sum_{i=0}^n\max_{i, j}\left|\left(X^n\right)_{i, j}\right| \leq C\sum_{i=0}^{\infty}\|X^{n}\|\leq C\sum_{i=0}^\infty \|X\|^{n}= \frac{C}{1 - \|X\|}.
$$

for some $C> 0$.

Hence, every component of $S_n$ is absolutely convergent and therefore the sum $S_n$ converges with $X^{n}\rightarrow 0$ as $n\rightarrow\infty$.

For the inverse we have

$$
(I - X)S_n = I - X^{n+1}
$$
and by taking limits, with $S := \sum_{i=0}^{\infty}X^{i}$, we have that

$$
(I-X)S = I.
$$
It follows that $(I-X)$ is nonsingular with $(I-X)^{-1} = S$. The estimate

$$
\|(I-X)^{-1}\| \leq \frac{1}{1-\|X\|}
$$

follows from

$$
\|S\| \leq \sum_{i=0}^{\infty}\|X\|^{n} = \frac{1}{1-\|X\|}.
$$

We can now estimate the condition number of the linear system of equations $Ay=b$.
Let $\Delta A$ and $\Delta b$ be perturbations in $A$ and $b$, and let $\Delta y $ satisfy

$$
(A + \Delta A)(y + \Delta y) = b + \Delta b.
$$

Collecting terms and using that $Ay = b$ results in

$$
\begin{aligned}
\Delta y &= (A + \Delta A)^{-1}(-\Delta A y + \Delta b)\\
         &= \left[A(I + A^{-1}\Delta A)\right]^{-1}(-\Delta A y + \Delta b)\\
         &= \left(I + A^{-1}\Delta A\right)^{-1}A^{-1}(\Delta Ay+\Delta b).
\end{aligned}
$$

Assuming that $\Delta A$ is sufficiently small so that $\|A^{-1}\Delta A\| < 1$ we can 
apply the previous lemma and obtain

$$
\begin{aligned}
\frac{\|\Delta y\|}{\|y\|} &\leq \frac{\|A^{-1}\|}{1-\|A^{-1}\|\cdot \|\Delta A\|}\left(\|\Delta A\| + \frac{\|\Delta b\|}{\|y\|}\right)\\
&= \frac{\|A^{-1}\|\cdot \|A\|}{1-\|A^{-1}\| \cdot \|A\|\frac{\|\Delta A\|}{\|A\|}}\left(\frac{\|\Delta A\|}{\|A\|} + \frac{\|\Delta b\|}{\|b\|}\right),\end{aligned}
$$

where in the last equation we have used that $\|b\| = \|Ay\| \leq \|A\|\cdot\|y\|$.

By ignoring higher order terms in $\|\Delta A\|$ we obtain

$$
\frac{\|\Delta y\|}{\|y\|} \leq \|A^{-1}\|\cdot \|A\|\left(\frac{\|\Delta A\|}{\|A\|} + \frac{\|\Delta b\|}{\|b\|}\right).
$$
The left-hand side is the relative output perturbation. The right-hand side is the product of
$\|A^{-1}\|\cdot \|A\|$ and the relative input perturbation $\left(\frac{\|\Delta A\|}{\|A\|} + \frac{\|\Delta b\|}{\|b\|}\right)$. Hence, we have $\kappa(A) = \|A^{-1}\|\|A\|$ being the condition number of the linear system. This argument is not completely precise since
one still needs to show that there actually exists a perturbation so that the left-hand side and right-hand side have equality. But we leave this technical detail here out.

**Note: Since we also allow perturbations in $b$ we should formally write $\kappa(A, b)$ as
condition number. But we see that the condition number only depends on $A$ and not on $b$. Therefore, one simply writes $\kappa(A)$.

Going back to our earlier equation we hence have the precise estimate that

$$
\frac{\|\Delta y\|}{\|y\|}\leq \frac{\kappa(A)}{1-\kappa(A)\frac{\|\Delta A\|}{\|A\|}}\left(\frac{\|\Delta A\|}{\|A\|} + \frac{\|\Delta b\|}{\|b\|}\right),
$$

which relates the relative forward error and the relative backward error in the linear system.

The condition number $\kappa(A)$ has an important interpretation. It measures how far away from being singular a linear system is. More precisely,

$$
\min\left\{\frac{\|\Delta A\|_2}{\|A\|_2}: A + \Delta A~singular \right\} = \frac{1}{\kappa(A)}.
$$

We are not going to prove this result here. Later in the term we will derive tools that make
the relationship between condition number and distance to singularity immediately obvious.