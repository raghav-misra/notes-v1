# math462; final

## 1—Where PDEs come from.

### 1.1—What is a PDE?

Skip.

### 1.2—First-order linear PDEs.

We look to solve PDEs of the form
$$
a(x, y) u_x + b(x, y) u_y = c(x, y).
$$
We say the **characteristic functions** of this problem satisfy the ODE
$$
\frac{dy}{dx} = \frac{b(x, y)}{a(x, y)}.
$$
*Process of solving for $u$.*

1. Solve for $y(x)$, the characteristic, in terms of $x$.

   Also solve for $C$, the constant in the general solution to $y$.

2. Let $z(x) = u(x, y(x))$. Then, $\frac{dz}{dx} = c(x, y)$.

3. Solve this ODE for $z$. The general solution for $u$ is identical, but the general solution for $z$ should have a constant $K$, for which we substitute value $f(C)$, for any single-variable $f$.

4. Based on the the initial condition, we find a specific definition for $f$ and the specific solution for $u$.

### 1.3—Flows, vibrations, diffusions.

### 1.4—ICs and BCs.

## 2—Waves and diffusions.

### 2.1—The wave equation.

The *initial value problem* for the wave equation is
$$
u_{xx} = c^2 u_{tt}, \qquad -\infty<x < \infty ,\, t > 0.
$$
**D'Alembert's Equation** is the solution to the wave equation *on the real line*.
$$
u(x, t) = \frac{1}{2} [\phi(x + ct) + \phi(x - ct)] + \frac{1}{2c} \int_{x-ct}^{x + ct} \psi(y) dy.
$$


### 2.2—Causality and energy.

**Causality**. For the wave defined by $u_{tt} = c^2 u_{xx}$, no part of the wave moves at a speed $> c$.

**Energy problems.** The total energy of a wave or diffusion system will be given on the exam. We need to do the differentiation/integration/substitution work to show that the energy is constant or decreases. (Depends on the system and the question.)

### 2.3—The diffusion equation.

**Heat/diffusion equation.** $u_t = ku_{xx}$.

**Maximum principle.** If $u$ satisfies the above equation in a rectangle of space-time, say $x \in [0, \ell]$ and $t \in [0, T]$, then $\max u(x, t)$ is either at $t = 0$ or when $x = 0$ or $\ell$. The same property applies to $\min u(x, t)$, as it is just $\max [-u(x, t)]$.

- *Interpretation.* A rod with no internal heat source will obtain its hottest or coldest point either initially or at one of the ends of the rod.

**Uniqueness of the Dirichlet problem.** There is only one solution to the problem
$$
\begin{align*}
u_t &= k u_{xx} \quad\text{for } 0 < x < \ell \text{ and } t > 0, \\
u(x, 0) &= \phi(x), \\
u(0, t) &= g(t), \qquad u(\ell, t) = h(t).
\end{align*}
$$

- **Proof.** Assume the contradiction. Let $u_1, u_2$ be distinct solutions. Then, consider the function $w = u_1 - u_2$. Clearly, $u(x, 0) = u(0, t) = u(\ell, t) = 0$. By maximum principle, $\max w = \min w = 0$. As such, $u_1 = u_2$, contradicting their definition. $\square$

### 2.4—Diffusion on the whole line.

We say the diffusion problem on the real line is
$$
u_t = k u_{xx} \quad (-\infty < x < \infty,\, t > 0) \\
u(x, 0) = \phi(x).
$$
Five **invariance properties** of the diffusion equation. If $u(x, t)$ is a solution,

1. **Translation.** $u(x - y, t)$ is a solution for some constant $y$.
2. **Derivative.** $u_t$ and $u_{x}$ are both solutions. (Recursively, so are further derivatives.)
3. **Combination.** If $u_1$ and $u_2$ are solutions, then $Au_1 + Bu_2$ is a solution as well, for some constants $A$ and $B$.
4. **Integral.** By (1), $u(x - y, t)$ is a solution. So is $\int_{-\infty}^{\infty} u(x-y, t) g(y) dy$, for any function $g(y)$ such that the integral converges.
5. **Dilation.** $u(\sqrt{a} x, at)$ is a solution for any $a > 0$.

The **solution to diffusion on the real line** (see start of the section) is
$$
u(x, t) = \frac{1}{\sqrt{4 \pi k t}} \int_{-\infty}^{\infty} e^{-\frac{(x - y)^2}{4kt}} \phi(y) dy,
$$
where recall that $\phi$ is the initial condition.

## 3—Reflections and sources.

### 3.1—Diffusion on the half-line.

### 3.2—Reflections of waves.

### 3.x—Inhomogeneous problems.

## 4—Boundary problems.

### 4.1—Solving Dirichlet condition.

**Heat equation** with *homogeneous Dirichlet BCs*.
$$
u(x, t) = \sum_{n=1}^{\infty}
    A_n e^{-(\frac{n \pi}{\ell})^2kt}
	\sin \left(\frac{n \pi}{\ell} x \right).
$$

### 4.2—Solving Neumann condition.

**Heat equation** with *homogeneous Neumann BCs*.
$$
u(x, t) = \frac{1}{2}A_0 + 
	\sum_{n = 1}^{\infty}A_n e^{-(\frac{n\pi}{\ell})^2 kt}
		\cos \left( \frac{n \pi}{\ell} x \right).
$$

### 4.3—Solving Robin condition.

Skipping.

## 5—Fourier series.

### 5.1—The coefficients.

*Expression* for **Fourier Sine Series** over $[0, \ell]$.
$$
\phi(x) = \sum_{n = 1}^{\infty} A_n \sin \frac{n \pi x}{\ell}.
$$
*Coefficients* for **Fourier Sine Series** over $[0, \ell]$.
$$
A_n = \frac{2}{\ell} \int_0^\ell \phi(x) \sin \frac{n \pi x}{\ell} dx.
$$

*Expression* for **Fourier Cosine Series** over $[0, \ell]$.
$$
\phi(x) = \frac{1}{2} A_0 + \sum_{n = 1}^{\infty} A_n \cos \frac{n \pi x}{\ell}.
$$
*Coefficients* for **Fourier Cosine Series** over $[0, \ell]$.
$$
\text{If $n \geq 1$}, \quad A_n = \frac{2}{\ell} \int_0^\ell \phi(x) \cos \frac{n \pi x}{\ell} dx. \\
\text{If $n = 0$}, \quad A_0 = \frac{2}{\ell} \int_0^\ell \phi(x) dx.
$$

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

### 5.2—Even, odd, periodic, complex functions.

$u$ is a **periodic function** if $\exists p$ for which $u(x + p) = u(x)$, for all $x$.

- $p$ is called the *period* of $u$.

Extensions of series.

- *Sine series* **oddly** extends $[0, \ell]$ to $[-\ell, \ell]$. Then a periodic extension to $\mathbb{R}$.
- *Cosine series* **evenly** extends $[0, \ell]$ to $[-\ell, \ell]$. Then a periodic extension to $\mathbb{R}$.
- *Full series* does a periodic extension from $[-\ell, \ell]$ to $\mathbb{R}$.

**Complex Fourier series** takes advantage of identities converting complex numbers to sines and cosines. As such, it is equivalent to the full Fourier series.
$$
c_n = \frac{1}{2\ell} \int_{-\ell}^{\ell} \phi(x) e^{-i n \pi x / \ell} dx.
$$
The series itself can be expressed as
$$
\phi(x) = \sum_{n = -\infty}^{\infty} c_n e^{in \pi x/\ell}.
$$
Let $A_n$ and $B_n$ be coefficients of a real Full Fourier Series and $C_n$ be coefficients of the analogous Complex Series. Then, for $n \geq 1$,
$$
C_0 = \frac{A_0}{2}, \quad C_n = \frac{A_n - i B_n}{2}, \quad C_{-n} = \frac{A_n + i B_n}{2}.
$$
The following two equalities are **Euler's Identities**,
$$
\cos x = \frac{e^{ix} + e^{-ix}}{2} \quad \text{and} \quad \sin x = \frac{e^{ix} - e^{-ix}}{2i},
$$
important for converting between real and complex series.

### 5.3—Orthogonality and general Fourier series.

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

### 5.4—Completeness.

**$L^2$ convergence.** The series converges to $f$ in **the $L^2$ or mean-squared sense** in $(a, b)$ if
$$
\int_a^b |f(x)|^2 \text{ is finite.}
$$
This type of convergence can be conceptually understood as asserting that the discrepancy between the series and the value of $f$ approaches zero, as the number of terms in the series increases.

**Pointwise convergence.** If $f$ is continuous and $f'$ is piecewise continuous on $[a, b]$, then the Fourier series of $f$ converges to $f$ on $x \in (a, b)$.

- *Pointwise convergence implies $L^2$ convergence.*
- *"Average Strat"* says that if $f$ is also piecewise continuous (finite discontinuities), then for some $x_0$ where $f$ is a *jump discontinuity*, the Fourier series of $f$ converges to $\frac{1}{2} [f(x_0 +) + f(x_0-)]$ ("from the right" and "from the left").

**Uniform convergence.** The Fourier series of $f$ converges to $f$ **uniformly** on $[a, b]$ provided that $f$, $f'$, and $f''$ are all continuous over $[a, b]$ and $f$ satisfies the given boundary conditions. 

- A much stronger property. *Uniform convergence implies pointwise convergence.**
- If the function is not smooth across periods, its series does not converge uniformly. But it is still likely to converge pointwise, and may converge at the average of the two endpoints (*average strat*).

**Bessel's Inequality**. If the Fourier series of $f$ is $L^2$ convergent ($\int_a^b |f(x)|^2$ is finite), then
$$
\sum_{n = 1}^{\infty} A_n^2 \int_a^b |X_n(x)|^2 dx \leq \int_a^b |f(x)|^2 dx.
$$
**Parseval's Equality**. The Fourier series of $f$ is $L^2$ convergent *if and only if* 
$$
\sum_{n = 1}^{\infty} |A_n|^2 \int_a^b |X_n(x)|^2 dx = \int_a^b |f(x)|^2 dx.
$$

## 6—Harmonic functions.

### 6.1—Laplace's equation.

**Laplace's equation.** $\Delta u = 0$.

- In one dimension, $u_{xx} = 0$.
- In two dimensions, $u_{xx} + u_{yy} = 0$.
- *Stationary* (time-independent) wave and heat equations reduce to $\Delta$.

A solution to such an equation is called a *harmonic function*. Inhomogeneous Laplace's equation is called **Poisson's equation**.

**Maximum principle.** Let $D$ be a connected, bounded open set (endpoints excluded) in either 2D or 3D space. Then, let $u(x, y)$ or $u(x, y, z)$ be a *harmonic function* which is continuous on $D$.

- Then, the minimum and maximum values of $u$ are obtained on the boundary of $D$, and nowhere inside $D$. (Unless $u$ is a constant function.)

**Uniqueness of the Dirichlet problem.** Consider the functions $u$ and $v$ such that
$$
\begin{align*}
	\Delta u = f \quad \text{in } D, 
	&\qquad \Delta v = f\quad \text{in } D, \\
	u = h \quad \text{on boundary of } D,
	&\qquad v = h \quad \text{on boundary of } D.
\end{align*}
$$

- Then, $u = v$ over $D$. **Proof.** Let $w = u - v$. Then $w$ is harmonic and is zero along all boundaries. By maximum principle, $\max w = \min w = 0$. As such, $w = 0$ and $u = v$.

**Invariance.** Laplace's equation is invariant under rigid motions. (Transform, rotate.)

### 6.2—Rectangles and cubes.

### 6.3—Poisson's formula.