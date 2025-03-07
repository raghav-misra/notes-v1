# math410; exam01

## Tools for analysis

### Completeness axiom & consequences

### 1.2—Integers and rational numbers

### 1.3—Inequalities and identities

## 2—Convergent sequences 

### 2.1—Convergence of sequences

### 2.2—Sequences and sets

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

      By the monotonicity assumption, we have that all elements which come before $n$ must also be $\leq L - \epsilon_0$.

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

We basically skipped this section in class, with the exception of the following result.

A set $S \sub \mathbb{R}$ is called **compact** (or *sequentially comp;l;;;;;;;;;;;;;act*) if every sequence in $S$ has a convergent subsequence that converges to a point in $S$.    

## 3—Continuous functions

### 3.1—Continuity

### 3.2—Extreme value theorem

### 3.3—Intermediate value theorem

### 3.4—Uniform continuity

### 3.5—The $\epsilon - \delta$ continuity criterion



> [!NOTE]
>
> You want to find a constant lower bound for $x$ when it appears in the denominator. You want a constant upper bound for $x$ when it appears in the numerator.

### 3.6—Images, inverses, monotone functions

### 3.7—Limits
