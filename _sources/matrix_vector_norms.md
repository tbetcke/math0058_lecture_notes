# Matrix and vector norms

## Norm axioms

Let $V$ be a vector space and $\rho: V\rightarrow \mathbb{R}^{+}$ a
mapping from $V$ into the nonnegative numbers.
$\rho$ is called a norm if it satisfies the following properties

1. $\rho(\alpha x) = |\alpha| \rho(x)~\forall \alpha\in\mathbb{R};~x\in V$
2. $\rho(x + y) \leq \rho(x) + \rho(y)~\forall x, y\in V$ (triangle inequality)
3. $\rho(x) = 0$ if and only if $x = 0$.

From these axioms it immediately follows that
$$
0 = \rho(0) = \rho(x - x) \leq 2\rho(x)
$$

and therefore $\rho(x) \geq 0$ for all $x\in V$. Hence, a norm is always
nonnegative.

The first and third norm axiom are usually easy to prove. The difficult
one is the second one, the triangle inequality.

## Frequently used vector norms

Let $V$ be the real vector space $\mathbb{R}^n$. Let $x\in V$ and denote
by $x_j$ the $j$-th  component of $x$.

The most frequently used vector norms are:

- The $1$-norm $\|x\|_1 = \sum_{j=1}^n|x_j|$.
- The $2$-norm $\|x\|_2 = \left[\sum_{j=1}^n|x_j|^2\right]^{1/2}$.
- The $\infty$-norm $\|x\|_{\infty} = \max_j |x_j|$.

These are all special cases of the $\ell_p$-norm defined as

$$
\|x\|_p = \left[\sum_{j=1}^n]|x_j|^p\right]^{1/p}.
$$

## Norm equivalence

Which norm should we use? This usually depends on the application.
A taxi driver will prefer the $1$-norm when calculating distances as they
need to follow a street map and can't go in straight lines to locations.

In Numerics we often want to prove whether a given numerical approximation
is converging. Hence, we have some error quantity $e$ and want to show that
the sequence of errors $\left\{e_n\right\}$ converges to $0$. Can it happen
that an error converges to $0$ in one norm but not in another norm?
In finite dimensional vector spaces the answer is no. If a sequence converges in one norm it also converges in any other norm. This goes back
to the following norm equivalence theorem

### Norm equivalence in finite dimensional vector spaces

Let $V$ be a finite dimensional vector space. Consider two norms
$\|\cdot\|_a$ and $\|\cdot\|_b$ on $V$. Then there exist positive constants
$C_1$, $C_2$ such that for all $x\in V$

$$
C_1\|x\|_a\leq \|x\|_b\leq C_2\|x\|_a
$$

Proof: The proof requires some analysis and is not part of the lecture.
For those interested in how it works a good reference is the following
note by [Steve Johnson at MIT](https://math.mit.edu/~stevenj/18.335/norm-equivalence.pdf).

We note that norm equivalence is only a property of finite dimensional vector spaces. For infinite dimensional spaces (e.g. spaces of functions)
it is easy to construct examples of functions converging with respect to one norm but not with respect to another norm.


## Matrix norms

Let $A\in\mathbb{R}^{m\times n}$. Consider vector norms $\|x\|_a$ for $x\in\mathbb{R}^n$ and $\|y\|_b$ for $y\in\mathbb{R}^{m}$. Then an induced matrix norm can be defined as follows:

$$
\|A\|_{b, a}:= \max_{x\in\mathbb{R}^n\backslash\{0\}}\frac{\|Ax\|_b}{\|x\|_a}
$$

If $a = b$ then we abbreviate $\|A\|_a := \|A\|_{a, a}$.

The following three matrix norms derive from the corresponding vector norms.

- $\|A\|_1 :=\max_{1\leq j\leq n} \sum_{i=1}^n|a_{ij}|$
- $\|A\|_2 :=\sqrt{\lambda_{max}(A^TA)}$, where
$\lambda_max$ denotes the largest eigenvalue.
- $\|A\|_{\infty} := \max_{1\leq i\leq n}\sum_{j=1}^n|a_{ij}$

The $\|A\|_2$ matrix norm is difficult to evaluate as it requires computation of the largest eigenvalue of $A^TA$, which is an expensive operation. In practice, the following **Frobenius** norm is therefore frequently used instead of the matrix $2$-norm.

$$
\|A\|_F:=\left(\sum_{ij}|a_{ij}|^2\right)^{1/2}.
$$

We will later show that 

$$
\|A\|_2\leq \|A\|_F\leq\sqrt{r}\|A\|_2
$$

## Submultiplicativity

Let $A\in\mathbb{R}^{m\times n}$ and $B\in\mathbb{R}^{n\times k}$ with corresponding vector induced matrix norm $\|\cdot\|$. For any $v\in\mathbb{R}^k$ it holds that

$$
\|ABv\|\leq \|A\|\cdot\|Bv\|\leq \|A\|\cdot \|B\| \cdot \|v\|.
$$

Dividing by $\|v\|$ and taking the maximum over all $v\in\mathbb{R}^k\backslash\{0\}$ shows that

$$
\|A\cdot B\|\leq \|A\|\cdot \|B\|.
$$

This property is called submultiplicativty. We have just proved it for any vector induced matrix norm. But what about the Frobenius norm?

First of all, since $\|A\|_2\leq \|A\|_F$ we have that

$$
\|Ax\|_2 \leq \|A\|_2\|x\|_2 \leq \|A\|_F\|x\|_2.
$$



We can now prove the following statement.

### Submultiplicativity of the Frobenius norm

For matrices $A$ and $B$ with compatible dimensions such that the product $AB$ exists it holds that

$$
\|AB\|_F\leq \|A\|_F\cdot \|B\|_F.
$$

**Proof:** We denote by $B_{:, j}$ the $j$-th colon of the matrix $B$. We can now write

$$
\|AB\|_F^2 = \sum_{j}\|AB_{:, j}\|_2^2\leq \|A\|_F^2\sum_{j}\|B_{:, j}\|_2^2 = \|A\|_F^2\cdot \|B\|_F^2,
$$
from which the result follows.
