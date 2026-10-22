# Essence of Linear Algebra, Chapter 7
## Inverse Matrices, Column Space, and Null Space

**Source:** [3Blue1Brown, Chapter 7](https://www.youtube.com/watch?v=uQhTuRlWMxw)

## 1. The central idea: solving equations geometrically

Consider a system of linear equations:

```text
2x + 2y = -4
 x + 3y = -1
```

We can combine its coefficients into a matrix and its unknowns into a vector.

```text
A = [ 2  2 ]
    [ 1  3 ]

x = [ x ]
    [ y ]

b = [ -4 ]
    [  -1 ]
```

The whole system becomes:

```text
A*x = b
```

This equation says: apply the transformation represented by `A` to the unknown vector `x`, and the result should be `b`.

**Solving the system means finding the input vector that transforms into the desired output.**

That geometric interpretation is the foundation of this entire chapter.

There are three important possibilities:

- The transformation can be reversed uniquely, giving exactly one solution.
- The transformation collapses some dimensions, so some outputs cannot be reached.
- Multiple input vectors can produce the same output, giving infinitely many solutions when a solution exists.

The determinant, inverse, column space, rank, and null space help us understand which situation we have.

---

## 2. Inverse matrices: reversing a transformation

Imagine rotating every vector in the plane 90 degrees counterclockwise.

To undo that transformation, rotate every vector 90 degrees clockwise.

The reverse transformation is the **inverse**.

If `A` represents a transformation, its inverse is written `A^(-1)`.

The defining property is:

```text
A^(-1) * A = I
A * A^(-1) = I
```

Here, `I` is the identity matrix, which leaves every vector unchanged.

For two dimensions:

```text
I = [ 1  0 ]
    [ 0  1 ]
```

For three dimensions:

```text
I = [ 1  0  0 ]
    [ 0  1  0 ]
    [ 0  0  1 ]
```

The identity matrix is the matrix equivalent of doing nothing.

### Why does the order matter?

Matrix multiplication represents composition of transformations. The matrix on the right acts first.

```text
A^(-1) * A
```

means apply `A`, then undo it with `A^(-1)`.

But:

```text
A * A^(-1)
```

means undo a transformation first, then apply it.

Both compositions give the identity when `A^(-1)` really is the inverse of `A`.

### When does an inverse exist?

For a square matrix:

```text
det(A) != 0  =>  A is invertible
det(A) = 0   =>  A is not invertible
```

This connects directly to Chapter 6, where we learned that a zero determinant means a transformation collapses space into a lower-dimensional region.

If a transformation squashes an entire plane onto a line, it cannot be reversed uniquely. Once several different inputs have become the same output, the original input is lost.

This is called **information loss**.

### Example: a reversible transformation

Consider:

```text
A = [ 2  2 ]
    [ 1  3 ]
```

Its determinant is:

```text
det(A) = (2*3) - (2*1)
       = 6 - 2
       = 4
```

Since the determinant is nonzero, the inverse exists.

For a 2-by-2 matrix:

```text
A = [ a  b ]
    [ c  d ]
```

the inverse formula is:

```text
A^(-1) = (1 / (a*d - b*c)) * [  d  -b ]
                                  [ -c   a ]
```

Applying it to our matrix:

```text
A^(-1) = (1/4) * [  3  -2 ]
                   [ -1   2 ]
```

Now suppose we want to solve:

```text
A*x = b

b = [ -4 ]
    [ -1 ]
```

Multiply both sides by the inverse:

```text
A^(-1) * A * x = A^(-1) * b

I*x = A^(-1) * b

x = A^(-1) * b
```

The result is:

```text
x = [ -5/2 ]
    [  1/2 ]
```

Therefore:

```text
x = -2.5
y =  0.5
```

Substituting these values into the original equations confirms the solution.

**Important:** the inverse formula is useful for understanding the mathematics, but for larger systems, Gaussian elimination or numerical linear algebra methods are generally preferred over explicitly computing an inverse.

---

## 3. What happens when a matrix is not invertible?

Consider this matrix:

```text
A = [  3  -1 ]
    [ -9   3 ]
```

Its determinant is:

```text
det(A) = (3*3) - ((-1)*(-9))
       = 9 - 9
       = 0
```

The second row is `-3` times the first row. The two rows do not provide independent information.

Geometrically, the transformation collapses the plane onto a line.

Because multiple input vectors can land at the same output, there is no unique reverse transformation.

But here's the subtle part:

**No inverse does not mean no solution.**

A singular matrix can still produce a solution to `A*x = b`. It depends on whether `b` is one of the outputs that the transformation can actually produce.

That leads us to column space.

---

## 4. Column space: all outputs a matrix can produce

The **column space** of a matrix is the set of all possible output vectors of its transformation.

It is the span of the matrix's columns.

Consider:

```text
A = [ 1  -2   4 ]
    [ -2  4  -8 ]
    [ 5 -10  20 ]
```

The columns are:

```text
c1 = [  1 ]
     [ -2 ]
     [  5 ]

c2 = [ -2 ]
     [  4 ]
     [-10 ]

c3 = [  4 ]
     [ -8 ]
     [ 20 ]
```

Notice:

```text
c2 = -2*c1
c3 =  4*c1
```

All three columns point along the same line. They are different scalar multiples of one vector.

Consequently, every linear combination of these columns remains on that line.

The column space is therefore:

```text
Col(A) = span{c1}
```

It is a line through the origin in three-dimensional space.

Although the matrix accepts a 3D input vector and produces a 3D output vector, its outputs cannot fill all of 3D space.

### Why does column space determine whether a solution exists?

Consider:

```text
A*x = b
```

Expanding matrix multiplication gives:

```text
A*x = x1*c1 + x2*c2 + ... + xn*cn
```

The output is a linear combination of the columns of `A`.

Therefore, the system has a solution exactly when `b` lies in the column space of `A`.

```text
b belongs to Col(A)  =>  at least one solution
b outside Col(A)     =>  no solution
```

For the example above, every possible output has the form:

```text
b = t * [  1 ]
          [ -2 ]
          [  5 ]
```

for some real number `t`.

If `b = [2, -4, 10]`, a solution exists because it is `2*c1`.

If `b = [1, 0, 0]`, no solution exists because that vector does not lie on the column-space line.

The matrix cannot produce an output outside its column space, regardless of which input you choose.

---

## 5. Rank: how many dimensions survive?

The **rank** of a matrix is the dimension of its column space.

In plain language, rank tells us how many independent output directions remain after the transformation.

For a transformation whose outputs lie in 3D space:

<| Rank | Geometry of column space |
|---|---|
| 0 | Only the origin |
| 1 | A line through the origin |
| 2 | A plane through the origin |
| 3 | All of 3D space |

For a 2-by-2 matrix, the rank can be at most 2. For a 3-by-3 matrix, it can be at most 3.

A matrix has **full column rank** when its rank equals its number of columns.

For an `n`-by-`n` square matrix:

```text
rank(A) = n  =>  full rank
rank(A) = n  =>  det(A) != 0
rank(A) < n  =>  det(A) = 0
```

These statements apply to square matrices. Rectangular matrices require more care: they do not have the usual square determinant, and full column rank does not necessarily mean the transformation maps onto its entire output space.

### Example: rank of the earlier matrix

Recall:

```text
A = [  1  -2   4 ]
    [ -2   4  -8 ]
    [  5 -10  20 ]
```

Every column is a multiple of the first column.

There is only one independent column direction, so:

```text
rank(A) = 1
```

Even though it is a 3-by-3 matrix, it has only a one-dimensional column space.

### Why rank matters

Rank measures the number of independent directions that the transformation can represent in its output.

A higher rank generally means more independent output variation is possible. A lower rank means that some output directions are unavailable.

Rank is not simply the number of nonzero rows or columns. A matrix may have many nonzero columns that are all multiples of one another.

---

## 6. Null space: all inputs that become zero

Now we examine the opposite side of the transformation.

The **null space**, also called the **kernel**, is the set of every input vector that gets mapped to the zero vector.

Its defining equation is:

```text
A*x = 0
```

The null space contains the zero vector because every linear transformation maps the origin to itself.

For an invertible matrix, no other vector maps to zero:

```text
A*x = 0  =>  x = 0
```

But a non-invertible matrix can send nonzero vectors to zero as well.

### Example: finding the null space

Take our matrix again:

```text
A = [  1  -2   4 ]
    [ -2   4  -8 ]
    [  5 -10  20 ]
```

We want to solve:

```text
A * [ x ] = [ 0 ]
    [ y ]   [ 0 ]
    [ z ]   [ 0 ]
```

Because the rows are multiples of the first row, the system reduces to a single independent equation:

```text
x - 2y + 4z = 0
```

Rearrange:

```text
x = 2y - 4z
```

Choose `y = s` and `z = t`. Then:

```text
x = 2s - 4t
```

Every vector in the null space can therefore be written as:

```text
[ x ]   [ 2s - 4t ]
[ y ] = [     s   ]
[ z ]   [     t   ]
```

Equivalently:

```text
[ x ]       [ 2 ]       [ -4 ]
[ y ] = s * [ 1 ] + t * [  0 ]
[ z ]       [ 0 ]       [  1 ]
```

There are two independent free parameters, `s` and `t`.

The null space is a **plane through the origin**.

Why a plane? Because this matrix maps three-dimensional inputs into a one-dimensional output space. Two independent input directions are lost, leaving a two-dimensional collection of vectors that all map to zero.

This is a beautiful example of the connection between rank and null space.

---

## 7. Column space versus null space

These two concepts describe different aspects of the same matrix.

| Concept | Question it answers | Lives in |
|---|---|---|
| Column space | Which outputs are possible? | Output space |
| Null space | Which inputs become zero? | Input space |
| Rank | How many independent output dimensions remain? | Dimension of column space |
| Nullity | How many independent null-space directions exist? | Dimension of null space |

For an `m`-by-`n` matrix:

```text
A maps R^n to R^m
```

The input vectors have `n` coordinates, while output vectors have `m` coordinates.

The null space lives in the input space, `R^n`. The column space lives in the output space, `R^m`.

This distinction becomes especially important when studying rectangular matrices in Chapter 8.

### The rank-nullity theorem

One of the most useful relationships in linear algebra is:

```text
rank(A) + nullity(A) = number of columns of A
```

For an `m`-by-`n` matrix:

```text
rank(A) + nullity(A) = n
```

For our 3-by-3 example:

```text
rank(A) = 1
nullity(A) = 2

1 + 2 = 3
```

One independent direction survives in the output, while two independent directions belong to the null space.

The dimensions add up exactly to the number of input dimensions.

---

## 8. How many solutions can a linear system have?

Now we can classify the solutions of:

```text
A*x = b
```

There are three possibilities.

### Case 1: no solution

If `b` lies outside the column space, the transformation cannot produce it.

```text
b is not in Col(A)  =>  no solution
```

Example: a transformation whose outputs lie on a particular line cannot produce a vector outside that line.

### Case 2: exactly one solution

If `A` has full column rank, its null space contains only the zero vector.

When a solution exists, it is unique.

For a square matrix, full rank means the matrix is invertible, so every output vector has exactly one preimage.

```text
A is invertible  =>  exactly one solution for every b
```

### Case 3: infinitely many solutions

If a solution exists and the null space contains nonzero vectors, then the solution cannot be unique.

Suppose `x0` is one solution:

```text
A*x0 = b
```

Let `z` be any vector in the null space:

```text
A*z = 0
```

Then:

```text
A*(x0 + z) = A*x0 + A*z
            = b + 0
            = b
```

So every vector of the form below is also a solution:

```text
x = x0 + z
```

where `z` is any vector in the null space.

This is the general structure of solutions to a consistent linear system:

```text
All solutions = one particular solution + Null(A)
```

If the null space has at least one nonzero direction, infinitely many solutions exist.

### A useful classification table

| Does a solution exist? | Is the null space trivial? | Result |
|---|---|---|
| No | Either | No solutions |
| Yes | Yes | Exactly one solution |
| Yes | No | Infinitely many solutions |

For square matrices, this reduces to a familiar rule: an invertible matrix always gives one unique solution; a singular matrix may give either no solutions or infinitely many.

---

## 9. Connecting the concepts to AI and machine learning

These ideas are not merely geometric curiosities. They help explain what happens inside data transformations and learning algorithms.

### A. Neural networks and lost information

A linear layer can be represented as:

```text
y = W*x + b
```

Here, `W` is the weight matrix and `b` is the bias vector.

If `W` has a nontrivial null space, there are nonzero changes to the input that the linear part of the layer cannot distinguish.

If:

```text
W*z = 0
```

then:

```text
W*(x + z) + b = W*x + b
```

The two inputs produce the same output from this layer.

This does not automatically mean the entire neural network cannot distinguish those inputs. Earlier layers, nonlinearities, or other pathways can change the situation. But the linear transformation itself loses those distinctions.

### B. Embeddings and dimensionality reduction

Suppose a representation begins with 1,000 features and is projected into 100 dimensions.

The transformation is represented by a matrix with 100 rows and 1,000 columns.

Its rank cannot exceed 100. Therefore, there are at least 900 independent input directions in its null space.

Some differences between input vectors are inevitably erased by that projection.

This is a mathematical reason dimensionality reduction can compress information, and why choosing which information to preserve matters.

### C. Solving parameter and optimization problems

Many scientific and machine learning problems involve systems of equations:

```text
A*x = b
```

The columns of `A` describe how different variables contribute to the output.

- If the columns are independent, the variables may be uniquely recoverable in a square, full-rank system.
- If columns are dependent, different variable combinations may explain the same output.
- If the target lies outside the column space, no exact solution exists.

In regression, for example, dependent features can make individual coefficients non-unique even when the model's predictions are well determined. Practical methods such as regularization help manage these ambiguities.

### D. Invertible neural networks and normalizing flows

Some generative models use invertible transformations.

If a transformation is invertible, the output can be mapped back to its input without losing information. In normalizing flows, this property helps calculate how probability density changes under a transformation.

The determinant of the transformation's Jacobian describes local volume scaling. An invertible transformation must have a nonzero Jacobian determinant wherever the inverse is well-defined and differentiable.

This is a direct application of the relationship between determinants, invertibility, and geometric volume.

---

## 10. Common misconceptions

**Misconception 1: If a matrix has no inverse, its system has no solution.**

Not true. A singular matrix can have no solution or infinitely many solutions. The right-hand side must first belong to the column space.

**Misconception 2: Column space and null space are the same thing.**

They are different. Column space describes possible outputs; null space describes inputs that become zero.

**Misconception 3: Rank is the number of nonzero columns.**

Rank counts independent column directions. Several nonzero columns can point along the same direction.

**Misconception 4: A 3-by-3 matrix always transforms space throughout 3D.**

It may collapse all of 3D space onto a plane, a line, or even the origin.

**Misconception 5: If one solution exists, it must be unique.**

Only when the null space contains no nonzero vectors. Otherwise, you can add null-space vectors to a solution and obtain more solutions.

**Misconception 6: The inverse matrix is just a reciprocal.**

`A^(-1)` is a matrix that reverses a transformation. It is not obtained by taking the reciprocal of each matrix entry.

---

## 11. Quick revision sheet

| Term | Remember this |
|---|---|
| Inverse matrix | Reverses a linear transformation |
| Identity matrix | Leaves vectors unchanged |
| Invertible square matrix | Has nonzero determinant and full rank |
| Singular matrix | Has zero determinant and no inverse |
| Column space | Span of the matrix columns, containing every possible output |
| Rank | Dimension of the column space |
| Null space / kernel | All vectors `x` satisfying `A*x = 0` |
| Nullity | Dimension of the null space |
| Rank-nullity theorem | `rank(A) + nullity(A) = number of columns` |
| Unique solution | A solution exists and the null space is trivial |
| Infinitely many solutions | A solution exists and the null space has nonzero directions |
| No solution | The target vector lies outside the column space |

### The three most important equations

```text
A*x = b
```

Find the input that produces the desired output.

```text
x = A^(-1)*b
```

When `A` is invertible, reverse the transformation to solve the system.

```text
rank(A) + nullity(A) = number of columns of A
```

Count the independent output directions and the independent input directions that vanish.

---

## 12. Self-test

Try answering these before checking the solutions.

**Q1.** What does `A^(-1)*A = I` mean geometrically?

**Q2.** A square matrix has determinant zero. Can its system `A*x = b` still have a solution?

**Q3.** What is the column space of a matrix?

**Q4.** A 3-by-3 matrix has rank 1. What is the dimension of its null space?

**Q5.** If `A*x0 = b` and `A*z = 0`, why is `x0 + z` also a solution?

**Q6.** Can a matrix have three nonzero columns but rank 1?

**Q7.** If `b` is outside the column space of `A`, how many solutions does `A*x = b` have?

### Answers

**A1.** Applying the transformation and then its inverse returns every input to its original position.

**A2.** Yes. A solution exists if `b` lies in the column space. If it does, a singular square matrix has infinitely many solutions.

**A3.** The span of its columns, or equivalently, the set of all possible outputs `A*x`.

**A4.** Nullity is `3 - 1 = 2`, so the null space is two-dimensional.

**A5.** By linearity, `A*(x0 + z) = A*x0 + A*z = b + 0 = b`.

**A6.** Yes. All three columns could be scalar multiples of the same nonzero vector.

**A7.** Zero solutions. The transformation cannot produce a vector outside its column space.

---

## Final takeaway

The most important shift in perspective is to stop seeing a matrix only as a grid of numbers. See it as a machine that transforms input space into output space.

- The **inverse** asks whether the transformation can be reversed.
- The **column space** tells you which outputs the machine can produce.
- The **rank** tells you how many independent output directions survive.
- The **null space** reveals which input directions disappear.

Once these ideas click, systems of equations become a story about geometry, information, and what a transformation can or cannot recover. That intuition will be especially useful in the next chapter, where matrices no longer need to be square and can transform between spaces of different dimensions.
