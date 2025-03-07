# math410; quiz02

## Things to know

A **sequence** is a real-valued function whose domain is the natural numbers $\mathbb{N}$.

A sequence ${a_n}$ is said to **converge** to $L$ if, for all $\epsilon > 0$, there exists a minimum index $N \in \mathbb{N}$ such that $\forall n \geq N$,
$$
|a_n - L| < \epsilon.
$$
The **Comparison Lemma** states that if ${a_n} \rightarrow a$, then ${b_n} \rightarrow b$ if there exists a $C \geq 0$ and index $N_1$ such that
$$
|b_n - b| \leq C |a_n - a| \qquad \forall n \geq N_1.
$$
A sequence is **bounded** if there exists some non-negative $M$ such that
$$
|a_n| \leq M \qquad \forall n.
$$
- Every convergent sequence is bounded. Logically!

A sequence $\set{x_n}$ is *in the set* $S$ if for all $n \in \mathbb{N}$, $x_n \in S$.

A set $S$ is dense in $\mathbb{R}$ if and only if every number $x$ is the limit of a sequence in $S$.

A set $S$ is **closed** if every convergent sequence in $S$ has a limit in $S$.

