# math410; exam01

## 1—Tools for analysis

### 1.1—Completeness axiom & consequences

#### The Completeness Axiom

The **Completeness Axiom** states if $S \sube \mathbb{R}$ is non-empty and bounded above, it must have a least upper bound ($\sup S$ exists).

#### Proving $\sup$ and $\inf$s

A brief walkthrough is to state what you'd like to prove the bound as.

-  Assume the contradiction.
- Try to find a tighter bound. 
- Fail by finding an element in the set which lies between the alleged tighter bound and what we claim is NOT the bound.
- By contradiction, it must be the right bound.

### 1.2—Integers and rational numbers

#### Archimedean Property

The **Archimedean Property** states that for any positive real number $c$, there exists a natural number greater than $c$. It is pretty useful when proving convergence of sequences.

#### Proof of A.P.

- We assume the contradiction: there exists no natural number greater than $c$. Then, $c$ is an upper bound of the naturals. By the Completeness Axiom, the naturals must then have a supremum.

  We let $b = \sup \mathbb{N}$. Since $b$ is the supremum, we know that $b - \frac{1}{2}$ is not an upper bound of $\mathbb{N}$. Thus, there must exist a natural greater than $b - \frac{1}{2}$. We pick $n$ as our natural $> b - \frac{1}{2}$. Then,
  $$
  n > b - \frac{1}{2} \\
  n + 1 > b - \frac{1}{2} + 1 > b
  $$
  So $n + 1$ is a natural number greater than $b$, which contradicts the definition of the supremum. Therefore, we must have a natural number greater than $c$.

#### Density

A set $S$ of real numbers is said to be **dense** in $\mathbb{R}$ if there exists an element of $S$ strictly between any two real numbers.

We have that the set of rationals $\mathbb{Q}$ and irrationals $\mathbb{Q^C}$ are both *dense in* $\mathbb{R}$.

- For the rationals. You use the bounding numbers $a$ and $b$ to cook up a new number.
- For the irrationals. You just pick a rational and "irrationalize" it somehow. Rational multiplied by irrational is irrational and you can use that.

### 1.3—Inequalities and identities

#### Absolute value

This is pretty trivial. But the **absolute value of** $x$ is defined as
$$
|x| = \begin{cases}
	x &\text{if } x \geq 0, \\
	-x &\text{if } x < 0.
\end{cases}
$$

#### Triangle inequality

*Awfully important property; used in many places.*

The **triangle inequality** states that for any pair of numbers $a$ and $b$,
$$
|a + b| \leq |a| + |b|.
$$
The proof is basically just a lot of cases for whether $a$ and $b$ are negative or not and associated algebra case-by-case.

## 2—Convergent sequences 

### 2.1—Convergence of sequences

##### TODO

### 2.2—Sequences and sets

##### TODO

### 2.3—Monotone convergence theorem

#### Monotonicity

Take a sequence $\{a_n\}$. It is **monotone** if for all indices $i, j \in \mathbb{N}$ such that $i < j$, it is one of the following:

- **Monotonically increasing**: $a_i \leq a_j$.
- **Monotonically decreasing:** $a_i \geq a_j$.

A constant sequence is logically monotone, but meets both criteria and so can be considered both monotonically *increasing* and *decreasing*.

---

#### Monotone Convergence Theorem

The **Monotone Convergence Theorem (MCT)** states that a monotone sequence $a_n$ is convergent *if and only if* $a_n$ is bounded. In addition, it states that the bounded monotone $a_n$ converges to:

- $\sup\, \{a_n \mid n \in \mathbb{N}\}$, if $a_n$ is monotonically *increasing*.
- $\inf\, \{a_n \mid n \in \mathbb{N}\}$, if $a_n$ is monotonically *decreasing*.

---

#### Proof of MCT

*The proof below is not identical to the one in the book, but I am pretty confident both hold.*

- We take $a_n$ to be a monotone sequence. Let $\epsilon > 0$ be given.

  **Proof that bounded implies convergent:**

  *Case 1: $a_n$ is monotonically increasing.*

  - Since $a_n$ is bounded, the set of all its elements must have a supremum, by the completeness axiom. Then,
    $$
    \text{Let } L = \sup\,\{a_n \mid n \in \mathbb{N}\}
    $$
    We would like to show that $a_n \rightarrow L$. We approach by way of contradiction, assuming that $a_n \nrightarrow L$. Then, by negating the definition of convergence, we have that $\exists \epsilon_0 > 0$ such that $\forall N \in \mathbb{N}$, $\exists n \geq N$ such that
    $$
    |a_n - L| \geq \epsilon_0 \\
    a_n - L \leq -\epsilon_0 
    	\quad \text{or} \quad 
        a_n - L \geq \epsilon_0
    $$
    We break this into subcases:

    *Case 1a: $a_n - L \leq -\epsilon_0$*.

    - Proceeding with more algebra,
      $$
      \begin{align*}
      	a_n - L &\leq -\epsilon_0 \\
      	L - a_n &\geq \epsilon_0 \\
      	a_n &\leq L - \epsilon_0,
      \end{align*}
      $$
      So we have shown there exists that $a_n$ is at most $L - \epsilon_0$. 

      > [!NOTE]
      >
      > This proof and similar proofs (like on the homework) make interesting uses of the monotonicity assumption. Consider the implications of monotonicity, if you know something about an element then you also know something about every element before.

      By the monotonicity assumption, all elements which come before $n$ must also be $\leq L - \epsilon_0$.

      We now pick our $N$ to be $n + 1$, and find that there is another index $n'$ such that  $n' > n$ for which $a_{n'}$ is at most $L - \epsilon_0$ as well. By the monotonicity assumption, all elements between $a_n$ and $a_{n'}$ are also $\leq L - \epsilon$.

      We then pick our $N$ to be $n' + 1$, and find a new such $n''$ such that $n'' > n'$ and $a_{n''} \leq L - \epsilon_0$. By the monotonicity assumption, all elements between $a_{n'}$ and $a_{n''}$ are also $\leq L - \epsilon$.
      
      We can keep picking infinitely large such $N$ values and find a new element bounded by $L - \epsilon_0$, and monotonicity implies that all previous elements also have the same bound.
      
      Since $L - \epsilon_0 < L$, we have an upper bound which is less than our supremum, which contradicts $L$'s definition as the supremum, and so $a_n$ must converge to $L$.
    
    *Case 1b: $a_n - L \geq \epsilon_0$*.
    
    - Proceeding with more algebra,
      $$
      \begin{align*}
      	a_n - L &\geq \epsilon_0 \\
      	a_n &\geq \epsilon_0 + L > L,
      \end{align*}
      $$
      so we have found some $a_n$ which is greater than $L$. This contradicts $L$'s definition as the supremum, and so $a_n$ must converge to $L$.
    
    We have shown that $a_n \rightarrow L$, as needed.

  *Case 2: $a_n$ is monotonically decreasing.*

  - The proof follows very similarly to *Case 1*, but you just sort of flip everything around.
  
  **Proof that convergent implies bounded:**
  
  Let $a_n \rightarrow A$ and $\epsilon = 1$. By def'n of convergence, we can choose $N \in \mathbb{N}$ such that $\forall n \geq N$,
  $$
  |a_n - a| < 1.
  $$
  By the Triangle Inequality, $\forall n \geq N$,
  $$
  \begin{align*}
  	|a_n| 
  		&= |(a_n - a) + a| \\
  		&\leq |a_n - a| + |a| \\
  		&< \epsilon + |a| = 1 + |a|
  \end{align*}
  $$
  We know then that all elements at index $N$ or greater are bounded by $1 + |a|$. So, all elements of the $a_n$ must either also be bounded be $1 + |a|$, or the largest such element in the finite set of elements $\{a_k \mid 0< k < N, \ k \in \mathbb{N}\}$.
  
  Then we have $a_n$ bounded by $\max\{a_1, \dots, a_{N - 1}, 1 + |a|\}$.

---

#### Nested Interval Theorem

The **Nested Interval Theorem** states that for each $n \in \mathbb{N}$, let $a_n$ and $b_n$ be numbers such that $a_n < b_n$ and consider the  closed interval $I_n = [a_n, b_n]$. Assume that for each $n$,
$$
I_{n + 1} \sube I_n \quad \text{and} \quad \lim_{n \rightarrow \infty} [b_n - a_n] = 0.
$$
Then, there is exactly *one point* $x$ which belongs to the interval $I_n$ for all $n$, and both $a_n$ and $b_n$ converge to $x$. That is,
$$
\bigcup_{n \in \mathbb{N}} I_n = \{x\} \quad \text{and} \quad 
	\lim_{n \rightarrow \infty} a_n = \lim_{n \rightarrow \infty} b_n = x.
$$

---

#### Proof of Nested Interval Theorem

- Consider the relationship between closed intervals $I_j$ and $I_k$ for some $j, k \in \mathbb{N}$ where $j < k$. As defined, we have
  $$
  I_k \sube I_j \leftrightarrow [a_k, b_k] \sube [a_j, b_j].
  $$
  For the interval $I_j$ to be a subset of (contained in) $I_k$, it must have a lower bound at least that of $I_k$ and an upper bound at most that of $I_k$. That is,
  $$
  a_k \geq a_j \quad \text{and} \quad b_k \leq b_j.
  $$
  By definition of monotonicity, we have that $a_n$ is monotonically *increasing* and $b_n$ is monotonically *decreasing*. 

  Consider then that $a_n \leq b_n \leq b_1$ by the definitions of the sequences and monotonicity of $b_n$. Similarly, we have $b_n \geq a_n \geq a_1$. So both $a_n$ and $b_n$ are monotone and bounded. By the MCT, both $a_n$ and $b_n$ must converge. 

  We let $a_n \rightarrow A$ and $b_n \rightarrow B$. By properties of convergent sequences,
  $$
  \begin{align*}
  	\lim_{n \rightarrow \infty} [b_n - a_n] &= 0 \\
  	\lim_{n \rightarrow \infty} b_n - \lim_{n \rightarrow \infty} a_n &= 0 \\
  	\lim_{n \rightarrow \infty} b_n &= \lim_{n \rightarrow \infty} a_n \\
  	B &= A,
  \end{align*}
  $$
  so we have $\lim_{n \rightarrow \infty} a_n = \lim_{n \rightarrow \infty} b_n = A = B$, as desired. Let $x = A = B$.

  Next, notice that every interval of the sequence $I_n$ has every subsequent interval in the sequence as a subset. The smallest interval must have the largest possible lower bound ($\lim_{n \rightarrow \infty} a_n = x$) and smallest possible upper bound ($\lim_{n \rightarrow \infty} b_n = x$). So the interval $I_n$ approaches $[x, x]$ as $n \rightarrow \infty$, and thus, 
  $$
  \bigcap_{n \in \mathbb{N}} I_n = [x, x] = \{x\},
  $$
  as needed.

### 2.4—Sequential compactness theorem

#### Subsequences

Consider a sequence $\{a_n\}$ and a sequence of natural numbers (in ascending order, not necessarily contiguous) $\{n_k\}$. Then the sequence $\{b_k\}$ defined by $b_k = a_{n_k}$ for all $k \in \mathbb{N}$ is a **subsequence** of $\{a_n\}$.

> [!NOTE] 
>
> Intuitively, a subsequence of $\{a_n\}$ is just picking some infinite number of elements of $a_n$ and placing them in the order they appeared in $\{a_n\}$.

---

#### Some relevant theorems, summarized

**Theorem:** If $\{a_n\} \rightarrow A$, then all of its subsequences converge to $A$ as well.

- Proof is pretty intuitive. Let $\{b_k\}$ be a subsequence of $\{a_n\}$.

  By definition of convergence, we have all indices $n \geq$ some $N$ such that $|a_n - A| < \epsilon$.

  Pick sufficiently large $K$ for which the element $b_K$ appears after $a_N$ in $\{a_n\}$.

  All such elements  $b_k$ for $k \geq K$ must also fulfill $|b_n - A| < \epsilon$.

  So $b_k$ fulfills definition of convergence!

**Theorem:** Every sequence has a monotone subsequence.

- Proof is a bit more complex. 

  We let $k$ be a *peak index* of $\{a_n\}$ provided that all elements after $a_k$ are at most as large as $a_k$.

  - $\forall n \geq k$, $a_n \leq a_k$.

  There are either finite or infinite such peak indices in $\{a_n\}$.

  - **Finite peak indices:** If there are finite peak indices, we pick all the elements after the last such peak index to form a subsequence. Since none of the elements in this subsequence are peak indices, we know that the subsequence must eventually be strictly increasing, or else we would have an additional peak index. So of this subsequence, we pick all elements once the subsequence starts becoming strictly increasing to form a new subsequence. As defined, this new subsequence is monotonically increasing.

    **Infinite peak indices:** If there are infinite peak indices, we pick all the elements at peak indices to form a subsequence. By the definition of peak indices, such a sequence must be monotone decreasing, as needed.

**Theorem:** Every bounded sequence has a convergent subsequence.

- Every subsequence of a bounded sequence is bounded. (Pretty logical, the definition involves all elements of the sequence and therefore involves all elements of the subsequence.)

  As shown above, every sequence has a monotone subsequence.

  So every bounded sequence has a monotone subsequence, which is also bounded and is therefore convergent by the **Monotone Convergence Theorem**.

---

#### Sequentially compact

Recall a sequence is **in** $S$ provided that all terms of the sequence are contained in $S$.

A set of real numbers $S$ is **sequentially compact** provided that every sequence *in* $S$ has a subsequence which converges to a point in $S$.

- Is $[0, 1)$ sequentially compact? No. Consider $\{1 - \frac{1}{n}\}$ is in $[0, 1)$ but converges to $1$, which is not in the interval. It is monotone decreasing so all subsequences are also monotone decreasing and then must also converge to $1$.

> [!IMPORTANT]
>
> One thing that confused me was why there was an emphasis on subsequence convergence if all subsequences of a convergent sequence also converge to the same point.
>
> The answer is that divergent (or otherwise non-convergent) sequences can have convergent subsequences to various values. For instance $\{(-1)^n\}$ does not converge, but has the subsequence $\{1,1,1,1,\dots\} \rightarrow 1$ which is in $[-1, 1]$. 

---

#### Sequential compactness theorem

The **Sequential Compactness Theorem** states that if $a$ and $b$ are numbers such that $a < b$, then the interval $[a, b]$ is *sequentially compact*. 

---

#### Proof of Sequential Compactness Theorem

- Consider a closed interval $[a, b] \sub \mathbb{R}$.

  All sequences in $[a, b]$ must be bounded by $\max\,\{|a|, |b|\}$.

  Every sequence in $[a, b]$ has a monotone subsequence. (Proved above.) By the **Monotone Convergence Theorem**, this subsequence must converge. (As it is bounded and convergent.)

  We consider whether this subsequence, which we denote as $\{s_n\}$. is monotonically increasing or decreasing.

  - *Case 1: It is monotone increasing.*

    - By the MCT, this sequence must converge to $L = \sup \, \{s_n \mid n \in \mathbb{N}\}$.

      Consider that $L \leq b$, since $\{s_n\}$ is in $[a, b]$. We have $L \geq a$ since the first element of $\{s_n\} \geq a$, and by definition of monotonicity all other elements must also be $\geq a$.

      We then have $a \leq L \leq b$, so we have a subsequence which converges to a point in $[a, b]$, as needed. 

    *Case 2: It is monotone decreasing.*

    - Literally the same thing except you use the $\inf$ and flip everything basically.

### 2.5—Covering properties of sets

#### Set compactness

A set $S \sub \mathbb{R}$ is called **compact** (or *sequentially compact*) if every sequence in $S$ has a convergent subsequence that converges to a point in $S$.

---

#### Important result

*We basically skipped this section in class, with the exception of the following result.*

A set $S \sub \mathbb{R}$ is **closed and bounded** *if and only if* $S$ is (sequentially) **compact**.

## 3—Continuous functions

### 3.1—Continuity

#### Def'n of continuity

A function $f: D \rightarrow \mathbb{R}$ is **continuous** *at the point* $x_0$ provided that whenever a sequence $\{x_n\}$ in $D$ converges to $x_0$, the corresponding image sequence $\{f(x_n)\}$ converges to $f(x_0)$. 

---

#### Basic examples

**Example.** Let $f: \mathbb{R} \rightarrow \mathbb{R}$ and $f(x) = x^2 - 2x + 4$. Show that $f$ is continuous everywhere on $\mathbb{R}$.

- **Proof.** Let $x_0 \in \mathbb{R}$ be given. And let $\{x_n\}$ be in $\mathbb{R}$ and converge to $x_0$. Then,
  $$
  \begin{align*}
  	\lim_{n \rightarrow \infty} f(x_n) 
      	&= \lim_{n \rightarrow \infty} [x_n^2 - 2x_n + 4] \\
      	&= \lim_{n \rightarrow \infty} x_n^2 
          	- 2 \lim_{n \rightarrow \infty} 2x_n
          	+ \lim_{n \rightarrow \infty} 4 \\
          &= x_0^2 - 2 x_0 + 4 = f(x_0),
  \end{align*}
  $$
  as needed. $\square$

**Example.** Let $f: \mathbb{R} \rightarrow \mathbb{R}$ and 
$$
f(x) = \begin{cases}
	1	&\text{if } x \geq 0 \\
	2	&\text{if } x < 0.
\end{cases}
$$
Show where $f$ is continuous and where it is not.

- **Proof.** We want to show that $f$ is continuous at $x_0 \in (-\infty, 0) \cup (0, \infty)$ and is discontinuous at $x_0 = 0$.

  Let $x_0 \in \mathbb{R}$.

  *Case 1: $x_0 \in (-\infty, 0)$:*

  - Let $\epsilon > 0$ be given.

    We consider a sequence $\{A_n\}$ in $\mathbb{R}$ $\rightarrow x_0$. Since $A_n$ converges to $x_0 \in (-\infty, 0)$, there exists an $N \in \mathbb{R}$ such that for all $n \geq N$, $A_n \in (-\infty, 0)$. Then $\forall n \geq N$,
    $$
    |f(A_n) - f(x_0)| = |2 - 2| = 0 \leq \epsilon,
    $$
    so $\{f(A_n)\} \rightarrow f(x_0)$ and $f$ is continuous over $(-\infty, 0)$.

  *Case 2: $x_0 = 0$*:

  - Consider $\{B_n\} = \{\frac{-1}{n}\}$. $B_n$ can be expressed as the product of the harmonic series and a constant sequence of $-1$s and by the product property of convergent sequences, $\{B_n\} \rightarrow 0$. Also note that $\{B_n\}$ is in $(\infty, 0)$.

    For $f$ to be continuous at $0$, we must have $\{f(B_n)\} \rightarrow f(0) = 1$. 
    $$
    \begin{align*}
    	\lim_{n \rightarrow \infty} f(B_n) 
    		&= \lim_{n \rightarrow \infty} 2 
    		&\text{def'n of $f$ over $(\infty, 0$)}\\
    		&= 2 \neq 1,
    \end{align*}
    $$
     and so $f$ must not be continuous at $x_0 = 0$.
  
  *Case 3: $x_0 \in (0, \infty)$:*
  
  - Let $\epsilon > 0$ be given.
  
    We consider a sequence $\{C_n\}$ in $\mathbb{R}$ $\rightarrow x_0$. Since $C_n$ converges to $x_0 \in (0, \infty)$, there exists an $N \in \mathbb{R}$ such that for all $n \geq N$, $C_n \in (0, \infty)$. Then $\forall n \geq N$,
    $$
    |f(x_n) - f(x_0)| = |1 - 1| = 0 \leq \epsilon,
    $$
    so $\{f(C_n)\} \rightarrow f(x_0)$ and $f$ is continuous over $(0, \infty)$.

> [!WARNING]
>
> I think I can mess these up when proving continuity by not expressing that the sequence will *eventually* be in the domain where $f$ is defined as some expression vs. another expression. If you say that, that is the main premise that lets you find the limit of the image sequence.

---

#### Operations on continuous functions

The **sum property** states that if $f$ and $g$ are functions from $D \rightarrow \mathbb{R}$ and are continuous at $x_0$, then the function $(f + g): D \rightarrow \mathbb{R}$ is continuous at $x_0$.

- **Proof.** Let $\{x_n\} \rightarrow x_0$. Then by definition of continuity, we know that

  - $\{f(x_n)\} \rightarrow f(x_0)$.
  - $\{g(x_n)\} \rightarrow g(x_0)$.

  We show $f + g$ is continuous at $x_0$ if $\{(f + g)(x_n)\} \rightarrow (f + g)(x_0)$. Consider the limit:
  $$
  \begin{align*}
  	\lim_{n \rightarrow \infty} (f + g)(x_n)
      	&= \lim_{n \rightarrow \infty} [f(x_n) + g(x_n)] \\
      	&= \lim_{n \rightarrow \infty} f(x_n)
      		+ \lim_{n \rightarrow \infty} g(x_n)
          &\text{sum of convergent seqs} \\
          &= f(x_0) + g(x_0) = (f + g)(x_0),
  \end{align*}
  $$
  as needed.

The **product/quotient properties** follow similarly for a product/quotient instead of a sum of two continuous functions; the proof also follows almost identically, but using the product/quotient  properties of convergent sequences.

> [!NOTE]
>
> The quotient property only holds when $g(x) \neq 0 ,\, \forall x$, as we can't have division by zero.

---

#### Composition of continuous functions

The **composition property** states that given $f: D \rightarrow \mathbb{R}$ and $g: U \rightarrow \mathbb{R}$, if $f$ is continuous at $x_0$ and $g$ is continuous at $f(x_0)$, then $g \circ f: D \rightarrow \mathbb{R}$ is continuous at $x_0$.

- **Proof.** Let $\{x_n\} \in \mathbb{R} \rightarrow x_0$. Then, by definition of continuity for $f$ at $x_0$,
  $$
  \{f(x_n)\} \rightarrow f(x_0).
  $$
  By definition of continuity for $g$ at $f(x_0)$,
  $$
  \{g(f(x_n)\} \rightarrow g(f(x_0)).
  $$
  We consider the continuity of $g \circ f$ at $x_0$, wanting to show $\{(g \circ f)(x_n)\} \rightarrow (g \circ f)(x_0).$
  $$
  \begin{align*}
  	\lim_{n \rightarrow \infty} [(g \circ f) (x_n)]
  		&= \lim_{n \rightarrow \infty} g(f(x_n)) \\
  		&= g(f(x_0)) = (g \circ f)(x_0),
  \end{align*}
  $$
  as needed.

### 3.2—Extreme value theorem

#### Relevant definitions

For a function $f: D \rightarrow \mathbb{R}$, we let the **image** of $f$ be
$$
f(D) = \{f(u) \mid u \in D\}.
$$
If $f(D)$ has a maximum, we say that $x_0$ for which $f(x_0) = \max f(D)$ is the **maximizer** and that $f$ *attains a* **maximum value**.

If $f(D)$ has a minimum, we say that $x_0$ for which $f(x_0) = \min f(D)$ is the **minimizer** and that $f$ *attains a* **minimum value**.

In general, a nonempty set has a maximum when is bounded above and contains its supremum. It has a minimum when it is bounded below and contains its infimum.

---

#### Extreme Value Theorem

The **Extreme Value Theorem (EVT)** states that a continuous function on a closed, bounded interval $f: [a, b] \rightarrow \mathbb{R}$ *attains both a maximum and minimum value*.

---

#### Proof of EVT

> [!TIP]
>
> Not covered in class, so likely not on the exam. But probably a good exercise to figure out how the proof works.

**Lemma I.** The image of a continuous function on a closed and bounded interval $f: [a, b] \rightarrow \mathbb{R}$ is bounded above. That is, there is a number $M$ for which $f(x) \leq M$ for all $x \in [a, b]$.

- We prove this by way of contradiction. Assume no such $M$ exists. Then, for all $n \in \mathbb{N}$,
  $$
  f(x) > n \quad \exists x \in [a, b].
  $$
  Pick a point which fulfills the above inequality for each $n$ and label it $x_n$. We now have a sequence $\{x_n\}$ in $[a, b]$ with the property that $f(x_n) > n$ for each index $n$.

  The Sequential Compactness Theorem states that a sequence in $[a, b]$ should have a subsequence that converges to a point in $[a, b]$. So there exists a convergent subsequence of $\{x_n\}$. We label this subsequence $\{x_{n_k}\} \rightarrow x_0$.

  Since $f$ is continuous, we have that $\{f(x_{n_k})\} \rightarrow f(x_0)$. However, this contradicts the previously derived inequality that
  $$
  f(x_{n_k}) > x_{n_k} \geq k \quad \text{for all $k$}.
  $$
  As such, we must have the $f([a, b])$ is bounded above.

**Proof of the Extreme Value Theorem.**

- Let $S = f([a, b])$, the image of $f: [a, b] \rightarrow \mathbb{R}$. By *Lemma I*, $S$ is bounded above. Then by the Completeness Axiom, $S$ must have a supremum. Let $C = \sup S$. 

  We want to find a point $x_0 \in [a, b]$ such that $f(x_0) = C$.

  For all $n \in \mathbb{N}$, $c - \frac{1}{n} < c$ and is therefore not an upper bound of $S$. Therefore, we have a point $x$ in $[a, b]$ for which $f(x) > c - \frac{1}{n}$. We pick such a point for each $n$ and label it $x_n$.

  Since $\{c - \frac{1}{n}\} \rightarrow c$ and $c - \frac{1}{n} < f(x_n) \leq c$ for all $n$, we must have that $\{f(x_n)\} \rightarrow c$.

  By the Sequential Compactness Theorem, $\{x_n\}$ in $[a, b]$ must have a subsequence $\{x_{n_k}\}$ which converges to some $x_0 \in [a, b]$.

  By definition of continuity of $f$ over $[a, b]$, since $\{x_{n_k}\} \rightarrow x_0$, we must have $\{f(x_{n_k})\} \rightarrow f(x_0)$.

  We know $\{f(x_n)\} \rightarrow c$, so in order for its subsequence $\{f(x_{n_k})\} \rightarrow f(x_0)$, $f(x_0)$ must be $= c$.

  Thus, $c$ is both the supremum of $S$ and in $S$, so $x_0$ must be a maximizer of $f$ over $[a, b]$. That is, $f$ attains a maximum value over $[a, b]$.

  Let $g = -f$ and $g: [a, b] \rightarrow \mathbb{R}$. Then a maximum of $g$ would be a minimum of $f$. Using the previous proof, we can find such a maximum of $g$ over $[a, b]$ and therefore $f$ must also attain a minimum value over $[a, b]$.

> [!TIP]
>
> Consider how the Sequential Compactness Theorem was used in the proof of the Extreme Value Theorem. We used it to find a subsequence which converged to a point *in the interval*, and then used that to demonstrate:
>
> - **Lemma I:** The subsequence is bounded (as it converges), so the larger sequence must also be bounded.
> - **Main Proof:** The subsequence converges to a value in the interval, so the larger sequence, which we already knew was convergent, must also converge to a value in the interval.

###  3.3—Intermediate value theorem

#### Intermediate Value Theorem

The **Intermediate Value Theorem (IVT)** states that if a function is continuous over a closed, bounded interval, $f: [a, b] \rightarrow \mathbb{R}$, then for all $c$ strictly between $f(a)$ and $f(b)$, there exists an $x_0$ in the open interval $(a, b)$ for which $f(x_0) = c$.

---

#### Proof of IVT

We use the **bisection method** to prove this.

- We will only consider the case where $f(a) < c < f(b)$. The other case ($f(b) < c < f(a)$) follows from the first when we replace $f$ with $-f$ and $c$ with $-c$.

  We will recursively define a sequence of nested, closed subintervals of $[a, b]$ whose endpoints converge to a point in $[a, b]$ at which $f(x) = c$.

  Let $a_1 = a$ and $b_1 = b$. For $n \in \mathbb{N}$, suppose the closed interval $[a_n, b_n]$ has been defined such that $f(a_n) \leq c$ and $f(b_n) \geq c$. Consider the midpoint $m_n = (a_n + b_n)/2$.

  - If $f(m_n) \leq c$, define $a_{n + 1} = m_n$ and $b_{n + 1} = b_n$.
  - If $f(m_n) > c$ define $a_{n + 1} = a_n$ and $b_{n + 1} = m_n$.

  Observe that $\forall n \in \mathbb{N}$,
  $$
  a \leq a_n \leq a_{n + 1} \leq b_{n + 1} \leq b_n \leq b, \\
  f(a_{n + 1}) \leq c \quad \text{and} \quad f(b_{n + 1}) > c,
  $$
   and
  $$
  b_{n + 1} - a_{n + 1} = \frac{b_n - a_n}{2}.
  $$
  Recursively substituting that last equality into itself, we find the closed form
  $$
  b_n - a_n = (b - a) / 2^{n - 1}.
  $$
  From this, we find that $\lim_{n \rightarrow \infty} [b_n - a_n] = 0$ and therefore the criteria of the Nested Interval Theorem are met. That is, there exists some $x_0 \in [a, b]$ for which
  $$
  \lim_{n \rightarrow \infty} a_n = \lim_{n \rightarrow \infty} b_n = x_0, \\
  \bigcap_{n \in \mathbb{N}} [a_n, b_n] = [x_0, x_0] = \{x_0\}.
  $$
  Since $f$ is continuous at $x_0 \in [a, b]$, the image sequences $\{f(a_n)\}$ and $\{f(b_n)\}$ must both converge to $f(x_0)$.

  By definition of $a_n$ and $b_n$, we have that $\{f(a_n)\} \rightarrow f(x_0) \leq c$ and $\{f(b_n\} \rightarrow f(x_0) \geq c$. So we have that $f(x_0) = c$ for $x_0 \in (a, b)$. (We can assume it's an open interval since it can't be $a$ or $b$ as $c$ lies strictly between $f(a)$ and $f(b)$, by definition.)

---

#### IVT Applications

**Example.** Demonstrate that there is an $x$ for which $x^5 + x = -1$.

- We can frame it as finding some $x$ for which $x^5 + x + 1 = 0$.

  Pick $x = 1$: $1^5 + 1 + 1 = 3 > 0$.

  Pick $x = -1$: $(-1)^5 + (-1) + 1 = -1 < 0$.

  We have some $[-1, 1]$ where $f(-1) < 0$ and $f(1) > 0$.

- Then, by IVT, $\exists x_0 \in (-1, 1)$ such that $x_0^5 + x_0 + 1 = 0$,

  - So we have an $x$ for which $x^5 + x = -1$.

**Example.** Demonstrate that $\exists x$ such that $x^2 = c$ for $c > 0$.

- We frame it as finding some $x$ for which $x^2 - c = 0$.

- Pick $x = 0$: $0^2 - c = -c$.

- If $c > 1$, we pick $x = c$: $c^2 - c$.

  - Since $c > 1$, $c^2 > c$. So $c^2 - c > 0$.

    We have some $[0, c]$ where $f(0) < 0 < f(c)$.

    Then, by IVT, $\exists x_0 \in (0, c)$ such that $x_0^2 - c = 0$.

  If $c = 1$, we pick $x = 2$: $2^2 - c = 4 - c = 4 - 1 = 3$.

  - We have $-c = -1$ when $x$ is $0$, as $c = 1$.

    We have some $[0, 2]$ where $f(0) < 0 < f(2)$.

    Then, by IVT, $\exists x_0 \in (0, 2)$ for which $x_0^2 - c = 0$.

  If $c < 1$, we pick $x = \frac{1}{c}$: $\frac{1}{c^2} - c$.

  - We have $\frac{1}{c} > 1 > c$ so $\frac{1}{c^2} > \frac{1}{c}$. Thus, $\frac{1}{c^2} - c > 0$.

    We have some $[0, \frac{1}{c^2}]$ such that $f(0) < 0 < f(\frac{1}{c^2})$.

    Then, by IVT, $\exists x_0 \in (0, \frac{1}{c^2})$ for which $x_0^2 - c = 0$.

  In all cases for $c$, we have shown the existence of an $x$ which satisfies $x^2 = c$.

> [!TIP]
>
> The trick here is to heuristically find $x$-values whose corresponding $y$-values strictly *bound* the desired $y$-value. Finding such bounds lets use IVT to ensure there exists an $x$ with the corresponding desired $y$.

### 3.4—Uniform continuity

#### Def'n of uniform continuity

A function $f: D \rightarrow \mathbb{R}$ is **uniformly continuous** if for any two sequences $\{u_n\}$ and $\{v_n\}$ have the property that $\{u_n - v_n\} \rightarrow 0$, $\{f(u_n) - f(v_n)\} \rightarrow 0$ as well.

A function which is uniformly continuous in $D$ is continuous in $D$. The inverse is not necessarily true.

---

#### (Dis)proving uniform continuity

**Example.** Show that $f: \mathbb{R} - \mathbb{R}$ where $f(x) = ax + b$ is uniformly continuous, for constants $a$ and $b$.

- **Proof.** Let $\{u_n\}$ and $\{v_n\}$ be two sequences such that $\{u_n - v_n\} \rightarrow 0$.

  Then we consider the convergence of $\{f(u_n) - f(v_n)\}$:
  $$
  \begin{align*}
  	\lim_{n \rightarrow \infty} [f(u_n) - f(v_n)]
  		&= \lim_{n \rightarrow \infty} [a u_n + b - a v_n - b] \\
  		&= \lim_{n \rightarrow \infty} a [u_n - v_n] \\
  		&= a \lim_{n \rightarrow \infty} [u_n - v_n]
  			&\text{props. of conv. seqs} \\
          &= a \cdot 0,
  \end{align*}
  $$
  as needed.

*The result above states that all linear functions are uniformly continuous over all $\mathbb{R}$.*

**Example.** Show that $f: \mathbb{R} \rightarrow \mathbb{R}$ where $f(x) = x^2$ is not uniformly continuous.

- **Proof.** Let $\{u_n\} = \{n + \frac{1}{n}\}$ and $\{v_n\} = \{n\}$ such that $\{u_n - v_n\} \rightarrow 0$.

  Consider $\{u_n - v_n\} = \{n + \frac{1}{n} - n\} = \{\frac{1}{n}\} \rightarrow 0$.

  Then we look at $\{f(u_n) - f(v_n)\}$,
  $$
  \begin{align*}
  	\{f(u_n) - f(v_n)\} 
  		&= \{(n + \frac{1}{n})^2 - n^2\}
  		&\text{def'n of $f$} \\
  		&= \{n^2 + 2 + \frac{1}{n^2} - n^2\} \\
  		&= \{2 + \frac{1}{n^2}\} \\
  		&= 2 \neq 0,
  \end{align*}
  $$
  so $f$ is not uniformly continuous.

---

#### Relevant theorems

**Theorem.** A continuous function on a closed, bounded interval $f: [a, b] \rightarrow \mathbb{R}$ is always uniformly continuous.

- **Proof.** We show this by contradiction. Let $\{u_n\}$ and $\{v_n\}$ be sequences that satisfy the property
  $$
  \lim_{n \rightarrow \infty} [u_n - v_n] = 0.
  $$
  Assuming the contradiction, there exists some $\epsilon$ for which
  $$
  \begin{align*}
  	|f(u_n) - f(v_n)| &\geq \epsilon &\forall n
  \end{align*}
  $$
  Since the domain is closed and bounded, we apply the Sequential Compactness Theorem to both $\{u_n\}$ and $\{v_n\}$, finding subsequences $\{u_{n_k}\}$ and $\{v_{n_k}\}$, respectively, which converge to a point in $[a, b]$.

  We let $\{u_{n_k}\}$ converge to $x_o \in [a, b]$. By the original property, we must then have that $\{v_{n_k}\}$ converges to $x_0$ as well. Therefore, $\{u_{n_k} - v_{n_k}\} \rightarrow 0$. 

  However, this contradicts the property $|f(u_{n_k}) - f(v_{n_k})| \geq \epsilon$ for all $k$ (if it applies to all the elements of the sequences, it applies to all the elements of the subsequence).

  And then we see that $f$ must be uniformly continuous over $[a, b]$.

### 3.5—The $\epsilon - \delta$ continuity criterion

#### Def'n of $\epsilon - \delta$ criterion

A function $f: D \rightarrow \mathbb{R}$ satisfies the $\epsilon - \delta$ criterion at a point $x_0 \in D$ if $\forall \epsilon > 0$, $\exists \delta > 0$ such that 
$$
\text{if } |x - x_0| < \delta, \text{ then } |f(x) - f(x_0)| < \epsilon.
$$

---

#### Some examples 

> [!TIP]
>
> When trying to prove a function satisfies the $\epsilon - \delta$ criterion, consider the following points:
>
> - You want to find a constant lower bound for $x$ when it appears in the denominator.
> - You want a constant upper bound for $x$ when it appears in the numerator.
> - Oftentimes, the $|x| = |x - x_0 + x_0|$ can help you bound $x$ with $\delta$.
> - You can try to bound $\delta$ in terms of $x_0$ so the terms can combine, like $\delta \leq x_0/2$.
> - Remember $|x| \geq x$ if you ever need to lower bound that term.

**Example.** Define $f(x) = x^3$ for all $x$. Show that $f$ satisfies the $\epsilon - \delta$ criterion for all $x_0$.

- **Proof.** Let $\epsilon > 0$ and $x_0 \in \mathbb{R}$ be given. Also, let $\delta > 0$ and assume that $|x - x_0| < \delta$.

  We let $\delta \leq 1$. Then consider $|x|$,
  $$
  \begin{align*}
  	|x| 
  		&= |x - x_0 + x_0| \\
  		&= |x - x_0| + |x_0|
  			&\text{triangle inequality} \\
          &< \delta + |x_0| \\
          &\leq 1 + |x_0|
  \end{align*}
  $$

  $$
  \begin{align*}
  	|x - x_0| &< \delta \leq 1 \\
  	-1 &< x - x_0 \\
  	x &> x_0 -1 \\
  	x^2 &> (x_0 - 1)^2 \\
  	\frac{1}{x^2} &< \frac{1}{(x_0 - 1)^2}
  \end{align*}
  $$

  

  Now we consider the difference of $f(x)$ and $f(x_0)$,
  $$
  \begin{align*}
  	|f(x) - f(x_0)| 
  		&= |x^3 - x_0^3| \\
  		&= |(x - x_0) \cdot (x^2 + x x_0 + x_0^2)| 
  			&\text{diff. of cubes} \\
  		&= \delta |x^2 + x x_0 + x_0^2| \\
  		&= \delta |x(x + x_0) + x_0^2| \\
  		&< \delta [|x|\cdot|(x + x_0)| + |x_0^2|]
  			&\text{triangle inequality} \\
          &< \delta [|x| \cdot (|x| + |x_0|) + |x_0^2|]
          	&\text{triangle inequality} \\
          &< \delta [(|x_0| + 1)(|x_0| + 1 + |x_0|) + |x_0^2|] \\
          &= \delta [(|x_0| + 1)(2|x_0| + 1) + |x_0^2|] \\
          &= \delta (2|x_0|^2 + 2|x_0| + |x_0| + 1 + |x_0^2|) \\
          &= \delta (3|x_0|^2 + 3|x_0| + 1)
  \end{align*}
  $$
  Now we choose our $\delta = \min(1, \frac{\epsilon}{3|x_0|^2 + 3|x_0| + 1})$.

  Then it follows that
  $$
  |f(x) - f(x_0)| < \epsilon,
  $$
  as desired! So $f$ satisfies the criterion.

**Example.** Prove that $f(x) = \frac{1}{x^2}$ on $(0, \infty)$ satisfies the $\epsilon - \delta$ criterion for continuity.

- **Proof.** Let $\epsilon > 0$ and $x_0 \in (0, \infty)$ be given.

  Then we let $\delta > 0$ and assume $|x - x_0| < \delta$. We will find a value for $\delta$ such that $|f(x) - f(x_0)| < \epsilon$. We let $\delta \leq 1$. Then, consider $|x|$,
  $$
  \begin{align*}
  	|x| 
  		&= |x - x_0 + x_0| \\
  		&\leq |x - x_0| + |x_0|
  			&\text{triangle inequality} \\
          &= \delta + |x_0| \\
         |x| &< 1 + |x_0| &\text{(I)}
  \end{align*}
  $$
  To find a lower bound for $x$, consider $|x - x_0|$,
  $$
  \begin{align*}
  	|x - x_0| &< \delta \leq 1 \\
  	-1 &< x - x_0 \\
  	x &> x_0 -1 \\
  	x^2 &> (x_0 - 1)^2 = x_0^2 - 2x_0 + 1 > -2x_0 \\
  	\frac{1}{x^2} &< -\frac{1}{2x_0}
  		&\text{(II)}
  \end{align*}
  $$
  Then, consider $|f(x) - f(x_0)|$,
  $$
  \begin{align*}
  	|f(x) - f(x_0)| 
  		&= |\frac{1}{x^2} - \frac{1}{x_0^2}| \\
  		&= |\frac{x_0^2 - x^2}{x^2 x_0^2}| \\
  		&= \frac{|x_0 + x| \cdot |x_0 - x|}{|x^2| \cdot |x_0^2|} 
  			&\text{diff. of squares} \\
  		&\leq \frac{(|x_0| + |x|) |x_0 - x|}{|x^2| \cdot |x_0^2|}
  			&\text{triangle inequality} \\
          &< \frac{\delta (|x_0| + 1 + |x+0|)}{|x^2| \cdot |x_0^2|}
          	&\text{substitute (I)} \\
          &= \delta \frac{2|x_0| + 1}{|x^2| \cdot |x_0^2|} \\
          &< \delta \frac{2|x_0| + 1}{2x_0 \cdot |x_0^2|}
          	&\text{substitute (II)}
  \end{align*}
  $$
  Now, we explicitly let $\delta = \min(1, \frac{\epsilon \cdot 2x_0 \cdot |x_0^2|}{2|x_0| + 1})$. Then, we have
  $$
  |f(x) - f(x_0)| < \epsilon,
  $$
  as needed. So we have shown that $f$ is continuous over $(0, \infty)$.

### 3.6—Images, inverses, monotone functions

##### TODO

### 3.7—Limits

##### TODO
