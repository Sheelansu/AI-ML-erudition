# Essence of Linear Algebra, Chapter 14: Eigenvectors and Eigenvalues

**Video:** [Eigenvectors and Eigenvalues | 3Blue1Brown](https://www.youtube.com/watch?v=PFDu9oVAE-g)  
**Series:** Essence of Linear Algebra  
**Main question:** Are there special directions that a linear transformation stretches or shrinks without turning them away from their original line?

---

## 1. The Big Idea: Some Directions Are Special

Imagine applying a linear transformation to every vector in a 2D plane.

Some vectors might be:
- Rotated.
- Stretched.
- Shrunk.
- Flipped.
- Sheared into different directions.

Usually, the output vector points in a different direction from the input.

But some vectors have a special property: **after the transformation, they still lie along the same line as before.**

They may become longer, shorter, or point in the opposite direction, but they do not leave their original line.

These special vectors are called **eigenvectors**.

The number describing how much such a vector is scaled is its **eigenvalue**.

### The fundamental equation

```text
A*v = lambda*v
```

Where:

- `A` is a square matrix representing a linear transformation.
- `v` is a nonzero eigenvector.
- `lambda` is the corresponding eigenvalue.
- `A*v` is the result of applying the transformation.
- `lambda*v` is the original vector scaled by a number.

Both sides describe the same resulting vector.

The equation says that applying the transformation to `v` has exactly the same effect as multiplying `v` by the scalar `lambda`.

### What can the eigenvalue tell us?

| Eigenvalue | Effect on the eigenvector |
|---|---|
| `lambda > 1` | Stretched, without changing its direction |
| `0 < lambda < 1` | Shrunk, without changing its direction |
| `lambda = 1` | Remains unchanged |
| `lambda < -1` | Flipped and stretched |
| `-1 < lambda < 0` | Flipped and shrunk |
| `lambda = -1` | Flipped without changing its length |
| `lambda = 0` | Mapped to the zero vector, so it cannot be an eigenvector |

The last row deserves special attention. By definition, an eigenvector must be nonzero. If a transformation maps a nonzero vector to zero, the eigenvalue is zero, but that vector is not an eigenvector under the usual definition.

---

## 2. A Concrete Example

Consider this matrix:

```text
A = [3  1]
    [0  2]
```

Let's investigate how it transforms vectors.

For any vector:

```text
v = [x]
    [y]
```

the transformed vector is:

```text
A*v = [3x + y]
      [2y]
```

Most choices of `x` and `y` will produce a vector pointing in a different direction.

But some vectors behave differently.

### Example A: A vector along the x-axis

Take:

```text
v = [1]
    [0]
```

Apply the matrix:

```text
A*v = [3  1] * [1]
      [0  2]   [0]
```

The result is:

```text
A*v = [3]
      [0]
```

Therefore:

```text
A*v = 3*v
```

The vector remains on the x-axis and is stretched by a factor of 3.

So:

```text
Eigenvector: [1, 0]

Eigenvalue: 3
```

Any nonzero vector along the x-axis is also an eigenvector with eigenvalue 3.

For example, `[5, 0]` is another such eigenvector.

### Example B: A vector along a diagonal line

Now try:

```text
v = [ 1]
    [-1]
```

Apply the matrix:

```text
A*v = [3  1] * [ 1]
      [0  2]   [-1]
```

Calculate:

```text
A*v = [3 - 1]
      [0 - 2]
```

Therefore:

```text
A*v = [ 2]
      [-2]
```

Which means:

```text
A*v = 2*v
```

The vector stays on its original line and is stretched by a factor of 2.

Thus:

```text
Eigenvector: [1, -1]

Eigenvalue: 2
```

Any nonzero scalar multiple of `[1, -1]` is also an eigenvector with eigenvalue 2.

### What did we discover?

For this matrix, there are two independent eigenvector directions:

- The x-axis, with eigenvalue 3.
- The line `y = -x`, with eigenvalue 2.

Most other vectors are turned away from their original directions, but vectors along these two lines retain their respective directions.

That is the geometric intuition behind eigenvectors.

---

## 3. Eigenvectors Are About Lines, Not Individual Arrows

Suppose `v` is an eigenvector:

```text
A*v = lambda*v
```

Now multiply the vector by a nonzero scalar `c`.

The new vector is:

```text
u = c*v
```

Apply the transformation:

```text
A*u = A*(c*v)
```

By linearity:

```text
A*u = c*(A*v)
```

Substitute the eigenvector equation:

```text
A*u = c*(lambda*v)
```

Rearrange:

```text
A*u = lambda*(c*v)
```

Since `u = c*v`:

```text
A*u = lambda*u
```

Therefore, `u` is also an eigenvector with the same eigenvalue.

**Every nonzero vector along an eigenvector's line is an eigenvector with the same eigenvalue.**

This is why eigenvectors are best understood geometrically as special directions or lines.

Strictly speaking, an eigenvector is a particular nonzero vector, while the collection of all eigenvectors associated with a given eigenvalue, together with the zero vector, forms its eigenspace.

---

## 4. Why Do Eigenvalues Matter?

Eigenvectors reveal directions in which a transformation behaves particularly simply.

Imagine a transformation that stretches one direction by 3 and another direction by 2.

If you choose those two directions as your basis, then the transformation can be described using a diagonal matrix:

```text
D = [3  0]
    [0  2]
```

Applying this matrix is easy:

```text
D * [x] = [3x]
    [y]   [2y]
```

Each coordinate is simply scaled independently.

There are no extra terms mixing the two coordinates.

This is the key connection to the previous chapter, **Change of Basis**.

If a transformation has enough linearly independent eigenvectors to form a basis, we can express it in that eigenvector basis. The matrix then becomes diagonal.

This process is called **diagonalization**.

It is not always possible, but when it is, many calculations become much simpler.

---

## 5. Finding Eigenvalues Mathematically

So far, we have found eigenvectors by inspecting the geometry.

But how do we find them systematically for an arbitrary matrix?

Start with the defining equation:

```text
A*v = lambda*v
```

Move everything to one side:

```text
A*v - lambda*v = 0
```

The scalar `lambda` can be written as multiplication by the identity matrix:

```text
lambda*v = lambda*I*v
```

Therefore:

```text
A*v - lambda*I*v = 0
```

Factor out the vector:

```text
(A - lambda*I)*v = 0
```

This is the key equation for finding eigenvectors and eigenvalues.

### Why does the identity matrix appear?

The identity matrix does not change a vector:

```text
I*v = v
```

Therefore:

```text
lambda*I*v = lambda*v
```

Using the identity matrix lets us subtract a scalar from a matrix in a mathematically meaningful way.

For example:

```text
A = [3  1]
    [0  2]
```

Then:

```text
A - lambda*I = [3-lambda       1]
               [0              2-lambda]
```

Notice that `lambda` is subtracted from the diagonal entries.

This operation is called shifting the matrix by `lambda*I`.

---

## 6. The Determinant Reveals the Eigenvalues

Recall the equation:

```text
(A - lambda*I)*v = 0
```

We want a **nonzero** solution for `v`.

From our earlier chapters, we know that a homogeneous system:

```text
M*v = 0
```

has a nonzero solution only when `M` is singular, meaning it is not invertible.

For a square matrix, this happens precisely when its determinant is zero.

Therefore, for an eigenvalue:

```text
det(A - lambda*I) = 0
```

This is the **characteristic equation**.

The expression:

```text
det(A - lambda*I)
```

is a polynomial in `lambda`, called the **characteristic polynomial**.

The roots of that polynomial are the eigenvalues.

### Why this is a powerful connection

We have now connected several earlier concepts:

- Matrix multiplication.
- Homogeneous linear systems.
- Invertibility.
- Determinants.
- Eigenvalues.

The determinant is not an arbitrary trick for finding eigenvalues. It tells us when the shifted transformation collapses at least one direction to zero, allowing a nonzero vector to satisfy the eigenvector equation.

---

## 7. Worked Example: Find the Eigenvalues

Consider:

```text
A = [3  1]
    [0  2]
```

### Step 1: Subtract `lambda*I`

```text
A - lambda*I = [3-lambda       1]
               [0              2-lambda]
```

### Step 2: Calculate the determinant

For a 2×2 matrix:

```text
M = [a  b]
    [c  d]
```

the determinant is:

```text
det(M) = a*d - b*c
```

Therefore:

```text
det(A - lambda*I) = (3-lambda)*(2-lambda) - (1*0)
```

Simplify:

```text
det(A - lambda*I) = (3-lambda)*(2-lambda)
```

### Step 3: Set the determinant equal to zero

```text
(3-lambda)*(2-lambda) = 0
```

Thus:

```text
lambda = 3

lambda = 2
```

The eigenvalues are 3 and 2.

Notice that these are exactly the scaling factors we discovered geometrically.

The algebra confirms our visual understanding.

---

## 8. Finding the Eigenvectors

Finding eigenvalues is only half the process.

Once we know an eigenvalue, we substitute it into:

```text
(A - lambda*I)*v = 0
```

and solve for the nonzero vectors `v`.

### Find the eigenvector for `lambda = 3`

Our matrix is:

```text
A = [3  1]
    [0  2]
```

Subtract `3*I`:

```text
A - 3*I = [0  1]
          [0 -1]
```

Let:

```text
v = [x]
    [y]
```

Solve:

```text
[0  1] * [x] = [0]
[0 -1]   [y]   [0]
```

The equations reduce to:

```text
y = 0
```

There is no restriction on `x`, except that the eigenvector must not be zero.

Therefore:

```text
v = [x]
    [0]
```

where `x` can be any nonzero number.

The eigenspace is the x-axis.

One convenient eigenvector is:

```text
v = [1]
    [0]
```

### Find the eigenvector for `lambda = 2`

Subtract `2*I`:

```text
A - 2*I = [1  1]
          [0  0]
```

Solve:

```text
[1  1] * [x] = [0]
[0  0]   [y]   [0]
```

The nontrivial equation is:

```text
x + y = 0
```

Therefore:

```text
y = -x
```

The eigenvectors have the form:

```text
v = [ x]
    [-x]
```

where `x` is nonzero.

One convenient eigenvector is:

```text
v = [ 1]
    [-1]
```

The eigenspace is the line `y = -x`.

### General recipe

For a square matrix `A`:

1. Calculate `det(A - lambda*I)`.
2. Set it equal to zero.
3. Solve for the eigenvalues.
4. Substitute each eigenvalue into `(A - lambda*I)*v = 0`.
5. Solve for the corresponding nonzero eigenvectors.

---

## 9. Not Every Transformation Has Real Eigenvectors

Consider a rotation by 90 degrees counterclockwise.

Its matrix is:

```text
R = [0 -1]
    [1  0]
```

Every nonzero real vector is rotated by 90 degrees.

No such vector remains on its original line after the transformation.

Therefore, this transformation has no real eigenvectors.

Let's confirm algebraically.

### Step 1: Construct the characteristic equation

```text
R - lambda*I = [-lambda  -1]
               [1       -lambda]
```

Calculate the determinant:

```text
det(R - lambda*I) = (-lambda)*(-lambda) - (-1*1)
```

Simplify:

```text
det(R - lambda*I) = lambda^2 + 1
```

Set it equal to zero:

```text
lambda^2 + 1 = 0
```

So:

```text
lambda^2 = -1
```

The solutions are:

```text
lambda = i

lambda = -i
```

These are complex eigenvalues, not real eigenvalues.

### What does this mean?

The 90-degree rotation has no real eigenvectors, but it does have complex eigenvalues and complex eigenvectors when we extend the vector space to complex numbers.

For ordinary real 2D geometry, the transformation has no nonzero vector that remains on its original line.

This illustrates an important point:

**A real matrix does not necessarily have real eigenvalues or real eigenvectors.**

However, every square matrix over the complex numbers has at least one complex eigenvalue.

---

## 10. Negative Eigenvalues: Flipping Directions

An eigenvalue can be negative.

For example:

```text
A = [-2  0]
    [ 0  3]
```

Consider the vector:

```text
v = [1]
    [0]
```

Applying the matrix:

```text
A*v = [-2]
      [ 0]
```

Therefore:

```text
A*v = -2*v
```

The vector flips direction and doubles in length.

The eigenvalue is `-2`.

Now consider:

```text
u = [0]
    [1]
```

Applying the matrix:

```text
A*u = [0]
      [3]
```

Thus:

```text
A*u = 3*u
```

This vector is stretched by a factor of 3 without changing its direction.

The eigenvalue is 3.

### Why this matters

Eigenvalues do not merely describe the magnitude of a scaling.

Their signs tell us whether the eigenvector's direction is preserved or reversed.

In a diagonal matrix, negative diagonal entries correspond to flips along their respective coordinate axes.

---

## 11. A Shear: Only One Eigenvector Direction

Consider this shear transformation:

```text
A = [1  1]
    [0  1]
```

Its effect on a vector is:

```text
A * [x] = [x+y]
    [y]   [y]
```

The x-axis remains fixed.

For example:

```text
A * [1] = [1]
    [0]   [0]
```

Every nonzero vector along the x-axis has eigenvalue 1.

Are there other eigenvector directions?

Let's find out.

### Step 1: Find the eigenvalues

```text
A - lambda*I = [1-lambda  1]
               [0        1-lambda]
```

Its determinant is:

```text
det(A - lambda*I) = (1-lambda)^2
```

Set it equal to zero:

```text
(1-lambda)^2 = 0
```

Therefore:

```text
lambda = 1
```

The only eigenvalue is 1, with algebraic multiplicity 2.

### Step 2: Find its eigenvectors

Substitute `lambda = 1`:

```text
A - I = [0  1]
        [0  0]
```

Solve:

```text
[0  1] * [x] = [0]
[0  0]   [y]   [0]
```

This gives:

```text
y = 0
```

Therefore, the eigenvectors lie along the x-axis.

The matrix has only one independent eigenvector direction.

### Why is this interesting?

A 2D matrix needs two linearly independent eigenvectors to form an eigenbasis.

This shear has only one independent eigenvector direction, so it cannot be diagonalized.

The eigenvalue appears twice in the characteristic polynomial, but there is only one independent eigenvector direction.

This distinction becomes important when studying algebraic and geometric multiplicity.

---

## 12. A Special Case: Every Direction Is an Eigenvector

Consider a transformation that doubles every vector:

```text
A = [2  0]
    [0  2]
```

For any vector:

```text
v = [x]
    [y]
```

we have:

```text
A*v = [2x]
      [2y]
```

Therefore:

```text
A*v = 2*v
```

Every nonzero vector is an eigenvector with eigenvalue 2.

This is because the transformation uniformly scales the entire plane.

There is no preferred direction. Every direction behaves identically.

The matrix is already diagonal, and its eigenspace for eigenvalue 2 is the entire 2D space.

This example shows that the number of distinct eigenvalues does not determine the number of eigenvectors.

A matrix with just one eigenvalue can have many independent eigenvectors.

---

## 13. Eigenbasis and Diagonalization

Now connect everything to Chapter 13, Change of Basis.

Suppose a matrix `A` has enough linearly independent eigenvectors to form a basis.

Let the eigenvectors be:

```text
v1, v2, ..., vn
```

and their corresponding eigenvalues be:

```text
lambda1, lambda2, ..., lambdan
```

Construct a matrix `P` whose columns are those eigenvectors:

```text
P = [v1  v2  ...  vn]
```

Because the columns form a basis, `P` is invertible.

In this eigenvector basis, the transformation matrix becomes diagonal:

```text
D = P^(-1) * A * P
```

The diagonal entries are the eigenvalues:

```text
D = [lambda1   0       ...   0]
    [0         lambda2 ...   0]
    [...       ...     ...   ...]
    [0         0       ...   lambdan]
```

This diagonal matrix is much easier to work with than a general matrix.

### Why does this work?

Each basis vector is an eigenvector.

Therefore:

```text
A*v1 = lambda1*v1

A*v2 = lambda2*v2

...

A*vn = lambdan*vn
```

The transformation simply scales each basis vector by its associated eigenvalue.

There is no mixing between the basis directions.

This is exactly what a diagonal matrix does.

### The key identity

If:

```text
D = P^(-1) * A * P
```

then equivalently:

```text
A = P * D * P^(-1)
```

The matrix `P` converts eigenbasis coordinates into standard coordinates, while `P^(-1)` performs the reverse conversion.

This is the change-of-basis formula applied to a particularly useful basis: an eigenbasis.

---

## 14. Why Diagonalization Makes Matrix Powers Easier

Suppose we want to compute:

```text
A^100
```

Repeatedly multiplying a complicated matrix by itself 100 times is tedious and expensive.

But if `A` can be diagonalized:

```text
A = P * D * P^(-1)
```

then:

```text
A^2 = P * D * P^(-1) * P * D * P^(-1)
```

Since:

```text
P^(-1) * P = I
```

the middle factors cancel:

```text
A^2 = P * D^2 * P^(-1)
```

The same pattern continues:

```text
A^n = P * D^n * P^(-1)
```

This is a very powerful result.

Why?

Because raising a diagonal matrix to a power is easy.

If:

```text
D = [lambda1  0]
    [0        lambda2]
```

then:

```text
D^n = [lambda1^n  0]
      [0          lambda2^n]
```

Instead of repeatedly multiplying a general matrix, we raise each eigenvalue to the desired power.

We then transform back to the original coordinate system.

### When is this useful?

This idea appears in:
- Repeated linear transformations.
- Discrete dynamical systems.
- Difference equations.
- Population models.
- Markov processes, with additional conditions depending on the problem.
- Analyses of numerical algorithms.
- Some methods for solving linear differential equations.

Diagonalization is not always possible, and it may not always be the most numerically stable computational method. But conceptually, it reveals why eigenvectors are so valuable.

---

## 15. The Fibonacci Connection

The video closes with a wonderful connection between eigenvalues, matrix powers, and the Fibonacci sequence.

The Fibonacci sequence begins:

```text
0, 1, 1, 2, 3, 5, 8, 13, 21, ...
```

Each term is the sum of the two preceding terms.

We can encode this recurrence using a matrix:

```text
A = [0  1]
    [1  1]
```

Consider a vector containing two consecutive Fibonacci numbers:

```text
v_n = [F_n]
      [F_(n+1)]
```

Multiplying by `A` gives:

```text
A*v_n = [F_(n+1)]
        [F_n + F_(n+1)]
```

By the Fibonacci recurrence:

```text
F_(n+2) = F_n + F_(n+1)
```

Therefore:

```text
A*v_n = [F_(n+1)]
        [F_(n+2)]
```

Multiplying by `A` advances the sequence by one step.

Consequently, multiplying by `A^n` advances it by `n` steps.

This means that understanding the powers of `A` lets us understand the Fibonacci sequence.

### Step 1: Find the eigenvalues

Calculate:

```text
A - lambda*I = [-lambda    1]
               [1         1-lambda]
```

The determinant is:

```text
det(A - lambda*I)
    = (-lambda)*(1-lambda) - 1
```

Simplifying:

```text
det(A - lambda*I) = lambda^2 - lambda - 1
```

Set it equal to zero:

```text
lambda^2 - lambda - 1 = 0
```

Using the quadratic formula:

```text
lambda1 = (1 + sqrt(5))/2

lambda2 = (1 - sqrt(5))/2
```

The first value is the golden ratio:

```text
phi = (1 + sqrt(5))/2
```

Approximately:

```text
phi = 1.618...
```

The second eigenvalue is approximately:

```text
lambda2 = -0.618...
```

### Step 2: Use the eigenbasis

The matrix has two distinct eigenvalues, so its corresponding eigenvectors are linearly independent.

Construct `P` using those eigenvectors as columns.

Then:

```text
A = P * D * P^(-1)
```

where:

```text
D = [lambda1  0]
    [0        lambda2]
```

Now:

```text
A^n = P * D^n * P^(-1)
```

and:

```text
D^n = [lambda1^n  0]
      [0          lambda2^n]
```

The complicated repeated recurrence has been reduced to powers of two numbers.

With the appropriate initial conditions, this leads to the closed-form Fibonacci formula:

```text
F_n = (phi^n - psi^n) / sqrt(5)
```

where:

```text
phi = (1 + sqrt(5))/2

psi = (1 - sqrt(5))/2
```

This is known as **Binet's formula**.

For example, when `n = 5`:

```text
F_5 = (phi^5 - psi^5) / sqrt(5)

F_5 = 5
```

The matrix formulation and diagonalization explain why a recurrence involving repeated additions can be described using powers of the golden ratio.

That is the deeper payoff of eigenvalues: they can reveal the long-term behavior hidden inside repeated transformations.

---

## 16. Connections to AI and Machine Learning

Now let's connect eigenvectors and eigenvalues to the topics you will encounter in ML.

### A. Principal Component Analysis (PCA)

PCA is a dimensionality-reduction method that identifies orthogonal directions of maximum variance in a centered dataset.

These directions are eigenvectors of the dataset's covariance matrix.

Their corresponding eigenvalues describe the variance along those directions.

For example, suppose a covariance matrix has eigenvalues:

```text
lambda1 = 9

lambda2 = 1
```

The first principal direction accounts for much more variance than the second.

The total variance represented by these two components is proportional to their sum:

```text
Total variance = 9 + 1 = 10
```

The first component accounts for:

```text
9/10 = 90%
```

of the total variance.

Keeping only the first component would retain 90% of the variance in this example, while reducing the data from two dimensions to one.

This is useful when a dataset has many features but much of its variation lies along a smaller number of directions.

### B. Covariance and correlated features

Suppose two features are strongly correlated.

Their data points may cluster around a diagonal direction rather than spreading equally along the original coordinate axes.

The covariance matrix's eigenvectors reveal the principal directions of variation.

Its eigenvalues quantify how much variance lies along those directions.

This is one reason PCA can sometimes provide a more informative coordinate system than the original features.

### C. Understanding curvature in optimization

In optimization, the Hessian matrix describes second-order curvature of a sufficiently smooth objective function.

Near a suitable point, its eigenvectors identify special directions of curvature, while its eigenvalues quantify the curvature along those directions.

Very different eigenvalues can indicate that the objective has steep directions and shallow directions.

That can make optimization difficult because a step size suitable for a steep direction may make little progress along a shallow one, or even destabilize the update.

Eigenvalues therefore help explain conditioning and the behavior of some optimization algorithms.

### D. Stability of dynamical systems

Consider a repeated linear update:

```text
x_(t+1) = A*x_t
```

Repeated application gives:

```text
x_t = A^t*x_0
```

If `A` is diagonalizable, its eigenvalues help describe how different eigenvector components evolve over time.

In a discrete-time linear system:
- Eigenvalues with magnitude less than 1 correspond to decay along their eigenvector directions.
- Eigenvalues with magnitude greater than 1 correspond to growth along those directions.
- Eigenvalues with magnitude equal to 1 require more careful analysis, particularly when there are repeated eigenvalues or non-diagonalizable behavior.

This provides a foundation for understanding stability in control systems and other dynamical systems.

### E. Neural networks and representations

Neural networks learn representations through repeated transformations.

Eigenvectors and eigenvalues are not a complete description of a general neural network, especially when nonlinear activation functions are involved.

However, they are useful tools for analyzing linear layers, covariance matrices, Hessians, and some aspects of training dynamics.

The broad lesson is that a good coordinate system can expose the important structure of a problem.

---

## 17. Common Misconceptions

### Misconception 1: Every vector is an eigenvector

No.

Only vectors that remain on their own span under the transformation qualify.

Most vectors are not eigenvectors.

### Misconception 2: An eigenvector must remain unchanged

No.

An eigenvector may be stretched, shrunk, or flipped.

The requirement is that its direction remain on the same line, not that its coordinates remain identical.

### Misconception 3: Eigenvectors cannot have negative eigenvalues

They can.

A negative eigenvalue means the vector is flipped as well as scaled.

### Misconception 4: An eigenvector can be the zero vector

No.

The zero vector satisfies `A*v = lambda*v` for every `lambda`, so allowing it would make the definition meaningless. An eigenvector must be nonzero.

### Misconception 5: Every real matrix has real eigenvalues

No.

A 90-degree rotation in real 2D space has no real eigenvalues or real eigenvectors.

Its eigenvalues are complex.

### Misconception 6: A repeated eigenvalue means there is only one eigenvector

No.

A repeated eigenvalue can have multiple independent eigenvectors.

For example, the matrix that scales the entire plane by 2 has only one distinct eigenvalue, but every nonzero vector is an eigenvector.

### Misconception 7: Every matrix can be diagonalized

No.

A matrix is diagonalizable when it has enough linearly independent eigenvectors to form a basis.

The shear matrix from this chapter does not have enough independent eigenvectors.

### Misconception 8: Eigenvalues depend on the coordinate basis

A change of basis can change the entries of a matrix representing a transformation, but it does not change that transformation's eigenvalues.

Similar matrices have the same eigenvalues.

---

## 18. Quick Revision Sheet

| Concept | Meaning |
|---|---|
| Eigenvector | A nonzero vector that remains on its own span after transformation |
| Eigenvalue | The scalar by which an eigenvector is multiplied |
| Eigenvector equation | `A*v = lambda*v` |
| Characteristic equation | `det(A - lambda*I) = 0` |
| Characteristic polynomial | The polynomial obtained from `det(A - lambda*I)` |
| Eigenspace | The null space of `A - lambda*I` for a particular eigenvalue |
| Eigenbasis | A basis consisting entirely of eigenvectors |
| Diagonalization | Expressing a matrix as `A = P*D*P^(-1)` |
| Diagonal matrix | A matrix with all off-diagonal entries equal to zero |
| Similar matrices | Matrices representing the same transformation in different bases |
| Algebraic multiplicity | How many times an eigenvalue occurs as a root of the characteristic polynomial |
| Geometric multiplicity | The dimension of the eigenvalue's eigenspace |

### The four formulas to remember

**1. Definition**

```text
A*v = lambda*v
```

**2. Characteristic equation**

```text
det(A - lambda*I) = 0
```

**3. Eigenvectors for a known eigenvalue**

```text
(A - lambda*I)*v = 0
```

**4. Diagonalization**

```text
D = P^(-1)*A*P
```

Equivalently:

```text
A = P*D*P^(-1)
```

---

## 19. Self-Test

Try these before checking the answers.

### Question 1: Identify the eigenvalues

Consider:

```text
A = [4  0]
    [0  2]
```

What are its eigenvalues?

### Question 2: Identify an eigenvector

For the same matrix, is this an eigenvector?

```text
v = [1]
    [0]
```

If so, what is its eigenvalue?

### Question 3: Find the characteristic polynomial

For:

```text
A = [2  1]
    [0  3]
```

Calculate:

```text
det(A - lambda*I)
```

Then find the eigenvalues.

### Question 4: Understand the geometry

Why does a 90-degree rotation in real 2D space have no real eigenvectors?

### Question 5: Connect to diagonalization

A 3×3 matrix has three linearly independent eigenvectors.

Can it be diagonalized?

### Question 6: Understand matrix powers

If:

```text
A = P*D*P^(-1)
```

what is the expression for `A^n`?

### Question 7: Think like an ML engineer

A covariance matrix has eigenvalues 8 and 2.

What proportion of the total variance is explained by the first principal component, assuming these are the only two eigenvalues?

---

## 20. Self-Test Answers

### Answer 1

The matrix is diagonal, so its diagonal entries are its eigenvalues:

```text
lambda1 = 4

lambda2 = 2
```

### Answer 2

Yes.

```text
A*[1, 0] = [4, 0]
```

Therefore:

```text
A*v = 4*v
```

Its eigenvalue is 4.

### Answer 3

First:

```text
A - lambda*I = [2-lambda  1]
               [0         3-lambda]
```

Its determinant is:

```text
det(A - lambda*I) = (2-lambda)*(3-lambda)
```

Set it equal to zero:

```text
(2-lambda)*(3-lambda) = 0
```

Therefore:

```text
lambda = 2

lambda = 3
```

### Answer 4

A 90-degree rotation turns every nonzero real vector away from its original line.

No nonzero real vector remains on its own span.

The matrix has complex eigenvalues, but no real eigenvectors.

### Answer 5

Yes.

Three linearly independent eigenvectors form a basis for 3D space. Using them as the columns of `P` produces an invertible matrix, allowing diagonalization.

### Answer 6

```text
A^n = P*D^n*P^(-1)
```

The diagonal entries of `D` are raised individually to the power `n`.

### Answer 7

The total variance is:

```text
8 + 2 = 10
```

The first principal component explains:

```text
8/10 = 0.8 = 80%
```

of the total variance.

---

## 21. Final Takeaway

The central insight of this chapter is that **eigenvectors reveal the directions in which a linear transformation behaves like simple scalar multiplication**.

Once we discover those directions, we can often choose them as a new basis and represent the transformation with a diagonal matrix.

That change of basis can turn repeated matrix multiplication into simple powers of eigenvalues.

It also explains why eigenvectors and eigenvalues appear in PCA, dynamical systems, optimization, and many other areas of applied mathematics.

### Your checkpoint

Before moving on, make sure you can:

1. Explain `A*v = lambda*v` geometrically.
2. Find eigenvalues using `det(A - lambda*I) = 0`.
3. Find eigenvectors by solving `(A - lambda*I)*v = 0`.
4. Explain why some matrices have no real eigenvectors.
5. Explain how an eigenbasis makes diagonalization possible.
6. Derive `A^n = P*D^n*P^(-1)` from `A = P*D*P^(-1)`.

If you understand those six points, you have the foundation needed for the next chapter, which explores a useful computational shortcut for finding eigenvalues.
