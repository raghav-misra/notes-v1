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

  More specifically, we want to find the number of $3$-permutations of the set. $P(10, 3) = \frac{10!}{(7)!} = (10)(9)(8)$

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

  **Answer:** The total number of rearrangements of the string is $\frac{8!}{(4!)(2!)(1!)(1!)} = \frac{8!}{(4!)(2!)}$, where $8!$ is the total number of arrangements including repeats.






---



## Permutations

A **permutation** of an $n$-element set is an arrangement of the elements in a specific order. A **$k$-permutation** is an arrangement of $k$ elements of the set.

The total $k$-permutations of an $n$-element set can be expressed as:
$$
P(n, k) = \frac{n!}{(n - k)!} = n(n - 1)...(n-k+1)
$$

### Total $3$-tuples $(x, y, z)$ of $\set{1, 2, 3, ... 10}$.

$x$ has $10$ options, $y$ has $9$ options (one has been taken), and $z$ has $8$ (as $x$ and $y$ have already occupied two options. 

So $P(10, 3) = (10)(9)(8) = 720$.

## Falling factorials.

**CATCHUP**

## Permutations with repetition.

### Total rearrangements of $AAAABBCD$.

Let's try subscripting the $A$'s to distinguish: $A_1A_2A_3A_4BBCD$. If the $A$'s were distinct, this would be easily $8! = 40320$. 

But they are not. $A_1A_2A_3A_4BBCD$ and $A_2A_1A_4A_3BBCD$ are the same case here. The $A$'s themselves can be rearranged in $4! = 24$ ways. But we only want this arrangement counted once.

Similarly, the two $B$'s can be rearranged in $2! = 2$ ways.

### Theorem for repetition.

Suppose object $1$ occurs $a_1$ times, ... object $k$ occurs $a_k$ times, where $a_1 + ... + a_k = n$. Then, the total # of rearrangements can be expressed as:
$$
\frac{n!}{(a_1!)(...)(a_k!)}
$$
The above expression is called the **multinomial coefficient**.

## Combinations.

A **combination** is the total # of ways to form a $k$-length subset of a set $n$, a combination is denoted as follows:
$$
_nC_k = \frac{n!}{k!(n-k)!} = n \text{ choose } k
$$

### Of $5$ cats, $5$ dogs, and $4$ mice, $3$ are chosen. 

#### How many ways can we get $2$ cats and $1$ dog?

**Cats:** $5$ cats choose $2$, $(_5C_2)$.

**Dogs:** $5$ dogs choose $1$, $(_5C_1)$

We want these both to happen, so the answer is $(_5C_2)(_5C_1)$.

#### How many ways can we get at least $1$ cat?

**Think:** Total combinations $-$ all combinations with no cats.

Total combinations = $_{14}C_3$.

All combinations with no cats = $_{9}C_3$.

So final answer is $_{14}C_3 - {_{9}C_3}$.

## Binomial theorem.

### Defining the theorem.

The theorem below holds for any positive integer $n$.
$$
(x + y)^n = \sum_{k = 0}^{n} (_nC_k)x^ky^{n-k}
$$
Fun but pretty obvious note, the formula $(a + b)^2 = a^2 + 2ab + b^2$ can be directly derived from the above theorem. 

### Proving it.

Note the following (pretty obvious).
$$
(x + y)^n = (x + y)(x + y)(...)(x + y) \\ 
\text{multiplied $n$ times}
$$
Consider that the expansion of this expression would consist of multiplying all combinations of $x$ and $y$ from each binomial, and summing the resulting products of each combination.

Say we choose only $x$ terms from each binomial. This implies that we **choose zero $y$ terms**. The resultant term in the expansion would be $(_nC_0)x^ny^0$. Next, let's choose only $x$ terms from each binomial except for one. From that binomial, we will **choose one $y$ term**. The resultant term in the expansion would be $(_nC_1)x^{n-1}y^1$

To generalize this idea of "choosing" terms, let us choose $x$ terms from $k$ of the binomials, assuming that $k < n$. This implies that will **choose $y$ terms from $n - k$** binomials. The generalized resultant term would be $(_nC_k)x^ky^{n-k}$.

To calculate the expansion of the entire expression, we would need to calculate and sum the products of every combination of $x$ and $y$ that can be chosen from each binomial.

Note that $k$ (the # of times $x$ is chosen) can range between $0$ and $n$, inclusive. For each of these choices, $y$ must be chosen a total of $n - k$ times, so that $n$ terms are chosen in total (one from each binomial). With this in mind, we can express the summation of the combination products as such:
$$
\sum_{k = 0}^{n}(_nC_k)x^ny^{n-k}
$$

## Multinomial theorem.

**CATCHUP** wtf.	
