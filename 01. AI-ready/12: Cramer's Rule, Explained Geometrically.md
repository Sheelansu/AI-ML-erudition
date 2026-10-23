# Essence of Linear Algebra, Chapter 12
## Cramer's Rule, Explained Geometrically

**Source:** [3Blue1Brown, Chapter 12](https://www.youtube.com/watch?v=jBsC34PxzoM)

## 1. The big question: can we reverse a linear transformation?

Recall what we learned in Chapter 3.

A matrix represents a linear transformation. Given an input vector, multiplying by the matrix produces an output vector.

For example:

```text
A = [2  1]
    [0  3]

x = [x]
    [y]
```

The transformation is:

```text
A*x = [2x + y]
       [  3y  ]
```

Now suppose we know the output but not the input.

```text
A*x = b
```

Here:

- `A` is a known matrix.
- `b` is a known output vector.
- `x` is the unknown input vector we want to recover.

This is the problem of solving a system of linear equations.

For example:

```text
2x + y = 7
  3y   = 6
```

We want to find the values of `x` and `y` that produce the required output.

In matrix form:

```text
[2  1] [x] = [7]
[0  3] [y]   [6]
```

Solving the equations gives:

```text
y = 2
x = 2.5
```

Therefore:

```text
x_vector = [2.5]
           [2  ]
```

But how can we derive the solution directly using determinants?

That is where Cramer's rule comes in.

---

## 2. What is Cramer's rule?

Cramer's rule gives a formula for each unknown coordinate in a square linear system.

Suppose:

```text
A*x = b
```

where `A` is an invertible `n × n` matrix.

To find the `i`-th coordinate of `x`:

1. Start with the original matrix `A`.
2. Replace its `i`-th column with the output vector `b`.
3. Calculate the determinant of this modified matrix.
4. Divide that determinant by the determinant of the original matrix.

The formula is:

```text
x_i = det(A_i) / det(A)
```

Here, `A_i` means the matrix obtained by replacing column `i` of `A` with `b`.

For a two-variable system:

```text
a*x + b*y = e
c*x + d*y = f
```

the coefficient matrix is:

```text
A = [a  b]
    [c  d]
```

Its determinant is:

```text
det(A) = a*d - b*c
```

Cramer's rule gives:

```text
x = (e*d - b*f) / (a*d - b*c)
```

and:

```text
y = (a*f - e*c) / (a*d - b*c)
```

These formulas work when the denominator is nonzero.

However, the formulas alone don't explain why they work. To understand that, we need to return to the geometry of determinants.

---

## 3. A linear system is a vector-combination puzzle

Consider a general two-dimensional matrix:

```text
A = [a  b]
    [c  d]
```

Its columns are:

```text
u = [a]
    [c]

v = [b]
    [d]
```

When we multiply `A` by an unknown vector:

```text
x = [x]
    [y]
```

the result is:

```text
A*x = x*u + y*v
```

This equation is extremely important.

It says that the output vector `b` is a linear combination of the columns of `A`.

```text
b = x*u + y*v
```

The unknown coordinates `x` and `y` are the coefficients telling us how much of each column vector is needed to construct the output.

Geometrically, we have two known vectors and one known target vector. We want to discover the coefficients that combine the known vectors into the target.

If the two columns are linearly independent, they span the entire plane. Every target vector has exactly one representation using those two columns.

If the columns are parallel, they span only a line. Then some target vectors cannot be reached, while others have infinitely many possible input vectors.

The determinant distinguishes these situations.

```text
det(A) != 0  -> unique solution for every output vector

det(A) = 0   -> no unique solution in general
```

The zero-determinant case is important, but Cramer's rule in its usual form assumes a nonzero determinant.

---

## 4. Why not use dot products to recover the coordinates?

From Chapter 9, we know that the coordinates of a vector can be extracted using dot products with the standard basis vectors.

For example:

```text
x = [x]
    [y]
```

Its coordinates are:

```text
x_coordinate = x_vector · i

y_coordinate = x_vector · j
```

where:

```text
i = [1]       j = [0]
    [0]           [1]
```

It might seem natural to apply the transformation and then use dot products with the transformed basis vectors to recover the original coordinates.

But there is a problem.

**Most linear transformations do not preserve dot products.**

A transformation may stretch vectors, compress them, or change the angles between them.

For example, two perpendicular vectors might no longer be perpendicular after a shear transformation.

Therefore, the dot product between transformed vectors generally differs from the dot product between their original versions.

There is a special case: orthogonal transformations preserve dot products. These include rotations and reflections that preserve lengths and angles.

For a general matrix, though, we need a different geometric quantity that we can track through the transformation.

The determinant gives us exactly that.

---

## 5. The surprising idea: coordinates can be represented by signed areas

Consider an unknown vector:

```text
x = [x]
    [y]
```

Recall the standard basis vectors:

```text
i = [1]       j = [0]
    [0]           [1]
```

Let's find a geometric interpretation of the `y`-coordinate.

Look at the parallelogram formed by `i` and `x`.

Its signed area is:

```text
det([1  x])
    ([0  y])
```

Calculate the determinant:

```text
area = (1*y) - (0*x)
     = y
```

So:

```text
y = det([i  x])
```

In other words, the `y`-coordinate equals the signed area of the parallelogram formed by the first basis vector and the unknown vector.

Now consider the parallelogram formed by `x` and `j`.

Its signed area is:

```text
det([x  0])
    ([y  1])
```

Calculate:

```text
area = (x*1) - (0*y)
     = x
```

Therefore:

```text
x = det([x  j])
```

This gives us an unexpected way to describe the coordinates of a vector:

- The `x`-coordinate can be represented as a signed area involving `x` and `j`.
- The `y`-coordinate can be represented as a signed area involving `i` and `x`.

It may seem like a roundabout way to represent coordinates, but it becomes powerful when the vector is transformed.

### Why signed area matters

If the vector lies below the horizontal axis, its `y`-coordinate is negative.

The corresponding signed area is negative too.

The determinant therefore preserves the sign information that ordinary, unsigned area would lose.

This is why the determinant, rather than just the geometric area, is the right tool.

---

## 6. What happens to these areas after a transformation?

Let the transformation matrix be:

```text
A = [a  b]
    [c  d]
```

Its determinant is:

```text
det(A) = a*d - b*c
```

The transformation maps:

```text
i -> u
j -> v
x -> b
```

where `u` and `v` are the columns of `A`, and `b` is the known output vector.

Remember the determinant's geometric interpretation from Chapter 6.

A linear transformation scales every signed area by the same factor:

```text
transformed_signed_area =
    det(A) * original_signed_area
```

The sign of the determinant also records whether orientation is preserved or reversed.

Now return to the parallelogram formed by `i` and `x`.

Its original signed area is:

```text
det([i  x]) = y
```

After applying the transformation, its sides become `u` and `b`.

Therefore, its transformed signed area is:

```text
det([u  b])
```

But the determinant tells us that this new area equals the original signed area multiplied by `det(A)`:

```text
det([u  b]) = det(A) * y
```

Rearrange:

```text
y = det([u  b]) / det(A)
```

We have recovered the `y`-coordinate using only the known matrix columns and the known output vector.

Similarly, start with the parallelogram formed by `x` and `j`.

Its signed area is `x`.

After transformation, its sides become `b` and `v`.

Therefore:

```text
det([b  v]) = det(A) * x
```

Rearrange:

```text
x = det([b  v]) / det(A)
```

These are precisely the two-variable formulas of Cramer's rule.

**The trick works because the determinant scales signed areas uniformly, allowing us to recover the original coordinate by dividing out the scaling factor.**

---

## 7. A complete worked example

Let's solve:

```text
2x + y = 7
3y     = 6
```

The matrix equation is:

```text
A*x = b
```

where:

```text
A = [2  1]
    [0  3]

b = [7]
    [6]
```

### Step 1: Calculate the original determinant

```text
det(A) = (2*3) - (1*0)
       = 6
```

Since the determinant is nonzero, the matrix is invertible and the system has a unique solution.

### Step 2: Calculate x

Replace the first column of `A` with `b`:

```text
A_x = [7  1]
      [6  3]
```

Calculate its determinant:

```text
det(A_x) = (7*3) - (1*6)
         = 21 - 6
         = 15
```

Apply Cramer's rule:

```text
x = det(A_x) / det(A)
  = 15 / 6
  = 2.5
```

### Step 3: Calculate y

Replace the second column of `A` with `b`:

```text
A_y = [2  7]
      [0  6]
```

Calculate:

```text
det(A_y) = (2*6) - (7*0)
         = 12
```

Apply Cramer's rule:

```text
y = det(A_y) / det(A)
  = 12 / 6
  = 2
```

### Final solution

```text
x = 2.5
y = 2
```

Check the original equations:

```text
2*(2.5) + 2 = 7

3*2 = 6
```

Both equations hold.

---

## 8. Cramer's rule in three dimensions

The same idea works in 3D, except that signed areas become signed volumes.

Suppose:

```text
A*x = b
```

where `A` is a 3 × 3 matrix:

```text
A = [a11  a12  a13]
    [a21  a22  a23]
    [a31  a32  a33]
```

The unknown vector is:

```text
x = [x1]
    [x2]
    [x3]
```

The columns of `A` are three vectors, and their linear combination produces the output vector `b`.

How can we recover `x3` geometrically?

Imagine the parallelepiped formed by the first two standard basis vectors and the unknown input vector.

Its signed volume is:

```text
det([i  j  x]) = x3
```

After the transformation, those three vectors become the first two columns of `A` and the output vector `b`.

The transformed signed volume is:

```text
det([a1  a2  b])
```

where `a1` and `a2` denote the first and second columns of `A`.

The determinant scales signed volume by `det(A)`, so:

```text
det([a1  a2  b]) = det(A) * x3
```

Therefore:

```text
x3 = det([a1  a2  b]) / det(A)
```

The same construction works for the other coordinates.

Replace the relevant column of `A` with `b`, calculate the new determinant, and divide by the original determinant.

The geometric idea is identical in two, three, and higher dimensions:

- Coordinates correspond to signed areas or volumes.
- The transformation scales those measurements by its determinant.
- Dividing by the determinant recovers the original coordinate.

---

## 9. The general formula

For a square matrix `A` and output vector `b`, suppose:

```text
A*x = b
```

and:

```text
det(A) != 0
```

Let `A_i` be the matrix obtained by replacing the `i`-th column of `A` with `b`.

Then:

```text
x_i = det(A_i) / det(A)
```

For a 3 × 3 system:

```text
x1 = det([b  a2  a3]) / det(A)

x2 = det([a1  b  a3]) / det(A)

x3 = det([a1  a2  b]) / det(A)
```

Here, `a1`, `a2`, and `a3` are the columns of `A`.

Notice that only one column changes at a time.

This is not an arbitrary recipe. Each replaced-column determinant measures the transformed signed area or volume associated with one original coordinate.

---

## 10. When does Cramer's rule work?

Cramer's rule in this form requires a square matrix with a nonzero determinant.

### Case 1: Nonzero determinant

```text
det(A) != 0
```

The matrix is invertible.

For every output vector `b`, there is exactly one input vector `x`.

Cramer's rule produces that solution.

### Case 2: Zero determinant

```text
det(A) = 0
```

The matrix maps the input space into a lower-dimensional subspace.

There are two possibilities for a given output vector:

- The output lies outside the matrix's image, so no solution exists.
- The output lies inside the image, so there may be infinitely many solutions.

For example:

```text
x + y = 2
2x + 2y = 4
```

The second equation is just twice the first.

There are infinitely many solutions because every pair satisfying `x + y = 2` works.

The coefficient matrix is:

```text
A = [1  1]
    [2  2]
```

Its determinant is:

```text
det(A) = (1*2) - (1*2)
       = 0
```

Cramer's rule cannot be applied because it would require division by zero.

The zero determinant is telling us that the transformation has collapsed the plane onto a line.

---

## 11. Why Cramer's rule is not usually the preferred computational method

Cramer's rule is valuable for understanding linear algebra, but it is not generally the best way to solve large systems numerically.

For practical computation, methods such as Gaussian elimination and LU decomposition are usually preferred.

Why?

For an `n × n` matrix, Cramer's rule requires calculating the determinant of the original matrix and another determinant for every unknown.

That can become expensive as `n` grows.

Gaussian elimination, by contrast, solves a system using row operations and is generally much more efficient.

Cramer's rule is still useful when:

- You want a closed-form expression for an unknown.
- You need to prove a theoretical result.
- You are solving a small system by hand.
- You want to understand the geometric role of determinants.
- You are studying how linear systems relate to invertibility and volume scaling.

The lesson is not that you should use Cramer's rule everywhere. The lesson is that understanding *why* it works strengthens your intuition about matrices and determinants.

---

## 12. Connections to AI and machine learning

Cramer's rule is not the standard numerical method used to train neural networks, but the concepts behind it are important.

### A. Linear systems appear throughout machine learning

Many algorithms require solving equations of the form:

```text
A*x = b
```

Examples include certain least-squares methods, linear models, and optimization subproblems.

Understanding when a matrix is invertible helps explain whether a solution is unique.

### B. Singular matrices and redundant information

If:

```text
det(A) = 0
```

for a square matrix, its columns are linearly dependent.

This means the transformation loses some dimensions of information.

In machine learning, rank-deficient matrices can arise when features are redundant or when a problem is underdetermined.

For example, if two input features always contain the same information, a model may have difficulty uniquely identifying their individual coefficients.

The determinant provides a theoretical signal of this loss of invertibility, although for large matrices other tools are often more informative.

### C. Least squares and normal equations

In linear regression, a common mathematical expression is:

```text
X_transpose * X * beta = X_transpose * y
```

These are the normal equations.

When the relevant matrix is invertible, one can write:

```text
beta = inverse(X_transpose * X) * X_transpose * y
```

However, explicitly computing the inverse is usually not the preferred numerical implementation. QR decomposition or singular value decomposition can be more stable, especially when features are highly correlated.

Cramer's rule helps build the conceptual background for understanding what a unique solution means, but it is not the recommended algorithm for large regression problems.

### D. Determinants and information loss

A zero determinant means that a square linear transformation is not invertible.

Geometrically, it collapses at least one dimension.

This idea connects to the broader question of whether a model or data transformation preserves enough information to recover its input.

In practical ML, rank and singular values are often more useful than calculating a determinant directly, especially in high dimensions.

---

## 13. Common misconceptions

**Misconception 1: Cramer's rule is just a formula with no geometric meaning.**

It follows from representing coordinates as signed areas or volumes and using the determinant's scaling property.

**Misconception 2: You replace rows of the matrix.**

In the standard column-vector formulation, you replace the column corresponding to the unknown you want to find.

**Misconception 3: You divide by the modified determinant.**

No. You divide the modified determinant by the determinant of the original coefficient matrix.

**Misconception 4: Cramer's rule always produces a unique solution.**

Only when the original square matrix has a nonzero determinant.

**Misconception 5: A zero determinant means no solutions exist.**

Not necessarily. The system may have no solutions or infinitely many solutions, depending on the output vector.

**Misconception 6: Cramer's rule is the best way to solve every linear system.**

It is mainly useful for small systems and theoretical understanding. Gaussian elimination and related methods are generally more efficient for computation.

**Misconception 7: The determinant itself gives the solution.**

The determinant measures signed area or volume scaling. Cramer's rule uses ratios of determinants to recover individual coordinates.

---

## 14. Quick revision sheet

| Concept | Key idea |
|---|---|
| Linear system | `A*x = b` |
| Columns of `A` | Vectors combined to produce `b` |
| Unknown coordinates | Coefficients in that linear combination |
| Determinant | Signed area or volume scaling factor |
| Coordinate as signed area | In 2D, `x` and `y` can be represented using signed areas |
| Cramer's rule | Replace one column with `b`, then divide determinants |
| Unique solution | Requires `det(A) != 0` |
| Zero determinant | Transformation collapses at least one dimension |
| Higher dimensions | Signed areas generalize to signed volumes and higher-dimensional analogues |
| Practical numerical methods | Gaussian elimination, LU, QR, or SVD depending on the problem |

### The four equations to remember

**1. Linear system**

```text
A*x = b
```

**2. Determinant of a 2 × 2 matrix**

```text
det(A) = a*d - b*c
```

**3. Cramer's rule**

```text
x_i = det(A_i) / det(A)
```

**4. The geometric principle**

```text
transformed_signed_area_or_volume =
    det(A) * original_signed_area_or_volume
```

That final principle is the reason Cramer's rule works.

---

## 15. Self-test

Try these before checking the answers.

**Q1.** What does `A*x = b` mean geometrically?

**Q2.** Why is the determinant relevant when solving a linear system?

**Q3.** For a 2 × 2 matrix, what is the determinant formula?

**Q4.** What do you replace to calculate the `y`-coordinate using Cramer's rule?

**Q5.** Solve the following system using Cramer's rule:

```text
x + y = 5
x - y = 1
```

**Q6.** What does a zero determinant tell you about a square matrix?

**Q7.** Does a zero determinant always mean that the system has no solution?

**Q8.** Why is Cramer's rule usually not the preferred method for large systems?

### Answers

**A1.** A known linear transformation maps an unknown input vector `x` to the known output vector `b`. We are trying to recover the input.

**A2.** The determinant tells us how the transformation scales signed areas or volumes and whether the transformation is invertible.

**A3.**

```text
det(A) = a*d - b*c
```

**A4.** Replace the second column of the original coefficient matrix with the output vector `b`.

**A5.**

The coefficient matrix is:

```text
A = [1  1]
    [1 -1]
```

Its determinant is:

```text
det(A) = (1*(-1)) - (1*1)
       = -2
```

For `x`, replace the first column:

```text
A_x = [5  1]
      [1 -1]
```

```text
det(A_x) = (5*(-1)) - (1*1)
         = -6
```

Therefore:

```text
x = (-6)/(-2) = 3
```

For `y`, replace the second column:

```text
A_y = [1  5]
      [1  1]
```

```text
det(A_y) = (1*1) - (5*1)
         = -4
```

Therefore:

```text
y = (-4)/(-2) = 2
```

The solution is:

```text
x = 3
y = 2
```

**A6.** The matrix is singular and not invertible. Its columns are linearly dependent, and its transformation collapses at least one dimension.

**A7.** No. Depending on the output vector, the system may have no solutions or infinitely many solutions.

**A8.** It requires many determinant calculations and is generally less computationally efficient than methods such as Gaussian elimination.

---

## Final takeaway

Cramer's rule is much more than a determinant trick.

A linear system asks us to recover an unknown input vector from its output. The coordinates of that input can be interpreted as signed areas or volumes. When the matrix transforms the input space, those measurements are scaled by the determinant.

By calculating the corresponding signed areas or volumes in the output space and dividing by the determinant, we recover the original coordinates.

**The deepest idea is this: determinants let us track how a linear transformation changes geometric quantities, and Cramer's rule uses that information to recover unknown coordinates.**

Next up: **Chapter 13, “Change of Basis.”** We'll explore how the same vector can have different coordinate descriptions depending on the basis we choose, and why changing the coordinate system can make mathematical problems much easier.
