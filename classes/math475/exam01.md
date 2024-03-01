# math475 / exam01

## permutations, combinations, and general counting.

### $k$-permutations of $[n]$:

$$
P(n, k) = \frac{n!}{(n - k)!}
$$

### $k$-length subsets, or combinations, of $[n]$:

$$
\binom{n}{k} = \frac{P(n, k)}{k!} = \frac{n!}{k!(n - k)!}
$$

### **Proof** of the binomial theorem:

Consider that $(x + y)^n$ can be expanded as $(x + y)(...)(x + y)$. If this expression were to be manually expanded and then summed, in theory, it would result in an expression where each term takes the form $Cx^a y^b$. When calculating each term, we must choose either $x$ or $y$ from each $(x+y)$ group. If we decide to choose $x$ from $i$ of the $n$ group, there are $\binom{n}{i}$ ways to do so. In addition, this implies we choose $n - i$ of the $y$ terms to multiply. As a result, our term becomes $\binom{n}{i}x^i y^{n-i}$​. 

We can feasibly choose $x$ anywhere between $0$ and $n$ times, inclusive. So we sum $i$ from $0$ to $n$, inclusive, to determine the sum of all terms in the expansion of $(x + y)^n$.

As a result, we find that:
$$
(x + y)^n = \sum_{i = 0}^{n} \binom{n}{i} x^i y^{n - i}
$$

### Permutations with repetitions:

**Theorem:** object $1$ occurs $a_1$ times, ... object $k$ occurs $a_k$ times, where $a_1 + ... + a_k = n$. Then, the total # of rearrangements can be expressed as:
$$
\binom{n}{a_1,..., a_k} = \frac{n!}{(a_1!)(...)(a_k!)}
$$

### Counting strategies.

Let's say we want to count all elements of a set that satisfy some condition $x$. This might be a complicated process. Instead, we might be able to find all elements that don't satisfy $x$ and subtract them from the total length of the set.

## counting in two ways.

### Group leader strategy

$$
\text{Prove that} \sum_{k = 0}^{n} k \binom{n}{k} = n2^{n - 1}
$$

**LHS:** Counts all possible subgroups of a committee of $n$ people, where one of the subgroup members is assigned as the group leader.

**RHS:** $n$ counts the total number of ways to choose one member as the leader and $2^{n - 1}$​ assigns them zero or more followers from the committee.

Both **LHS** and **RHS** count the total number of subgroups of committee $[n]$ where exactly one member is a leader. $\blacksquare$

### Partitioning strategy

$$
\text{Prove that} \sum_{i = 1}^{n} i(n - i + 1) = \binom{n + 2}{3}
$$

**RHS:** Counts all subsets of length 3 of $[n + 2]$.

**LHS:** Consider that a 3-length subset can be expressed as $\{a, b, c\}$ where $a < b < c$. For some $1 \leq i \leq n$, we fix $b = i + 1$ . This leaves $i$ possibilities for $a$. For $c$, there are $n - 2 - (i + 1 ) = n - i + 1$ possibilities. Summing the expression for all possible values of $i$, we find the total number of 3-length subsets of $[n + 2]$.

As such, **LHS** equals **RHS**. $\blacksquare$

### Yapping strategy

$$
\text{Prove that} \sum_{k = 0}^{n} {k^2} \binom{n}{k} = n(n - 1)2^{n - 2} + n2^{n - 1}
$$

In a certain market, companies are either profitable or not profitable. The market can either be a monopoly or a duopoly, i.e. if any companies are profitable, there must be exactly one or two dominant companies. Let $[n]$​ be the set of all companies in our market. 

A valid market is one where if any companies are profitable, exactly one or two are dominant.

**LHS:** Let $0 \leq k \leq n$ be the number of profitable companies in the market. $\binom{n}{k}$ counts the total arrangements of which $k$ companies are profitable, implying that the remaining $n - k$ companies are unprofitable. Of the profitable companies, $k^2$ selects two with replacement. If the two chosen companies are the same, the one company chosen twice is dominant (monopoly); if they are different, the two different companies form a duopoly. Summing the expression for all $k$, we find the total number of valid markets.

**RHS:** The expression $n(n - 1)2^{n - 2}$ counts the total number of valid markets in a duopoly. $n(n - 1)$ chooses two profitable companies to be dominant, and $2^{n - 2}$ assigns the remaining companies to be profitable or not. The expression $n2^{n - 1}$ counts the total number of valid markets in a monopoly. $n$ chooses one profitable company to be dominant, and $2^{n-1}$​ assigns the remaining companies to be profitable or not. Summing the two expressions, we find the total number of valid markets.

As such, **LHS** equals **RHS**. $\blacksquare$

## pigeonhole principle.

The **pigeonhole principle** states that if $n$​ pigeons are placed in $k$​ pigeonholes, at least one pigeonhole contains $\lceil \frac{n}{k} \rceil$​ pigeons.

### Basic examples

**Prove** that in a group of 40 people, at least 4 people have a birthday in the same month.

- Let the pigeons be people, and pigeonholes be birth months. It follows that we wish to assign 40 pigeons into 12 pigeonholes; by the **PHP**, there exists one month such that $\lceil \frac{40}{12} \rceil = 4$ people have a birthday in that month. $\blacksquare$

**Prove** that if six distinct numbers are chosen from $\{1, 2, 3, 4, 5, 6, 7, 8, 9\}$, two of the numbers will sum to ten. 

- Let us group the numbers into pairs, such that each pair adds up to ten. We will let 5 stay on its own as it has no pair: $\{ \{1,9\}, \{2,8\}, \{3,7\}, \{4,6\}, \{5\} \}$. These 5 groups will be the pigeonholes and the six distinct numbers will be the pigeons. By the **PHP**, there exists one pair with at least $\lceil \frac{6}{5} \rceil = 2$ of the distinct numbers. Since the group $\{5\}$ cannot hold more than one number, another pair must take on the second number, meaning that two of the numbers chosen must add up to ten. $\blacksquare$

### More complex examples

An athlete works out in the blocks of hours. He plans to work out a total of 45 hours in
a 30-day month. Assume he works out at least 1 hour each day. **Prove** that there is a period
of consecutive days where the cumulative hours he has worked out is a total of exactly 14
hours.

- Let $a_i$ be the accumulated hours worked out up to and including day $i$​. Now let $b_i = a_i + 14$, such that $b_{30} = 59$​. Since he works out every day, every value in $a$ is distinct, meaning every value in $b$ is also distinct. Consider that both sequences combined have $60$ instances, and there are 59 possible values that each value can take one. By the **PHP**, there must be $\lceil \frac{60}{59} \rceil = 2$ instances that take on the same value.
- Since all elements of $a$ are distinct from each other and all elements in $b$ are also distinct from each other, the two instances that share the same value must be in $a$ and $b$. As such, there exists a value $a_j = a_i + 14$, for $i \neq j$. Therefore, there exists a period of consecutive days in which the athlete works out exactly $14$ hours. $\blacksquare$

## compositions, and stirling and bell numbers.

### Compositions; weak and strong

The number of **weak compositions** of $n$ into $k$ parts (weak means that the parts can have value $0$) is defined as $\binom{n + k - 1}{k - 1}$.

The number of **strong compositions** of $n$ into $k$ parts (strong means that each part must be $\geq 1$) is defined as $\binom{n - 1}{k - 1}$.

- Logically derivable from the weak compositions. Consider that we want to enforce that each of the $k$ parts must be at least $1$. So we remove $k$ options from $n + k - 1$, as we have "forced them to be used."

### Stirling numbers

The **Stirling number of the second kind**, denoted $S(n, k)$, counts the ways to partition $[n]$ into $k$​ non-empty parts.

- By convention, $S(0, 0) = 1$. 
- Example, $S(3, 2) = 3$.
  - All the sets: $\{\{\{1\}, \{2, 3\}\}, \{\{2\}, \{1, 3\}\}, \{\{1\}, \{2, 3\}\}, \{\{3\}, \{1, 2\}\}\}$.

**Prove** that $S(n, k) = S(n - 1, k - 1) + kS(n - 1, k)$.

- **LHS:** Counts the number of ways to partition a set of length $n$ into $k$ parts.
- **RHS:** Consider where we are placing the $n$th element. 
  - We are starting a new part. In this case, we can place one element in its own part. For the remaining $n - 1$ elements, we have $k - 1$​ parts, hence $S(n - 1, k - 1)$.
  - We are adding to an existing part. In this case, we have $k$ parts to add our additional element to. As for the remaining $n - 1$ elements, we need to distribute them among the $k$ parts we have as well, hence $kS(n - 1, k)$​.

### Bell numbers

The total number of partitions of $[n]$ is the **Bell number**, i.e.
$$
B(n) = \sum_{k = 1}^{n} S(n, k)
$$
 **Prove** that $B(n) = \sum_{i = 1}^{n} \binom{n - 1}{i - 1} B(n - i)$.

- **LHS:** Counts the number of ways to partition $[n]$​ into non-empty parts.
- **RHS:** Let us consider a $i$-length part of $[n]$. We will fix one of the elements to be in the part, meaning there are $\binom{n - 1}{i - 1}$ possibilities for the remaining $i - 1$ elements of the part. We then have $n - i$ elements remaining. $B(n - i)$ counts the ways to partition these $n - i$. Summing from $i = 1$ to $n$, we determine the total number of ways to partition $[n]$ into non-empty parts.

## integer partitions.

An **integer partition** of $n$ is a positive sequence of integers that sum up to $n$. The total number of integer partitions of $n$ is denoted $p(n)$.

Let $p_k(n)$ denote the total integer partitions of $n$ into exactly $k$​ parts.

**Prove** that for $1 < k < n$, $p_k(n) = p_{k - 1}(n - 1) + p_k(n - k)$​.

- **LHS:** Counts the number of integer partitions of $n$ into exactly $k$ parts.
- **RHS:** Consider the following cases:
  - A part of size $1$ exists: In this case, we can simply calculate the partitions of $n - 1$ into $k - 1$ parts, hence $p_{k - 1}(n - 1)$.
  - A part of size $1$ does not exist. In this case, we distribute $1$ to each of our $k$ parts, to ensure that no part has size $1$. We are then left with $n - k$ to partition across our $k$ parts, hence the expression $p_k(n - k)$.

## twelvefold way.

**Memorize these I guess?**

1. $n$ labeled balls to $k$ labeled bins.
   1. **No restriction:** $k^n$
      1. Differ between each ball and have $k$ choices for each of them.
   2. **At least 1:** $S(n, k)k!$
      1. The number of surjective functions from $[n]$ to $[k]$.
   3. **At most 1** (if $n \leq k$): $P(k, n)$. 
2. $n$ unlabeled balls to $k$ labeled bins.
   1. **No restriction:** $\binom{n + k - 1}{k - 1}$
      1. Number of weak compositions, as all balls are the same.

   2. **At least 1:** $\binom{n - 1}{k - 1}$.
      1. At least one in each, so strong compositions.

   3. **At most 1** (if $n \leq k$): $\binom{k}{n}$
      1. Because balls aren't distinct.

3. $n$ labeled balls to $k$ unlabeled bins.
   1. **No restriction:** $\sum_{i = 1}^{k} S(n, i)$.
      1. Some bins can be empty.

   2. **At least 1:** $S(n, k)$
      1. No bins can be empty.

   3. **At most 1** (if $n \leq k$): 1 way.

4. $n$ unlabeled balls to $k$ unlabeled bins.
   1. **No restriction:** $\sum_{i = 1}^{k} p_i(n)$
      1. Integer partitions, order doesn't matter.

   2. **At least 1:** $p_k(n)$​
      1. No empty bins.
      2. **At most 1** (if $n \leq k$): 1 way.


## inclusion-exclusion principle.

Let $A_1, ... A_n \sube X$, assuming that $A_i$ nonempty for all $i$:
$$
| \bigcup_{i = 1}^{n} A_i | = \sum_{J \sube \{1, ..., n\}} (-1)^{|J| + 1} |\bigcap_{j \in i} A_j|
$$
**Steps:**

1. Add the lengths of all individual sets.
2. Subtract the lengths of all unions of two sets.
3. Add the lengths of all unions of three sets.
4. Subtract the lengths of all unions of four sets.
5. And so on...

## ordinary generating functions.

Let $a_i$ be some sequence. Then the **ordinary generating function** of $a$ is
$$
F(x) = \sum_{n = 0}^{\infty} a_n x^n
$$
Important identity is that for $x \in (-1, 1)$,
$$
\sum_{n = 0}^{\infty} x^n = \frac{1}{1 - x}
$$
With the above identity, we can find $f_n$ given its ogf:
$$
\begin{align*}
F(x) &= \frac{-4x + 3}{(1 - x)(1 - 2x)} \\
&= \frac{1}{1 - x} + \frac{2}{1 - 2x} \\
&= \sum_{i = 0}^{\infty} x^n + 2 \sum_{i = 0}^{\infty} (2x)^n \\
&= \sum_{i = 0}^{\infty} (2^{n + 1} + 1)x^n \\
&= \sum_{i = 0}^{\infty} a_n x^n, a_n = 2^{n+1} + 1
\end{align*}
$$

### recurrences and ogfs

**Question:** Use ogf to find an explicit formula for $a_{n + 2} = 3a_{n + 1} - 2a_n$ where $a_0 = 0$ and $a_1 = 1$.
$$
\begin{align*}
G(x) &= \sum_{n \geq 0} a_n x^n \\
\sum_{n \geq 0} a_{n + 2} x^{n + 2} 
&= 3 \sum_{n \geq 0} a_{n + 1} x^{n + 2} -2 \sum_{n \geq 0} a_n x^{n+2} \\
G(x) - a_0 - a_1x &= 3xG(x) - 2x^2G(x) \\
G(x) - x &= 3xG(x) - 2x^2G(x) \\
G(x) (1 - 3x + 2x^2) &= x \\
G(x) &= \frac{1}{2x^2 - 3x + 1} \\
&= \frac{1}{(1 - x)(1 - 2x)} \\
&= \frac{-1}{(1 - x)} + \frac{1}{(1 - 2x)} \\
&= \sum_{n \geq 0} -x^n + \sum_{n \geq 0} (2x)^n \\
&= \sum_{n \geq 0} (-1 + 2^n)x^n \\
a_n &= 2^n -1
\end{align*}
$$
