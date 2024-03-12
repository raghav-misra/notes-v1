# math401 / exam01

## topics.

1. Linear algebra review.
2. Leontief input-output models.
3. Computer graphics.
4. Least squares.
5. Curve fitting.
6. Markov chains.

## linear algebra review.

### determinant?

Well, first know how to calculate for a 2x2 matrix. Take the following:
$$
A = \begin{bmatrix}a & b \\ c & d\end{bmatrix}
$$
The determinant of $A$ can be expressed as:
$$
\det A = ad - bc
$$
We can use this as a building block to find the determinants of larger matrices. For each number in the first row, we find the determinant of the "submatrix" that excludes the current row and column, and multiply it by the current element. Also, alternate adding and subtracting these terms. That's a lot, but:
$$
\det \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i \end{bmatrix} = 
a \begin{bmatrix}e & f \\ h & i \end{bmatrix}
- b \begin{bmatrix}d & f \\ g & i\end{bmatrix}
+ c \begin{bmatrix}d & e \\ g & h\end{bmatrix}
$$
In this case, our "submatrices" are all 2x2, where we apply the first formula. But if the are larger, we recursively apply this "cofactor expansion" until we can make 2x2 matrices.



### inverse?

The inverse of a matrix $A$, written $A^{-1}$, is the matrix such that:
$$
AA^{-1} = A^{-1}A = I
$$
Consider the following matrix product:
$$
\begin{bmatrix}5 & 7 \\ 2 & 3\end{bmatrix}
\begin{bmatrix}3 & 7 \\ -2 & 5\end{bmatrix} =
\begin{bmatrix}1 & 0 \\ 0 & 1\end{bmatrix}
$$
Therefore, the two matrices are inverses of each other.

We can find the inverse of a 2x2 matrix pretty easily. 
$$
\begin{bmatrix}a & b \\ c & d\end{bmatrix}^{-1} = 
\frac{1}{ad - bc} \begin{bmatrix}d & -b \\ -c & a\end{bmatrix} =
\frac{1}{\det A} \begin{bmatrix}d & -b \\ -c & a\end{bmatrix}
$$

### linear independence?

A matrix is **linearly independent** if none of the columns can be written as linear combinations of any other columns. 

## leontief i/o models.

### content.

The economic model equation itself is:
$$
\vec{p} = M\vec{p} + \vec{d}
$$
In the above, $\vec{p}$ represents total production, $\vec{d}$ represents the external demand, and $M\vec{p}$ represents internal demand. The **consumption matrix** $M$ scales total production to determine internal demand. 

When $\vec{d} = 0$, we consider the economy to be **closed**. However, when $\vec{d} \neq \vec{0}$​, we are in an **open economy**.

Basically, we can mess with the model equation to find cool and interesting things. For example, we can solve for $\vec{p}$ given $M$ and a certain external demand $\vec{d}$:
$$
\begin{align*}
\vec{p} &= M\vec{p} + \vec{d} \\
\vec{p} - M\vec{p} &= \vec{d} \\
\vec{p}(I-M) &= \vec{d} \\
\vec{p} &= (I-M)^{-1} \vec{d}
\end{align*}
$$
As seen above, the matrix $(I - M)^{-1}$ is significant. It shows us how much we need to scale external demand by to determine total product. $(I - M)^{-1}_{ij}$ tells us the amount of additional $i$ that must be produced to accomodate a +1 increase in $j$​ production.

Finding these change coefficients is very useful. We can use adjugate method to determine entries in an inverse of $I - M$:
$$
(I - M)^{-1}_{ij} = \frac{(-1)^{i + j} \det (I - M)_{ji}}{\det (I - M)}
$$

### practice.

Suppose we know the following about a consumption matrix $M$:
$$
\begin{align*}
    M = \begin{bmatrix}
    0.1000 & 0.1500 & 0.0500 \\
    0.1200 & 0 & 0.0200 \\
    0.0600 & 0.0400 & 0
    \end{bmatrix} &&
    (I - M)^{-1} = \begin{bmatrix}
    1.1382 & 0.1731 & 0.0604 \\
    0.1381 & 1.0218 & 0.0273 \\
    0.0738 & 0.0513 & \alpha
    \end{bmatrix}
\end{align*}	
$$
**Question:** Write down the meaning of $0.0600$ in $M$.

The scenario has three products. In this case, it would take $0.0600$​ units of some Product 3 to produce one unit of some Product 1.

**Question:** Write down the meaning of $0.0738$ in $(I - M)^{-1}$.

If demand for Product 1 changes by +1, then production of Product 3 must change by $0.0738$ to meet the new requirements.

**Question:** Write down the value of $\alpha$​ using the adjugate method.

$\alpha$ is basically just $(I - M)^{-1}_{3,3}$. So $i = 3, j = 3$.

Let's use the adjugate method:
$$
\alpha = \frac{(-1)^{3 + 3} \det(I-M)_{3,3}}{\det(I - M)} 
=\frac{\det \begin{bmatrix}0.9000 & -0.1500 \\ -0.1200 & 1\end{bmatrix}}{\det \begin{bmatrix}  0.9000 & -0.1500 & -0.0500 \\ -0.1200 & 1 & -0.0200 \\ -0.0600 & -0.0400 & 1\end{bmatrix}}
$$

## computer graphics.

### content.

Translate by $(a, b)$ in 2D.
$$
T(a, b) = \begin{bmatrix}
1 & 0 & a \\
0 & 1 & b \\
0 & 0 & 1
\end{bmatrix}
$$
Rotate a point $\theta$ clockwise in 2D:
$$
R(\theta) = \begin{bmatrix} 
\cos \theta & -\sin \theta & 0 \\ 
\sin \theta & \cos \theta & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
Translate a point by $(a, b, c)$ in 3D.
$$
T(a, b, c) = \begin{bmatrix}
1 & 0 & 0 & a \\
0 & 1 & 0 & b \\
0 & 0 & 1 & c \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
Rotate a point $\theta$ around the $z$-axis in 3D:
$$
RZ(\theta) = \begin{bmatrix}
\cos \theta & -\sin \theta & 0 & 0 \\
\sin \theta & \cos \theta & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
Rotate a point $\theta$ around the $x$-axis in 3D:
$$
RX(\theta) = \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & \cos \theta & -\sin \theta & 0 \\
0 & \sin \theta & \cos \theta & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
Rotate a point $\theta$ around the $y$-axis in 3D:
$$
RY(\theta) = \begin{bmatrix}
\cos \theta & 0 & \sin \theta & 0 \\
0 & 1 & 0 & 0 \\
- \sin \theta & 0 & \cos \theta & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
Perspective projection matrix given $d$:
$$
P(d) = \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & -\frac{1}{d} & 1
\end{bmatrix}
$$

### practice.

Write out the matrix product for the following transformations.

**Question:** Rotate by $\pi/5$ counterclockwise about the point $(-1, 5)$:

First we shift $(-1, 5)$ to the origin. Then we rotate by $\pi/5$. Then we move our origin back to $(-1, 5)$.
$$
T(1, -5) R(\frac{\pi}{5})T(-1, 5) = \begin{bmatrix}
1 & 0 & 1 \\
0 & 1 & -5 \\
0 & 0 & 1
\end{bmatrix} \begin{bmatrix}
\cos \frac{\pi}{5} & - \sin \frac{\pi}{5} & 0 \\
\sin \frac{\pi}{5} & \cos \frac{\pi}{5} & 0 \\
0 & 0 & 1
\end{bmatrix} \begin{bmatrix}
1 & 0 & -1 \\
0 & 1 & 5 \\
0 & 0 & 1
\end{bmatrix} 
$$
**Question:** Reflect across the line $y = x + 3$:

First we shift $x = 3$ down to the $x$-axis. Then we reflect across $y = x$. Then we shift the $x$-axis back up to $x = 3$.
$$
T(3, 0)(\text{reflect matrix})T(-3, 0) = \begin{bmatrix}
1 & 0 & -3 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix} \begin{bmatrix}
0 & 1 & 0 \\
1 & 0 & 0 \\
0 & 0 & 1
\end{bmatrix} \begin{bmatrix}
1 & 0 & 3 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

## least squares/curve fitting.

### content.

The idea is that we want to determine coefficients to most closely fit a set of inputs to outputs.

Say we wanted to fit the equation:
$$
y = ax^2 + bx + c
$$
For each term on the right-hand-side, we calculate the value that the coefficient is being multiplied by so that we can approximate the coefficient itself. This values would be $f_a(x) = x^2$ for $a$, $f_b(x) = x$ for $b$ and $f_c(x) = 1$ for $c$. 

Calculate all these values and build a matrix equation from it. Say we have the pairs of data $(x_1, y_1), ... (x_n, y_n)$:
$$
\begin{bmatrix}
f_a(x_1) & f_b(x_1) & f_c(x_1) \\
f_a(x_2) & f_b(x_2) & f_c(x_2) \\
... & ... & ... \\
f_a(x_n) & f_b(x_n) & f_c(x_n)
\end{bmatrix} \begin{bmatrix}
a \\ b \\ c
\end{bmatrix} = \begin{bmatrix}
y_1 \\
y_2 \\
... \\ 
y_n
\end{bmatrix}
$$
If this equation was solvable as-is, we would be good to go, i.e. all the points perfectly line up on a specific $y = af_a(x) + bf_b(x) + cf_c(x)$. However, the idea of least-squares is to find an approximation, oftentimes for messy data. So the above matrix equation very well may be unsolvable.

To make the equation solvable, we multiply both sides of the equation by $A^T$, where $A$ is the matrix of transformed $x$-values. The above equation would become:
$$
\begin{align*}
\begin{bmatrix}
f_a(x_1) & f_b(x_1) & f_c(x_1) \\
f_a(x_2) & f_b(x_2) & f_c(x_2) \\
... & ... & ... \\
f_a(x_n) & f_b(x_n) & f_c(x_n)
\end{bmatrix}^{T} & \begin{bmatrix}
f_a(x_1) & f_b(x_1) & f_c(x_1) \\
f_a(x_2) & f_b(x_2) & f_c(x_2) \\
... & ... & ... \\
f_a(x_n) & f_b(x_n) & f_c(x_n)
\end{bmatrix}  \begin{bmatrix}
a \\ b \\ c
\end{bmatrix} \\
&= \begin{bmatrix}
f_a(x_1) & f_b(x_1) & f_c(x_1) \\
f_a(x_2) & f_b(x_2) & f_c(x_2) \\
... & ... & ... \\
f_a(x_n) & f_b(x_n) & f_c(x_n)
\end{bmatrix}^{T} \begin{bmatrix}
y_1 \\
y_2 \\
... \\ 
y_n
\end{bmatrix}
\end{align*}
$$
Solving the above equation, we find our constant approximations for $a$, $b$, and $c$, and we can plug that back into our original curve to find the best fit.

Least-squares is cool because we can just as easily use it to find an output variable from two (or more) inputs! Let's say we wanted to fit some points to the curve:
$$
z = ax^2 + bxy + cy^2 + d
$$
Then we could find $x^2$, $xy$, $y^2$, and $1$ as our functions for each data point, and throw that into the matrix equation as in the previous example. The rest stays the same, and we will find approximations for $a$, $b$, $c$, and $d$.

Least-squares **fails** when one of the $f_a, f_b, ...$ term functions can't be calculated using just the input variables. For example, 
$$
y = ax + \sin (bx)
$$
We can't calculate $\sin (bx)$ without knowing $b$, and as such there isn't a way to express this term as $b \cdot f_b(x)$​. If you don't do that, least-squares is pretty fire.

Least-squares, when successful, will have at least one solution. For the system to have exactly **one** solution, the columns of the matrix must be li

### practice.

**Question:** Give an example of a matrix equation $A\vec{x} = b$ which does not have a solution, for which the least-squares solution would be unique.

Maybe something like:
$$
\begin{bmatrix}
1 & 1 \\
3 & 1 \\
\end{bmatrix} \begin{bmatrix}
a \\ b
\end{bmatrix} = \begin{bmatrix}
4 \\ 8
\end{bmatrix}
$$
Because it has linearly independent columns.

**Question:** Which of the following functions could be calculated using least-squares?

1. $f(x) = ax^2 + b\sqrt{x} + c$ **(YES)**
2. $f(x) = \sqrt{x + a} + bx + c$ **(NO)**
3. $f(x) = a \sin x + b \cos x$ **(YES)**
4. $f(x) = \sin (ax) + \cos (bx)$ **(NO)**

## markov chains.

### content.

A **transition matrix** shows how some data will change to its next state. The **steady state** is the state that the data approaches as the transition matrix is applied repeatedly.

Each entry $T_{ij}$ of the transition matrix represents how the data changes from a state $j$ to state $i$ of the Markov chain. Each column of $T$ is a **probability vector**, meaning all their values sum up to $1$.

### practice.

**Question:** Give an example of a 3x3 non-regular transition matrix which has 7 nonzero entries.
$$
\begin{bmatrix}
0.1 & 0.4 & 0.3 \\
0 & 0.6 & 0.4 \\
0.9 & 0 & 0.3
\end{bmatrix}
$$
**Question:** There is a visual representation of Markov chain in Fall 2018 exam. Find the $(4, 1)$ entry of the transition matrix.

We want to find the "percent of data leaving state 4 for state 1" in a given transition. This is zero, as there is no arrow from 4 to 1.

