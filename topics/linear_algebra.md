# linear algebra.

## hello.

These notes are the product of me cramming for my **MATH2B** (Linear Algebra) course through De Anza College. They should cover most, if not all, topics of an introductory linear algebra course. 

I was not a big fan of the textbook/reading materials we used in class, so the structure of these notes is heavily guided by the 3Blue1Brown series, [Essence of linear algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab), as its visual-first approach transformed my own understanding of the subject. Where the series skims over technical/computational rigor, I refer to the online textbook, [Interactive Linear Algebra](https://textbooks.math.gatech.edu/ila/), by Dan Margalit and Joseph Rabinoff, to fill in those gaps. This textbook does really good justice to the visual understanding of the subject and has many interactive examples.

## vectors?

In **physics**, vectors are *arrows pointing in space*, defined by their direction and their length. This is the interpretation that I learned in my high school calculus, and physics classes.

In **computer science**: vectors are *ordered lists of numbers*. This interpretation is very useful for data analysis when you need to represent groups of different observations/features. The dimension of the vector is the length of the list, a 2D-vector would have two features in it.

More generally, however, **vectors** are any structure such that those structures interact with each other according to a set of axioms. This perspective seeks to generalize both the above interpretations and more. The form that vectors take doesn't matter! As long as they can be added and scaled according to these axioms.

The 8 **axioms** are as follows:
- $\vec{u} + (\vec{v} + \vec{w}) = (\vec{u} + \vec{v}) + \vec{w}$.
- $\vec{v} + \vec{w} = \vec{w} + \vec{v}$.
- There is a vector $\mathbb{0}$ such that $\mathbb{0} + \vec{v} = \vec{v}$ for all $\vec{v}$.
- For all $\vec{v}$, there exists $-\vec{v}$ such that $\vec{v} + (-\vec{v}) = \mathbb{0}$.
- $a(b\vec{v}) = (ab)\vec{v}$.
- $1\vec{v} = \vec{v}$.
- $a(\vec{v} + \vec{w}) = a\vec{v} + a\vec{w}$.
- $(a + b)\vec{v} = a\vec{v} + b\vec{v}$.

No need to memorize these or anything, but they provide a very good and naturally intuitive understanding for what defines a vector: the existence of **vector addition** and **scalar-vector** multiplication!

The term **scalar** refers to any "number." Why this term? Because if we look at what multiplying a number by a vector does visually (think of the physics perspective of a vector), it *scales* the vector by that number!

**Vector addition** is pretty straightforward:
$$
\begin{bmatrix}
a \\
b \\
c
\end{bmatrix}
+
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
=
\begin{bmatrix}
a + x \\
b+y \\
c+z
\end{bmatrix}
$$
**Scalar-vector multiplication** effectively *scales* each component of the vector:
$$
c
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
=
\begin{bmatrix}
c*x \\
c*y \\
c*z
\end{bmatrix}
$$
**Vector subtraction** is easier to think about when expressed as a combination of addition and scaling:
$$
\begin{bmatrix}
a \\
b \\
c
\end{bmatrix}
-
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
=
\begin{bmatrix}
a \\
b \\
c
\end{bmatrix}
+ (
-1
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
) =
\begin{bmatrix}
a \\
b \\
c
\end{bmatrix}
+
\begin{bmatrix}
-x \\
-y \\
-z
\end{bmatrix}
=
\begin{bmatrix}
a-x \\
b-y \\
c-z
\end{bmatrix}
$$

## subspaces, basis, and spans.

What we visually consider the $xy$-plane can be mathematically expressed as $\mathbb{R}^2$, the set of all possible pairs of two real numbers. Not all of our work will take place in $\mathbb{R}^2$, sometimes we want to focus on subsets of it. 

A **subspace** $V$ is a specific kind of subset in $\mathbb{R}^n$ where:

- The zero vector is in $V$.
- If $\vec{u}$ and $\vec{v}$ are in $V$, then $\vec{u} + \vec{v}$ is also in $V$.
  - Closure under vector addition.
- If $\vec{v}$ is in $V$ and $a$ is in $R$, then $a\vec{v}$ is also in $V$.
  - Closure under scalar multiplication.

We define our coordinate system in terms of basis vectors. In 2 dimensions, we have two basis vectors, one for each dimension. Every possible vector in this dimension, is internally written as some linear combination of the basis vectors. 

A **linear combination** is essentially some expression that involves vector addition and/or scalar-vector multiplication.

We most often use the following basis vectors, as they make representing other vectors very convenient (a number multiplied by $1$ is just itself): 
$$
\vec{i} = \begin{bmatrix} 1 \\ 0 \end{bmatrix} &
\vec{j} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}
$$
Thanks to the simplicity of our basis vectors, we can easily rewrite any vector (like the one below) as a linear combination of them. 
$$
\begin{align*}
\begin{bmatrix}
2 \\ 
3
\end{bmatrix} 
= 2
\begin{bmatrix}
1 \\
0
\end{bmatrix}
+ 3
\begin{bmatrix}
0 \\
1
\end{bmatrix}
= 2\vec{i} + 3\vec{j}
\end{align*}
$$
Let's flesh out our definition a bit: **basis vectors** are a set of vectors that can be linearly combined to form any possible vector that lies in our coordinate space. See how the expression $a\vec{i} + b\vec{j}$ can result in any possible vector in the 2d space, given the correct values of $a$ and $b$?

Now we introduce a new term, the span. The **span** of vectors $\vec{v}$ and $\vec{w}$ is the set of all of their linear combinations, i.e. the set containing $a\vec{v} + b\vec{w}$ where $a$ and $b$ both vary over all real numbers. 
$$
\operatorname{Span}\set{\vec{v_1}, \vec{v_2}, \dots, \vec{v_m}} = \set{c_1\vec{v_1}, c_2\vec{v_2}, \dots, c_m\vec{v_m} \mid c_1, c_2, \dots, c_m \in \mathbb{R}}
$$
Think about the similarities in our definitions of the **basis vectors** and **span**. 

Let's refine our definition again: a basis of a subspace $V$ is some set of vectors $\set{\vec{v_1}, \vec{v_2}, \dots, \vec{v_m}}$ such that $V = \operatorname{Span}\set{\vec{v_1}, \vec{v_2}, \dots, \vec{v_m}}$. Why does this make sense? Well, in order for some set of vectors to be a basis of a subspace, they must *span* the entire subspace. In other words, the set of their linear combinations must be equivalent to the subspace.

## introducing linear transformations!

A **transformation** is essentially a specific function that takes in a vector, and outputs a vector. Considering a transformation can take in and output an infinite number of vectors in a space, we can visualize a transformation as shifting the coordinate plane itself. This is well explained visually in the [3b1b video](https://www.youtube.com/watch?v=kYB8IZa5AuE&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=3&t=224s).

Transformations can often have chaotic and complex effects on the vectors they take in, which is why linear algebra focuses on a specific type that are easier to understand and represent mathematically: the **linear transformation.**

A **linear transformation** takes the following properties visually:

- Straight lines in the original plane remain straight in the transformed plane.
- The origin must remain fixed in place before and after the transformation.
- "Grid lines remain parallel and evenly spaced."

To represent a linear transformation numerically, we only need to record how the basis vectors, $\vec{i}$ and $\vec{j}$ change when transformed. This is because we can determine how any vector in the span of the basis will be transformed just from knowing what happens to the basis vectors!

Let's say we have some transformation that changes the basis vectors in the following manner:
$$
\vec{i}:
\begin{bmatrix}
1 \\ 
0
\end{bmatrix}
\rightarrow
\begin{bmatrix}
2 \\
3
\end{bmatrix}
&
\vec{j}:
\begin{bmatrix}
0 \\ 
1
\end{bmatrix}
\rightarrow
\begin{bmatrix}
4 \\
5
\end{bmatrix}
$$
How would the vector $\vec{u} = \begin{bmatrix}2 \\ 3\end{bmatrix}$ change under the transformation described above? 

Note that the linear combination of $\vec{u}$ in terms of $\vec{i}$ and $\vec{j}$ stays the same before and after the transformation. In other words, if $\vec{u} = a\vec{i} + b\vec{j}$, then $\vec{u}_{f} = a\vec{i}_{f} + b\vec{j}_{f}$. All we need to find are $a$ and $b$, which are pretty easy to find with our choice of basis vectors. (Also, the $f$ subscript here just refers to the transformed equivalents of those vectors).
$$
\vec{u} = \begin{bmatrix}2 \\ 3\end{bmatrix} = 2\begin{bmatrix}1 \\ 0\end{bmatrix} + 3\begin{bmatrix}0 \\ 1\end{bmatrix} = 2\vec{i} + 3\vec{j}
\\\\

\vec{u}_{f} = 2\vec{i}_{f} + 3\vec{j}_{f} 
= 2\begin{bmatrix}2 \\ 3\end{bmatrix} + 3\begin{bmatrix}4 \\ 5\end{bmatrix} = \begin{bmatrix}16 \\ 21\end{bmatrix}
$$
And there's our answer! From just the resulting transformed vectors of $\vec{i}$ and $\vec{j}$, we can find the output of the transformation of any vector in our space.

## matrices as linear transformations.



