# Backward error of the LU decomposition and pivoting

The backward error of the LU decomposition is a fascinating topic. Despite the LU decomposition having been well known for decades there are still many open questions regarding the backward error.

First of all, the LU decomposition itself is not backward stable and we will see examples of why this is not the case. Indeed, LU decomposition can catastrophically increase the backward error.

We will then learn about a small modification to the LU decomposition, called pivoting, which makes the algorithm stable in almost all situations. One can still construct matrices for which the improved algorithm is not backward stable. But these
are quite pathological and do not tend to be relevant in practice.

## A first backward error result

The following theorem provides a backward error result for
the basic LU decomposition. We will give the statement and then
discuss its consequences. We will not provide the proof here.

### Backward error of the LU decomposition

Let $A = LU$ be the LU decomposition of a nonsingular matrix
$A\in\mathbb{R}^{n\times n}$., and $\tilde{L}, \tilde{U}$ the
computed LU factors by Gaussian elimination in floating
point arithmetic. The computed factors $\tilde{L}$ and $\tilde{U}$ satisfy

$$
\tilde{L}\tilde{U} = A + \Delta A
$$

for some $\Delta A\in\mathbb{R}^{n\times n}$ with

$$
\frac{\|\Delta A\|}{\|L\|\cdot \|U\|} = \mathcal{O}(\epsilon_{mach}).
$$

We might naively think that this shows the LU decomposition is backward stable. However, for a backward stability result we would require that $\|\Delta A\| / \|A\| = \mathcal{O}(\epsilon_{mach})$. But instead we have $\|L\|\cdot \|U\|$ in the denominator.

So the question of backward stability of the $LU$ decomposition is reduced to the problem of when we have that 

$$
\|A\| \approx \|L\|\cdot \|U\|.
$$

## Failure of backward stability

Let 

$$
A_{\epsilon} = 
\begin{bmatrix}
\epsilon & 1\\
1 & 1
\end{bmatrix}.
$$

We have

$$
A_{\epsilon} =
\begin{bmatrix}
1 & 0\\
\epsilon^{-1} & 1
\end{bmatrix}
\begin{bmatrix}
\epsilon & 1\\
0 & 1 - \epsilon^{-1}.
\end{bmatrix}
$$

In this example $\|A\|\approx 1$ (depending on the norm) but
$\|L\|\cdot \|U\|\approx \mathcal{O}(\epsilon^{-2})$.

The norms of $L$ and $U$ can differe wildly from the norm of $A$. But there is an easy fix in this example. We can swap the first and second row of $A$ to obtain

$$
\begin{bmatrix}
1 & 1\\
\epsilon & 1
\end{bmatrix}
= 
\begin{bmatrix}
1 & 0\\
\epsilon & 1
\end{bmatrix}
\begin{bmatrix}
1 & 1\\
0 & 1-\epsilon.
\end{bmatrix}
$$

We now have $\|L\|\cdot \|U\|\approx 1$, simply by swapping the two rows of the matrix.

This motivates the following motivation of the LU decomposition, called **column pivoted** (or simply **pivoted**) LU.

## LU decomposition with pivoting

The idea is simple. Consider again the $3\times 3$ matrix

$$
A = \begin{bmatrix}
a_{11} & a_{12} & a_{13}\\
a_{21} & a_{22} & a_{23}\\
a_{31} & a_{32} & a_{33}
\end{bmatrix}.
$$

Assume that $a_{31}$ is the element with the largest magnitude in the first column. We then exchange the third and the first row to get

$$
P_1A = \begin{bmatrix}
a_{31} & a_{32} & a_{33}\\
a_{21} & a_{22} & a_{23}\\
a_{11} & a_{12} & a_{13}
\end{bmatrix}
$$

with

$$
P_1 = \begin{bmatrix}
0 & 0 & 1\\
0 & 1 & 0\\
1 & 0 & 0
\end{bmatrix}.
$$

We now proceed with the LU decomposition as normal to zero out the elements in the first column. We then obtain a matrix with the structure

$$
\begin{bmatrix}
x & x & x\\
0 & x & x\\
0 & x & x &
\end{bmatrix}.
$$

Before we proceed with the LU decomposition we swap the second and third row if the element at position $(3, 2)$ is larger by magnitude than the entry at position at $(2, 2)$.

This pivoting strategy guarantees that we have $|\ell_{i, j}|\leq 1$ for all $i, j$. However, we now have a decomposition not of $A$ but of $PA$ in the form

$$
PA = LU,
$$

where $P$ is a permutation matrix that swaps the rows of $A$ around. Note that we do not $P$ in advance. The correct permutation of the rows of $A$ is determined by progressing through the LU decomposition.

## Growth factors

Let us consider how pivoting influences the size of the factors in the LU decomposition. As already stated we have $\ell_{i, j}| \leq 1$ with pivoting. Hence, $\|L\| \approx 1$ and 

$$
\|L\|\cdot \|U\| \approx \|U\|
$$

(all up to small norm and dimension dependent factors)

To measure how $\|U\|$ grows the following definition of the growth factor $\rho$ is useful.

$$
\rho := \frac{\max_{i, j}|u_{i,j}|}{\max_{i, j}|a_{i,j}|}
$$

Hence, we have that

$$
\|U\| \approx \rho \|A\|.
$$

We can now go back to our original backward error result and obtain that the computed LU factors satisfy

$$
\tilde{L}\tilde{U} \approx PA + \Delta A
$$

with

$$
\frac{\|\Delta A\|}{\|A\|}= \mathcal{O}(\rho\epsilon_{mach}).
$$

**Note that the notation $\mathcal{O}(\rho\epsilon_{mach})$ is a bit misleading since the $O$-notation absorbs constants. Nevertheless, this is done to emphasise the importance of the factor $\rho$**.

It follows that the LU decomposition with pivoting is backward stable if $\rho$ is small.
