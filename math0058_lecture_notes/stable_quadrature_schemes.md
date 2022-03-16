# Stable quadrature schemes

We know that Newton-Cotes quadrature rules are unstable as we decrease the polynomial degree $n$ of the
underlying interpolation. The reason is Runge's phenomenon. In the following we will briefly present
some quadrature schemes that do not suffer from this problem and are highly useful in practical computations.


## Summated (or composite) quadrature rules

The idea of summated quadrature rules is simple but powerful. Consider the integral $I = \int_a^bf(x)dx$.
Instead of using a Newton-Cotes rule for the whole interval we split up the interval in many small intervals
of size $h$.

Let $x_j = a + jh$ for $h = (b-a)/N$, $j = 0, \dots, N$ be N+1 distinct points with $x_0=a$ and $x_N=b$.

We write

$$
I = \int_{a}^{b}f(x)dx = \sum_{j=0}^{N-1} \int_{x_j}^{x_{j+1}}f(x)dx.
$$

Each integral is now posed on a small interval of size $h$. Instead of applying the Newton-Cotes rule to the
large interval we apply the Newton-Cotes rule to each subinterval. Let us demonstrate this with the trapezoid rule

$$
\int_{a}^{b}f(x)dx \approx \frac{b-a}{2} \left(f(b) + f(a)\right).
$$

Applying this rule to each subinterval $[x_j, x_{j+1}]$ we obtain

$$
I\approx \frac{h}{2}\sum_{j=0}^{N-1}\left(f(x_{j+1}) + f(x_j)\right).
$$

Note that for each interior point $x_j$ with $0<j<N$ the corresponding value $f(x_j)$ appears twice. We hence
have the very simple expression

$$
I\approx \frac{1}{2}f(a) + \sum_{j=1}^{N-1}f(x_j) + \frac{1}{2}f(b).
$$

It is possible to show that the rate of convergence of this rule is quadratic in $h$ for sufficiently smooth functions, 
that is the error decreases with $\mathcal{O}(h^2)$. But what happened to Runge's phenomenon?

The trick is that we are not increasing the polynomial degree $N$ but keep it fixed. We rather decrease the
interval size $h$. So Runge's phenomenon is irrelevant for this rule as it only applies for growing polynomial degree.

If $f$ is periodic with period $(b - a)$ the composite trapezoid rule becomes even simpler. In that case we have
$f(a) = f(b)$ and

$$
I\approx h\sum_{j=0}^{N-1}f(x_j).
$$

For periodic and analytic functions one can show that this quadrature rule even converges with exponential accuracy.
This is a feature used by many practical fast algorithms.

## Clenshaw-Curtis Quadrature rules

We define Chebychev points as follows. 
Let $\theta_j = \frac{j}{N+1}\pi$ for $j = 0, \dots, N+1$ and define

$z_j = e^{i\theta_j}$.

The Chebychev points are defined as $x_j = \frac{1}{2}\left(z_j + z_j^{-1}\right) = \text{Re}\{z_j\}$.

Chebychev points have the property that they cluster towards the boundary of the interval $[-1, 1]$.
It is this property that allows them to overcome the Runge phenomenon. It is possible to show that
interpolation in Chebychev points is completely stable, no matter the number of points. Moreover,
if we return to the question of approximation of functions via interpolation it is possible to show that
interpolation polynomials in Chebychev points converge against the functions if it is sufficiently smooth.

Quarature in Chebychev points is called Clenshaw-Curtis quadrature. It is highly efficient for numerically
integrating smooth functions and remains stable for large number of quadrature points.

## Gauss quadrature

The final quadrature technique that we want to mention is Gauss quadrature. The basic idea is the following.

Consider a quadrature rule $I\approx \sum_{j=0}^N f(x_j)\omega_j$. We have
two sets of unknowns, the points $x_j$ and the weights $\omega_j$. Gauss quadrature rules
are designed in such a way as to integrate polynomials with as high order as possible, exactly.

We have $2n+2$ unknowns (the $n+1$ quadrature points and associated weights). We can therefore
hope to integrate exactly polynomials up to degree $2n+1$, which are defined by $2n+2$ coefficients. Indeed,
that is exactly what Gauss quadrature is able to do.

The main drawback of Gauss quadrature is the more involved computation of the nodes and weights. We will not
go into detail of this here. However, this is a step that only needs to be performed once.
One can then simply tabulate the nodes and weights in the program code without recomputing them. This is exactly
what is done in many practical applications that require quadrature.

Traditionally, Gauss quadrature is preferred over Clenshaw-Curtis quadrature since
it integrates polynomials of higher order exactly (Clenshaw-Curtis is only exact for polynomials up to degree $n$).
However, this is not the whole story and recent work by Trefethen shows that in practice
both rules are similarly accurate for the integration of sufficiently smooth functions.





