# math475 / final

## formulas.

**Turan's Theorem:** Maximum edges on a graph, order $n$, without clique $K_r$ is $(\frac{r - 1}{2r})(n + 1)^2$​.

**Ramsey's Theorem:** There exists (minimal) number $R(k, l)$ so that the graph $K_{R(k, l)}$ has either a $K_k$ subgraph with only RED edges, or a $K_l$ subgraph with only BLUE edges. Notably, $R(k, l) \leq R(k, l - 1) + R(k - 1, l)$. 



## m3ow.

Let $G$ be a connected regular graph that is NOT Eulerian. Show that $\overline{G}$, if connected, is Eulerian.

>Say $G$ is $k$-regular on $n$ vertices. Since $G$ is not Eulerian, $k$ must be odd. There must be an even number of vertices of odd degree, so $n$​​ must be even. Each vertex is connected to $k$ other vertices, and not connected to $n - 1 - k$ vertices. As such, the degree of each vertex in $\overline{G}$ is $n - 1 - k$, if it is connected.
>
>Since $n$ is even, $n - 1$ must be odd. Since $k$ is odd, $n - 1 - k$ must be even. Therefore, every vertex on $\overline{G}$ has even degree, and $\overline{G}$​ must be Eulerian.

$100$ lactose tolerant mice are *assigned a specific seat* at a gigantic circular table with $100$ seats for a cheese dinner. The mice sit down randomly but realize every mouse is in the wrong seat! Prove that if all the mice rotate left the same number of times, at some point there must be at least two mice in their assigned seats.

>Let's name one mouse Joe. Initially, Joe (and all the other mice) is not in his assigned seat. Consider the number of rotations for Joe to have sat in every seat is $99$, as he starts in one of the $100$ seats already.
>
>Clearly, one of these $99$ seats must be Joe's, as his starting point is not correct. Now consider all the mice. Within these $99$ rotations, each mouse would have sat in their seat exactly once. Since no mouse started in their correct seat, we have $100$ mice to $99$ rotations. By the Pigeonhole principle, there exists a rotation where at least $\text{ceil}(\frac{100}{99}) = 2$ are seated correctly.

Find a closed form for:
$$
f(x) = \sum_{n = 1}^{\infty} n x^{n - 1}
$$
And then use generating functions fand (a) to find a closed form for:
$$
a_n = a_{n - 1} + n, a_0 = 1
$$

> Consider the following function:
> $$
> F(x) = \sum_{n = 0}^{\infty} x^n = \frac{1}{1 - x} = \sum_{n = 1}^{\infty} x^n - 1
> $$
>
> Take the derivative:
> $$
> F'(x) = \sum_{n = 1}^{\infty} n x^{n - 1} = -(1 - x)^{-2} = - \frac{1}{(1 - x)^2}
> $$
> Now, we find closed form for $a_n$:
> $$
> \begin{align*}
> 	A(x) &= \sum_{n \geq 0} a_n x^n \\
> 	a_n &= a_{n - 1} + n \\
> 	\sum_{n \geq 0} a_n x^n &= \sum_{n \geq 0} a_{n - 1} x^n + \sum_{n \geq 0} nx^n \\
> 	A(x) &= x \sum_{n \geq 0} a_{n} x^{n} + a_0 + x \sum_{n \geq 1} nx^{n - 1} \\
> 	A(x) &= x A(x) + 1 - \frac{x}{(1 - x)^2} \\
> 	A(x)[1 - x] &=  1 - \frac{x}{(1 - x)^2}\\
> 	A(x) &= \frac{1}{1 - x} - \frac{x}{(1 - x)^3}
> \end{align*}
> $$
> Now we find $a_n$ from the closed form OGF.
> $$
> \sum_{n \geq 0} a_n x^n = \frac{1}{1 - x} - \frac{x}{(1 - x)^3} = \sum_{n \geq 0} x^n
> $$
> 

We count the number of labeled trees on $n$ vertices with exactly $n$ vertices with exactly $t \geq 2$ leaves. First, if index $i$ is a leaf, how many times does it show up in the Prufer code? Answering this, it is easy to see that the converse is true as well.

Using the above and its converse, determine the number of labeled trees with exactly $t$ leaves by first choosing which indices of $n$ are leaves, and then relating the other indices with the Prufer code.

> If $i$ is a leaf, it does not show up in the Prufer code.
>
> Now we count the total number of labeled trees. We want to count the number of Prufer codes of length $n - 2$ where exactly $t$ elements of $[n]$ do not appear. In other words, we count the codes with exactly $n - t$ distinct indices:
>
> Consider $n - 2$ labeled balls (the code positions) and $n - t$ labeled bins (the indices):
> $$
> S(n - 2, n - t) (n - 2)!
> $$
> 



## final things.

- Nothing on Catalans and parking functions.
- OGF/EGF, told which one to use.
- Ramsey theory, 

## review questions.

Let $a_n = $ binary strings of length $n$ containing $3$ or more consecutive zeroes. Show that $a_n = a_{n - 1} + a_{n - 2} + a_{n-3} + 2^{n - 3}$​

> We can prove this with a counting argument.
>
> **LHS:** Defined to count $n$-length binary strings with $3+$ consecutive zeroes.
>
> **RHS:** 
>
> - Suppose we hold the last three digits to be zeroes. Regardless of what the first $n - 3$ digits are, we will have a valid string. There are $2^{n - 3}$ possible strings in this case.
> - Suppose we hold the last digit to be a $1$. The $3+$ consecutive zeroes must appear somewhere in the first $n - 1$ digits. There are $a_{n - 1}$ possible strings in this case.
> - Suppose we hold the last two digits to be $10$. The $3+$ consecutive zeroes must appear somewhere in the first $n - 2$ digits. There are $a_{n - 2}$ possible strings in this case.
> - Suppose we hold the last three digits to be $100$. The $3+$ consecutive zeroes must appear somewhere in the first $n - 3$ digits. There are $a_{n - 3}$ possible strings in this case.
> - Summing these cases, we find the expression $a_{n - 1} + a_{n - 2} + a_{n - 3} + 2^{n - 3}$.

Find the closed form **ogf** of the above recurrence:

>Let $a_0 = a_1 = a_2 = 0$ and $a_3 = 1$. 
>$$
>\begin{align*}
>	A(x) &= \sum_{n = 0}^{\infty} a_n x^n \\
>	a_{n} 
>		&= a_{n - 1} + a_{n - 2} + a_{n - 3} + 2^{n - 3} \\
>
>	A(x)
>		&= \sum_{n = 0}^{\infty}  a_{n - 1} x^n 
>		+ \sum_{n = 0}^{\infty} a_{n - 2}  x^n 
>		+ \sum_{n = 0}^{\infty} a_{n - 3}  x^n 
>		+ \sum_{n = 0}^{\infty} 2^{n - 3}  x^n \\
>
>   A(x)
>		&= a_0 + x A(x) 
>		+ a_0 + a_1 x + x^2 A(x) 
>		+ a_0 + a_1 x + a_2 x^2 + x^3 A(x) 
>		+ x^3 \frac{1}{1-2x} \\
>
>   A(x) &=x A(x) + x^2 A(x) + x^3 A(x) + \frac{x^3}{1 - 2x} \\
>   A(x) &= \frac{x^3}{(1 - 2x) (1 - x - x^2 - x^3)}
>\end{align*}
>$$

Suppose $n$ points are placed on a circle. For any $2$ points, draw a chord between them. Assume that no three of these chords intersect at one place.

**(a)** How many point of intersections lie in the circle?

>  Consider that we have one point of intersection for every four points on the circle, as two chords must intersect.
>
> As such, we get $\binom{n}{4}$ intersection points.

**(b)** If we treat intersection points as vertices, as well as the initial $n$ points, we get a planar graph. Count the number of faces in this planar graph, where the circle boundary itself connects vertices together as well.

> Clearly, $V = n + \binom{n}{4}$.
>
> We can use the total degree formula to find $E$. Consider the degree of each of the original $n$ points. They connect to $2$ points that lie adjacent on the circle, as well as $n - 1$ additional vertices). Each boundary point connects to $4$ vertices.
>
> As such, $\sum \deg = n(n - 1 + 2) + 4 \binom{n}{4} = n(n + 1) + 4 \binom{n}{4}$, double of $E$.
>
> Recall Euler's formula on planar graphs: $E - V + F = 2$.
>
> Solving for $F$,
> $$
> \begin{align*}
> 	F	&= 2 + V - E \\
>     	&= 2 + n + \binom{n}{4} - \frac{n(n + 1)}{2} - 2 \binom{n}{4} \\	
>     	&= 2 + n - \frac{n(n + 1)}{2} - \binom{n}{4}
> \end{align*}
> $$
