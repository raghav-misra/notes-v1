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

**Note.** The partial derivative of $f$ can be calculated by holding all over components fixed and differentiating $f$ as if it was a single-variable function of the co

## 13.3: mean value theorem + directional derivatives

## 14.1: first-order approximation + tangent planes + affine functions

## 14.2: quadratic functions + hessian matrices + second derivatives

## 14.3: second order approximation + second-derivative test

