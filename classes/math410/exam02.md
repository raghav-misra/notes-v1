# math410; exam02

## 4—Differentiation

### 4.1—Derivatives

If the following limit for a function $f: I \rightarrow \mathbb{R}$ exists at $x_0$, we say it is the **derivative** $f'(x_0)$:
$$
\lim_{x \rightarrow x_0} \frac{f(x) - f(x_0)}{x - x_0}.
$$
**Power rule** says that for $f(x) = x^n$,
$$
f'(x) = n  x^{n - 1}.
$$

### 4.2—Inverses and Chain Rule

**Derivative of inverse** is defined at $y_0 = f(x_0)$ as
$$
(f^{-1})'(y_0) = \frac{1}{f'(x_0)},
$$
if $f: I \rightarrow \mathbb{R}$ is monotone and differentiable.

**Chain rule** says if $f: I \rightarrow \mathbb{R}$ and $g: J \rightarrow \mathbb{R}$ and $f(I) \subseteq J$, then
$$
(g \circ f)'(x) = f'(x) \cdot g'(f(x)).
$$

### 4.3—Mean Value Theorem

**Mean Value Theorem** states that if $f: [a, b] \rightarrow \mathbb{R}$ and $f$ is *continuous* and *differentiable* over $(a, b)$, then $\exists x_0 \in (a, b)$ such that
$$
f'(x_0) = \frac{f(b) - f(a)}{b - a}.
$$
**Rolle's Theorem** is the same thing but specific to when $f(a) = f(b)$, then $\exists x_0 \in (a, b)$ such that $f'(x_0) = 0$.

**Identity Criterion**:

- If $f$ is a constant function everywhere, $f' = 0$ everywhere.
- If $g$ and $h$ differ by a constant everywhere, $(g - h)' = 0$ everywhere.

If a function's derivative is:

- $\geq 0$, it is monotonically increasing.
- $> 0$, it is strictly increasing.
- $\leq 0$, it is monotonically decreasing.
- $< 0$, it is strictly decreasing.

### 4.4—Cauchy MVT

**Cauchy Mean Value Theorem**. Suppose $f, g: [a, b] \rightarrow \mathbb{R}$ are continuous and their restrictions to $(a, b)$ are differentiable. Also, $g'(x) \neq 0$ for all $x \in (a, b)$. Then, $\exists x_0 \in (a, b)$ such that
$$
\frac{f(b) - f(a)}{g(b) - g(a)} = \frac{f'(x_0)}{g'(x_0)}.
$$
 

## 6—Integration

### 6.1—Darboux Sums

### 6.2—Archimedes-Riemann Theorem

### 6.3—Integral Properties

### 6.4—Continuity + Integrability

### 6.5—FTC: Integrating Derivatives

### 6.6— FTC: Differentiating Integrals

## 8—Taylor Polynomials

### 8.1—Approximations by Taylor Polynomials

### 8.2—Lagrange Remainder Theorem

### 8.3—Convergence of Taylor Polynomials

### 8.5—Cauchy Integral Remainder Theorem



