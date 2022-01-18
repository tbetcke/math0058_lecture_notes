# A quick survey of the $\mathcal{O}$-notation

Throughout this module we are interested in leading order complexities of quantities.
Consider a polynomial

$$
p(n) = 3n^3 + 5n^2 + 1.
$$

If we are only interested in the asymptotic behaviour for large $n$ then only the cubic term of $p$ is relevant. Moreover, if we only want to express that the polynomial is growing cubically the $3$ in front of $n^3$ is not relevant either. A convenient notation to express this is the $\mathcal{O}$-notation.

The formal definition is as follows

### Definition of $\mathcal{O}$-notation

Let $g(n)$ and $f(n)$ be two given functions for $n\in\mathbb{N}$. If there exists $n_0 \in \mathbb{N}$ and a constant $C> 0$ such that

$$
|g(n)| \leq Cf(n)
$$

for all $n\geq n_0$ we say that $g(n) = \mathcal{O}(f(n))$.

This definition naturally extends to real variables $x\in\mathbb{R}$ instead of integer variables $n$.

Correspondingly, we can also use the $\mathcal{O}$-notation to describe how a function behaves as $x\rightarrow 0$.

We say that $g(x) = \mathcal{O(f(x))}$ as $x\rightarrow 0$ if $|g(x)| \leq Cf(x)$ for sufficiently small $x$.

### Examples

For the above polynomial we have that 

$$
p(n) = \mathcal{O}(n^3).
$$

At the same time we have that $p(n) = \mathcal{O}(5n^3)$. However, we usually do not express constants inside the $\mathcal{O}$-notation unless we want to emphasise their importance, since the definition of the $\mathcal{O}$-notation is independent of constant factors.

For small $x$ a typical example of the $\mathcal{O}$-notation is in Taylor's theorem. For example we have that

$$
e^{x} = 1 + x + \mathcal{O}(x^2)
$$

as $x\rightarrow 0$ as the remainder term decreases quadratically.

