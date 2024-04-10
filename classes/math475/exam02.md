# math475 / exam02

## things on the exam.

1. Graph theory proofs. None of the proofs are very long; two to three lines and very simple arguments. Meant to be short.
2. For EGFs, know the permutation, even and odd cases.
3. For OGFs, know the integer partition and weak composition formulas.
4. Nothing on Catalan numbers.
5. Know the Prufer Code (both ways).
6. Know the degree sequence formula; Havel-Hakimi algorithm.

## formula sheet.

Useful OGF formula #1: $\sum_{n \geq 0} x^n = \frac{1}{1 - x}$, when $ -1 < x < 1$​.

OGF of weak compositions: $\sum_{n \geq 0} \binom{n}{k} x^n = \frac{1}{(1 - x)^k}$.

OGF of strong compositions: $(\frac{x}{1 - x})^k$.

OGF of $p(n)$: $\prod_{k = 1}^{\infty} \frac{1}{1 - x^k} = (1 + x + x^2 \dots)(1 + x^2 + x^4+ \dots)(1 + x^3 + x^6 + \dots)(\dots)$.

OGF of $p_k(n)$: $(1 + x + x^2 + \dots x^k)(1 + x^2 + x^4 + \dots x^{2k})(1 + x^3 + x^6 + \dots x^{3k})(\dots)$.

Multiplying OGFs: $(\sum_{n \geq 0} a_n x^n)(\sum_{n \geq 0} b_n x^n) = \sum_{n \geq 0}c_n$, where $c_n = \sum_{i = 0}^{n} a_i b_{n - i}$.

Useful EGF power series: $\sum_{n \geq 0} \frac{x^n}{n!} = e^x$.

EGF of even occurrences: $\frac{e^x + e^{-x}}{2}$; EGF of odd occurrences: $\frac{e^x - e^{-x}}{2}$​. 

Multiplying EGFs: $(\sum_{n \geq 0} a_n \frac{x^n}{n!}) (\sum_{n \geq 0} b_n \frac{g^n}{n!}) = \sum_{n \geq 0}\frac{x^n}{n!} h_n$, where $c_n = \sum_{i = 0}^{n} \binom{n}{i} f_i g_{n - i}$.

$C_n$ counts total NE lattice paths from $(0, 0)$ to $(n, n)$​ that never cross diagonal.

Order is number of vertices; size is number of edges.

For simple graph, there must be even number of odd degrees.

Bipartite sets $S$ and $T$​​ both have same number of edges.

A tree with order $n$ always has $n - 1$​ edges.

Cayley's formula: the number of trees on $n$ labeled vertices is $n^{n - 2}$.

Forest is a graph of disconnected trees; tree is a forest but not always vice versa.

Tree to Prufer Code: pop the smallest leaf and add neighbor until $2$​ vertices left.

Prufer Code to Tree: Make a list of vertices, depending on list length:

1. $>2$ nums: Edge from leftmost num in **code** to smallest num in **list**. Remove and repeat.
2. $= 2$​ nums: Edge between these two.

Valid degree sequence: even amount of odd nums, sum $< n(n - 1)$, max $<$ order.

## ordinary generating functions.

The following is an important property that we abuse:
$$
\sum_{n = 0}^{\infty} x^n = \frac{1}{1 - x}\text{ , for } x \in (-1, 1)
$$
**Example:** Determine a sequence that corresponds to the following OGF.

>$$
>F(x) = \sum_{n = 0}^{\infty} a_n x^n = \frac{1 - 5x}{1 - 4x + 3x^2}
>$$
>
>Factor the denominator:
>$$
>3x^2 - 4x + 1 = 3x^2 - 3x - x + 1 = 3x(x - 1) - 1(x - 1) = (3x - 1)(x - 1)
>$$
>Split the fraction using partial fraction decomposition:
>$$
>\frac{1 - 5x}{(3x - 1)(x - 1)} = \frac{1}{3x - 1} - \frac{2}{x - 1}
>$$
>
>Now we find $a_x$:
>$$
>\begin{align*}
>	\frac{1}{3x - 1} - \frac{2}{x - 1} 
>	&= -\frac{1}{1 - (3x)} + \frac{2}{1 - x} \\
>	&= - \sum_{n = 0}^{\infty} (3x)^n + \sum_{n = 0}^{\infty} 2(x)^n \\
>	&= \sum_{n = 0}^{\infty} \left[-(3x)^n + 2x^n\right] \\
>	&= \sum_{n = 0}^{\infty} x^n(-3^n + 2) \\
>	a_n &= 2 - 3^n
>\end{align*}
>$$

**Example:** Determine a sequence that corresponds to the following OGF.

>$$
>F(x) = \sum_{n = 0}^{\infty} a_n x^n = \frac{3 + 3x}{1 + x - 2x^2}
>$$
>
>Factor the denominator:
>$$
>-2x^2 + x + 1
>= -2x^2 + 2x - x + 1
>= -2x(x - 1) - (x - 1)
>= (-2x - 1)(x - 1)
>= -(2x + 1)(x - 1)
>$$
>Split fraction using partial fraction decomposition:
>$$
>\begin{align*}
>	-\frac{3 + 3x}{(x - 1)(2x + 1)} &= -\left[\frac{A}{x - 1} + \frac{B}{2x + 1}\right] \\
>	A(2x + 1) + B(x - 1) &= 3 + 3x \\
>	\text{let } x &= 1 \\
>	&\rightarrow A(2 + 1) = 3 + 3 \\
>	&\rightarrow A = \frac{6}{3} = 2 \\
>	\text{let } x &= \frac{1}{2} \\
>	&\rightarrow B(\frac{1}{2} + 1) = 3 - \frac{3}{2} \\
>    &\rightarrow B = \frac{3}{2} (\frac{2}{3}) = 1
>\end{align*}
>$$
>Plugging back in,
>$$
>\begin{align*}
>	F(x) &= -\left[\frac{2}{x - 1} + \frac{1}{2x + 1}\right] \\
>	&= -\left[\frac{-2}{1 - x} + \frac{1}{1 - (-2x)} \right] \\
>	&= \sum_{n = 0}^{\infty} -\left[(-2x^n)+(-2x)^n\right] \\
>	&= \sum_{n = 0}^{\infty} 2x^n + (-2)^n x^n \\
>	&= \sum_{n = 0}^{\infty} x^n (2 + (-2^n)) \\
>	a_n &= 2 + (-2)^n
>\end{align*}
>$$
>

**Example:** Find the closed form of the OGF for the following recurrence:

>$$
>a_n = 3a_{n - 1} + 2a_{n - 2}, a_{0} = 1, a_{1} = 2
>$$
>
>**TODO:** when I figure this out later.

**Example:** Find the closed form of the OGF for the following recurrence:
$$
a_n = 2a_{n - 1} + 4^{n - 1}, a_0 = 1
$$

>Our definition of OGF:
>$$
>F(X) = \sum_{n \geq 0} a_n x^n
>$$
>Take the recurrence and rearrange:
>$$
>\begin{align*}
>	a_n 
>		&= 2a_{n - 1} + 4^{n - 1} 
>		&\text{recurrence} \\
>	\sum_{n \geq 1} a_n x^n 
>		&= \sum_{n \geq 1} 2a_{n - 1} x^n + \sum_{n \geq 1} 4^{n - 1} x^n 
>		&\text{sum both sides} \\
>    \sum_{n \geq 0} a_n x^n - a_0 
>    	&= x\sum_{n \geq 0} 2a_n x^n + x\sum_{n \geq 0} 4^n x^n 
>    	&\text{write sums as $n \geq 0$} \\
>    G(x) - 1
>    	&= 2G(x) + \frac{x}{1 - 4x}
>    	&\text{simplify sums w/ogf} \\
>    G(x) - 2xG(x) &= \frac{x}{1 - 4x} + 1 \\
>    G(x)[1 - 2x] &= \frac{1 - 3x}{1 - 4x} \\
>    G(x) &= \frac{1-3x}{(1 - 2x)(1 - 4x)}
>\end{align*}
>$$

**Example:** We have invested $1000$ dollars into a savings account that pays $5\%$ interest at the end of each year. At the beginning of each year, we deposit another $500$ dollars into this account. How much money will be in this account after $n$​ years?

> We can quickly find a recurrence for this situation:
> $$
> a_n = 1.05a_{n - 1} + 500, a_0 = 1000
> $$
> Recall our definition of OGF:
> $$
> F(X) = \sum_{n \geq 0} a_n x^n
> $$
> Take the recurrence and rearrange:
> $$
> \begin{align*}
> 	\sum_{n \geq 1} a_n x^n 
> 		&= \sum_{n \geq 1} 1.05a_{n - 1} x^n + \sum_{n \geq 1} 500 x^n
>         &\text{sum recurrence} \\
> 	\sum_{n \geq 0} a_n x^n - a_0 
> 		&= 1.05x\sum_{n \geq 0} a_n x^n + \sum_{n \geq 0} 500x^n
> 		&\text{write sums as $n \geq 0$} \\
>     F(x) - 1000 
>     	&= 1.05xF(x) + \frac{500}{1 - x}
>     	&\text{def of ogf} \\
>     F(x)[1 - 1.05x] 
>     	&= \frac{1}{1 - x} + 500 = \frac{501 - 500x}{1 - x}
>     	&\text{move $F$ to one side} \\
>     F(x) &= \frac{501 - 500x}{(1 - x)(1 - 1.05x)}
>  \end{align*}	
> $$
> 

**Example:** Determine the ogf and the relevant coefficient for the total ways to distribute $25$ identical pieces of candy to $5$ children such that everyone gets an odd number of pieces and no child can get more than $10$ pieces.

>We want the coefficient of $x^{25}$ in the following:
>$$
>(x^1 + x^3 + x^5 + x^7 + x^9)^5
>$$

**Example:**  A businessman has $\$20000$ to invest in $5$ different stocks. However, each stock requires that investments must be given in multiples of $\$1000$, and not all the money can be put into $1$ stock. Determine the ogf that would determine the total ways the businessman could invest his $\$20000$.

> Each stock must have a value between $1000$ and $19000$, inclusive.
>
> As such, we look to find the coefficient of $x^{20}$ in:
> $$
> (x + x^2 + x^3 + \dots + x^{18} + x^{19})^5
> $$

**Example:** Find the ogf and the relevant coefficient to determine the total partitions of $50$, where each number is used at most twice.

>OGF of integer partitions:
>$$
>(1 + x + x^2 + x^3 + \dots) (1 + x^2 + x^4 + x^6 + \dots) (1 + x^3 + x^6 + x^9 + \dots) (\dots) 
>$$
>We restrict each integer to be used twice at most, and we want the coefficient of $x^{50}$:
>$$
>(1 + x + x^2) (1 + x^2 + x^4) (1 + x^3 + x^6) (\dots)
>$$

**Example:** Determine the OGF that would count the total ways to partition integer $n$ so that if a part occurs, it occurs at least $6$​ times.

> OGF of integer partitions:
> $$
> (1 + x + x^2 + x^3 + \dots)(1 + x^2 + x^4 + x^6 + \dots)(1 + x^3 + x^6 + x^9 + \dots)(\dots)
> $$
> We restrict each integer part to be used at least $6$ times:
> $$
> (1 + x^6 + x^7 + x^8 + \dots) (1 + x^{12} + x^{14} + x^{16} + \dots) (1 + x^{18} + x^{21} + x^{24} + \dots) (\dots)
> $$
> Notice that we keep the $1$ in each parentheses, as that is the case where the integer never shows up in the partition. However, we get rid of $x^1$ through $x^5$, as it either doesn't exist or shows up at least $6$ times.

## exponential generating functions.

**Example:** Determine closed form egf that counts total strings of length $n$ using the characters $A, B, C, D, E, F, G$ (not all letters need to be used), such that an even number of $C$s are used and at least one $G$ is used. If $a_n$ counts these strings, find a closed form.

>For the letters with no conditions, A, B, D, E, F, we have $e^{5x}$.
>
>For an even number of $C$s, we have $\frac{e^x + e^{-x}}{2}$.
>
>For at least one $G$, we have $e^x - 1$.
>
>This leaves us with the following OGF:
>$$
>\begin{align*}
>	e^{5x} \left(\frac{e^x + e^{-x}}{2} \right) (e^x - 1)
>	&= \frac{1}{2}(e^{6x} - e^{5x})(e^x + e^{-x}) \\
>	&= \frac{1}{2}(e^{7x} - e^{6x} + e^{5x} - e^{4x})
>\end{align*}
>$$
>Let's now find $a_n$:
>$$
>\begin{align*}
>	\frac{1}{2}(e^{7x} - e^{6x} + e^{5x} - e^{4x}) &= \sum_{n \geq 0} \frac{\frac{1}{2} (7x)^n - (6x)^n + (5x)^n - (4x)^n}{n!} \\
>	&= \sum_{n \geq 0} \frac{x^n}{n!} \left( \frac{7^n - 6^n + 5^n - 4^n}{2} \right) \\
>	
>\end{align*}
>$$

**Example:** Determine closed form of the EGF that would count the total strings of length $n$ using letters $A, B, C, D$ (not all required) such that there is at least one $A$ and there are an odd number of $D$'s. Also find $a_n$ which denotes the total strings.

> For letters $B$ and $C$ without conditions: $e^{2x}$.
>
> For at least one $A$: $e^x - 1$.
>
> For odd number of $D$'s: $\frac{e^x - e^{-x}}{2}$.
>
> This leaves us with the following EGF:
> $$
> \begin{align*}
> 	e^{2x}(e^x - 1)\left( \frac{e^x - e^{-x}}{2} \right) 
> 		&= \frac{1}{2}(e^{3x} - e^{2x})(e^x - e^{-x}) \\
>     	&= \frac{1}{2}(e^{4x} - e^{3x} - e^{2x} + e^x)
> \end{align*}
> $$
> From this we can find $a_n$:
> $$
> \begin{align*}
> 	\frac{1}{2}(e^{4x} - e^{3x} - e^{2x} + e^x)
> 		&= \frac{1}{2} \sum_{n \geq 0} \frac{(4x)^n - (3x)^n - (2x)^n + x^n}{n!} \\
> 		&= \sum_{n \geq 0} \frac{x^n}{n!} \left( \frac{4^n - 3^n - 2^n + 1}{2} \right) \\
>     a_n &= \frac{4^n - 3^n - 2^n + 1}{2}
> \end{align*}
> $$
> 

**Example:** Determine $a_n$ that corresponds to the EGF $\frac{e^x}{1 - x}$.

> Let $F(x) = e^x$ and $G(x) = \frac{1}{1 - x}$. Note that $F(x)G(x)$ is just our EGF.
> $$
> \begin{align*}
>     F(x) &= e^x \\
>     	&= \sum_{n \geq 0} \frac{x^n}{n!} \\
>     G(x) &= \frac{1}{1 - x} \\
>     	&= \sum_{n \geq 0} x^n \\
>     \text{let } f_n &= 1 \\ 
>     \text{and } g_n &= n! \\
>     F(x)G(x) &= \left[\sum_{n \geq 0} \frac{x^n}{n!}\right] \left[\sum_{n \geq 0} x^n \right] \\
>         &= \left[\sum_{n \geq 0} f_n \frac{x^n}{n!}\right] \left[\sum_{n \geq 0} g_n \frac{x^n}{n!} \right] \\
>         &= \sum_{n \geq 0} \frac{x^n}{n!} \left( \sum_{i = 0}^{n} \binom{n}{i} (n - i)! \right) \\
>     a_n &= \sum_{i = 0}^{n} \binom{n}{i} (n - i)!
> \end{align*}
> $$

**Example:** Use EGFs to find a closed form for $a_n = na_{n - 1}$, where $a_0 = 2$.

>$$
>\begin{align*}
>	a_n &= na_{n - 1} \\
>	\sum_{n \geq 1} a_n \frac{x^n}{n!} &= \sum_{n \geq 1} a_{n - 1} \frac{x^n}{(n-1)!} \\
>	\sum_{n \geq 0} \frac{a_n x^n}{n!} - a_0 &= x\sum_{n \geq 0} \frac{a_n x^n}{n!} \\
>	F(x) - 2 &= xF(x) \\
>	F(x) [1 - x] &= 2 \\
>    F(x) &= \frac{2}{1 - x}
>\end{align*}
>$$
>
>From this closed form of $F(x)$, we can find $a_n$:
>$$
>\begin{align*}
>	F(x) &= \frac{2}{1 - x} \\
>		&= \sum_{n \geq 0} 2x^n \\
>		&= \sum_{n \geq 0} (2n!)\frac{x^n}{n!} \\
>	a_n &= 2n!
>\end{align*}
>$$

**Example:** Use generating functions to show that:
$$
\sum_{i = 0}^{k} \binom{m}{i} \binom{n}{k - i} = \binom{m + n}{k}
$$

> Take RHS. This is the binomial coefficient of the summation:
> $$
> (x + 1)^{m + n} = \sum_{k = 0}^{m + n} \binom{m + n}{k} x^k
> $$
> Split $(x + 1)^{m + n}$:
> $$
> \begin{align*}
> 	(x + 1)^{m + n} 
> 		&= (x + 1)^m(x + 1)^n \\
> 		&= \left[\sum_{i = 0}^{m} \binom{m}{i} x^{k} \right] \cdot \left[ \sum_{i = 0}^{n} \binom{n}{i} x^k \right] \\
> 		&= \sum_{i = 0}^{k} \binom{m}{i} \binom{n}{k - 1}
> \end{align*}
> $$
> Proved using the product of series formula!

**Example:** Use EGFs to find the number of ways to order $n$ books into $k$ bookshelves.

> Consider ordering $i$ books on one shelf. This clearly has $a_i = i!$ ways and has the following EGF:
> $$
> \sum_{i = 1}^{\infty} i! \frac{x^i}{i!} = \sum_{i = 1}^{\infty} x^i = \frac{1}{1 - x} - 1 = \frac{x}{1 - x}
> $$
> To find the EGF of total orderings across $k$ shelves, multiply the above $k$ times:
> $$
> \left(\frac{x}{1 - x} \right)^k
> $$
> Notice that the above is the OGF of compositions of $n$ into $k$ parts.

## catalan numbers.

**Example:** Prove that the number of integer sequences $a_1, ..., a_n$ restricted such that $1 \leq a_1 \leq a_2 \leq \dots \leq a_n$ satisfying $a_i \leq i$ is the $n$th Catalan number.

>Recall that the $n$th Catalan number $C_n$ counts the number of northeastern lattice paths from the point $(0, 0)$ to $(n, n)$ that never cross over the diagonal $y = x$. 
>
>At any given $(x, y)$ point across any of these paths, $x \geq y$, due to the restriction that the diagonal is never crossed. Furthermore, $x$ must at some point be every integer from $0$ to $n$ for each path.
>
>With this in mind, each path can be expressed as an integer sequence $a$, where each point  $(x, y)$ the path touches is represented by $a_x = y$ in the sequence. This results in a non-decreasing sequence $\{a_n\}$ that satisfies $a_i \leq i$.
>
>Since there is a sequence $\{a_n\}$ described above for each path counted by $C_n$, we have our result. $\blacksquare$

## properties of simple graphs and trees.

**Example:** Consider the sequence $\{6, 6, 4, 4, 2, 1, 1, x\}$. For what values of $x$ is the reordered sequence graphical?

> A **graphical sequence** is another word for degree sequence. Basically, what degrees can the last vertex have?
>
> There are $8$ nodes in total, meaning $x$ can be at most $7$. Recall that we assume all graphs to be simple, so vertices can't connect to themselves. 
>
> Excluding $x$, we have $2$ nodes with odd degrees. If $x$ were odd, we'd have an odd number of nodes with odd degrees. This is an invalid degree sequence. 
>
> We then have $2, 4, 6$ as the possible values for $x$.

**Example:** Why is there no bipartite graph with the degree sequence:
$$
\{6, 6, 6, 6, 6, 6, 6, 6, 5, 3, 3, 3, 3, 3\}
$$

> If the above were bipartite, we should be able to form two sets $S$ and $T$ whose union is the vertices of the graph, where vertices in $S$ only connect to those in $T$, and vice versa. This means that the edges coming out of $S$ must be equal to those coming out of $T$.
>
> The total number of edges in the graph is $\frac{6(8) + 5 + 3(5)}{2} = 34$. In other words, there should be $34$ connections leaving $S$ and $T$ each.
>
> Take the eight $6$'s. There must be at least $4$ of these $6$-degree vertices in either $S$ or $T$. Since $6 \cdot 6 = 36$, we cannot have more than six $6$​-degree vertices in this partite set. 
>
> **Case 1:** one of the partite sets has four $6$-degree vertices. In this case, there must be $24$ connections leaving this partite set solely from these four nodes. The remaining nodes in this partite set must contribute $10$ connections. However, making exactly $10$ is not possible with the remaining nodes (one $5$ and five $3$'s).
>
> **Case 2:** one of the partite sets has five $6$-degree vertices. In this case, there must be $30$ connections leaving this partite set solely from these five nodes. The remaining nodes in the partite set must contribute $4$ connections. However, making exactly $4$ connections is not possible with the remaining nodes (one $5$ and five $3$'s).
>
> In both possible cases, we have shown that this bipartite graph cannot exist.  

**Example:** Suppose in graph $G$ of order $n$, $\deg u + \deg v \geq n - 1$ for any vertices $u, v$ in $G$. Prove $G$​ is connected.

>Let $a$ and $b$ represent any two vertices in $G$. To show that $G$ is connected, we want to demonstrate that there exists a walk from $a$ to $b$.
>
>**Case 1:** there exists an edge between $a$ and $b$. There exists a walk from $a$ to $b$: $a \rightarrow b$.
>
>**Case 2:** such an edge does not exist. In this case, consider the neighborhoods of $a + b$. It is given that $\deg a + \deg b \geq n - 1$. There exists $n - 2$ nodes other than $a$ and $b$, but at least $n - 1$ edges for them to be placed into. As such, $a$ and $b$ must share a neighbor. Call this neighbor $y$. There exists a walk from $a$ to $b$: $a \rightarrow y \rightarrow b$. 

**Example:** A bipartite graph with partite sets $S$ and $T$ satisfies the condition that the order of the graph equals the size of the graph. Moreover, every vertex in $S$ has degree of at most $5$. Prove that $|T| \leq 4|S|$.

> In the highest case, the total degree of the vertices in $S$ is $5|S|$. This is also equal to the size of the graph. Since $S$ and $T$ are partite sets of the bipartite graph, $|S| + |T|$ must be the order, which is given to be equal to the size. We can set up an inequality:
> $$
> \begin{align*}
> 	|S| + |T| &\leq 5|S| \\
> 	|T| &\leq 4|S| & \blacksquare
> \end{align*}
> $$

**Example:** A tree has vertices of degree $1, 2, 3, 4, 5$ only. There are $50$ vertices of degree $1$. The number of vertices of degree $2, 3, 4, 5$ are all the same. Determine the order of the tree. 

>Let $w$ be the number of vertices of degree $2, 3, 4, 5$ each. It follows that the total number of vertices, the order, must be $4w + 50$.
>
>Recall that the number of edges must then be $4w + 49$. The total degree of the graph is then $2(4w + 49) = 8w + 98$.
>
>We can also find total degree with the expression: $50 + w(2 + 3 + 4 + 5) = 14w + 50$.
>$$
>\begin{align*}
>	8w + 98 &= 14w + 50 \\
>    6w &= 48 \\
>    w &= 8
>\end{align*}
>$$
>We can substitute back into our order expression:
>$$
>n = 4(8) + 50 = 82 \text{ is the order}
>$$

**Example:** A bipartite graph has partite sets $A$ and $B$. The graph has $22$ vertices, and $A$ has $12$ vertices. Every vertex in $A$ has degree $3$, and every vertex in $B$ has degree $2$ or $4$. How many vertices have degree $4$?

> $B$ has $22 - 12 = 10$ vertices, each of which has degree $2$ or $4$. 
>
> The total degree of the vertices in $A$ is $3(12) = 36$. The vertices in $B$ must then also have a total degree of $36$. 
>
> Let $v_2$ be the number of vertices with degree $2$, and $v_4$ be those with degree $4$:
> $$
> \begin{align*}
> 	2v_2 + 4v_4 &= 36 \\
> 	2[v_2 + v_4 &= 10] \\
> 	2v_4 &= 16 \\
> 	v_4 &= 8
> \end{align*}
> $$

**Example:** If graph $G$ has $n$ vertices, determine all values of $n$ where both $G$ and $\overline{G}$ could be trees. Explain.

> A tree $n$ must have $n - 1$ edges. We want to determine all ways where $\overline{G}$ could also have $n - 1$ edges.
> $$
> \begin{align*}
> 	\binom{n}{2} - (n - 1) &= (n - 1) \\
> 	\binom{n}{2} &= 2(n - 1) \\
> 	\frac{n!}{2! (n - 2)!} &= 2(n - 1) \\
> 	\frac{n(n - 1)(n - 2)!}{2! (n - 2)!} &= 2(n - 1) \\
> 	\frac{n}{2} &= 2 \\
> 	n &= 2 \cdot 2 = 4
> \end{align*}
> $$
> We have shown that $n$ can be $4$. However, consider the case of a sole vertex. This would be considered a tree, as would its complement, which is also a so.
>
> So our choices become $n = 1$ and $n = 4$​​.

**Example:** A forest has $n$ vertices, $m$ edges, and $c$​ components. Relate the three parameters.

> Let $n_i$ be the number of vertices in the $i$th component.
>
> The total number of edges across all trees must then be:
> $$
> \begin{align*}
> 	m &= \sum_{i = 1}^{c} [n_c - 1] \\
> 	&= \sum_{i = 1}^{c} n_c - \sum_{i = 1}^{c} 1 \\
> 	&= n - c
> \end{align*}
> $$

**Example:** How many simple graphs are there on the vertex set $[n]$?

> If we have $n$ vertices, there can be $\binom{n}{2}$ pairs of vertices. To form a simple graph, each of these pairs can either have an edge connected them, or not have one. The number of ways to build a graph with these requirements is then $2^{\binom{n}{2}}$.

**Example:** The degree of every vertex of a graph $G$ of order $2n + 1 \geq 5$ is either $n + 1$ or $n + 2$. Prove that $G$ contains either $n + 1$ vertices of degree $n + 2$ or $n + 2$ vertices of degree $n + 1$.

> We will prove this by contradiction. Let there be less than $n + 1$ vertices with degree $n + 2$ and less than $n + 2$ vertices with degree $n + 1$​.
>
> Let $x$ be the number of vertices with degree $n + 2$. We know that $x < n + 1$. The number of vertices with degree $n + 1$ is then $2n + 1 - x$.
> $$
> 2n + 1 - x < n + 2 \rightarrow x > n - 1
> $$
> If $n + 1 > x > n - 1$ and $x$ is an integer, $x = n$. There are exactly $n$ vertices with degree $n + 2$. 
>
> The number of vertices with degree $n + 1$ is then $2n + 1 - n = n + 1$.
>
> Consider the following two cases:
>
> - **Case 1:** $n$ is even. If so, then $n + 1$ vertices with degree $n + 1$ implies that $G$ has an odd number of vertices with odd degree. It cannot therefore be a valid simple graph, so we have a contradiction.
> - **Case 2:** $n$ is odd. If so, then $n + 2$ must also be odd. This implies that there are an odd number of vertices with odd degree. It cannot therefore be a valid simple graph, so we have a contradiction.
>
> Both cases yield a contradiction, so $G$ must contain either $n + 1$ vertices of degree $n + 2$ or $n + 2$ vertices of degree $n + 1$.

