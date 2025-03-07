# math410; quiz01

## Things to know

**Triangle Inequality:** $\forall a, b \in \mathbb{R}$,
$$
|a + b| \leq |a| + |b|.
$$
A subset $S \sube \mathbb{R}$ is:

- **Bounded above** if $\exists r \in \mathbb{R}$ such that $s \leq r$ for all $s \in S$.  
- **Bounded below** if $\exists r \in \mathbb{R}$ such that $s \geq r$ for all $s \in S$.
- Generally, **bounded** if it is both bounded above and below.

The *least upper bound* of a set $S$ is called its **supremum** ($\sup S$).

The *greatest lower bound* of a set $S$ is called its **infinum** ($\inf S$).

Proving $\sup S$ and $\inf S$ for $S = (0, 1)$:

- $\sup S = 1$. **Proof:**

  By definition, if $x \in (0, 1)$, then $x \leq 1$. So $1$ is an upper bound of set $S$.

  We prove this by contradiction: assume $\sup S \neq 1$. Since $1$ is still an upper bound of $S$, $0 < \sup S < 1$. Let $x$ be $\sup S$.

  But consider the number $\frac{1 + x}{2}$.
  $$
  \frac{1 + x}{2} < \frac{1 + 1}{2} = 1
  $$

  $$
  \frac{1 + x}{2} > \frac{x + x}{2} = x
  $$

  So we have,
  $$
  0 < x < \frac{1 + x}{2} < 1
  $$
  It follows that $\frac{1 + x}{2} \in (0, 1)$ and we have a contradiction: a number larger than our supremum $x$ is present in $S$.

  So $\sup S = 1$. $\square$

- $\inf S = 0$. **Proof:** Follows similarly to previous proof.


The **completeness axiom** states:
$$
S \sube \mathbb{R}, S \text{ is nonempty}, S \text{ is bdd above} \Rightarrow \sup S \text{ exists}.
$$
**Archimedean Principle:** Let $\epsilon > 0$ and $c$ be an arbitrarily large number.
$$
\begin{align*}
	\exists n 
		&\in \mathbb{N}, \text{s.t. } c < m 
		&\text{(a)} \\
	\exists m 
		&\in \mathbb{N}, \text{s.t. } \frac{1}{m} <  \epsilon
		&\text{(b)}
\end{align*}
$$
