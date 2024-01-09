# linear algebra final cramming!

## Given vectors $u$ and $v$, find $u + v$, $u - v$, $\text{span}\set{u, v}$, and $\text{proj}_u(v)$.

1. [Vector Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/vector-calculator/)
2. Determine if a vector is in $\text{span}\set{u, v}$ by writing a linear combination equation and solving with row reduction.
   1. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)
3. $\text{proj}_u(v) = \frac{u \cdot v}{|u|} u$ or the "projection of $v$ onto $u$".
   1. [Vector Projection Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/vector-projection-calculator/)
4. Vector component of $u$ orthogonal to $v$.
   1. $v - \text{proj}_u(v) = \frac{u \cdot v}{|u|} u$.

## Given vectors, find an orthogonal basis for the vectors.

1. Don't exactly know what this is asking but...
2. To check if a set of vectors is orthogonal, check if the dot products of all the vectors with each other are $0$.
3. To check if a matrix is orthogonal, check if the dot products of all the columns with each other are $0$.
4. Find an orthogonal basis.
   1. *"Orthogonal vectors are those that are at right angles to each other, meaning that their dot product is zero. Orthonormal vectors, on the other hand, not only have to be orthogonal but also have to have a length of one. This means that each vector in an orthonormal set is a unit vector."*
   2. We can use the Gram-Schmidt process to do this.
   3. [Gram-Schmidt Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/gram-schmidt-calculator/)

## Given a matrix $A$, find the eigenvectors and eigenvalues of $A$.

1. [Eigenvalues and Eigenvectors Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/eigenvalue-and-eigenvector-calculator/)

## Given a matrix $A$, find matrices $P$ and $D$ such that $A = PDP^{-1}$.

1. [Diagonalize Matrix Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/diagonalize-matrix-calculator/)

1. Solve the system of equations with row reduction and parameterize the solution set.
   1. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)
   2. To parameterize, write all the basic variables in terms of the free variables.
   3. Really easy! Just watch your arithmetic!
   4. [System of Equations Calculator](https://matrixcalc.org/slu.html)

## Write the system as $Ax = b$ and review all solutions.

1. Just convert the system of equations to matrix and reduce?
2. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)

## Given a matrix $A$, compute $\det A$.

1. [Determinant Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-determinant-calculator/)

## Given a matrix $A$, find a basis for $\text{col}A$ and $\text{nul} A$. Find the rank of $A$ and $\dim \text{nul} A$.

1. The basis of the column space is the span of its **pivot columns**.
   1. [Column Space Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/column-space-calculator/)
   2. First, row reduce the matrix.
      1. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)
   3. Determine each pivot column from the reduced matrix.
   4. The **basis of the column space** is the set of all pivot columns in the initial matrix.
2. The **null space** is the set of all vectors $x$ such that $Ax = 0$.
   1. The nullity of $A$ is just $\dim \text{nul} A$.
   2. [Null Space Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/null-space-calculator/)
3. The **rank** of a matrix is the dimension of its image.
   1. It's the number of columns that contain a pivot.

## Given a matrix $A$, find the eigenvectors and eigenvalues of $A$.

1. [Eigenvalues and Eigenvectors Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/eigenvalue-and-eigenvector-calculator/)

## Given a matrix $A$, compute $\det A$.

1. [Determinant Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-determinant-calculator/)

## Given a matrix $A$, determine whether the columns of $A$ are linearly independent or dependent. If it is dependent, find a dependence relation.

1. Set $A$ equal to the zero vector and row reduce.
   1. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)
2. If there's a row of all zeroes, it means that $A$ is linearly dependent.
3. To find a dependence relation, write each row as an equation and solve for the basic variables in terms of the free variables. 
   1. The coefficient on the free variable is the weight of that column in the dependence relation.

## Given a square matrix $A$, find the inverse of $A$, or $A^{-1}$.

1. [Matrix Inverse Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/inverse-of-matrix-calculator/)

## Possible linear transformation questions.
1. Find $T(u)$, given transformation matrix $A$ and vector $u$.
   1. They will give $T(x) = Ax$, where $A$ is a matrix.
   2. Perform matrix-vector multiplication to find $Au$, which is your answer.
      1. [Matrix Multiplication Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-multiplication-calculator/)
2. Find vector $u$, given transformation matrix $A$ and $T(u)$.
   1. Basically you know that $Au = T(u)$.
   2. Convert to an augmented matrix and row reduce.
      1. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)
3. Find $T(c)$ given vectors $a$, $b$, and $c$, as well as images $T(a)$ and $T(b)$.
   1. Basically you know that whatever combination of $x_1a + x_2b$ gets you $c$, that same $x_1T(a) + x_2T(b)$ will get you $T(c)$.
   2. This is due to the linearity of $T$.

## Given a linear transformation $T: \mathbb{R}^m \rightarrow \mathbb{R}^n$, determine whether it is one-to-one, onto, or an isomorphism.

1. Row reduce the transformation matrix $A$.
   1. [Row Reduction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/reduced-row-echelon-form-rref-calculator/)
2. If $A$ has a pivot in every column, it is **one-to-one**.
3. If $A$ has a pivot in every row, it is **onto**.

## Let $B = \set{ \vec{b_1}, \dots, \vec{b_n} }$ be a basis for $\mathbb{R}^n$. Find the B-coordinates of vector $u$.

1. Know that $\vec{u}_B$ = $P_{B \leftarrow S} \cdot \vec{u} = P_{S \leftarrow B}^{-1} \cdot \vec{u}$.
2. $P_{B \leftarrow S}$ is the matrix that transforms the standard basis into the basis $B$.
3. We know the matrix $P_{S \leftarrow B}$ that transforms basis $B$ to the standard basis. It is the matrix with basis $B$'s vectors as columns. 
4. We can take the inverse of it, and multiply by vector $u$.
   1. [Matrix Inverse Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/inverse-of-matrix-calculator/)
   2. [Matrix Multiplication Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-multiplication-calculator/)

## Review theorems and axioms of square matrices.

1. **No idea what this means.** Good luck!

1. 


## Let $A$ and $B$ be matrices of some dimensions. Calculate $A + B$, $A - B$, $A*B$, and $B*A$, if possible.

1. [Matrix Addition Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-addition-calculator/)
2. [Matrix Subtraction Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-subtraction-calculator/)
3. [Matrix Multiplication Calculator](https://www.emathhelp.net/en/calculators/linear-algebra/matrix-multiplication-calculator/)