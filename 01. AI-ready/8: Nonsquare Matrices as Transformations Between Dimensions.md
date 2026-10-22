# Essence of Linear Algebra, Chapter 8
## Nonsquare Matrices as Transformations Between Dimensions

**Source:** [3Blue1Brown, Chapter 8](https://www.youtube.com/watch?v=v8VSDg_WQlA)

## 1. The big idea

So far, we have mostly studied square matrices:

- A 2 × 2 matrix transforms 2D vectors into 2D vectors.
- A 3 × 3 matrix transforms 3D vectors into 3D vectors.

But why must the input and output spaces have the same number of dimensions?

They don't.

A matrix can represent a transformation from one dimension to another:

- 2D → 3D
- 3D → 2D
- 2D → 1D
- 5D → 3D
- 1,000D → 100D

These transformations are represented by **nonsquare matrices**, also called rectangular matrices.

The central insight is:

**The number of columns tells you the input dimension. The number of rows tells you the output dimension.**

That simple rule unlocks the geometry of rectangular matrices.

---

## 2. Reading matrix dimensions

Consider this matrix:

```text
A = [ 2  0 ]
    [-1  1 ]
    [-1  1 ]
```

It has 3 rows and 2 columns, so it is a **3 × 2 matrix**.

Its input has two coordinates:

```text
x = [ x1 ]
    [ x2 ]
```

Its output has three coordinates:

```text
y = A*x

y = [ y1 ]
    [ y2 ]
    [ y3 ]
```

Therefore, the transformation is:

```text
A: R^2 -> R^3
```

Here, `R^2` means the space of two-dimensional real vectors, and `R^3` means the space of three-dimensional real vectors.

More generally, if `A` has `m` rows and `n` columns:

```text
A is an m x n matrix

A: R^n -> R^m
```

Remember the order:

- **Columns = input coordinates**
- **Rows = output coordinates**

A useful memory trick: the matrix's columns describe the input basis directions, while the number of entries in each column tells you the number of coordinates in the output.

---

## 3. How does a 2D-to-3D transformation work?

Let's construct a transformation from a plane into three-dimensional space.

Suppose the two standard basis vectors of the input plane are:

```text
i = [1]
    [0]

j = [0]
    [1]
```

We define where these basis vectors land in 3D:

```text
T(i) = [ 2]
       [-1]
       [-1]

T(j) = [0]
       [1]
       [1]
```

The first basis vector lands at one point in 3D. The second basis vector lands at another.

As in earlier chapters, we build the transformation matrix by placing the transformed basis vectors into its columns:

```text
A = [ 2  0]
    [-1  1]
    [-1  1]
```

Notice the dimensions:

- Each input basis vector has two coordinates.
- Each transformed basis vector has three coordinates.
- There are two input basis vectors, so the matrix has two columns.
- Each transformed vector has three coordinates, so the matrix has three rows.

Thus, `A` is 3 × 2.

### Transforming an arbitrary vector

Every 2D vector can be expressed as a linear combination of the standard basis vectors:

```text
v = x*i + y*j
```

By linearity:

```text
T(v) = x*T(i) + y*T(j)
```

Substitute the basis images:

```text
T(v) = x*[ 2] + y*[0]
         [-1]    [1]
         [-1]    [1]
```

Therefore:

```text
T([x]) = [ 2x     ]
  ([y])   [-x + y  ]
          [-x + y  ]
```

Or, as a matrix product:

```text
[ 2  0] [x]   [ 2x     ]
[-1  1] [y] = [-x + y  ]
[-1  1]       [-x + y  ]
```

The transformation takes two numbers as input and produces three numbers as output.

### A numerical example

Choose the input vector:

```text
v = [3]
    [2]
```

Then:

```text
A*v = [ 2  0] [3]   [ 6]
      [-1  1] [2] = [-1]
      [-1  1]       [-1]
```

So the input `(3, 2)` maps to the output `(6, -1, -1)`.

The input lives in a 2D plane. The output lives in 3D space.

These are different spaces, even though both are represented using coordinates.

---

## 4. What does the transformed plane look like?

A linear transformation preserves the origin and maps lines to lines, though different lines can collapse onto the same line or point.

For our matrix:

```text
A = [ 2  0]
    [-1  1]
    [-1  1]
```

The output always satisfies:

```text
y2 = y3
```

Why? The second and third rows of the matrix are identical, so the second and third output coordinates must always be equal.

That means every output lies on the plane:

```text
y2 - y3 = 0
```

This is a plane passing through the origin in 3D space.

The transformation takes the entire 2D input plane and maps it onto a 2D plane embedded inside 3D space.

The input plane and output plane are not literally the same geometric object. They live in different spaces, even though both have two dimensions.

### Is this transformation full rank?

The two columns are:

```text
c1 = [ 2]
     [-1]
     [-1]

c2 = [0]
     [1]
     [1]
```

Neither column is a scalar multiple of the other, so they are linearly independent.

Therefore:

```text
rank(A) = 2
```

The input space is two-dimensional, and the column space is also two-dimensional.

This means the transformation preserves the full number of input dimensions, even though the output is embedded in a higher-dimensional space.

The matrix has **full column rank**.

---

## 5. What does a 2D-to-3D matrix tell us?

A 3 × 2 matrix has three output coordinates for every two input coordinates.

Its column space can have dimension at most two because it is spanned by only two columns.

Therefore, its outputs lie in one of the following:

- A plane through the origin, if the two columns are independent.
- A line through the origin, if the columns are dependent but at least one is nonzero.
- Just the origin, if both columns are zero.

It cannot fill all of 3D space.

This is an important distinction: **the output has three coordinates, but the transformation cannot create three independent output directions from only two input dimensions.**

For a 3 × 2 matrix, rank can be 0, 1, or 2, but never 3.

---

## 6. What about a 2D-to-1D transformation?

Now consider a transformation that takes a point in the plane and outputs a single number.

A simple example is:

```text
T([x]) = 3x + 2y
  ([y])
```

Its matrix is:

```text
A = [3  2]
```

This is a 1 × 2 matrix.

The transformation is:

```text
A: R^2 -> R^1
```

For the input:

```text
v = [2]
    [4]
```

the output is:

```text
A*v = [3  2] [2]
             [4]

     = [14]
```

The input is a point in the plane. The output is a single real number.

You can think of the output as a coordinate on a number line.

### Where do the basis vectors land?

For the standard basis vectors:

```text
i = [1]       j = [0]
    [0]           [1]
```

we get:

```text
T(i) = 3
T(j) = 2
```

Those two scalar values form the matrix's two columns, each containing one entry:

```text
A = [3  2]
```

Every 2D vector is mapped to a number according to its weighted combination of the two coordinates.

### What happens to lines?

The transformation sends the entire plane to the number line.

Many different points in the plane can produce the same output.

For example:

```text
3x + 2y = 6
```

Every point on this line maps to the number 6.

Thus, the set of inputs producing the same output forms a line in the input plane.

This connects directly to the null space from Chapter 7. The inputs that produce zero satisfy:

```text
3x + 2y = 0
```

which describes a line through the origin.

A 2D-to-1D transformation necessarily loses at least one independent input direction.

---

## 7. What does a 2 × 3 matrix represent?

Reverse the dimensions.

A 2 × 3 matrix has three columns and two rows:

```text
A = [ a  b  c ]
    [ d  e  f ]
```

Its input has three coordinates, and its output has two:

```text
A: R^3 -> R^2
```

It transforms 3D vectors into 2D vectors.

For example:

```text
A = [1  0  1]
    [0  1  1]
```

For an input:

```text
v = [x]
    [y]
    [z]
```

the output is:

```text
A*v = [x + z]
      [y + z]
```

So the transformation takes three numbers and produces two numbers.

### Why must information be lost?

The input has three independent dimensions, but the output has at most two.

The rank-nullity theorem says:

```text
rank(A) + nullity(A) = number of columns
```

For this matrix, the two rows are independent, so its rank is 2.

Therefore:

```text
2 + nullity(A) = 3

nullity(A) = 1
```

There is one independent input direction that gets mapped to zero.

To find it, solve:

```text
A*v = [0]
      [0]
```

This gives:

```text
x + z = 0
y + z = 0
```

Set `z = 1`. Then:

```text
x = -1
y = -1
z =  1
```

So one null-space direction is:

```text
v = [-1]
    [-1]
    [ 1]
```

Indeed:

```text
A*[-1] = [0]
  [-1]   [0]
  [ 1]
```

Any multiple of this vector is also mapped to zero.

This illustrates a general principle: a linear transformation from a higher-dimensional input space to a lower-dimensional output space cannot preserve every independent input direction.

---

## 8. The general rule for rectangular matrices

For an `m × n` matrix:

```text
A: R^n -> R^m
```

The rank can never exceed the smaller of the row count and column count:

```text
rank(A) <= min(m, n)
```

The rank-nullity theorem gives:

```text
rank(A) + nullity(A) = n
```

Together, these tell us a lot about the transformation.

### If output dimension is larger than input dimension

Example: 3 × 2 matrix.

```text
R^2 -> R^3
```

The transformation can embed the input plane into 3D space. If its columns are independent, it preserves both input dimensions.

It cannot fill all of 3D space because its rank is at most 2.

### If output dimension is smaller than input dimension

Example: 2 × 3 matrix.

```text
R^3 -> R^2
```

The transformation must collapse at least one independent input direction to zero.

It may fill all of 2D space if it has rank 2, but it cannot be one-to-one across the entire 3D input space.

### If input and output dimensions are equal

Example: 3 × 3 matrix.

```text
R^3 -> R^3
```

The matrix may be invertible if it has full rank. Otherwise, it collapses some input directions.

This is the square-matrix case from the earlier chapters.

---

## 9. Why this matters in AI and machine learning

Rectangular matrices are everywhere in machine learning. They are often more common than square matrices.

### A. Neural network layers

A fully connected layer typically performs:

```text
y = W*x + b
```

Suppose a layer accepts 784 input features and produces 128 output features.

Then:

```text
W has shape 128 x 784
x has shape 784 x 1
b has shape 128 x 1
y has shape 128 x 1
```

The matrix maps:

```text
R^784 -> R^128
```

The layer compresses a 784-dimensional representation into 128 dimensions.

Because the output has fewer dimensions than the input, the linear transformation cannot preserve all independent input directions. Different inputs can produce the same linear output.

This is one reason feature selection, representation learning, and the design of neural network architectures matter.

### B. Embeddings and dimensionality reduction

Imagine a dataset with 1,000 features. We want a compact representation with 100 features.

A linear projection can be represented by:

```text
W has shape 100 x 1000
```

The transformation is:

```text
R^1000 -> R^100
```

Its rank cannot exceed 100. Therefore, its null space has dimension at least 900.

That means at least 900 independent input directions are discarded by the linear projection.

This does not mean 900 original features are individually deleted. Rather, it means 900 independent directions in the input space cannot be distinguished through this projection.

Methods such as principal component analysis (PCA) choose a lower-dimensional representation that preserves as much of the relevant variation as possible under their objective.

### C. Increasing dimensionality

Sometimes a model maps a lower-dimensional representation into a higher-dimensional space.

For example:

```text
W has shape 512 x 128
```

The transformation is:

```text
R^128 -> R^512
```

This can expand the representation into a higher-dimensional space.

If `W` has full column rank, the transformation can preserve all 128 independent input directions. However, its outputs still lie in a subspace of dimension at most 128 inside the 512-dimensional output space.

Increasing the number of coordinates does not automatically create additional independent information.

### D. Tensor shapes and debugging

When coding neural networks, matrix dimensions determine which operations are valid.

Suppose:

```text
W: 128 x 784
x: 784 x 1
```

Then:

```text
W*x: 128 x 1
```

The inner dimensions, 784 and 784, match.

But this multiplication is invalid:

```text
W*x

W: 128 x 784
x: 128 x 1
```

The inner dimensions do not match.

A useful habit is to annotate shapes beside your equations. It makes many matrix-multiplication bugs obvious before you run the code.

---

## 10. Common misconceptions

**Misconception 1: Every matrix must be square to represent a transformation.**

False. Any `m × n` matrix represents a linear transformation from `R^n` to `R^m`.

**Misconception 2: A 3 × 2 matrix produces outputs that fill all of 3D space.**

False. Its rank is at most 2, so its outputs lie in a plane, line, or the origin.

**Misconception 3: More output coordinates mean more information.**

Not necessarily. A 2D input can be represented using three output coordinates, but those coordinates may be constrained to a 2D plane.

**Misconception 4: A rectangular matrix always loses information.**

The direction matters. A transformation from higher dimension to lower dimension must lose at least one independent input direction. A transformation from lower dimension to higher dimension can preserve all input information if it has full column rank.

**Misconception 5: The determinant works for every matrix.**

The usual determinant is defined for square matrices. A 3 × 2 matrix does not have a determinant in the standard sense.

**Misconception 6: Adding dimensions always adds independent directions.**

A vector in a 512-dimensional output space may still lie inside a 128-dimensional subspace. The number of coordinates and the dimension of the space spanned by the outputs are not the same thing.

---

## 11. Quick revision table

| Matrix shape | Transformation | Maximum rank |
|---|---|---:|
| 2 × 2 | 2D → 2D | 2 |
| 3 × 2 | 2D → 3D | 2 |
| 2 × 3 | 3D → 2D | 2 |
| 1 × 2 | 2D → 1D | 1 |
| 128 × 784 | 784D → 128D | 128 |
| 512 × 128 | 128D → 512D | 128 |

### The three equations to remember

```text
m x n matrix: R^n -> R^m
```

Columns determine input dimension; rows determine output dimension.

```text
rank(A) <= min(m, n)
```

A transformation cannot produce more independent output directions than the smaller of its input and output dimensions.

```text
rank(A) + nullity(A) = n
```

The number of independent output directions plus the number of independent input directions that vanish equals the input dimension.

---

## 12. Self-test

Try these before checking the answers.

**Q1.** A matrix has 4 rows and 7 columns. What is its input dimension and output dimension?

**Q2.** What does a 3 × 2 matrix represent geometrically?

**Q3.** Can a 3 × 2 matrix have rank 3?

**Q4.** A matrix maps 5D vectors into 2D vectors. What is the minimum possible nullity?

**Q5.** A matrix maps 2D vectors into 5D vectors and has rank 2. Has it lost an input dimension?

**Q6.** Why is the determinant not defined in the usual way for a 2 × 3 matrix?

**Q7.** In a neural network layer, the weight matrix has shape 256 × 64. What are the input and output dimensions?

### Answers

**A1.** Input dimension is 7; output dimension is 4.

**A2.** It maps 2D input vectors into 3D output vectors. Its outputs lie in a subspace of dimension at most 2.

**A3.** No. Its rank is at most the smaller dimension, which is 2.

**A4.** Rank is at most 2, so nullity is at least `5 - 2 = 3`.

**A5.** No. Rank 2 equals the input dimension, so the null space is trivial. It can preserve all independent input directions.

**A6.** The standard determinant describes signed area or volume scaling for a square transformation from a space to itself. A rectangular matrix maps between spaces of different dimensions, so that same determinant is not defined.

**A7.** It maps 64-dimensional inputs to 256-dimensional outputs.

---

## Final takeaway

A rectangular matrix is not a broken square matrix. It represents a transformation between spaces of different dimensions.

Think of it this way:

- **Columns** tell you how many independent input coordinates you supply.
- **Rows** tell you how many output coordinates you receive.
- **Rank** tells you how many independent output directions are actually reachable.
- **Null space** tells you which input directions disappear.

For machine learning, this is essential. A weight matrix changing a representation from 784 features to 128 features is doing the same mathematical kind of operation as a 3 × 2 matrix mapping a plane into 3D space.

Different scale, same geometry.
