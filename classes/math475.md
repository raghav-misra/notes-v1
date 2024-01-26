# math475 / 01.24

## permutations.

A **permutation** of an $n$-element set is an arrangement of the elements in a specific order. More specifically, a **$k$-permutation** is an arrangement of $k$ elements of the set.

The total $k$-permutations of an $n$-element set can be expressed as:
$$
P(n, k) = \frac{n!}{(n - k)!} = n(n - 1)...(n-k+1)
$$

When $k = n$, or the permutation is the length of the set itself, the number of permutations simplifies to $n!$.

**Find** the total number of $3$-tuples $(x, y, z)$ that can be formed from the set $\set{1, 2, 3, ..., 10}$ where $x \neq y \neq z$.

- If we allow $x$ to be any value in the set, there are $10$ choices for $x$. Next, we select $y$. Since one choice is occupied by $x$, there are $9$ left for $y$. Lastly, there are $8$ left for the $z$​ value.

  More specifically, we want to find the number of $3$-permutations of the set. 

  $P(10, 3) = \frac{10!}{(10 - 3)!} = \frac{10!}{7!} = (10)(9)(8)$
  
  **Answer:** the total number of $3$-tuples is $10(9)(8) = 720$​.

**Find** the number of $3$-color flags we can construct with the colors red, white, and green.

- In this case, we want to find the number of $3$-permutations of a set with size $3$. 

  **Answer:** the total number of $3$-color flags is $3! = 6$​.

## permutations with repetition.

These are permutations over a **multiset**, a set that can contain duplicates. The fundamental difference is that since elements are repeated, we will need to account for duplicate permutations. An example might demonstrate it well.

**Find** the total rearrangements of $AAAABBCD$.

- The nuance in the repeated elements may not be easy to understand at first glance, so let's subscript the duplicates: $A_1A_2A_3A_4B_1B_2CD$.

  While the permutations $A_2A_1A_4A_3B_2B_1CD$ and $A_2A_3A_4A_1B_1B_2CD$ are distinct due to subscripts, we may want to treat them (and other repeated cases) as the same case, since all letters are in the same position.

  To do this, we first count the number of ways that the repeated letters can be rearranged within themselves. For the $A$'s it is $4!$ ways, and for the $B$'s it is $2!$​ ways.

  We take the total number of rearrangements (including visual repeats) and divide by these groupings, to eliminate the repeated permutations.

  **Answer:** The total number of rearrangements of the string is $\frac{8!}{(4!)(2!)(1!)(1!)} = \frac{8!}{(4!)(2!)}$, where $8!$​ is the total number of arrangements including repeats.

**Theorem:** Suppose object $1$ occurs $a_1$ times, ... object $k$ occurs $a_k$ times, where $a_1 + ... + a_k = n$. Then, the total # of rearrangements can be expressed as:
$$
\binom{n}{a_1,..., a_k} = \frac{n!}{(a_1!)(...)(a_k!)}
$$
The above expression is called the **multinomial coefficient**.

## falling factorials.

**CATCHUP!**

## combinations.

A **combination** is the total # of ways to form a $k$-length subset of a set $n$, a combination is denoted as follows:
$$
_nC_k = \frac{n!}{k!(n-k)!} = n \text{ choose } k
$$

From a group of $5$ cats, $5$ dogs, and $4$ mice, $3$ animals are chosen.

**Find** how many ways we can get $2$ cats and $1$ dog.

- $5$ cats choose $2$, $\binom{5}{2}$.

  $5$ dogs choose $1$, $\binom{5}{1}$

  **Answer:** We want these both to happen, so $\binom{5}{2}\binom{5}{1}$.

**Find** how many ways we can get *at least* $1$ cat.

- **Subtract** the unwanted combinations from the total.

  - Total combinations: $\binom{14}{3}$.

    Combinations with $0$ cats: $\binom{9}{3}$.

    **Answer:** $\binom{14}{3} - \binom{9}{3} = 280$.

- Or, **add** up all the valid combinations:

  - Combinations with exactly $1$ cat: $\binom{5}{1}\binom{9}{2}$.
  - Combinations with exactly $2$ cats: $\binom{5}{2}\binom{9}{1}$.
  - Combinations with exactly $3$ cats: $\binom{5}{2}\binom{9}{0}$.
  - **Answer:** $\binom{5}{1}\binom{9}{2} + \binom{5}{2}\binom{9}{1} + \binom{5}{2}\binom{9}{0} = 280$.

## binomial theorem.

The theorem below holds for any positive integer $n$.
$$
(x + y)^n = \sum_{k = 0}^{n} \binom{n}{k}x^ky^{n-k}
$$
**Proof:** 

- Note that $(x + y)^n = (x + y)(x + y)(...)(x + y)$, the product of $n$ sums. Consider that the expansion of this expression would consist of multiplying all combinations of $x$ and $y$​ from each parentheses, and summing the resulting products of each combination.

  Every product would result in an expression of the form $x^ky^{n-k}$, as each product is the result of choosing the $x$ value $k$ times, leaving us to choose the $y$ value $n - k$​ times. In order for us to sum every possible product, $k$ must range between $0$ and $n$, inclusive.

  A product of $k$ $x$-values and $n-k$ $y$-values can be chosen $\binom{n}{k}$ times, meaning the sum of all products can be expressed as $\sum_{k = 0}^{n} \binom{n}{k}x^ky^{n-k}$.  $\blacksquare$

## multinomial theorem.

**CATCHUP!**

