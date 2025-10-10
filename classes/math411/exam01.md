# math411 / exam01

## 10.1: $\mathbb{R}^n$ and scalar products

Vector of length $n$ is in $\mathbb{R}^n$. 

- $u$ and $v$ are equal iff each component is equal.
- Can scale vectors by a constant.
- Adding vectors by adding components.
- $\mathbf{u} - \mathbf{v} = \mathbf{u} + (-\mathbf{v})$

**Scalar product** $\mathbf{u} \cdot \mathbf{v}$ is the sum of the products of each component.

The **norm** of a vector is defined as
$$
\|\mathbf{u}\| = \sqrt{\mathbf{u} \cdot \mathbf{u}} = \left|\sum_{i = 1}^{n} u_i^2 \right|.
$$
The distance function is $\text{dist}(\mathbf{u}, \mathbf{v}) = \|\mathbf{u} - \mathbf{v}\|$.

Two vectors are **orthogonal** if their scalar product is zero.

## 10.2: convergent sequences in $\mathbb{R}^n$

A sequence $\{\mathbf{u}_k\}$ *converges* to $\mathbf{u}$ if for each $\epsilon > 0$, there is an index $K$ such that
$$
\text{dist}(\mathbf{u}_k, \mathbf{u}) = \|\mathbf{u}_k - \mathbf{u}\| < \epsilon, \qquad \forall k \geq K.
$$
**Componentwise convergence theorem** says that $\{\mathbf{u}_k\}$ converges to $\mathbf{u}$ if and only each component sequence $p_i(\mathbf{u})$ converges to $\mathbf{u}_i$.

- If every component converges as desired, it is said the sequence converges *componentwise*. By the theorem, componentwise convergence implies convergence.

## 10.3: open and closed sets in $\mathbb{R}^n$

## 11.1: continuous functions and mappings

## 11.2: seq. compactness + other stuff.

## 11.3: pathwise connectedness + ivt

## 11.4: connectedness + ivp

