# real analysis.

## hi goat.

Using the textbook *Understanding Analysis* by Stephen Abbott.

## 1 ~ the real numbers.

### 1.1 ~ discussion: the irrationality of $\sqrt{2}$.

**Theorem:** There is no rational number whose square is $2$​.

>**Proof:** We will prove this by contradiction. Let there exist two integers $p$ and $q$, where $q \neq 0$, such that $(p / q)^2 = 2$​ (definition of a rational number). 
>
>We also assume $p$ and $q$ have no common factors. If they did, we could simplify the above fraction and find new values for $p$ and $q$.
>
>With some arithmetic, we find that,
>$$
>p^2 = 2q^2
>$$
>From the above, we gather that $p^2$ must be even, and $p$ must also be even. For some integer $r$,
>$$
>p = 2r
>$$
>Substituting $2r$ in for $p$​,
>$$
>\begin{align*}
>	(2r)^2 &= 2q^2 \\
>	4r^2 &= 2q^2 \\
>	2r^2 &= q^2
>\end{align*}
>$$
>We can gather from the above that $q^2$ and $q$ are both even, which means that both $p$ and $q$ are both divisible by $2$. And here lies our contradiction. $\square$

We denote the set of all natural numbers with $\mathbb{N}$:
$$
\mathbb{N} = \{1, 2, 3, 4, \dots\}
$$
The natural numbers are *closed* under addition, i.e., adding two numbers in $\mathbb{N}$ will always yield a number also in $\mathbb{N}$. However, $\mathbb{N}$ is not closed under subtraction:
$$
2 - 3 = -1 \notin \mathbb{N}
$$
For this, we have the set of *integers* $\mathbb{Z}$:
$$
\mathbb{Z} = \{\dots, -4, -3, -2, -1, 0, 1, 2, 3, 4, \dots\}
$$
Intuitively, $\mathbb{Z}$ is now also closed under subtraction and multiplication, but for division, we must define the set of *rational numbers* $\mathbb{Q}$:
$$
\mathbb{Q} = \{\text{all fractions } \frac{p}{q} \text{ for all integers $p$ and $q$ where $q \neq 0$} \}
$$
The properties of $\mathbb{Q}$ make it a **field**, which is a set for which the following hold:

1. Addition and multiplication are well-defined and obey the commutative, associative, and distributive properties.
2. All elements must have *additive inverses*. If $a$ is in a set, there must also exist $b$ such that $a + b = 0$.
3. All elements must have *multiplicative inverses*. If $a$ is in a set, there must also exist $b$ such that $a \cdot b = 1$. 

From the last two points, it's easy to see why neither $\mathbb{N}$ or $\mathbb{Z}$​ are fields.

The set $\mathbb{Q}$ also has an **order** defined on it. That is, for any two elements $a$ and $b$ in $\mathbb{Q}$, either $a > b$, $a = b$, or $a < b$​.

Since $\mathbb{Q}$ is a field, we can add, subtract, multiply, and divide the numbers in the set. What's missing? $\sqrt{2}$, among other things.

We introduce the *real numbers* $\mathbb{R}$. Loosely, it is just $\mathbb{Q}$ with all the "holes" (like $\sqrt{2}$) filled in, but a stronger definition will come later. It is the union of the sets of rational and irrational numbers.

### 1.2 ~ some preliminaries.

A **function** $f: A \rightarrow B$ is a rule/mapping that takes each element $x \in A$ and associates it with an element in $B$​.

1. For the above example, $A$ is the **domain** of the function.
2. The **range** of $f$ is the subset of values of $B$ that $f(x)$ can take on.

**Theorem:** Two real numbers $a$ and $b$ are equal *if and only if* for every real number $\epsilon > 0$, it follows that $|a - b| < \epsilon$​.

> **Proof (LTR):** If $a = b$, then $a - b = 0$. Since $\epsilon > 0$, it follows that $\epsilon > |a - b|$. $\square$
>
> ---
>
> **Proof (RTL):** We prove this by contradiction. Assume that for every real number $\epsilon > 0$, $|a - b| < \epsilon$, and that $a$ and $b$ are not equal.
>
> If $a \neq b$, then $|a - b| \in \mathbb{R}$ and $|a - b| > 0$. Here lies our contradiction. We assume that $|a - b|$ is less than all real numbers greater than zero, but have found a real number greater than zero which is equal to $|a - b|$. Therefore, $a = b$. $\square$

**Some Exercises:** 

1. Prove that $\sqrt{3}$ is irrational.

   >**Proof:** We can prove by contradiction. Let there be a rational number $p / q$, where $p \in \mathbb{Z}$, $q \in \mathbb{Z}$, and $q \neq 0$, such that $(p / q)^2 = p^2 / q^2 = 3$. 
   >
   >We can assume that $p$ and $q$ have no common factors, or else we could just choose simpler values for $p$ and $q$​. Basic arithmetic yields
   >$$
   >p^2 = 3q^2
   >$$
   >In other words, we have $p^2$ is divisible by $3$. In addition, $p^2$ and $q^2$ must have the same parity, i.e., they are either both even or both odd.
   >
   >If both $p^2$ and $q^2$ are even, it follows that both $p$ and $q$ are also even and therefore share a common factor of $2$. This contradicts the definition of the rational number, so both $p$ and $q$ must be odd.
   >
   >There exist integers $j$ and $k$, such that $p = 2j + 1$ and $q = 2k + 1$​.
   >
   >Substitute $j$ and $k$ into the previous equation:
   >$$
   >\begin{align*}
   >	(2j + 1)^2 &= 3(2k + 1)^2 \\
   >	4j^2 + 4j + 1 &= 12k^2 + 12k + 3 \\
   >	4j^2 + 4j &= 12k^2 + 12k + 1
   >\end{align*}
   >$$
   >Here lies our contradiction. In the last equality above, LHS is even (all terms are multiples of $2$), but RHS is odd (all terms are multiples of $2$ but one). An even and odd number cannot be equal, so $\sqrt{3}$ cannot be rational. $\square$

2. Show that there is no rational number satisfying $2^r = 3$.

   >**Proof:** We assume the contradiction. Let there be a rational number $r$ such that $2^r = 3$. We let $r = p/q$, where $p$ and $q$ are integers with greatest common factor of $1$, and $q \neq 0$.
   >$$
   >\begin{align*}
   >	2^r &= 3 \\
   >	2^{p/q} &= 3 \\
   >	\sqrt[q]{2^p} &= 3 \\
   >	2^p &= 3^q
   >\end{align*}
   >$$
   >Consider that $2^p$ is the product of even numbers, so $2^p$ is even. However, $3^q$ is the product of odd numbers, so it must be odd. An even and odd number cannot be equal, so we have our contradiction. There cannot be a rational $r$ such that $2^r = 3$. $\square$

3. Let $y_1 = 6$, and for each $n \in \mathbb{N}$ define $y_{n + 1} = (2y_n - 6) / 3$. Use induction to show that for all $n \in \mathbb{N}$, $y_n > -6$.

   >**Proof:** We will prove this by induction. 
   >
   >Consider the base case $y_1 = 6 > -6$.
   >
   >Say for some $i \in \mathbb{N}$, we assert that the claim holds for $y_{i}$.
   >$$
   >\begin{align*}
   >	y_{i + 1} 
   >		&= (2y_i - 6) / 3 \\
   >    	&> [2(-6) - 6] / 3 \\
   >        &= -18 / 3 \\
   >        &= -6
   >\end{align*}
   >$$
   >Given $y_i > -6$, we have shown that $y_{i + 1} > -6$ as well, for all $i \in \mathbb{N}$.

### 1.3 ~ the axiom of completeness.

$\mathbb{R}$, the set of *real numbers*, is a field just like $\mathbb{Q}$​. In other words, it is closed under addition and multiplication, and every element has an additive and multiplicative inverse.

In addition, $\mathbb{R}$ also has an ordering. For two elements $a$ and $b$ in $\mathbb{R}$, one of the following is true: $a < b$, $a = b$, or $a > b$.

Recall we said the real numbers are the rational numbers with "holes filled in." How do we formalize this?

A set $A \sube \mathbb{R}$ is **bounded above** if there exists a number $b \in \mathbb{R}$ such that $a \leq b$ for all $a \in A$. We say $b$ is an **upper bound** of $A$. Instead, if there exists some $c \in \mathbb{R}$ such that $a \geq c$ for all $a \in A$, we say $c$ is a **lower bound** of $A$.

A real number $s$ is the least upper bound of $A$, if $s$ is an upper bound of $A$, and $s$ is less than or equal to all upper bounds of $A$. We call the least upper bound the **supremum**. The equivalent for the lower bound is called the **infimum** (greatest lower bound).

The largest element of a set is its **maximum** and the smallest is its **minimum**. If the maximum exists, then it is also the supremum. If the minimum exists, then it is also the infimum. But the converse is not necessarily true. Take the following set:
$$
A = \{ \frac{1}{n} \mid n \in \mathbb{N} \}
$$
While we don't know how to prove anything yet, it is somewhat intuitive that the infimum of the above set is $0$, while there is no minimum. The maximum and supremum are obviously $1$.

**Axiom of Completeness:** Every nonempty set of real numbers that is bounded above has a *least upper bound*.

Let's see why the above is not true for the rational number.
$$
A = \{ r \in \mathbb{Q} \mid r^2 < 2 \}
$$
Clearly $2$ is an upper bound, but what is the *least upper bound*? We can keep approximating the least upper bound, but the value $\sqrt{2}$ does not exist in $\mathbb{Q}$, so there is none. But in the real numbers, the supremum of the set exists. 

**Some Exercises:**

1. Give an example of each of the following, or state that the request is impossible.

   1. A set $B$ with $\inf B \geq \sup B$​.

      > Consider the set $A = \{ 0 \}$. It has a minimum and maximum of zero, and as such it must have an infimum and supremum of zero.

   2. A finite set that contains its infimum but not its supremum.

      > This is not possible. If the set is finite, its supremum must be its maximum, which is obviously in the set.

   3. A bounded subset of $\mathbb{Q}$​ that contains its supremum but not its infimum.

      > Consider all the rational numbers between $\sqrt{3}$ and $12$. This can be written as $B = [\sqrt{3}, 12] \cap \mathbb{N}$. 

2. Let $A$ be nonempty and bounded below, and define the set $B$:
   $$
   B = \{ b \in \mathbb{R} \mid \text{$b$ is a lower bound of $A$} \}
   $$
   Show that $\sup B = \inf A$.

   > Consider that $B$ must have an upper bound, as $A$ is nonempty, and therefore must have a lower bound. It follows that the largest value in $B$, its maximum, must be the greatest lower bound of $A$, as if $A$ had a greater lower bound, it would also be in the set $B$​.
   >
   > Since the maximum is also the supremum, we have $\sup B = \inf A$.

3. Let $A$ and $B$ be nonempty sets, each of which is bounded above. Find an expression for $\sup (A \cup B)$.

   > Take some $x \in A \cup B$. If $x \in A$ as well, then $x \leq \sup A$. Otherwise, $x$ must be in $B$, in which case $x \leq \sup B$. For some arbitrary $x$ in $A \cup B$, we infer that $x \leq \max (\sup A, \sup B)$. We can say that $\max (\sup A, \sup B)$ is an upper bound of $A \cup B$, so,
   > $$
   > \begin{align*}
   > 	\sup (A \cup B) &\leq \max (\sup A, \sup B) &(1)
   > \end{align*}
   > $$
   > Consider adding the elements of $B$ to $A$. The supremum cannot decrease by adding more elements, so we say that $\sup (A \cup B) \geq \sup A$. Similarly, adding the elements of $A$ to $B$, we find that $\sup (A \cup B) \geq \sup B$​.
   >
   > Combining the last two inequalities, we say that the supremum of the union is greater than or equal to the larger of the two sets' supremums, i.e.,
   > $$
   > \begin{align*}
   > 	\sup (A \cup B) &\geq \max (\sup A, \sup B) &(2)
   > \end{align*}
   > $$
   > From results $(1)$ and $(2)$, we have $\sup (A \cup B) = \max (\sup A, \sup B)$.

4. If $A$ and $B$ are nonempty, bounded, and satisfy $A \sube B$, then $\sup A \leq \sup B$.

   > **Proof:** We prove the claim by contradiction. Assume $\sup A > \sup B$. For this to be true, $A$ must contain elements strictly larger than the largest element in $B$. Here lies our contradiction, as $A$ cannot be a subset of $B$ and contain elements not in $B$.

5. **Cut Property:** If $A$ and $B$ are nonempty, disjoint sets with $A \cup B = \mathbb{R}$ and $a < b$ for all $a \in A$ and $b \in B$, then there exists $c \in \mathbb{R}$ such that $x \leq c$ whenever $x \in A$ and $x \geq c$ whenever $x \in B$. Use the Axiom of Completeness to prove this.

   > **Proof:** By the Axiom of Completeness, $A$ must have a supremum. Let $c = \sup A$. By definition of the supremum, for all $x \in A$, $x \leq c$.
   >
   > All elements of $B$ are greater than all elements of $A$, and $A \cup B = \mathbb{R}$, so $B$ must contain all upper bounds of $A$. All upper bounds are greater than or equal to the supremum, so for all $x \in B$, $x \geq c$​.

6. Now prove the Axiom of Completeness using the Cut Property.

   > **Proof:** Let $E$ be a nonempty set that is bounded above. Let $F = \mathbb{R} - E$. 
   >
   > Since $E \cup F = \mathbb{R}$ and $e < f$ for all $e \in E$ and $f \in F$, by the Cut Property, there exists $c \in \mathbb{R}$ such that $e \leq c$ for all $e \in E$ and $f \geq c$ for all $f \in F$.

### 1.4 ~ consequences of completeness.



