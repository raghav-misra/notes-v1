# differential equations.

## hi goat.

Here is the book/exercises link: [Materials for Math 246 (umd.edu)](https://courses.math.umd.edu/math246/NODE/2223F/).

## 0.1 ~ what are differential equations?

### content.

A **differential equation** is an algebraic relation that involves the derivatives of one or more unknown functions with respect to one or more independent variables.

For example, some function $p(t)$​ may satisfy the differential equation
$$
\frac{dp}{dt} = 5p.
$$
While this does not involve $t$, it is a differential equation because it relates $p$ to a derivative of $p$.

An **ordinary differential equation (ODE)** involves single-variable functions like $p(t)$​. A **partial differential equation (PDE)** involve functions with respect to multiple variables.

A differential equation is **linear** if each side can be written as a sum of terms of the following form where each term is:

- Derivative of unknown function $\times$ independent factor.
- Unknown function $\times$ independent factor.
- Entirely independent of unknown function(s).

If it cannot be expressed as such, we consider the differential equation to be **non-linear**.

The **order** of a differential equation is the highest derivative that appears in one of the terms.

Every $n$th-order, linear ODE for a function $y(t)$ can be written in the form 
$$
p_0(t) \frac{d^n y}{d t^n} + p_1(t) \frac{d^{n-1} y}{d t^{n-1}} + \dots + p_{n - 1}(t) \frac{d y}{d t} + p_n(t) y = r(t),
$$
where $p_0(t) \neq 0$, $p_1(t), \dots, p_n(t), r(t)$ are functions independent of $y(t)$.

A **system of differential equations** is a **system of ODEs** if it involves derivatives with respect to only one variable. Otherwise, it is a **system of PDEs**.

A system is a **linear system** if all equations in it are linear. Otherwise it is a **non-linear system**.

### some exercises.

Determine if the following ODEs are linear/non-linear, as well as their order.

1. $y' + 5y = t^2 + 2$ is **linear** and is **first-order**.
2. $\frac{dx}{dt} = x^2$ is **linear** and **first-order**.
3. $xy^{(5)} + x^2 y^{(3)} + \sin(x) y' - y = e^x$ is **linear** and **fifth-order**.
4. $u \frac{du}{dt} + t^2 = 3u$​ is **non-linear** and **first-order**.

Determine if the following systems are linear/non-linear, as well as their order.

1. $y'' = y' + tx'$,

   $x' = y + 3x$ is **linear** and **second-order**.

2. $x' = x + t^2 y + 6z$,

   $y' = 3x + y + e^t$,

   $z' = y + tz$​ is **linear** and **first-order**.

## 1.1 ~ intro to first-order equations.

### content.

We care about differential equations in the form
$$
\frac{dy}{dt} = f(t, y).
$$
We use $t$ as the independent variable, as the independent variable is time in a lot of cases.

If $Y(t)$ is a function defined for every $t \in (t_L, t_R)$, we say $Y(t)$ is a solution for the above equation over $(t_L, \mathbb{R})$ if:

1. $Y'(t)$ is defined for all $t \in (t_L, t_R)$.
2. $f(t, Y(t))$ is defined for all $t \in (t_L, t_R)$.
3. $Y'(t) = f(t, Y(t))$ for all $t \in (t_L, t_R)$.

Let's show that over $(-2, 2)$, $y = \sqrt{4 - t^2}$​ is a solution to the differential equation
$$
\frac{dy}{dt} = -\frac{t}{y}.
$$
To do so, notice that $y = \sqrt{4 - t^2}$ is defined over all $(-2, 2)$. In addition, $y'$ (expanded below) is also defined over all $(-2, 2)$. And we show that $y' = -t / y$:
$$
\begin{align*}
	y'
		&= \frac{d}{dt} \left[\sqrt{4 - t^2} \right] \\
    	&= -t(4 - t^2)^{-\frac{1}{2}} \\
    	&= -\frac{t}{\sqrt{4 - t^2}} \\
    	&= -\frac{t}{y}
\end{align*}
$$
Wow! Relevant questions about these equations:

1. When does it have solutions?
2. Under what condition is a solution *unique*?
3. How can we find analytic expressions for solutions?
4. How can we approximate solutions, either analytically or numerically?
5. How can we visualize solutions graphically?

An **explicit** equation has the form
$$
\frac{dy}{dt} = f(t).
$$
Equations of this form have the solution
$$
y = \int f(t) dt = F(t) + c,
$$
where $c$ is any constant and $F'(t) = f(t)$. Since there are no other solutions, we consider the above a **general solution**. We call $c$ the **parameter** of the general solution.

To find a unique solution to these equations, we require an initial condition, so that we can pick a correct value for our parameter. The initial condition takes the form
$$
y(t_I)v= y_I,
$$
where $t_I$ is the **initial point** and $y_I$​ is the **initial value**.

Let's find the solution to the following equation with initial condition $w(1) = 5$:
$$
\frac{dw}{dx} = 6x^2 + 1
$$
To do so, we first solve for the general solution.
$$
w(x) = \int (6x^2 + 1) dx = 2x^3 + x + c
$$
Next, we look to find a value for $c$ using the initial condition.
$$
\begin{align*}
	w(1) = 5 
		&= 2(1)^3 + 1 + c \\
		&= 3 + c \\
    c &= 2
\end{align*}
$$
Now, we plug in $c$ to find our unique solution:
$$
w(x) = 2x^3 + x + 2.
$$
Wahoo!

Even when we can't find an antiderivative analytically, we can show that one exists. Since $f$ is continuous over some interval $(t_L, t_R)$, the following holds for all $t \in (t_L, t_R)$:
$$
\frac{d}{dt} \int f(s) ds = f(t)
$$

### some exercises.

Consider the differential equation $\frac{dy}{dt} = 2 \sin (t) \cos (t)$.

1. Show that $y(t) = \sin^2 (t)$ is a solution for $t \in (- \infty, \infty)$​.
   $$
   \begin{align*}
   	\text{Let } y(t) &= (\sin t)^2 \\
   	y'(t) &= 2 \sin (2t) \\
   		&= 2 \sin (t) \cos t \\
   		&= \frac{dy}{dt}
   \end{align*}
   $$
   Both expressions are defined for all $t \in (-\infty, \infty)$, so the solution holds for those bounds.

2. Give a general solution to this equation.
   $$
   \begin{align*}
   	\frac{dy}{dt} &= 2 \sin (t) \cos (t) \\
   	y = \int dy &= \int 2 \sin(t) \cos (t) dt \\
   	\text{Let } u &= \sin(t), \\
   	du &= \cos (t) dt \\
   	y &= \int 2 u du \\
   		&= u^2 + c_0 \\
   		&= \sin^2 x + c_0,
   \end{align*}
   $$
   where $c_0$ is the parameter of the general solution.

## 1.2 ~ linear equations.

### content.

The following is the **linear normal form** of a (linear) first-order equation:
$$
\frac{dy}{dt} + a(t) y = f(t),
$$
where $f(t)$ is called the **forcing function** and $a(t)$ is a **coefficient function**. The ODE is considered **homogenous** when the forcing function $f(t) = 0$ for all $t$, and **non-homogenous** otherwise.

Show that the following equation is linear and put it into normal form:
$$
e^t \frac{dz}{dt} + t^2 = \frac{2t + z}{1 + t^2}
$$
We can manipulate the equation as follows:
$$
e^t \frac{dz}{dt} - (\frac{1}{1 + t^2}) z =ik
$$
