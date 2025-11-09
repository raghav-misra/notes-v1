# math410; final

## 9.1. Sequences and series of numbers

**MCT** says a monotone sequence is convergent *if and only if* it is bounded.

- Not requirement on the limit itself; derived from monotonicity property.

**Cauchy sequence** if for all $\epsilon > 0$, $\exists N$ such that
$$
|a_n - a_m| < \epsilon \qquad \forall n \geq N,\, m \geq N.
$$
**Criterion:** a sequence is convergent *if and only if* it is Cauchy.

- **Proof ($\Rightarrow$):** Assume convergent. Pick $N$ satisfying some $\epsilon/2$. Then choose $n, m \geq N$.
  $$
  \begin{align*}
  a_n - a_m 
  &= |(a_n - a) + (a - a_m)| \\
  &\leq |(a_n - a)| + |(a - a_m)| &\text{triangle} \\
  &\leq |a_n - a| + |a_m - a| \\
  &< 2 *\epsilon/2 = \epsilon,
  \end{align*}
  $$
  as needed.

- **Proof ($\Leftarrow$):** Assume Cauchy. Find subsequence which converges to $a$ by sequential compactness and then use that to show sequence converges to $a$.

**Series** is a sequence of partial sums of a sequence. Explore tests for *sequence convergence*.
$$
s_n = \sum_{k = 1}^{n} a_n.
$$
If $s$ converges, we write $\sum_{k = 1}^{\infty} s_k = \lim_{n \rightarrow \infty} \sum_{k = 1}^{n} s_k$. Else, it diverges.

If $s_n$ converges, then the underlying $a_n \rightarrow 0$.

- *Intuition:* If the sum of the terms approaches a constant, it only makes sense for the terms themselves to get smaller. 

  **Proof.** Since $\lim_{n \rightarrow \infty} s_n = s$, $\lim_{n \rightarrow \infty} s_{n-1} = s$ as well.

  For $n \geq 2$, $s_{n} - s_{n - 1} = a_n$. And by difference of convergent sequences,
  $$
  \lim_{n \rightarrow \infty} a_n = \lim_{n \rightarrow \infty} [s_n - s_{n - 1}] = \lim_{n \rightarrow \infty} [s - s] = 0.
  $$

**Comparison Test.** Let $a_k$ and $b_k$ be sequences of numbers such that for all $k$,
$$
0 \leq a_k \leq b_k.
$$

- Then, if $\sum_{k = 1}^{\infty} a_k$ diverges, so does $\sum_{k = 1}^{\infty} b_k$ Also, if $\sum_{k = 1}^{\infty} b_k$ converges, so does $\sum_{k = 1}^{\infty} a_k$. *Intuition:* If bigger thing converges, I must too. If smaller thing diverges, I must too!

**Integral Test.** Let $\{a_n\}$ be a sequence of non-negative numbers and suppose function $f$ is continuous and monotonically decreasing and defined as $f(k) = a_k$.

- Then $\sum_{k = 1}^{\infty} a_n$ converges *if and only if* the sequence of integrals $\{\int_0^k f(x)dx\}$ is bounded. 
- **Proof.** idc ngl.

**$p$-test**. A series $\sum_{k = 1}^{\infty} \frac{1}{k^p}$ converges *if and only if* $p > 1$.

- $1/k^1$ is the harmonic series which we know to diverge.

**Alternating series test.** If $\{a_k\} \rightarrow 0$ is monotonically decreasing, then
$$
\sum_{k = 1}^{\infty} a_k \text{ converges.}
$$

- Use this to show alternating harmonic series converges.

**Cauchy Convergence For Series.** Series converges *if and only if* $\forall \epsilon > 0$, $\exists N$ such that for all $n \geq N$ and $k \in \mathbb{N}$,
$$
|a_{n + 1} + \cdots + a_{n + k}| < \epsilon.
$$

- *Intuition:* At any given point in the series, if the sum of the remaining terms is bounded by a constant, the series converges.
- **Proof.** Apply Cauchy convergence criterion for sequences to the sequence of partial sums.

A series $\sum_{k=1}^{\infty} a_k$ converges **absolutely** if $\sum_{k=1}^{\infty} |a_k|$ converges.

- **Test.** If $\sum_{k=1}^{\infty} |a_k|$ converges, $\sum_{k=1}^{\infty} a_k$ does too.

- A divergent series which converges absolutely is called **conditionally convergent**.

**Ratio Test.** For series $\sum_{k=1}^{\infty} a_k$, let
$$
\lim_{n \rightarrow \infty} \frac{|a_{n+1}|}{a_n} = \ell.
$$
Then, if $\ell > 1$, $\sum_{k=1}^{\infty} a_k$ converges *absolutely*. If $\ell < 1$, $\sum_{k=1}^{\infty} a_k$ diverges.

## 9.2. Pointwise convergence.

A sequence of functions $f_n$ **converges pointwise** to a function $f$ on $D$ if $\forall x_0 \in D$,
$$
\lim_{n \rightarrow \infty} f_n(x_0) = f(x_0).
$$
Pointwise convergence *says nothing* about the continuity of a sequence of functions vs. the function it converges to. Why? Let $f(x) = \{1 \text{ if } x = 1,\ 0 \text{ if } 0 \leq x < 1\}$.

Then consider the sequence of functions $f_n(x) = x_n$. It converges pointwise to $f$, but all functions in $f_n$ are clearly polynomial and therefore continuous, unlike $f$.

## 9.3. Uniform convergence.

A sequence of functions $f_n$ **converges uniformly** to $f$ on $D$ if for every $\epsilon > 0$, there exists some index $N$ such that for all $n \geq N$ and $x \in D$,
$$
|f_n(x) - f(x)| < \epsilon.
$$
A sequence of functions $f_n$ is **uniformly Cauchy** on $D$ if for all $\epsilon > 0$, there exists some index $N$ such that for all $n \geq N$, natural number $k$, $x \in D$,
$$
|f_{n + k}(x) - f_{n}(x)| < \epsilon.
$$
**Weierstrass Criterion.** Series of functions uniformly converges *if and only if* it is uniformly Cauchy.

## 9.4. Uniform limit of functions.

