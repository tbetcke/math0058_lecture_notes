# Principles of backward error analysis

Modern error analysis goes back to the seminal work by [James Hardy Wilkinson](https://en.wikipedia.org/wiki/James_H._Wilkinson).
It distinguishes between forward error, that is the error in the result of an algorithm, and the backward error, which is a perturbation
measure for the input data.

In the following we denote by $f:X\rightarrow Y$ a function that maps data from an input space $X$ into an output space $Y$. Correspondingly,
we define a function $\tilde{f}$, which represents an approximate evaluation of $f$. Consider for example the solution of the linear system
of equations

$$
Ay = b
$$

with $A\in\mathbb{R}^{n\times n}$ and $b\in\mathbb{R}^n$. Then the input space is the product space $X=\mathbb{R}^{n\times n} \times \mathbb{R}^n$ and our
input data is the tuple $(A, b)\in X$. The output space is $Y=\mathbb{R}^n$. The function $f$ is given as

$$
f(A, b) = A^{-1}b
$$

and the approximate function $\tilde{f}$ is for example the Gaussian elimination algorithm in IEEE double precision to compute the solution $y$.

## Forward Error

Let $y = f(x)$ and $\tilde{y} = \tilde{f}(y)$. The relative forward $E_{rel}$ is defined as 

$$
E_{rel} := \frac{\|y - \tilde{y}\|}{\|y\|}.
$$

It measures the difference in output between the exact function $f$ and the approximate function $\tilde{f}$ for the same input. In some situations it is not useful to talk about
the relative forward error (i.e. if $y=0$). We then use the absolute forward error $E_{abs} = \|y-\tilde{y}\|$.

## Backward error

The backward error answers the following question. Given the output $\tilde{y}$ from the perturbed function $\tilde{f}$ for the input $x$. By how much would I need to perturb $x$ to an input $\tilde{x} = x + \Delta x$ so that we have $\tilde{y} = f(\tilde{x})$. Hence, it asks
if the exact function $f$ could produce the same output as $\tilde{f}$ but with a slight perturbation in the input data. The idea is that our approximate function $\tilde{f}$ is useful if only a small perturbation is needed for the input data so that $f$ produces the same output as $\tilde{f}$ (the perturbation certainly being dependent on the input data).

Formally, the relative backward error is defined as

$$
\eta_{rel}(\tilde{y}) := \min\{\epsilon: f(x+ \Delta x) = \tilde{y}: \|\Delta x\|\leq \epsilon \|x\|\}.
$$

If the relative backward error for $\tilde{f}$ is bounded by a small constant times the uncertainty in the input data we say that the algorithm is backward stable. It means that the backward accuracy from the algorithm is as good as we can expect. Hence, for a numerical algorithm on a computer we say that an algorithm is backward stable if its backward error is bounded by a small multiple of machine precision.

## Condition number

The definition of the backward error seems convoluted at first. But it is very useful as the following shows. Assume that $f$ is differentiable. We have to first order the following statement.

$$
\begin{aligned}
\|y - \tilde{y}\| &\stackrel{(1)}{=} \|f(x) - \tilde{f}(x)\|\\
                  &\stackrel{(2)}{=} \|f(x)  - f(\tilde{x})\|\\
                  &\stackrel{(3)}{\leq} \|f'(x)\|\cdot \|x - \tilde{x}\|
\end{aligned}
$$

Equality (2) is possible by choosing $\tilde{x}$ such that $\tilde{f}(x) = f(\tilde{x})$. Hence, $\Delta x = x- \tilde{x}$ is the backward perturbation associated with the output $\tilde{y}$.
The right-hand side in (3) is the
product of the derivative of $f$ and the size of the backward error. It demonstrates that
the forward error depends on two quantities, namely the sensitivity of $f$ to small perturbations (i.e. $\|f'(x)\|$) and the size of the backward error $\|x-\tilde{x}\|$. This is of fundamental importance. We can devise an extremely good evaluation $\tilde{f}$ with small backward error. If the problem is highly sensitive to perturbations, the output forward error will still be large.

A more general definition of sensitivity is given by the *condition number*. The relative
condition number $\kappa_{rel}$ is defined as

$$
\kappa_{rel}(x) := \lim_{\delta\rightarrow 0}\sup_{\|\Delta x\|\leq \delta}\left(\frac{\|\Delta f\|}{\|f\|} / \frac{\|\Delta x\|}{\|x\|}\right)
$$

with $\Delta f = f(x) - f(\tilde{x})$ being the perturbation in the output data.

Hence, it measures the largest possible ratio of relative output error with respect to relative
input error. If $f$ is differentiable then $\kappa_{rel}(x) = \frac{\|f'(x)\|}{\|f(x\|}\|x\|$.

What is a good condition number in practice? Ideally, we want the condition number to be close
to $1$ since then errors in the input data are not amplified for the output error. For each
magnitude of the condition number we lose one digit of accuracy in the output error. This
can be seen as follows.

From the definition of the condition number we obtain for differentiable $f$ that to first order

$$
\frac{\|\Delta f\|}{\|f\|}\leq \kappa_{rel}(x)\cdot \frac{\|\Delta x\|}{\|x\|},
$$

or in other words the relative forward error is bounded by the product of condition number
and relative backward error.

Assume we work in double precision and that the algorithm is backward stable. Then the backward error is a small multiple of $\epsilon_{mach}$. Hence, if the condition number is $100$ we expect to lose two digits of accuracy in the forward error. If the condition number is in the order of $\epsilon_{mach}^{-1}$ then we will likely use almost all digits.

If a condition number is small we say that the problem is *well-conditioned*. If the condition
is large we say that the problem is *ill-conditioned*. The precise meaning of these terms depends on the requirements of the application. 

**Note: The condition number is a worst-case bound. In practice, the actual forward error may
be better than predicted by the condition number.**

**Note: In the following we will generally not use the subscript $rel$ for relative quantities. Unless otherwise stated we always work with relative quantities.**