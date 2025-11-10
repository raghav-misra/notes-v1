# math411 / exam02

## 13.1: limits

### content

**Recall.** For a function $f: I \rightarrow \R$ over interval $I$, $f$ is *differentiable* at $x_0$ if
$$
\lim_{x \rightarrow x_0} \frac{f(x) - f(x_0)}{x - x_0} \ \text{exists.}
$$
If $f$ is differentiable at every point in $I$, we say it is *differentiable* generally and let $f'(x_0)$ be the value of the limit above.

**Definition.** Let $A \sub \R^n$ and $x \in \R^n$. Then $x$ is a *limit point* of $A$ if there is a sequence in $A \setminus \{x\}$ which converges to $x$.

**Definition.** Let $A \sub \R^n$ and $x$ be a limit point of $A$. Given a function $f: A \rightarrow \R^n$ and $\ell \in \R$,  we write that
$$
\lim_{x \rightarrow x_0} f(x) = \ell
$$
if whenever $\{x_k\}$ in $A \setminus \{x_0\}$ converges to $x_0$, $\{f(x_k)\}$ converges to $\ell$.

**Note.** Let $A \sub \R^n$ and $x$ be a limit point of $A$.  From our definition of continuity, the function $f: A \rightarrow \R$ is continuous at $x_0$ if and only if
$$
\lim_{\mathbf{x} \rightarrow x_0} f(\mathbf{x}) = f(x_0).
$$
**Example.** Let $x_0 \in \R^n$. Then $\lim_{\mathbf{x} \rightarrow x_0} \| \mathbf{x} \| = \|x_0\|$. This follows from the continuity of the norm function.

**Note.** If a limit is the product or sum of two limits that exist, you can express it like that.

**Example.** Showing a limit doesn't exist can be done by showing two "paths" to the point yield different results.

- Consider the expression $\lim_{(x, y) \rightarrow (0, 0)} \frac{x_0 y_0}{x_0^2 + y_0^2}$. Clearly substituting the values (possible since the expression is a polynomial) yields $0/0$ which is indeterminate. 

- Notice that the sequence $(1/k, 1/k)$ converges to $(0, 0)$. Substituting $(1/k, 1/k)$ into the limit expression yields
  $$
  \frac{(1/k)(1/k)}{(1/k)^2 + (1/k)^2} = \frac{(1/k^2)}{(2/k^2)} = 1/2.
  $$
  For all $k$, the expression yields $1/2$, so if the limit existed, it must have a value of $1/2$.

- Next we consider the sequence $(1/k, 0)$, which also clearly converges to $(0, 0)$. Substituting $(1/k, 0)$ into the limit expression obviously yields $0$, so if the limit existed, it must be $0$.

- These two contradict each other so the limit doesn't exist.

### practice

Prove that $\lim_{(x, y) \rightarrow (0, 0)} \frac{x^3 y}{x^2 + y^4}  =0$. **Answer:**

- By the Squeeze Theorem, the above holds if $\lim_{(x, y) \rightarrow (0, 0)} \left| \frac{x^3 y}{x^2 + y^4} \right|  =0$.

- We can rewrite the expression in the limit:
  $$
  \left| \frac{x^3 y}{x^2 + y^4} \right| = \frac{|x^3| |y|}{x^2 + y^4} = \left(\frac{x^2}{x^2 + y^4}\right)  |x|  |y| \leq |x| |y|.
  $$

- $x$ and $y$ are continuous, $\lim_{(x, y) \rightarrow (0, 0)} |x| = 0$ and $\lim_{(x, y) \rightarrow (0, 0)} |y| = 0$.

- Since $\left(\frac{x^2}{x^2 + y^4}\right)$ must be non-negative,
  $$
  0 \leq \left(\frac{x^2}{x^2 + y^4}\right)  |x|  |y| \leq |x| |y|.
  $$

- The limit follows by the Squeeze Theorem.

Let $m$ and $n$ be naturals. Show that the limit
$$
\lim_{(x, y) \rightarrow (0, 0)} \frac{x^n y^m}{x^2 + y^2}
$$
exists if and only if $m + n > 2$. **Answer:**

- *First we prove the forward direction.* Assume the limit exists for some natural $m$ and $n$. By way of contradiction, assume $m + n \leq 2$. By definition of natural numbers, $m = n = 1$ is the only combination which satisfies this condition. Then the limit becomes
  $$
  \lim_{(x, y) \rightarrow (0, 0)} \frac{xy}{x^2 + y^2}.
  $$

- Consider the sequence $\{(1/k, 1/k)\} \rightarrow 0$. Substituting into the limit,
  $$
  \frac{1/k^2}{2/k^2} = \frac{1}{2}.
  $$

- Then, if the limit were to exist, it must converge to $1/2$. Now we look at the sequence $\{(1/k, 0)\} \rightarrow 0$. Substituting into the limit yields zero. We see that two different paths yield different endpoints, so the limit mustn't exist. $\square$

- *Next we prove the reverse direction.* Assume $m + n > 2$. By definition of the naturals, at least one of $m$ and $n$ must be $\geq 2$. Without loss of generality, assume that $n \geq 2$. This is okay because $x$ and $y$ are used equivalently in the expression and the limit $(0,0)$.

- By the Squeeze Theorem, the desired limit holds if the limit of its absolute value holds as well. Then, we consider the following expression:
  $$
  0 \leq \frac{|x^n||y^m|}{x^2 + y^2} = \left(\frac{x^2}{x^2 + y^2}\right) |x^{n-2}||{y^m}| \leq |x^{n - 2}||y^m|.
  $$
  Since $0^{n - 2} = 0$ and $0^m = 0$, the limit of the rightmost expression is zero.

- Then, by the Squeeze Theorem, $\left(\frac{x^2}{x^2 + y^2}\right) |x^{n-2}||{y^m}| \rightarrow 0$ as $(x, y) \rightarrow 0$, so the limit exists as desired! $\square$ 

## 13.2: partial derivatives

### content

**Definition.** Let $O$ be an open subset of $\R^n$ which contains the point $\mathbf{x}$. Then, a function $f: O \rightarrow \R$ is said to have a *partial derivative with respect to its $i$th component at $\mathbf{x}$* provided that the limit
$$
\lim_{t \rightarrow 0} \frac{f(\mathbf{x} + t \mathbf{e}_i) - f(\mathbf{x})}{t}.
$$
If this limit exists, we denote its value by $\partial f/\partial x_i (\mathbf{x}) = f_{x_i}(\mathbf{x})$, the *partial derivative of $f$ wrt. its $i$th component at $\mathbf{x}$*.

**Note.** The partial derivative of $f$ can be calculated by holding all over components fixed and differentiating $f$ as if it was a single-variable function of the component you which to get the partial derivative for.

**Note.** For functions of single real variables, *differentiability implies continuity*. This is not necessarily the case for a multi-variable function which has first-order partial derivatives.

**Definition.** Let $O$ be an open subset of $\R^n$. Then $f: O \rightarrow \R$ is *continuously differentiable* if it has first-order partial derivatives such that each partial derivative $\partial f/\partial x_i : O \rightarrow \R$ is continuous for each component $1 \leq i \leq n$. 

- If a function is *continuously differentiable*, it is *continuous*. Proved by MVT later.

**Definition.** Let $O$ be an open subset of $\R^n$. Then $f: O \rightarrow \R$ has *second-order partial derivatives* provided that it has first-order partial derivatives and that, for each component index $1 \leq i \leq n$, the function $\partial f / \partial x_i$ also has first-order partial derivatives. 

- If a function has *continuous second-order partial derivatives*, it is *continuously differentiable*.

**Note.** Order of derivatives taken does not matter, i.e., $f_{xy} = f_{yx}$.

### practice

Prove that the function $g: \R^2 \rightarrow \R$ defined by
$$
g(x, y) = \begin{cases}
x^2 y^4 / (x^2 + y^2) &\text{if} \ (x, y) \neq (0,0),\\
0 &\text{if} \ (x, y) = (0,0)
\end{cases}
$$
 has first-order partial derivatives. Is the function continuously differentiable? **Answer:**

- For $(x, y) \neq (0, 0)$, partial derivatives can be found using the quotient rule:
  $$
  \frac{\partial g}{\partial x} = \frac{(2xy^4)(x^2 + y^2) - (x^2y^4)(2x)}{(x^2 + y^2)^2}
  = \frac{2x^3y^4 + 2xy^6 - 2x^3y^4}{(x^2 + y^2)^2} = \frac{2xy^6}{(x^2 + y^2)^2}.
  $$

  $$
  \frac{\partial g}{\partial y} = \frac{(4x^2y^3)(x^2 + y^2) - (x^2y^4)(2y)}{(x^2 + y^2)^2}
  = \frac{4x^4y^3 + 4x^2y^5 - 2x^2 y^5}{(x^2 + y^2)^2} = \frac{4x^4y^3 + 2x^2y^5}{(x^2+y^2)^2}.
  $$

  

- For $(x, y) = (0, 0)$ we apply the limit definitions of partial derivatives.
  $$
  \frac{\partial g}{\partial x}(0, 0) = \lim_{t \rightarrow 0} \frac{g(t, 0) - g(0, 0)}{t} 
  = \frac{\frac{0}{t^2}}{t} = 0.
  $$

  $$
  \frac{\partial g}{\partial y}(0, 0) = \lim_{t \rightarrow 0} \frac{g(0, t) - g(0, 0)}{t}
  = \frac{\frac{0}{t^2}}{t} = 0.
  $$

- We have shown that $g$'s partial derivatives exist for all $(x, y) \in \R^2$. Now we turn to $g$'s continuous differentiability. By the continuity of polynomials, both partial derivatives are continuous at $(x, y) \neq (0, 0)$. So we want to show that $\lim_{(x, y) \rightarrow (0, 0)} \frac{\partial g}{\partial x} = \lim_{(x, y) \rightarrow (0, 0)} \frac{\partial g}{\partial y} = 0$. (This is because we already showed the value of the partial derivatives at this point was zero in the previous step.) To show this, we want to analyze the limits of our $(x, y) \neq (0, 0)$ partial derivative expressions as they approach $(0, 0)$. Let's upper bound these expressions.
  $$
  \frac{2|x|y^6}{(x^2 + y^2)^2} \leq \frac{2|x|y^6}{(0 + y^2)^2} = \frac{2|x|y^6}{y^4} = 2|x|y^2.
  $$

  $$
  \frac{|4x^4y^3 + 2x^2y^5|}{(x^2+y^2)^2} = \frac{2x^2|y^3|(2x^2 + y^2)}{(x^2 + y^2)^2}
  = \frac{2x^2|y^3|}{x^2 + y^2} \cdot \frac{2x^2 + y^2}{x^2 + y^2}
  \leq \frac{2x^2|y^3|}{0 + y^2} \cdot \frac{2x^2 + 2y^2}{x^2 + y^2} = 4|x^2||y|.
  $$

- As $(x, y) \rightarrow (0, 0)$, both expressions on the rightside go to zero, so we apply the squeeze theorem to see our initial expressions go to zero as well! Thus, our first-order partial derivatives are continuous, and $g$ is continuously differentiable!

## 13.3: mean value theorem + directional derivatives

### content

**Definition.** The *directional derivative* of a function $f$ in the direction of point $\mathbf{p}$ at $\mathbf{x}$ is defined as
$$
\frac{\partial f}{\partial \mathbf{p}}(\mathbf{x}) = \lim_{t \rightarrow 0} \frac{f(\mathbf{x} + t \mathbf{p}) - f(\mathbf{x})}{t}.
$$
**Directional Derivative Theorem.** The above is equivalent to $\sum_{i = 1}^{n} p_i \frac{\partial f}{\partial x_i}(\mathbf{x})$. That is, the dot product of $\mathbf{p}$ and the vector whose components are the partial derivatives of $f$ at point $\mathbf{x}$. (Gradient.)

**Definition.** The *gradient* of $f$ at $\mathbf{x}$ is defined by the vector whose components are the partial derivatives of $f$ at point $\mathbf{x}$.
$$
\nabla f(\mathbf{x}) = \left( \frac{\partial f}{\partial x_1}(\mathbf{x}), \frac{\partial f}{\partial x_2}(\mathbf{x}), \dots, \frac{\partial f}{\partial x_n}(\mathbf{x}) \right).
$$
**Mean Value Theorem.** Let $O$ be an open subset of $\R^n$ and suppose $f: O \rightarrow \R$ is continuously differentiable. If the segment joining the points $\mathbf{x}$ and $\mathbf{x + h}$ lies in $O$, then there is a number $\theta$ with $0 < \theta < 1$ such that
$$
f(\mathbf{x+h}) - f(\mathbf{x}) = \nabla f(\mathbf{x + \theta h}) \cdot \mathbf{h}.
$$

- How do we interpret this? Recall MVT for single-variable functions: $f(b) - f(a) = f'(c) \cdot (b - a)$.
- In this case, our $b$ is actually $\mathbf{x + h}$, $a$ is obviously $\mathbf{x}$, and $\theta$ is our variable which allows us to determine the value of $c = \mathbf{x} + \theta \mathbf{h}$.

**Note.** Mentioned previously, but the MVT lets us prove that a continuously differentiable function is continuous.

### practice

 Define the function $f: \R^2 \rightarrow \R$ by
$$
f(x, y) = \begin{cases}
(x/|y|) \sqrt{x^2 + y^2} &\text{if} \ y \neq 0, \\
0 &\text{if} \ y = 0.
\end{cases}
$$

- Prove that $f$ is not continuous at $(0, 0)$. **Answer.**

  - We can do this by finding two "paths" which approach $(0, 0)$ but their image under $f$ does not approach $0$. Consider the sequence $\{1/k, 1/k\} \rightarrow (0, 0)$. The limit of its image sequence under $f$ is
    $$
    \lim_{k \rightarrow \infty} f(1/k, 1/k) =  (1/k)/(1/k) \sqrt{(2/k^2)} = (\sqrt2) / k = 0.
    $$

  - Next, consider the path $y = x^2$. Letting $x \rightarrow 0$ would imply that $y \rightarrow 0$ as well. Then,
    $$
    \lim_{x \rightarrow 0} f(x, x^2) = x/(x^2) \sqrt{x^2 + x^4} = x/(x^2) \sqrt{x^2(1 + x^2)} = \sqrt{1 + x^2} = 1.
    $$

  - As you can see, these two limits differ, so there must be a discontinuity at $(x, y) = (0, 0)$.

- Prove that $f$ has directional derivatives in all directions at $(0, 0)$. **Answer.**

  - Let $\mathbf{p}$ be a vector with components $(p_1, p_2)$. Then, we apply the definition of the directional derivative at the point $(0, 0)$.
    $$
    \frac{\partial f}{\partial \mathbf{p}}(0, 0) = \lim_{t \rightarrow 0} \frac{f(tp_1, tp_2) - f(0, 0)}{t} = \frac{tp_1 \sqrt{t^2(p_1^2+p_2^2)}}{t|tp_2|} = \frac{p_1 \sqrt{p_1^2 + p_2^2}}{|p_2|}.
    $$

  - Clearly, the above limit exists for all points $(p_1, p_2)$ where $p_2 \neq 0$. Let us analyze the case $p_2 = 0$ further. By definition of $f$, when $p_2 = 0$, the expression $f(tp_1, tp_2) = 0$, so the limit is defined there as well. 

- Prove that for any $c$, there exists a vector $\mathbf{p}$ of norm $1$ such that $\frac{\partial f}{\partial \mathbf{p}} (0, 0) = c$. **Answer.**

  - We can find an acceptable $p_1$ and $p_2$ given a $c$ using our expression for the directional derivative found above. Clearly, the norm of $(p_1, p_2)$ is $1$, so the expression resolves to $p_1/|p_2| = c$. Then, $p_1 = c|p_2|$. 
    $$
    \|(p_1, p_2)\| = \sqrt{p_2^2 + c^2p_2^2} = p_2 \sqrt{1 + c^2} = 1.
    $$

  - Then, $p_2 = \frac{1}{\sqrt{1 + c^2}}$ and $p_1 = \frac{c}{\sqrt{1 + c^2}}$. So we have found a satisfactory vector!

## 14.1: first-order approximation + tangent planes + affine functions

### content

**Definition.** Let $O$ be an open subset of $\R^n$ which contains the point $\mathbf{x}$. For a positive integer $k$, two functions $f: O \rightarrow \R$ and $g: O \rightarrow \R$ are *$k$-th order approximations of each other* if
$$
\lim_{\mathbf{h} \rightarrow \mathbf{0}} \frac{f(\mathbf{x + h}) - g(\mathbf{x + h})}{\|\mathbf{h}\|^k} = 0.
$$
**First-Order Approximation Theorem.** Let $O$ be an open subset of $\R^n$ which contains the point $\mathbf{x}$ and suppose $f: O \rightarrow \R$ is continuously differentiable. Then,
$$
\lim_{\mathbf{h \rightarrow 0}} \frac{f(\mathbf{x+h}) - [f(\mathbf{x}) + (\nabla f(\mathbf{x}) \cdot  \mathbf{h})  ]}{\|\mathbf{h}\|} = 0.
$$
**Definition.** Let $O$ be an open subset of $\R^2$ which contains the point $(x_0, y_0)$ and suppose $f: O \rightarrow \R$ is continuous at $(x_0, y_0)$. Then, the *tangent plane* to $f$ at $(x_0, y_0, f(x_0, y_0))$ is described by the function
$$
T(x, y) = a + b(x - x_0) + c(y - y_0),
$$
where $a$, $b$, and $c$ are real numbers.

- Furthermore, the tangent plane has the property that
  $$
  \lim_{(x, y) \rightarrow (x_0, y_0)} \frac{f(x, y) - T(x, y)}{\sqrt{(x - x_0)^2 + (y - y_0)^2}} = 0.
  $$

- The tangent plane is a first-order approximation of $f$. This is clear by using $\mathbf{h} = (x - x_0, y - y_0)$; the above property then satisfies the definition of the $k$-th order approximation for $k = 1$.

**Definition.** A function is *affine* if it is defined by
$$
g(\mathbf{u}) = c + \sum_{i = 1}^{n} a_i u_i.
$$
**Corollary.** Let $O$ be an open subset of $\R^n$ which contains the point $\mathbf{x}$ and suppose $f: O \rightarrow \R$ is continuously differentiable. Then, there exists an affine function that is a first-order approximation of $f$ at the point $\mathbf{x}$, defined asg
$$
g(\mathbf{u}) = f(\mathbf{x}) + [\nabla f(\mathbf{x}) \cdot (\mathbf{u - x})].
$$

- This is a pretty natural extension of the "tangent line" defined as $g(x) = f(a) + f'(a) [x - a]$. 

### practice

Define $f(x, y) = e^{\sin(x - y)}$. Find the first-order approximating affine function to $f$ at $(0, 0)$. **Answer.**

- General equation is $g(\mathbf{u}) = f(\mathbf{x}) + [\nabla f(\mathbf{x}) \cdot (u - x)]$.
- $f(0, 0) = 1$.
- $f_x(x, y) = \cos (x - y) e^{\sin (x - y)}$ and $f_y(x, y) = -\cos(x - y) e^{\sin(x - y)}$.
- $f_x(0, 0) = 1$ and $f_y(0, 0) = -1$.
- Substituting, you yield $g(u_1, u_2) = 1 +  u_1 - u_2$.

Prove the following limit expression is true.
$$
\lim_{(x, y) \rightarrow (0, 0)} \frac{(1 + 2x + y^2)^{3/2} - 1 - 3x}{\sqrt{x^2 + y^2}} = 0.
$$
**Answer.** Apply the First-Order Approximation Theorem to $f(x, y) = (1 + 2x + y^2)^{3/2}$ at $(0,0)$.

## 14.2: quadratic functions + hessian matrices + second derivatives

**Definition.** I hope I know what a matrix is.

**Definition.** For a matrix $\mathbf{A}$, $Q(\mathbf{x}) = (\mathbf{Ax})\mathbf{x}$ is the quadratic function associated with $\mathbf{A}$. 

-  A linear combination of $x_i x_j$ terms, which means highest degree on a term is $2$.

**Definition.** The *Hessian matrix* of $f$ at the point $\mathbf{x}$, written $\nabla^2 f(\mathbf{x})$ is the $n \times n$ matrix which satisfies
$$
(\nabla^2 f(\mathbf{x}))_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j} (\mathbf{x}).
$$

- Basically a matrix of all possible second derivatives.
- The $i$-th row of the Hessian is the gradient of the $i$-th first-order derivative.
- The Hessian is symmetric, as its $ij$-th entry is equal to its $ji$-th entry.

**Theorem.** Let $O$ be an open subset of $\R^n$ which contains $\mathbf{x}$ and suppose $f: O \rightarrow \R$ has continuous second-order partial derivatives. Choose $r > 0$ such that $\mathcal{B}_r(\mathbf{x}) \sube O$. Then if $\|\mathbf{h}\| < r$ and $|t| < 1$,
$$
\frac{d}{dt} [f(\mathbf{x} + t \mathbf{h})] = \lang \nabla f(\mathbf{x} + t \mathbf{h}), \mathbf{h}\rang \quad \text{and} \quad \frac{d^2}{dt^2}[f(\mathbf{x} + t \mathbf{h})] =\lang \nabla^2 f(\mathbf{x} + t \mathbf{h}), \mathbf{h}\rang.
$$
**Definition.** An $n \times n$ matrix $\mathbf{A}$ is *positive definite* provided $\mathbf{Au} \cdot \mathbf{u} > 0$ for all nonzero $\mathbf{u} \in \R^n$. It is *negative definite* provided $\mathbf{Au} \cdot \mathbf{u} < 0$ for all nonzero $\mathbf{u} \in \R^n$.

- The 2D symmetric matrix $\begin{bmatrix} a & b \\ b & c \end{bmatrix}$ is positive definite if and only if $a > 0$ and $ac - b^2 > 0$. It is negative definite if and only if $a < 0$ and $ac - b^2 > 0$.

## 14.3: second order approximation + second-derivative test

