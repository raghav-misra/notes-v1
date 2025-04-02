# math410; quiz06

## Things to know

### Differentiability

A function $f: I \rightarrow \mathbb{R}$ is **differentiable** at $x_0$ provided that the limit
$$
f'(x_0) = \lim_{x \rightarrow x_0} \frac{f(x) - f(x_0)}{x - x_0}
$$
 exists. If so, we say that $f'(x_0)$ is the **derivative** of $f$ at $x_0$.

**Differentiable functions are continuous.**

- You can manipulate the derivative limit to show $\lim_{x \rightarrow x_0} f(x) = f(x_0)$, which means $f$ is continuous.

### Derivative rules

**Power rule.** If $f(x) = x^n$, then $f'(x) = nx^{n - 1}$.

**Product rule.** $(f \cdot g)'(x) = f'(x) g(x) + f(x) g'(x)$.

**Quotient rule.** $(f / g)'(x) = \frac{g(x)f'(x) - g'(x)f(x)}{[g(x)]^2}$.

**Chain rule.** $(f \circ g)'(x) = g'(x) (f' \circ g)(x)$.

### Lagrange MVT

**Lagrange Mean Value Theorem.** If $f: [a, b] \rightarrow \mathbb{R}$ is continuous and $f$ is differentiable over $(a, b)$, then there exists some $x_0 \in (a, b)$ such that
$$
f'(x_0) = \frac{f(b) - f(a)}{b - a}.
$$
**Rolle's Theorem** is a special case of the above MVT. If $f: [a, b] \rightarrow \mathbb{R}$ is continuous, $f$ is differentiable over $(a, b)$, and $f(a) = f(b)$, then there exists some $x_0 \in (a, b)$ such that
$$
f'(x_0) = 0.
$$

### MVT Applications

