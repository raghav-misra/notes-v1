# math411 / exam01

## 10.1: $\mathbb{R}^n$ and scalar products

Vector of length $n$ is in $\mathbb{R}^n$. 

- $u$ and $v$ are equal iff each component is equal.
- Can scale vectors by a constant.
- Adding vectors by adding components.
- $\mathbf{u} - \mathbf{v} = \mathbf{u} + (-\mathbf{v})$

**Scalar product** $\mathbf{u} \cdot \mathbf{v}$ is the sum of the products of each component.

The **norm** of a vector is defined as
$$
\|\mathbf{u}\| = \sqrt{\mathbf{u} \cdot \mathbf{u}} = \left|\sum_{i = 1}^{n} u_i^2 \right|.
$$
The distance function is $\text{dist}(\mathbf{u}, \mathbf{v}) = \|\mathbf{u} - \mathbf{v}\|$.

Two vectors are **orthogonal** if their scalar product is zero.

## 10.2: convergent sequences in $\mathbb{R}^n$

A sequence $\{\mathbf{u}_k\}$ *converges* to $\mathbf{u}$ if for each $\epsilon > 0$, there is an index $K$ such that
$$
\text{dist}(\mathbf{u}_k, \mathbf{u}) = \|\mathbf{u}_k - \mathbf{u}\| < \epsilon, \qquad \forall k \geq K.
$$
**Componentwise convergence theorem** says that $\{\mathbf{u}_k\}$ converges to $\mathbf{u}$ if and only each component sequence $p_i(\mathbf{u})$ converges to $\mathbf{u}_i$.

- If every component converges as desired, it is said the sequence converges *componentwise*. By the theorem, componentwise convergence implies convergence.

## 10.3: open and closed sets in $\mathbb{R}^n$

The **open ball** of radius $r > 0$ around $\mathbf{u} \in \mathbb{R}^n$ is defined as
$$
\mathcal{B}_r(\mathbf{u}) = \{ \mathbf{v} \in \mathbb{R}^n \mid \text{dist}(\mathbf{u}, \mathbf{v}) < r \}.
$$
A point $\mathbf{u} \in A$ is called an **interior point of $A$** if there exists an open ball around $\mathbf{u}$ which is completely contained in $A$.

- The set $\text{int} \ A$ is the set of all interior points of $A$.

A set $S$ is **open in $\mathbb{R}^n$** if point in $S$ is an interior point of $S$.

- That is, $\text{int} \ A = A$.

A set $S$ is **closed in $\mathbb{R}^n$** if every convergent sequence in $S$ converges to a point which is in $S$.

**Complementing Characterization** states that the complement set of an open set is closed, and vice versa.

**Proposition 10.17:**

- The intersection of closed sets is closed.
- The union of open sets is open.

**Proposition 10.18:**

- The intersection of a *finite* number of open sets is open.
- The union of a *finite* number of closed sets is closed.

A **boundary point** of a set is in the set, and each open ball around it contains points which are both inside and outside the set.

An **exterior point** is one which is not in the set.

## 11.1: continuous functions and mappings

A **mapping** is a function where the codomain is $\mathbb{R}^m$ for $m > 1$.

A mapping $F: A \rightarrow \mathbb{R}^m$ is **continuous at the point** $\mathbf{u}$ if for every sequence that converges to $\mathbf{u}$, its image sequence under $F$ converges to $F(\mathbf{u})$.

- Natural extension of function continuity.

Generally, a mapping is **continuous** if it is *continuous at every point* in its domain.

The projection function $p_i$ for some index $i$ is continuous by definition.

- *Why is this useful?* It means that multivariate functions can be shown continuous for any polynomials in their component variables $x$, $y$, $z$, etc... by pairing it with the continuity of polynomials and sum/product/composition of continuous functions.

Mappings remain continuous under sums, products, compositions.

**Componentwise continuity criterion** states that a mapping is continuous if and only if each of its component functions (return value components) are also continuous.

**$\epsilon-\delta$ criterion for continuity of mappings**: $F$ is continuous at $\mathbf{u}$ if for all $\epsilon > 0$, there exists a positive $\delta$ such that for any $\mathbf{v}$ in the domain,
$$
\text{dist}(F(\mathbf{u}), F(\mathbf{v})) < \epsilon \qquad \text{if} \ \text{dist}(\mathbf{u}, \mathbf{v}) < \delta.
$$
**Corollary 11.13**. If $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is continuous and $c$ is a real number. 

- $\{\mathbf{u} \in \mathbb{R}^n | f(\mathbf{u}) <c \}$ and $\{\mathbf{u} \in \mathbb{R}^n | f(\mathbf{u}) > c \}$ are **open**.
- $\{\mathbf{u} \in \mathbb{R}^n | f(\mathbf{u}) \leq c \}$ and $\{\mathbf{u} \in \mathbb{R}^n | f(\mathbf{u}) \geq c \}$ are **closed**.

## 11.2: seq. compactness + evt + uni. continuity.

Let $A \in \mathbb{R}^n$. Then $A$ is **sequentially compact** if every sequence in $A$ has a subsequence which converges to a point in $A$.

Let $A \in \mathbb{R}^n$. Then $A$ is bounded if there exists $M$ for which
$$
\|\mathbf{u}\| \leq M \qquad \text{for all } \mathbf{u} \in A.
$$
**Sequential Compactness Theorem** states that a subset of $\mathbb{R}^n$ is sequentially compact if and only if it is closed and bounded.

Let $A \in \mathbb{R}^n$ be nonempty and sequentially compact. **Extreme Value Theorem** states that $f: A \rightarrow \mathbb{R}$, if continuous, attains a smallest and largest value.

- *More!* Let $A \in \mathbb{R}^n$ be nonempty. Then $A$ has EVP if and only if it is sequentially compact.

A mapping $F: A \rightarrow \mathbb{R}^m$ is said to be **uniformly continuous** if for any two sequences in $A$, $\{\mathbf{u}_k\}$ and $\{\mathbf{v}_k\}$, such that $\lim_{k \rightarrow \infty} \text{dist}(\mathbf{u}_k, \mathbf{v}_k) = 0$,
$$
\lim_{k \rightarrow \infty} \text{dist}(F(\mathbf{u}_k), F(\mathbf{v}_k)) = 0.
$$
*Equivalent:* For any two points $\mathbf{u}$ and $\mathbf{v}$ and $\epsilon > 0$, there exists a $\delta > 0$ such that
$$
\text{dist}(F(\mathbf{u}), F(\mathbf{v})) < \epsilon \qquad \text{if} \ \text{dist}(\mathbf{u}, \mathbf{v}) < \delta.
$$
*If a function is continuous over its domain and its domain is sequentially compact, the function is uniformly continuous.*

## 11.3: pathwise connectedness + ivt

Let $a$ and $b$ be reals with $a < b$. Then, a continuous mapping $\gamma: [a, b] \rightarrow \mathbb{R}^n$ is called a **parameterized path**. $\gamma$'s domain is a called the **parameter space**, and the image of $\gamma$ is called a **path**.

- Distinction: a path is a subset of $\mathbb{R}^n$, while a parameterized path is a *mapping*.

A *path joining two points $\mathbf{u}$* and $\mathbf{v}$ in $A$ refers to the image of $\gamma: [a, b] \rightarrow \mathbb{R}^n$ where $\gamma(a) = \mathbf{u}$, $\gamma(b) = \mathbf{v}$, and the image of $\gamma$ is contained in $A$.

A subset $A$ of $\mathbb{R}^n$ is said to be **pathwise-connected** if every two points in $A$ can be joined by a path in $A$.

- This must be an interval in $\mathbb{R}$.

The image of a continuous function on a pathwise-connected domain is also pathwise-connected.

- If the image is in $\mathbb{R}$, it must then be an interval.

A subset $A$ of $\mathbb{R}^n$ is said to have the **intermediate value property** if every continuous function $f: A \rightarrow \mathbb{R}$ has an interval as its image.

- Then, all pathwise-connected domains have the intermediate value property.

## 11.4: connectedness + ivp

Let $A \in \mathbb{R}^n$. Two open subsets $U$ and $V$ of $\mathbb{R}^n$ separate $A$ if:

1. $A \cap U$ and $A \cap V$ are nonempty.
2. $(A \cap U) \cap (A \cap V) = \emptyset$.
3. $(A \cap U) \cup (A \cap V) = A$.

A subset $A$ of $\mathbb{R}^n$ is **connected** if there do not exist two open subsets of $\mathbb{R}^n$ which separate $A$.

A set is connected if and only if it has the intermediate value property.

- So, all pathwise-connected sets are connected.
