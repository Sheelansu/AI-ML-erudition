# Essence of Linear Algebra: Chapter 3
## Linear Transformations and Matrices

**Video:** [Linear Transformations and Matrices | 3Blue1Brown](https://www.youtube.com/watch?v=kYB8IZa5AuE)

**Playlist:** [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

---

## 1. Recap: What We Learned in Previous Chapters

Before understanding transformations, let's recall the ideas from the first two chapters.

### Chapter 1: Vectors

A vector can be represented as an arrow or an ordered list of numbers.

```text
v = [3, 2]
```

We learned two fundamental operations:

- Vector addition: combining vectors.
- Scalar multiplication: scaling a vector by a number.

### Chapter 2: Linear Combinations, Span, and Basis Vectors

We learned that vectors can be constructed by combining scaled versions of other vectors.

For example, the standard 2D basis vectors are:

```text
i = [1, 0]
j = [0, 1]
```

Any 2D vector can be constructed using these two vectors.

```text
v = [x, y]

v = x*i + y*j
```

For example:

```text
v = [3, 2]

v = 3*i + 2*j
```

This means three copies of `i` and two copies of `j`, added together.

### The question in this chapter

What happens if we apply a function that transforms every vector in a space?

Can we describe that transformation using numbers?

**The central discovery of this chapter is that a linear transformation can be represented by a matrix.**

Understanding this connection makes matrix multiplication much more intuitive.

---

## 2. What Is a Transformation?

A transformation is essentially a function that takes an input and produces an output.

In linear algebra, we are particularly interested in functions that take vectors as inputs and return vectors as outputs.

We can represent a transformation using the notation:

```text
T(v) = transformed version of vector v
```

For example, suppose a transformation doubles every vector.

```text
v = [2, 3]

T(v) = [4, 6]
```

The transformation changes the vector while preserving its direction.

Another transformation might rotate vectors, reflect them, or compress the space in which they exist.

### 2.1 Transforming a vector versus transforming space

Imagine a 2D coordinate plane containing millions of vectors.

A transformation doesn't have to act on just one vector. It can define what happens to every vector in that space.

For example, if every vector is doubled, the entire plane expands away from the origin.

If every vector is rotated by 90 degrees around the origin, the entire plane rotates.

If one coordinate is removed from every vector, the plane might collapse onto a line.

Thinking about a transformation as an operation on the entire space gives us a much richer understanding than looking at one vector in isolation.

### 2.2 Visualizing transformations using a grid

Imagine a grid covering the entire plane.

Initially, the grid has:
- Straight horizontal and vertical lines.
- Parallel grid lines.
- Equal spacing between adjacent lines.
- An origin at the center.

As a transformation acts on the plane, every point moves to a new location.

Instead of tracking every point separately, we can watch what happens to the grid.

The grid gives us a visual summary of the transformation.

For example:
- A rotation turns the grid.
- A scaling transformation stretches or compresses it.
- A shear transformation slants it.
- A projection can collapse it onto a line.

The behavior of the grid reveals the nature of the transformation.

---

## 3. What Makes a Transformation Linear?

Not every transformation is a linear transformation.

A linear transformation must preserve two fundamental operations:

1. Vector addition.
2. Scalar multiplication.

These rules can be written as follows.

### 3.1 Property 1: Preservation of vector addition

If we add two vectors and then transform their sum, we must obtain the same result as transforming each vector separately and then adding the transformed vectors.

```text
T(u + v) = T(u) + T(v)
```

For example, suppose:

```text
u = [1, 0]
v = [0, 1]
```

Their sum is:

```text
u + v = [1, 1]
```

A linear transformation must satisfy:

```text
T([1, 1]) = T([1, 0]) + T([0, 1])
```

This means the transformation preserves the way vector addition works.

### 3.2 Property 2: Preservation of scalar multiplication

Scaling a vector before transforming it must give the same result as transforming it first and then applying the same scalar.

```text
T(c*v) = c*T(v)
```

Here, `c` is any scalar.

For example:

```text
v = [1, 2]
c = 3
```

A linear transformation must satisfy:

```text
T(3*v) = 3*T(v)
```

These two operations must agree regardless of which order we use.

### 3.3 Combining both properties

Together, the two properties imply that linear transformations preserve every linear combination.

```text
T(a*u + b*v) = a*T(u) + b*T(v)
```

This equation is one of the most important ideas in this chapter.

It means we can determine the transformation of a linear combination by knowing how the transformation acts on the individual vectors.

### 3.4 The geometric interpretation

In the video's visual explanation, a linear transformation has two important geometric characteristics:

- Straight lines remain straight, although a line may collapse into a single point.
- The origin remains fixed.

A linear transformation also preserves parallelism, and its grid lines remain evenly spaced in the transformed grid.

Angles and lengths, however, do not necessarily remain unchanged.

A rotation preserves both lengths and angles, while a shear can change angles and a scaling transformation can change lengths.

### 3.5 Examples of linear and non-linear transformations

| Transformation | Linear? | Reason |
|---|---|---|
| Rotation about the origin | Yes | Preserves vector addition and scalar multiplication |
| Reflection through the origin | Yes | Preserves both operations |
| Scaling about the origin | Yes | Preserves both operations |
| Shearing | Yes | Preserves both operations |
| Projection onto a line through the origin | Yes | Preserves both operations |
| Translation by a nonzero vector | No | Moves the origin |
| Squaring each coordinate | Generally no | Does not preserve vector addition or scalar multiplication |

**Important:** A transformation that looks visually simple is not necessarily linear. The mathematical properties, not the appearance alone, determine whether it is linear.

---

## 4. The Origin Must Remain Fixed

One consequence of linearity is that the zero vector must always transform into itself.

Let's derive this using the scalar multiplication property.

```text
T(0*v) = 0*T(v)
```

Since `0*v` is the zero vector, and multiplying any vector by zero also produces the zero vector:

```text
T([0, 0]) = [0, 0]
```

Therefore, every linear transformation fixes the origin.

### Example: Translation

Suppose a transformation adds `[2, 3]` to every point.

```text
T(v) = v + [2, 3]
```

Applying it to the zero vector gives:

```text
T([0, 0]) = [2, 3]
```

The origin moves, so this transformation is not linear.

This is an important distinction between a linear transformation and an arbitrary transformation.

**Note:** A translation by the zero vector changes nothing and is linear. A translation by a nonzero vector is not linear, although it is an example of an affine transformation.

---

## 5. The Big Idea: A Matrix Represents a Linear Transformation

Now we reach the most important connection in the video.

Suppose we have a linear transformation operating on 2D vectors.

We want to determine what happens to every possible input vector.

Do we need to calculate the output of every vector individually?

No.

Because the transformation is linear, we only need to know what happens to the two standard basis vectors.

Recall:

```text
i = [1, 0]
j = [0, 1]
```

Every vector can be constructed from these two vectors.

```text
v = [x, y]

v = x*i + y*j
```

Apply the transformation:

```text
T(v) = T(x*i + y*j)
```

Using the linearity properties:

```text
T(v) = x*T(i) + y*T(j)
```

This is the crucial result.

**If we know where the basis vectors go, we can calculate the transformation of every vector in the space.**

### 5.1 Example

Suppose the transformation sends the standard basis vectors to these destinations:

```text
T(i) = [1, -2]
T(j) = [2, 0]
```

Now consider an arbitrary input vector:

```text
v = [x, y]
```

We know:

```text
v = x*i + y*j
```

Therefore:

```text
T(v) = x*T(i) + y*T(j)
```

Substitute the transformed basis vectors:

```text
T(v) = x*[1, -2] + y*[2, 0]
```

Multiply each vector by its scalar:

```text
T(v) = [x, -2*x] + [2*y, 0]
```

Add corresponding components:

```text
T(v) = [x + 2*y, -2*x]
```

We now have a formula for transforming every 2D vector.

No matter which vector we choose, we can calculate its output using this formula.

---

## 6. Constructing the Matrix

We have discovered that a linear transformation can be completely described by the images of the standard basis vectors.

The next step is to organize those images into a matrix.

We found:

```text
T(i) = [1, -2]
T(j) = [2, 0]
```

Place the first transformed basis vector in the first column and the second transformed basis vector in the second column.

```text
A = [ 1   2 ]
    [ -2  0 ]
```

This matrix represents the transformation.

### 6.1 Why are the vectors placed in columns?

The first column contains the transformed first basis vector.

```text
First column = T(i) = [1, -2]
```

The second column contains the transformed second basis vector.

```text
Second column = T(j) = [2, 0]
```

Each column tells us where one of the original basis directions ends up.

The matrix therefore records how the transformation acts on the fundamental directions of the space.

### 6.2 The general 2D matrix

A general 2D linear transformation can be represented by:

```text
A = [ a  c ]
    [ b  d ]
```

The columns tell us:

```text
T(i) = [a, b]
T(j) = [c, d]
```

For an arbitrary vector:

```text
v = [x, y]
```

Its transformed vector is:

```text
T(v) = x*[a, b] + y*[c, d]
```

Expanding:

```text
T(v) = [a*x, b*x] + [c*y, d*y]
```

Adding the components:

```text
T(v) = [a*x + c*y, b*x + d*y]
```

The matrix provides a compact numerical description of the transformation.

---

## 7. Matrix-Vector Multiplication

Matrix-vector multiplication is the numerical operation used to apply the transformation to an input vector.

Consider:

```text
A = [ 1   2 ]
    [ -2  0 ]

v = [x, y]
```

The matrix-vector product is:

```text
A*v = [1*x + 2*y, -2*x + 0*y]
```

Simplifying:

```text
A*v = [x + 2*y, -2*x]
```

This is exactly the transformation formula derived earlier.

Matrix-vector multiplication is therefore not an arbitrary arithmetic rule.

**It is the numerical expression of applying a linear transformation to a vector.**

### 7.1 A worked numerical example

Using the same matrix:

```text
A = [ 1   2 ]
    [ -2  0 ]
```

Suppose:

```text
v = [3, 1]
```

The output is:

```text
A*v = [1*3 + 2*1, -2*3 + 0*1]
```

Calculate each component:

```text
A*v = [3 + 2, -6 + 0]

A*v = [5, -6]
```

The original vector `[3, 1]` is transformed into `[5, -6]`.

### 7.2 The row-wise calculation

A useful way to perform matrix-vector multiplication is to calculate one output component per row.

For the matrix:

```text
A = [ 1   2 ]
    [ -2  0 ]
```

And vector:

```text
v = [3, 1]
```

First row:

```text
1*3 + 2*1 = 5
```

Second row:

```text
-2*3 + 0*1 = -6
```

Combine the results:

```text
A*v = [5, -6]
```

This is the standard computational procedure. The column-based interpretation explains why it represents a transformation.

Both interpretations are useful:
- Columns explain where the basis vectors go.
- Rows provide a convenient way to calculate the output coordinates.

---

## 8. What Different Matrices Do to Space

Different matrices produce different transformations.

Let's explore several common examples.

### 8.1 Identity transformation

```text
I = [1  0]
    [0  1]
```

For any vector:

```text
v = [x, y]
```

We obtain:

```text
I*v = [x, y]
```

Nothing changes.

The identity matrix is the transformation that leaves every vector exactly where it is.

### 8.2 Scaling transformation

```text
A = [2  0]
    [0  3]
```

Applying it to a vector:

```text
v = [x, y]
```

Produces:

```text
A*v = [2*x, 3*y]
```

The horizontal coordinate doubles, while the vertical coordinate triples.

The space stretches by different amounts along the two axes.

### 8.3 Rotation

A 90-degree counterclockwise rotation about the origin is represented by:

```text
R = [0  -1]
    [1   0]
```

Applying it:

```text
R*[x, y] = [-y, x]
```

For example:

```text
v = [2, 1]

R*v = [-1, 2]
```

The vector rotates 90 degrees counterclockwise without changing its length.

### 8.4 Reflection

Reflection across the y-axis is represented by:

```text
F = [-1  0]
    [ 0  1]
```

The transformation is:

```text
F*[x, y] = [-x, y]
```

The x-coordinate changes sign, while the y-coordinate remains unchanged.

### 8.5 Shear transformation

Consider:

```text
S = [1  1]
    [0  1]
```

Applying it:

```text
S*[x, y] = [x + y, y]
```

The y-coordinate stays the same, but the x-coordinate shifts according to the value of y.

This slants the grid while preserving straightness, parallelism, and the origin.

### 8.6 Projection onto the x-axis

Consider:

```text
P = [1  0]
    [0  0]
```

Applying it:

```text
P*[x, y] = [x, 0]
```

Every vector loses its vertical component.

The entire 2D plane collapses onto the x-axis.

This is still a linear transformation even though it destroys one dimension of the space.

### Summary

| Transformation | Effect |
|---|---|
| Identity | Leaves every vector unchanged |
| Scaling | Stretches or compresses space |
| Rotation | Turns vectors around the origin |
| Reflection | Flips space across an axis or line through the origin |
| Shear | Slants the coordinate grid |
| Projection | Collapses space onto a lower-dimensional subspace |

---

## 9. The Geometric Meaning of Matrix Columns

This deserves special attention because it is one of the most useful intuitions in linear algebra.

Suppose:

```text
A = [a  c]
    [b  d]
```

Its columns are:

```text
First column  = [a, b]
Second column = [c, d]
```

These are the destinations of the original basis vectors.

```text
T(i) = [a, b]
T(j) = [c, d]
```

Now consider:

```text
v = [x, y]
```

The original vector is constructed from the basis vectors:

```text
v = x*i + y*j
```

After transformation:

```text
T(v) = x*T(i) + y*T(j)
```

Substitute the columns:

```text
T(v) = x*[a, b] + y*[c, d]
```

This gives the output vector.

### The intuition

Imagine the original coordinate grid as a flexible sheet.

The first basis vector indicates where the horizontal unit direction goes.

The second basis vector indicates where the vertical unit direction goes.

Once you know those two destinations, the transformation of every other vector follows from the same linear combinations.

The matrix stores these two transformed directions.

This is why understanding matrix columns can be more insightful than memorizing multiplication rules.

---

## 10. Why This Matters for AI and Machine Learning

Linear transformations are fundamental to many machine learning computations.

### 10.1 Transforming feature vectors

Suppose a data point has three numerical features.

```text
x = [age, income, experience]
```

A model may transform this vector into a new representation using a matrix.

```text
y = W*x
```

The matrix `W` determines how the input components are combined to produce the output components.

Depending on the dimensions of `W`, the transformation can preserve the number of components or map the input into a space with a different number of dimensions.

### 10.2 Neural network layers

A common operation in a neural network layer is:

```text
y = W*x + b
```

Here:
- `x` is the input vector.
- `W` is a weight matrix.
- `b` is a bias vector.
- `y` is the output before applying an activation function.

The matrix multiplication mixes input features using learned weights.

The bias adds an offset. If the bias is nonzero, this entire operation is generally affine rather than linear.

A typical neural network then applies a nonlinear activation function, such as ReLU, to introduce nonlinear behavior.

### 10.3 Why matrices matter in deep learning

Neural networks repeatedly transform vector representations.

For example:

```text
input vector
     |
     v
weight matrix multiplication
     |
     v
bias addition
     |
     v
activation function
     |
     v
new representation
```

Understanding linear transformations helps explain how a network changes the representation of its inputs from one layer to another.

### 10.4 Embeddings

An embedding represents an object using a vector.

A learned matrix can transform one embedding representation into another.

For example:

```text
new_embedding = W*old_embedding
```

The matrix combines the original components to produce a new representation.

In actual models, these matrices are learned from data, and their effects can be much more complex than simple geometric rotations or stretches.

### 10.5 Important distinction

A matrix transformation alone is linear if it has no added offset and acts through ordinary matrix multiplication.

A neural network layer with a bias is generally affine, and a layer that also applies a nonlinear activation is generally nonlinear.

This distinction will become useful when you study neural network architectures in detail.

---

## 11. Common Misconceptions to Avoid

1. **A matrix is not merely a grid of numbers.** It can encode a linear transformation.
2. **Not every transformation is linear.** It must preserve vector addition and scalar multiplication.
3. **The origin must remain fixed.** A linear transformation always maps the zero vector to itself.
4. **Knowing the transformed basis vectors is sufficient.** For a linear transformation, these determine the output of every vector in the space.
5. **Matrix columns have a geometric meaning.** Each column represents the transformed version of a standard basis vector.
6. **Matrix-vector multiplication is not an arbitrary rule.** It computes the transformed vector.
7. **Lengths and angles need not be preserved.** Linear transformations can stretch, compress, shear, reflect, and rotate space.
8. **A linear transformation can reduce dimension.** For example, a 2D plane can collapse onto a line.
9. **A neural network layer is not always linear.** Bias addition makes it affine, and nonlinear activation functions make the overall mapping nonlinear.
10. **The order of matrix entries matters.** Changing a matrix's entries can produce a different transformation.

---

## 12. Quick Revision Sheet

| Concept | Meaning |
|---|---|
| Transformation | A function mapping inputs to outputs |
| Linear transformation | A function preserving vector addition and scalar multiplication |
| Origin | The zero vector, which every linear transformation fixes |
| Basis vector | A vector belonging to a basis of the space |
| Matrix | A numerical representation of a linear transformation |
| Matrix column | The transformed image of a standard basis vector |
| Matrix-vector multiplication | Applying the matrix's transformation to a vector |
| Identity matrix | Leaves all vectors unchanged |
| Scaling | Changes vector magnitudes along specified directions |
| Rotation | Turns vectors around the origin |
| Reflection | Flips vectors across a line or plane through the origin |
| Shear | Slants the coordinate grid |
| Projection | Maps vectors onto a lower-dimensional subspace |

### Essential formulas

**Linearity: vector addition**

```text
T(u + v) = T(u) + T(v)
```

**Linearity: scalar multiplication**

```text
T(c*v) = c*T(v)
```

**Transformation of a linear combination**

```text
T(a*u + b*v) = a*T(u) + b*T(v)
```

**Transformation from basis vectors**

```text
v = x*i + y*j

T(v) = x*T(i) + y*T(j)
```

**Matrix representation**

```text
A = [a  c]
    [b  d]

First column  = T(i) = [a, b]
Second column = T(j) = [c, d]
```

**Matrix-vector multiplication**

```text
A*[x, y] = [a*x + c*y, b*x + d*y]
```

**Origin remains fixed**

```text
T([0, 0]) = [0, 0]
```

---

## 13. Self-Test

Try answering these questions without looking at the notes.

1. What is a transformation?
2. What two properties define a linear transformation?
3. Why must the origin remain fixed under a linear transformation?
4. If `T(i) = [1, -2]` and `T(j) = [2, 0]`, what is the matrix representing the transformation?
5. Using the same transformation, calculate the output of `[3, 1]`.
6. What do the columns of a transformation matrix represent?
7. Why is matrix-vector multiplication equivalent to applying a linear transformation?
8. Is translation by `[2, 3]` a linear transformation? Why?
9. Can a linear transformation collapse a plane onto a line?
10. How does matrix multiplication help transform feature vectors in a neural network?

### Answers

1. A function that maps inputs to outputs.
2. It must preserve vector addition and scalar multiplication.
3. Because `T(0*v) = 0*T(v)`, which implies `T(0) = 0`.
4. `A = [[1, 2], [-2, 0]]`.
5. `T([3, 1]) = [5, -6]`.
6. The transformed images of the standard basis vectors.
7. Matrix columns encode the transformed basis vectors, and linearity lets us combine those columns using the input coordinates.
8. No. A nonzero translation moves the origin.
9. Yes. Projection onto a line through the origin is a linear transformation.
10. A weight matrix combines input components to produce new output components.

---

## Final Takeaway

This chapter introduces one of the central ideas of linear algebra:

**A matrix is a way to describe a linear transformation numerically.**

The most important reasoning chain is:

1. Every vector can be expressed as a linear combination of basis vectors.
2. A linear transformation preserves linear combinations.
3. Therefore, knowing where the basis vectors go tells us where every vector goes.
4. Those transformed basis vectors become the columns of a matrix.
5. Multiplying that matrix by a vector computes the transformed vector.

Keep this chain of reasoning in mind. It will make matrix multiplication, composition of transformations, determinants, and eigenvectors much easier to understand in the chapters ahead.
