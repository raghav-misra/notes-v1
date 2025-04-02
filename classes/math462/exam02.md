# math462; exam02

## High level information

### Professor notes

**Textbook sections:** 2.4, 3.1, 3.2, 3.5, 4.1, 4.2, 4.3.

- The theorems in 3.5 were just stated (no proofs).
- We found inhomogeneous solutions by finding a specific solution and subtracting it from the homogeneous general solution. The book goes into much more detail, giving general formulas, which we are *not responsible for*.
- The book's discussion of Robin conditions in 4.3 is much more general than ours from class. They consider arbitrary $a_0$ and $a_1$, whereas we just did the case where $a_0 = 1$ and $a_1 = 1$ for simplicity. We *aren't responsible* for just general conditions, just the work done in class.

### Things to memorize

The wave equation itself is $u_{tt} = c^2 u_{xx}$. where $c$ is wave speed.

D'Alembert's equation (general solution for wave on the real line):
$$
u(x, t) = \frac{1}{2} [\phi(x + ct) + \phi(x - ct)] + \frac{1}{2c} \int_{x - ct}^{x + ct} \psi(y) dy.
$$
The heat equation itself is $u_t = ku_{xx}$.

The general solution for heat equation on the real line:
$$
u(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{4 kt}} \phi(y) dy, \quad \text{for } t > 0.
$$
The error function:
$$
\text{Erf}(x) = \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-p^2} dp.
$$
An ODE of the form $X'' + \mu^2 X = 0$ has solution $X(x) = A \cos (\mu x) + B \sin (\mu x)$.

An ODE of the form $X'' - \mu^2 X = 0$ has solution $X(x) = C_1 e^{\mu t} + C_2 e^{-\mu t}$.

### Homework problems

**Homework 4** problems:

- If $u$ satisfies heat equation, show that $u_x$ and $u_{t}$ do as well.
- Verify a function $Q$ is a solution to the heat equation.
- If $\phi(x) = u(x, 0)$ is even/odd, show that $u$ is even/odd.
- Solve heat equation with given initial condition over the real line and express solution in terms of the error function $\text{Erf}$. 
- If $u$ solves some non-standard heat equation, and $v$ is a function involving $u$, then show that $v$ solves the ordinary heat equation and find an integral formula for $u$.

**Homework 5** problems:

- Solve heat/wave equation with Dirichlet/Neumann BCs on the half-line.
- Find general solutions inhomogeneous heat and wave equations by combining a specific inhomogeneous solution found by observation with the general homogeneous solution.

**Homework 6** problems:

- Use general series solutions found in class to solve heat/wave equations with homogeneous Dirichlet/Neumann BCs and provided IC.
- Derive properties of hyperbolic sine and cosine ($\sinh$ and $\cosh$) using their definitions.
- Solve eigenvalue problem with mixed boundary conditions.
- Apply separation of variables to find series solutions to modified heat/wave equations.

## Notes from textbook

### 2.4—Diffusion on the whole line

Our purpose is to solve the following equation:
$$
u_t = k u_{xx} \quad (-\infty < x < \infty,\ 0 < t < \infty), \quad u(x, 0) = \phi(x).
$$
Five basic invariance properties of the diffusion equation:

1. The *translate* $u(x - y, t)$ of solution $u(x, t)$ is another solution.
2. Any derivative $u_t, u_x, u_{tt}, \dots$ is also a solution.
3. A linear combination of solutions is also a solution.
4. An integral of solutions is also a solution.
5. If $u(x, t)$ is a solution, so is the *dilated* function $u(\sqrt{a} x, at)$ for any $a > 0$.

The general solution for diffusion on the whole line:
$$
u(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{4 kt}} \phi(y) dy, \quad \text{for } t > 0.
$$
Written in terms of the source kernel $S$,
$$
u(x, t) = \int_{-\infty}^{\infty} S(x - y, t) \phi(y) dy, 
	\quad \text{where} \quad
	S(x, t) = \frac{1}{\sqrt{4 \pi k t}} e^{-\frac{x^2}{4kt}}.
$$
It's usually impossible to evaluate such an integral with a result of just elementary functions. Answers to problems are often expressible in terms of the error function ($\text{Erf}$), which is defined by
$$
\text{Erf}(x) = \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-p^2} dp.
$$

### 3.1—Diffusion on the half-line

### 3.2—Reflections of waves

### 3.4—Waves with a source

### 4.1—Separation of variables, Dirichlet condition

The infinite series solution to the wave equation with homogeneous Dirichlet conditions
$$
u_{tt} = c^2 u_{xx} \quad (0 < x < \ell) \quad u(0, t) = u(\ell, t) = 0,
$$
is the expression
$$
u(x, t) = \sum_{n = 1}^{\infty} \left[ A_n \cos \left(\frac{n \pi c t}{\ell}\right) + B_n \cos \left( \frac{n \pi c t}{\ell} \right)  \right] \sin \left( \frac{n \pi x}{\ell} \right).
$$
Consider a similar problem for heat diffusion:
$$
u_t = k u_{xx} \quad (0 < x < \ell) \quad u(0, t) = u(\ell, t) = 0.
$$
This has the following general infinite series solution:
$$
u(x, t) = \sum_{n = 1}^{\infty} A_n \left( e^{-(\frac{n \pi}{\ell})^2 kt} \right) \sin \left(\frac{n \pi x}{\ell} \right).
$$

### 4.2—Separation of variables, Neumann condition

The infinite series solution to the wave equation with homogeneous Neumann BCs
$$
u_{tt} = c^2 u_{xx} \quad (0 < x < \ell) \quad u_x(0, t) = u_x(\ell, t) = 0,
$$
is the expression
$$
\begin{align*}
	u(x, t) &= \frac{1}{2} A_0 + \frac{1}{2} B_0 \\
	&\quad + \sum_{n = 1}^{\infty} \left[
    A_n \cos \left( \frac{n \pi c t}{\ell} \right) +
    	B_n \sin \left( \frac{n \pi c t}{\ell} \right)\right] \cos \left( \frac{n \pi x}{\ell} \right).
\end{align*}
$$

Consider a similar problem for heat diffusion:
$$
u_t = k u_{xx} \quad (0 < x < \ell) \quad u_x(0, t) = u_x(\ell, t) = 0.
$$
This has the following general infinite series solution:
$$
u(x, t) = \frac{1}{2} A_0 + \sum_{n = 1}^{\infty} A_n e^{-(\frac{n \pi}{\ell})^2 kt} \cos \left(\frac{n \pi x}{\ell} \right).
$$

### 4.3—Separation of variables, Robin condition

## Problems from textbook

### 2.4 problems

**Problem 1.** Solve the diffusion equation with initial condition
$$
\phi(x) = \begin{cases}
	1 &\text{if } |x| < \ell,
	0 &\text{if } |x| > \ell.
\end{cases}
$$
Express your solution in terms of the error function.

- **Answer.** Substitute into general solution:
  $$
  \begin{align*}
  u(x, t) &= \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{4kt}} \phi(y) dy \\
  &= \frac{1}{\sqrt{4 \pi kt}} \int_{-\ell}^{\ell} e^{-\frac{(x - y)^2}{4kt}} dy.
  \end{align*}
  $$
  Recall the error function:
  $$
  \text{Erf}(x) = \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-p^2} dp.
  $$
  We transform our solution as needed:
  $$
  \begin{align*}
  u(x, t) &= \frac{1}{\sqrt{4 \pi kt}} \int_{-\ell}^{\ell} e^{-\frac{(y - x)^2}{4kt}} dy \\
  \text{Let } p = \frac{(y - x)}{\sqrt{4kt}} \quad &\text{and} 
  	\quad dp = \frac{dy}{\sqrt{4kt}} \Rightarrow dy = \sqrt{4kt} dp \\
  	u(x, t) &= \frac{1}{\sqrt{\pi} \cancel{\sqrt{4kt}}} \int_{\frac{-\ell - x}{\sqrt{4kt}}}^{\frac{\ell - x}{\sqrt{4kt}}} e^{-p^2} \cancel{\sqrt{4kt}}dp \\
  	&= -\frac{1}{\sqrt{\pi} \cancel{\sqrt{4kt}}} \int_{\frac{x - \ell}{\sqrt{4kt}}}^{\frac{x + \ell}{\sqrt{4kt}}} e^{-p^2} \cancel{\sqrt{4kt}}dp \\
  	&= \frac{1}{2}\left [\text{Erf} \left(\frac{x - \ell}{\sqrt{4kt}} \right) - \left(\frac{x + \ell}{\sqrt{4kt}} \right) \right]
  \end{align*}
  $$

