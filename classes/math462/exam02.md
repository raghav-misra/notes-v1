# math462; exam02

## High level information

### Professor notes

**Textbook sections:** 2.4, 3.1, 3.2, 3.5, 4.1, 4.2, 4.3.

- The theorems in 3.5 were just stated (no proofs).
- We found inhomogeneous solutions by finding a specific solution and subtracting it from the homogeneous general solution. The book goes into much more detail, giving general formulas, which we are *not responsible for*.
- The book's discussion of Robin conditions in 4.3 is much more general than ours from class. They consider arbitrary $a_0$ and $a_1$, whereas we just did the case where $a_0 = 1$ and $a_1 = 1$ for simplicity. We *aren't responsible* for just general conditions, just the work done in class.

### Things to memorize

#### General equations/solutions

**The wave equation** itself is $u_{tt} = c^2 u_{xx}$. where $c$ is wave speed.

**D'Alembert's equation** (general solution for wave on the real line):
$$
u(x, t) = \frac{1}{2} [\phi(x + ct) + \phi(x - ct)] + \frac{1}{2c} \int_{x - ct}^{x + ct} \psi(y) dy.
$$
**The heat equation** itself is $u_t = ku_{xx}$.

**The general solution for heat equation** on the real line:
$$
u(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{4 kt}} \phi(y) dy, \quad \text{for } t > 0.
$$
**The error function:**
$$
\text{Erf}(x) = \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-p^2} dp.
$$
Some characteristic function stuff yields:

- An ODE of the form $X'' + \mu^2 X = 0$ has solution $X(x) = A \cos (\mu x) + B \sin (\mu x)$.
- An ODE of the form $X'' - \mu^2 X = 0$ has solution $X(x) = C_1 e^{\mu x} + C_2 e^{-\mu x}$.
  - Equivalent form: $X(x) = C_1 \cosh(\mu x) + C_2 \sinh(\mu x)$.

#### Half-line general solutions

**Wave, homogeneous Dirichlet.**

**Wave, homogeneous Neumann.**

**Heat, homogeneous Dirichlet.** 
$u_t = k u_{xx} \quad (0 < x < \infty) \quad u(x, 0) = \phi(x), \quad u(0, t) = 0.$
$$
u(x, t) = \int_{0}^{\infty} [e^{-\frac{(x - y)^2}{4kt}} - e^{-\frac{(x + y)^2}{4kt}}] dy.
$$
**Heat, homogeneous Neumann. **
$u_t = k u_{xx} \quad (0 < x < \infty) \quad u(x, 0) = \phi(x), \quad u_x(0, t) = 0.$
$$
u(x, t) = \int_{0}^{\infty} [e^{-\frac{(x - y)^2}{4kt}} + e^{-\frac{(x + y)^2}{4kt}}] dy.
$$

#### Series solutions for specific BCs

**Wave, homogeneous Dirichlet:** 
$u_{tt} = c^2 u_{xx} \quad (0 < x < \ell) \quad u(0, t) = u(\ell, t) = 0$.
$$
u(x, t) = \sum_{n = 1}^{\infty} \left[ A_n \cos \left(\frac{n \pi c t}{\ell}\right) + B_n \sin \left( \frac{n \pi c t}{\ell} \right)  \right] \sin \left( \frac{n \pi x}{\ell} \right).
$$
**Heat, homogeneous Dirichlet.** 
$u_t = k u_{xx} \quad (0 < x < \ell) \quad u(0, t) = u(\ell, t) = 0$.
$$
u(x, t) = \sum_{n = 1}^{\infty} A_n \left( e^{-(\frac{n \pi}{\ell})^2 kt} \right) \sin \left(\frac{n \pi x}{\ell} \right).
$$
**Wave, homogeneous Neumann.** 
$u_{tt} = c^2 u_{xx} \quad (0 < x < \ell) \quad u_x(0, t) = u_x(\ell, t) = 0$.
$$
\begin{align*}
	u(x, t) &= \frac{1}{2} A_0 + \frac{1}{2} B_0 \\
	&\quad + \sum_{n = 1}^{\infty} \left[
    A_n \cos \left( \frac{n \pi c t}{\ell} \right) +
    	B_n \sin \left( \frac{n \pi c t}{\ell} \right)\right] \cos \left( \frac{n \pi x}{\ell} \right).
\end{align*}
$$

**Heat, homogeneous Neumann.** 
$u_t = k u_{xx} \quad (0 < x < \ell) \quad u_x(0, t) = u_x(\ell, t) = 0$.
$$
u(x, t) = \frac{1}{2} A_0 + \sum_{n = 1}^{\infty} A_n e^{-(\frac{n \pi}{\ell})^2 kt} \cos \left(\frac{n \pi x}{\ell} \right).
$$

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

### Diffusion on the whole line

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

### Half-line reflections

#### Heat diffusion

**Dirichlet.** Consider the following problem:
$$
u_t = k u_{xx} \quad (0 < x < \infty, t > 0) \quad u(x, 0) = \phi(x), \quad u(0, t) = 0.
$$
This is the diffusion PDE over half of the real line, with Dirichlet BC at one endpoint.

$\phi$ is only defined for $x \geq 0$. To solve, we take the odd extension of $\phi$ to the whole line:
$$
\phi_{odd}(x) = \begin{cases}
	\phi(x) &\text{if } x > 0, \\
	-\phi(-x) &\text{if } x < 0, \\
	0 &\text{if } x = 0.
\end{cases}
$$
We substitute this into the general form:
$$
u(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi_{odd}(y) dy, \quad \text{for $x$ > 0}.
$$
We can rewrite in terms of $\phi$ using our odd property of $\phi_{odd}$.
$$
\begin{align*}
u(x, t) &= \frac{1}{\sqrt{4 \pi k t}} \int_{0}^{\infty} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi(y) dy \\
	&\quad- \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{0} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi(-y) dy \\
	&= \int_{0}^{\infty} [e^{-\frac{(x - y')^2}{4kt}} - e^{-\frac{(x + y')^2}{4kt}}] dy' &\text{u-sub } y' = -y.
\end{align*}
$$
**Neumann.** Now, consider the following problem:
$$
u_t = k u_{xx} \quad (0 < x < \infty, t > 0) 
	\quad u(x, 0) = \phi(x),
	\quad u_x(0, t) = 0.
$$
This is the diffusion PDE over half of the real line, with Neumann BC at one endpoint.

We solve by taking an even reflection of $\phi$:
$$
\begin{align*}
\phi_{even} = \begin{cases}
	\phi(x) &\text{if } x > 0, \\
	\phi(-x) &\text{if } x < 0, \\
	0 &\text{if } x = 0.
\end{cases}
\end{align*}
$$
Now we substitute this into our general solution:
$$
u(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi_{even}(y) dy, \quad \text{for $x$ > 0}.
$$
We can rewrite in terms of $\phi$ using our even property of $\phi_{even}$.
$$
\begin{align*}
u(x, t) &= \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi_{even}(y) dy \\
	&= \frac{1}{\sqrt{4 \pi k t}} \int_{0}^{\infty} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi(y) dy \\
	&\quad+ \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{0} 
	e^{-\frac{(x - y)^2}{4 kt}} \phi(-y) dy \\
	&= \int_{0}^{\infty} [e^{-\frac{(x - y')^2}{4kt}} + e^{-\frac{(x + y')^2}{4kt}}] dy' &\text{u-sub } y' = -y.
\end{align*}
$$

#### Waves



### Waves with a source

### Separation of variables

#### Dirichlet conditions

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

#### Neumann conditions

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

#### Robin conditions

## Practice problems

Solve the diffusion equation with initial condition
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
  We transform our solution as needed. Let $p = \frac{x - y}{\sqrt{4kt}}$. Then, $dp = \frac{-dy}{\sqrt{4kt}}$.
  $$
  \begin{align*}
  u(x, t)
  	&= \frac{1}{\sqrt{\pi}} \cancel{\frac{1}{\sqrt{4kt}} } \int_{\frac{x + \ell}{\sqrt{4kt}}}^{\frac{x - \ell}{\sqrt{4kt}}} e^{-p^2} (- \cancel{\sqrt{4kt}} dp) \\
      &= \int_{\frac{x - \ell}{\sqrt{4kt}}}^{\frac{x + \ell}{\sqrt{4kt}}} e^{-p^2} dp 
      = \frac{1}{2} \left[ \text{Erf}\left(\frac{x + \ell}{\sqrt{4kt}} \right) - \text{Erf} \left( \frac{x - \ell}{\sqrt{4kt}} \right) \right].
  \end{align*}
  $$
  

Find a general solution for the following PDE over the real line:
$$
u_t - 3u_{xx} = \sin x.
$$

- **Answer.**

  We approach by finding a specific solution and subtracting the general homogeneous solution. Consider a time-independent solution $u_P(x, t) = P(x)$. Then, $u_{P_t} = 0$.

  So we end up with $0 - 3 P''(x) = \sin x$. Solving,
  $$
  \begin{align*}
  	P''(x) &= -\frac{1}{3} \sin x \\
  	P'(x) &=  \frac{1}{3} \cos x + C_1 \\
  	u_P(x, t) = P(x) &= \frac{1}{3} \sin x + C_1 x + C_2.
  \end{align*}
  $$
  Recall our general homogeneous solution for $v_{t} = 3u_{xx}$:
  $$
  v(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{4kt}} \phi(y) dy.
  $$
  Then, we find our integral expression for $u$:
  $$
  \begin{align*}
  	u(x, t) &= u_p(x, t) + v(x, t) \\
  		&= \frac{1}{\sqrt{12 \pi t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{12t}} \phi(y) dy + \frac{1}{3} \sin x + C_1 x + C_2.
  \end{align*}
  $$
  

