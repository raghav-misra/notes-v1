# math462 exam3 crashout

## 5.1 stuff

sine series
$$
\phi(x) = \sum_{n= 1}^{\infty} A_n \sin \left( \frac{n \pi x}{\ell} \right)
$$
sine coefficients
$$
A_n = \frac{2}{\ell} \int_0^\ell \phi(x) \sin \left( \frac{n \pi x}{\ell} \right)
$$


cosine series
$$
f(x) = \frac{1}{2}A_0+ \sum_{n= 1}^{\infty} A_n \cos \left( \frac{n \pi x}{\ell} \right)
$$
cosine coefficients
$$
A_n = \frac{2}{\ell} \int_0^\ell \phi(x) \cos \left( \frac{n \pi x}{\ell} \right)
$$
full fourier series over $[-\ell, \ell]$
$$
\phi(x) = \frac{1}{2} A_0 + \sum_{n = 1}^{\infty} [A_n \cos \frac{n \pi x}{\ell} + B_n \sin \frac{n \pi x}{\ell}]
$$
full coefficients are same as sine and cosine; except $1/\ell$ and over whole interval.

## 5.2 stuff

Euler formula
$$
e^{ix} = \cos x + i \sin x \quad \text{and} \quad e^{i \pi} = -1.
$$
complex series over $[-\ell, \ell]$
$$
\phi(x) = \sum_{n = 1}^{\infty} c_n e^{\frac{i n \pi x}{\ell}}
$$
complex coefficients
$$
c_n = \frac{1}{2 \ell} \int_{-\ell}^{\ell} \phi(x) e^{-\frac{i n \pi x}{\ell}} dx.
$$

## 5.3 stuff

if BCs are symmetric, two eigenfunctions with different eigenvalues are *orthogonal*.
$$
\text{symmetric if } [f'(x)g(x) - f(x) g'(x)]_{x = a}^{x = b} = 0.
$$
consequences of symmetric BCs ... let $X_1$ and $X_2$ be eigenfunctions with diff. eigenvalues.

- $(\mathcal{L} f, g) = (f, \mathcal{L} g)$.
- all eigenvalues are real. (conjugate equal to itself.)

all eigenvalues are negative if for every eigenfunction...
$$
\Big[f(x)f'(x) \Big]_{x = a}^{x = b} \leq 0.
$$

## 5.4 stuff

Infinite number of eigenvalues.

General solution for Fourier coefficients:
$$
A_n = \frac{(\phi, X_n)}{(X_n, X_n)} 
= \frac{\int_a^b f(x) \overline{X_n(x)}dx}{\int_a^b |X_n(x)|^2 dx}.
$$
