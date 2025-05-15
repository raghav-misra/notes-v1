# math462; exam03

## Types of Series

### Sine Series

*Expression* for **Fourier Sine Series** over $[0, \ell]$.
$$
\phi(x) = \sum_{n = 1}^{\infty} A_n \sin \frac{n \pi x}{\ell}.
$$
*Coefficients* for **Fourier Sine Series** over $[0, \ell]$.
$$
A_n = \frac{2}{\ell} \int_0^\ell \phi(x) \sin \frac{n \pi x}{\ell} dx.
$$

### Cosine Series

*Expression* for **Fourier Cosine Series** over $[0, \ell]$.
$$
\phi(x) = \frac{1}{2} A_0 + \sum_{n = 1}^{\infty} A_n \cos \frac{n \pi x}{\ell}.
$$
*Coefficients* for **Fourier Cosine Series** over $[0, \ell]$.
$$
\text{If $n \geq 1$}, \quad A_n = \frac{2}{\ell} \int_0^\ell \phi(x) \cos \frac{n \pi x}{\ell} dx. \\
\text{If $n = 0$}, \quad A_0 = \frac{2}{\ell} \int_0^\ell \phi(x) dx.
$$

### Full Series (Real)

*Expression* for **Full Series (Real)** over $[-\ell, \ell]$.
$$
\phi(x) = \frac{1}{2} A_0 + \sum_{n = 1} 
	\left[A_n \cos \frac{n \pi x}{\ell} + B_n \sin \frac{n \pi x}{\ell} \right].
$$
*Coefficients* for **Full Series (Real)** over $[-\ell, \ell]$.
$$
\text{If $n \geq 1$}, \quad A_n = \frac{1}{\ell} \int_{-\ell}^\ell \phi(x) \cos \frac{n \pi x}{\ell} dx \text{ and} \\
\qquad \qquad B_n = \frac{1}{\ell} \int_{-\ell}^\ell \phi(x) \sin \frac{n \pi x}{\ell} dx. \\
\text{If $n = 0$}, \quad A_0 = \frac{1}{\ell} \int_{-\ell}^\ell \phi(x) dx.
$$

### Complex Series

The complex series is equivalent to the real series, just a more compact form.

*Expression* for **Complex Series** over $[-\ell, \ell]$.
$$
\phi(x) = \sum_{n = -\infty}^{\infty} C_n e^{i \frac{\pi n x}{\ell}} 
= C_0 + \sum_{n = 1}^{\infty} C_n e^{i \frac{\pi n x}{\ell}} + \sum_{n = 1}^{\infty} C_{-n} e^{-i \frac{\pi n x}{\ell}}
$$
*Coefficients* for **Complex Series** over $[-\ell, \ell]$.
$$
\text{If $n \geq 1$}, \quad C_n = \frac{1}{2\ell} \int_{-\ell}^\ell \phi(x) e^{-i\frac{\pi n x}{\ell}} dx. \\
\text{If $n = 0$}, \quad C_0 = \frac{1}{2\ell} \int_{-\ell}^\ell \phi(x) dx.
$$

### Real $\Leftrightarrow$ Complex

Let $A_n$ and $B_n$ be coefficients of a real Full Fourier Series and $C_n$ be coefficients of the analogous Complex Series. Then, for $n \geq 1$,
$$
C_0 = \frac{A_0}{2}, \quad C_n = \frac{A_n - i B_n}{2}, \quad C_{-n} = \frac{A_n + i B_n}{2}.
$$
The following two equalities are **Euler's Identities**,
$$
\cos x = \frac{e^{ix} + e^{-ix}}{2} \quad \text{and} \quad \sin x = \frac{e^{ix} - e^{-ix}}{2i},
$$
important for converting between real and complex series.

## Series Solutions

This is all Exam 2 material. Will probably be asked to pull out one of the following, substitute constants and initial conditions, and evaluate with a Fourier series of some sort.

### Heat Equation

Recall the heat equation: $u_{t} = k u_{xx}$.

For **Dirichlet** boundary conditions, $u(0, t) = u(\ell, t) = 0$,
$$
u(x, t) = \sum_{n=1}^{\infty} A_n e^{-(\frac{n \pi}{\ell})^2 kt} \sin \frac{n \pi x}{\ell}.
$$
For **Neumann** boundary conditions, $u_t(0, t) = u(\ell, t) = 0$,
$$
u(x, t) = \frac{1}{2} A_0 + \sum_{n = 1}^{\infty} A_n e^{-(\frac{n \pi}{\ell})^2 kt} \cos \frac{n \pi x}{\ell}.
$$

### Wave Equation

For **Dirichlet** boundary conditions $u(0, t) = u(\ell, t) = 0$,
$$
u(x, t) = \sum_{n = 1}^{\infty} \left[A_n \cos \frac{n \pi ct}{\ell} + B_n \sin \frac{n \pi ct}{\ell} \right] \sin \frac{n \pi x}{\ell}.
$$
For **Neumann** boundary conditions, $u_t(0, t) = u_t(\ell, t) = 0$,
$$
u(x, t) = \frac{1}{2} A_0 + \sum_{n=1}^{\infty} \left[ A_n \cos \frac{n \pi c t}{\ell} + B_n \sin \frac{n \pi ct}{\ell} \right] \cos \frac{n \pi x}{\ell}.
$$

## Orthogonality

### Symmetric Boundary Conditions

A set of boundary conditions is considered **symmetric** if for any pair of functions $f$ and $g$ which satisfy the conditions,
$$
\Big[ f'(x) g(x) - f(x)g'(x) \Big]_{x = a}^{x = b} = 0.
$$
It should be clear that homogeneous Dirichlet and homogeneous Neumann boundary conditions are symmetric.

**Consequence of Symmetric BCs:**

- Any two eigenfunctions with distinct eigenvalues are **orthogonal**.

- All eigenvalues are *real numbers*.

- All eigenvalues are non-negative *if* for all functions $f$ satisfying the BCs,
  $$
  \Big[f(x) f'(x) \Big]_{x = a}^{x = b} \leq 0.
  $$

## Convergence of Series

### $L^2$ Convergence

The series converges to $f$ in **the $L^2$ or mean-squared sense** in $(a, b)$ if
$$
\int_a^b |f(x)|^2 \text{ is finite.}
$$
This type of convergence can be conceptually understood as asserting that the discrepancy between the series and the value of $f$ approaches zero, as the number of terms in the series increases.

### Pointwise Convergence

*Pointwise convergence implies $L^2$ convergence.*

If $f$ is continuous and $f'$ is piecewise continuous on $[a, b]$, then the Fourier series of $f$ converges to $f$ on $x \in (a, b)$.

*"Average Strat"* says that if $f$ is also piecewise continuous (finite discontinuities), then for some $x_0$ where $f$ is a *jump discontinuity*, the Fourier series of $f$ converges to $\frac{1}{2} [f(x_0 +) + f(x_0-)]$ ("from the right" and "from the left").

### Uniform Convergence

A much stronger property. *Uniform convergence implies pointwise convergence.*

The Fourier series of $f$ converges to $f$ **uniformly** on $[a, b]$ provided that $f$, $f'$, and $f''$ are all continuous over $[a, b]$ and $f$ satisfies the given boundary conditions. 

*Observation.* Uniform continuity over the closed interval requires smoothness of the periodic extension of $f$. That is, $f$ is continuous at the endpoints $a$ and $b$. I believe this is what why the requirement is $f$ and its first two derivatives to be continuous at $a$ and $b$.

If the function is not smooth across periods, its series does not converge uniformly. But it is still likely to converge pointwise, and may converge at the average of the two endpoints (*average strat*).

### Bessel's and Parseval's.

If the Fourier series of $f$ is $L^2$ convergent, that is, $\int_a^b |f(x)|^2$ is finite, then
$$
\sum_{n = 1}^{\infty} A_n^2 \int_a^b |X_n(x)|^2 dx \leq \int_a^b |f(x)|^2 dx.
$$
This is **Bessel's Inequality**. A stronger statement is that the Fourier series of $f$ is $L^2$ convergent *if and only if* 
$$
\sum_{n = 1}^{\infty} |A_n|^2 \int_a^b |X_n(x)|^2 dx = \int_a^b |f(x)|^2 dx.
$$
This is **Parseval's Equality**.

