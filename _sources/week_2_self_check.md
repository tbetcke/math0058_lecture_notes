# Week 2 Self check questions and solutions

**Question 1:**

State the relative forward error, backward error, and condition number for the linear system of equations $Ax=b$.

Let $x$ be the exact solution, and $\tilde{x}$ the computed solution. Then the relative forward error is defined as

$$
e := \frac{\|x - \tilde{x}\|}{\|x\|}.
$$

**Solution:**

The relative backward error is

$$
\eta(\tilde{x}) = \frac{\|b - A\tilde{x}\|}{\|A\| \cdot \|\tilde{x}\| + \|b\|}.
$$

The condition number is

$$
\kappa(A) = \|A\|\cdot \|A^{-1}\|.
$$

**Question 2:**

Assuming you are working in single precision floating point arithmetic and you have a backward stable algorithm for a problem with condition number $\kappa = 10^{3}$. How many correct digits do you expect in your solution?

**Solution:**

The algorithm is backward stable. Hence, the backward error is expected to be a small multiple of machine precision. We have $\epsilon_{mach} \approx 6\times 10^{-8}$. The condition number is $10^3$. Hence, the forward error is expected to be a multiple of $10^{-5}$, giving us around 3 to 4 digits of accuracy in the solution depending on the pre-factors. 

**Question 3:**

Compute the $1-$norm condition number of

$$
A = \begin{bmatrix}1 & 1\\ 0 & \epsilon\end{bmatrix}
$$

in dependence of $\epsilon$. What happens as $\epsilon\rightarrow 0$?

**Solution:**

We have $A^{-1} = \begin{bmatrix}1 & -\epsilon^{-1}\\ 0 & \epsilon^{-1}\end{bmatrix}$. Hence,

$$
\kappa(A) = \|A\|_1\cdot \|A^{-1}\|_1 = (1+\epsilon) \cdot \frac{2}{\epsilon}.
$$

and $\kappa(A)\rightarrow\infty$ as $\epsilon\rightarrow 0$. The reason is simple. For $\epsilon=0$ the matrix is not invertible and we expect the condition number to become unbounded as we reach this limit case.

**Question 4:**

Let $x\in\mathbb{R}^2$ and $f(x) = x_1 - x_2$. Compute the $\infty$-norm condition number of $f$. Hint: Use the expression for the condition number of a differentiable function. For what inputs is the condition number large?

**Solution:**

The Jacobian of $f$ is $J = \begin{bmatrix}1 & -1\end{bmatrix}$. Hence, $\|J\|_{\infty} = 2$. For the condition number we obtain

$$
\begin{aligned}
\kappa &= \frac{\|J\|_{\infty}}{\|f(x)\|_{\infty} / \|x\|_{\infty}}\\
       &= \frac{2}{|x_1 - x_2| / \max\left\{|x_1|, |x_2|\right\}}.
\end{aligned}
$$

The condition number is large if $x_1\approx x_2$. This reflects the issue of cancellation errors. Consider two numbers $x_1$ and $x_2$ who agree to the first $5$ digits and each of them is accurate to 7 digits. Then the difference of the two numbers will only be accurate to 2 digits since the first 5 correct digits cancel each other out.
