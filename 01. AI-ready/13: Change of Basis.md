# Essence of Linear Algebra, Chapter 13: Change of Basis

**Video:** [Change of Basis | 3Blue1Brown](https://www.youtube.com/watch?v=P2LTAUO1TdA)  
**Series:** Essence of Linear Algebra  
**Main question:** How can we describe the same vector or linear transformation using different coordinate systems?

---

## 1. The Big Idea: A Vector Is Not Its Coordinates

Imagine you and your friend Jennifer are looking at the same arrow in 2D space.

You describe it as:

```text
v = [3, 2]
```

You mean:
- Move 3 units to the right.
- Move 2 units upward.

But Jennifer uses a different coordinate system. Her first basis vector points right and slightly upward, while her second points left and upward.

She describes the very same arrow as:

```text
[v]_B = [5/3, 1/3]
```

How can both descriptions be correct?

Because **the vector is the geometric object, while its coordinates are numbers that describe that object relative to a chosen basis.**

The numbers alone do not tell you which vector someone means. You must also know the basis they are using.

### A simple analogy

Imagine two people giving directions.

- Person A says, "Walk 3 blocks east and 2 blocks north."
- Person B uses streets running diagonally and describes the same destination using those streets.

Their numerical instructions differ, but they can reach the same location.

Changing the basis is like changing the reference system used to describe your journey.

### The key distinction

| Concept | Meaning |
|---|---|
| Vector | The underlying geometric object |
| Coordinates | The numbers used to represent the vector |
| Basis | The reference vectors that give those numbers meaning |
| Coordinate system | The rules for describing vectors using coordinates |
| Change of basis | Converting a vector's coordinates from one basis to another |

**Remember:** A vector does not change merely because you change the coordinate system used to describe it.

---

## 2. What Exactly Is a Basis?

In the earlier chapters, we used the standard basis for 2D space.

```text
e1 = [1, 0]

e2 = [0, 1]
```

These are the familiar unit vectors:

- `e1` points horizontally to the right.
- `e2` points vertically upward.

Any 2D vector can be expressed as a linear combination of these two vectors.

For example:

```text
v = [3, 2]

v = 3*e1 + 2*e2
```

The coordinates `[3, 2]` tell us how much of each basis vector to combine.

### A different basis

Suppose Jennifer uses these vectors instead:

```text
b1 = [2, 1]

b2 = [-1, 1]
```

Her basis is:

```text
B = {b1, b2}
```

To describe a vector using Jennifer's basis, we need to determine how much of `b1` and `b2` to combine.

The same vector `v` can be represented as:

```text
v = c1*b1 + c2*b2
```

Here, `c1` and `c2` are the coordinates relative to Jennifer's basis.

In other words:

```text
[v]_B = [c1, c2]
```

The subscript `B` means that these coordinates are expressed in basis `B`.

### What makes these vectors a basis?

For a 2D basis, the two vectors must satisfy two conditions:

1. They must span the entire 2D space.
2. They must be linearly independent.

Geometrically, the vectors cannot lie along the same line.

Jennifer's basis satisfies both conditions because `[2, 1]` and `[-1, 1]` point in different directions.

**Important:** A basis does not have to consist of perpendicular unit vectors. It can contain vectors of different lengths, and the vectors can point in non-perpendicular directions.

---

## 3. The Coordinate Grid Is Not the Space Itself

We often visualize 2D space using a square grid.

But that grid reflects our chosen coordinate system, not some intrinsic grid built into space.

With the standard basis, our grid has:
- A horizontal axis.
- A vertical axis.
- Equal spacing along both axes.

Jennifer's coordinate grid looks different because her basis vectors are different.

Her grid is oriented and spaced according to:

```text
b1 = [2, 1]

b2 = [-1, 1]
```

The origin remains the same, but the directions and spacing of the grid lines change.

A point that has coordinates `[1, 0]` in Jennifer's system corresponds to the vector `b1` in the standard system.

Likewise, Jennifer's `[0, 1]` corresponds to `b2` in the standard system.

That gives us a useful way to think about basis vectors:

**Every basis defines what the coordinate directions mean.**

This is why the same coordinate pair can represent different geometric vectors in different bases.

---

## 4. The Change-of-Basis Matrix

Now we reach the central mathematical idea of the chapter.

Jennifer's basis vectors, expressed in our standard coordinates, are:

```text
b1 = [2, 1]

b2 = [-1, 1]
```

Place these vectors into the columns of a matrix:

```text
B = [ 2  -1 ]
    [ 1   1 ]
```

This matrix is called a basis matrix.

Its columns are the basis vectors expressed in standard coordinates.

### Why put the basis vectors into columns?

Recall the earlier rule for matrix-vector multiplication:

> Multiplying a matrix by a vector forms a linear combination of the matrix's columns, using the vector's coordinates as coefficients.

Therefore, multiplying `B` by a vector of Jennifer's coordinates combines her basis vectors in exactly the right proportions.

The result is the same vector expressed in standard coordinates.

### The fundamental equation

Suppose a vector has coordinates `c` in Jennifer's basis.

```text
c = [c1, c2]
```

Its standard coordinates are:

```text
v = B*c
```

Expanded:

```text
v = c1*b1 + c2*b2
```

This gives us the first essential rule:

**To convert coordinates from Jennifer's basis to standard coordinates, multiply by Jennifer's basis matrix.**

In compact notation:

```text
[v]_standard = B * [v]_B
```

The matrix `B` translates Jennifer's coordinate description into ours.

### Why this feels backwards

Geometrically, the matrix maps the standard basis vectors to Jennifer's basis vectors.

But numerically, it converts Jennifer's coordinates into standard coordinates.

There is no contradiction.

The matrix takes the numerical coefficients and uses them to construct the actual vector from Jennifer's basis vectors, expressed in our coordinates.

---

## 5. Worked Example: Convert Jennifer's Coordinates to Ours

Suppose Jennifer describes a vector using these coordinates:

```text
[v]_B = [2, -3]
```

Her basis vectors are:

```text
b1 = [2, 1]

b2 = [-1, 1]
```

We want to find the vector's standard coordinates.

### Step 1: Write the basis matrix

```text
B = [ 2  -1 ]
    [ 1   1 ]
```

### Step 2: Multiply the basis matrix by Jennifer's coordinates

```text
v = B * [2, -3]
```

Using the columns:

```text
v = 2*b1 - 3*b2
```

Substitute the basis vectors:

```text
v = 2*[2, 1] - 3*[-1, 1]
```

Calculate each term:

```text
2*b1 = [4, 2]

-3*b2 = [3, -3]
```

Add them:

```text
v = [4, 2] + [3, -3]

v = [7, -1]
```

Therefore:

```text
[v]_standard = [7, -1]
```

### Interpretation

Jennifer's coordinates `[2, -3]` do not mean "move 2 units right and 3 units down."

They mean:

- Take 2 copies of her first basis vector.
- Subtract 3 copies of her second basis vector.
- Add the resulting vectors.

The final geometric vector has standard coordinates `[7, -1]`.

---

## 6. Going the Other Way: Standard Coordinates to Jennifer's Coordinates

Now suppose we know the vector's standard coordinates:

```text
v = [3, 2]
```

We want to find its coordinates relative to Jennifer's basis.

We know:

```text
v = B*c
```

where `c` is the unknown coordinate vector in Jennifer's system.

Therefore:

```text
B*c = v
```

If `B` is invertible, multiply both sides by its inverse:

```text
B^(-1) * B * c = B^(-1) * v
```

Since:

```text
B^(-1) * B = I
```

we get:

```text
c = B^(-1) * v
```

This gives us the second essential rule:

**To convert standard coordinates into Jennifer's coordinates, multiply by the inverse of Jennifer's basis matrix.**

In compact notation:

```text
[v]_B = B^(-1) * [v]_standard
```

### Calculate Jennifer's inverse basis matrix

Recall:

```text
B = [ 2  -1 ]
    [ 1   1 ]
```

Its determinant is:

```text
det(B) = (2*1) - (-1*1)

det(B) = 3
```

For a 2×2 matrix:

```text
M = [ a  b ]
    [ c  d ]
```

its inverse, when the determinant is nonzero, is:

```text
M^(-1) = (1 / (a*d - b*c)) * [ d  -b ]
                                   [ -c  a ]
```

Applying this formula gives:

```text
B^(-1) = [  1/3   1/3 ]
         [ -1/3   2/3 ]
```

### Now convert `[3, 2]`

Multiply the inverse by the standard coordinate vector:

```text
c = B^(-1) * [3, 2]
```

The first coordinate is:

```text
c1 = (1/3)*3 + (1/3)*2

c1 = 5/3
```

The second coordinate is:

```text
c2 = (-1/3)*3 + (2/3)*2

c2 = 1/3
```

Therefore:

```text
[v]_B = [5/3, 1/3]
```

This is the same vector previously described by `[3, 2]` in standard coordinates.

### Verify the result

Reconstruct the vector using Jennifer's basis:

```text
v = (5/3)*b1 + (1/3)*b2
```

Substitute:

```text
v = (5/3)*[2, 1] + (1/3)*[-1, 1]
```

Calculate:

```text
v = [10/3, 5/3] + [-1/3, 1/3]

v = [9/3, 6/3]

v = [3, 2]
```

It checks out!

### The two conversion rules

| Conversion | Formula | What it does |
|---|---|---|
| Jennifer's coordinates to standard | `v = B*c` | Reconstructs the vector in standard coordinates |
| Standard coordinates to Jennifer's | `c = B^(-1)*v` | Finds the coefficients relative to Jennifer's basis |

**Memory trick:** The basis matrix builds the vector from the new basis. Its inverse breaks the vector back into coordinates relative to that basis.

---

## 7. Why Must the Basis Matrix Be Invertible?

A valid basis for an `n`-dimensional space contains `n` linearly independent vectors.

Putting these vectors into the columns of a square matrix gives an invertible matrix.

For Jennifer's basis:

```text
det(B) = 3
```

Since the determinant is nonzero, the matrix is invertible.

That means every vector has exactly one coordinate representation in her basis.

Now imagine choosing two basis vectors that point along the same line.

They would be linearly dependent and could not span the entire 2D plane.

The corresponding matrix would have a determinant of zero.

In that case, the matrix would not be invertible, and it would not define a valid basis for the entire 2D space.

This connects directly to earlier chapters:

- **Chapter 2:** Linear independence, span, and basis vectors.
- **Chapter 6:** Determinants and geometric scaling.
- **Chapter 7:** Inverse matrices, column space, and null space.
- **Chapter 12:** Cramer's rule and the role of a nonzero determinant.

Change of basis brings these ideas together into one operation.

---

## 8. Changing the Basis of a Linear Transformation

So far, we've changed how we describe a vector.

But what happens when we want to describe an entire linear transformation using a different basis?

Suppose a transformation is represented by a matrix `M` in standard coordinates.

For example, consider a 90-degree counterclockwise rotation:

```text
M = [ 0  -1 ]
    [ 1   0 ]
```

When we apply `M` to a vector in standard coordinates, we get the rotated vector, also in standard coordinates.

But Jennifer wants to represent this transformation in her own coordinate system.

She wants a matrix that:
1. Accepts coordinates in Jennifer's basis.
2. Applies the rotation.
3. Returns coordinates in Jennifer's basis.

We need to translate between coordinate systems at the beginning and the end.

### Step 1: Start with Jennifer's coordinates

Let the input vector have coordinates `c` in Jennifer's basis.

```text
c = [v]_B
```

### Step 2: Convert the vector to standard coordinates

Use the basis matrix:

```text
v = B*c
```

### Step 3: Apply the transformation

Apply the standard transformation matrix `M`:

```text
w = M*B*c
```

The vector `w` is the transformed vector, expressed in standard coordinates.

### Step 4: Convert the result back to Jennifer's coordinates

Apply the inverse basis matrix:

```text
[w]_B = B^(-1)*M*B*c
```

Since this must work for every input coordinate vector `c`, the matrix representing the transformation in Jennifer's basis is:

```text
M_B = B^(-1) * M * B
```

This is the **change-of-basis formula for a linear transformation**.

It is one of the most important equations in this chapter.

### Why this formula matters

The three matrices perform three different jobs:

| Matrix | Role |
|---|---|
| `B` | Converts input coordinates from Jennifer's basis to standard coordinates |
| `M` | Applies the transformation in standard coordinates |
| `B^(-1)` | Converts the output back into Jennifer's coordinates |

The order matters because matrix multiplication represents composition of transformations.

The rightmost operation happens first.

So:

```text
M_B = B^(-1) * M * B
```

means:

```text
Convert to standard coordinates
        ↓
Apply the transformation
        ↓
Convert back to Jennifer's coordinates
```

---

## 9. Worked Example: A Rotation in Jennifer's Coordinate System

Let's use Jennifer's basis again:

```text
B = [ 2  -1 ]
    [ 1   1 ]
```

Its inverse is:

```text
B^(-1) = [  1/3   1/3 ]
         [ -1/3   2/3 ]
```

The standard matrix for a 90-degree counterclockwise rotation is:

```text
M = [ 0  -1 ]
    [ 1   0 ]
```

We want to find the matrix representing this rotation in Jennifer's coordinates.

### Step 1: Apply the standard rotation to the basis matrix

```text
M*B = [ 0  -1 ] * [ 2  -1 ]
      [ 1   0 ]   [ 1   1 ]
```

Calculate:

```text
M*B = [ -1  -1 ]
      [  2  -1 ]
```

### Step 2: Multiply by the inverse basis matrix

```text
M_B = B^(-1)*M*B
```

Therefore:

```text
M_B = [  1/3   1/3 ] * [ -1  -1 ]
      [ -1/3   2/3 ]   [  2  -1 ]
```

Multiplying gives:

```text
M_B = [  1/3    -2/3 ]
      [  5/3    -1/3 ]
```

This matrix looks quite different from the original rotation matrix.

But both matrices represent the same geometric transformation, just in different coordinate systems.

### What does this tell us?

The original matrix is simple because the standard basis aligns with the familiar horizontal and vertical directions.

Jennifer's basis is tilted relative to those directions, so the same rotation requires a different numerical description.

**The transformation has not changed. Its coordinate representation has changed.**

This is the central distinction between a geometric transformation and the matrix used to represent it.

---

## 10. Similar Matrices: Same Transformation, Different Representation

When two matrices are related by a change-of-basis formula, they are called *similar matrices*.

If:

```text
M_B = B^(-1) * M * B
```

then `M_B` and `M` are similar.

They represent the same underlying linear transformation in different bases.

Similarity is important because it preserves several key properties, including:

- Determinant.
- Trace.
- Characteristic polynomial.
- Eigenvalues.

The individual matrix entries may change, but these properties remain the same.

For example, changing coordinates cannot change the actual scaling of area or volume produced by a linear transformation. That is why the determinant is preserved.

Similarly, the trace remains unchanged because it is the sum of the diagonal entries and is invariant under a change of basis.

This gives us an important mathematical principle:

**Some properties belong to the transformation itself, rather than to the particular matrix used to represent it.**

The matrix entries depend on the coordinate system. The underlying transformation does not.

---

## 11. Why Eigenvectors and Eigenvalues Come Next

The video ends by pointing toward the next chapter, which explores eigenvectors and eigenvalues.

The connection is powerful.

An eigenvector of a linear transformation is a nonzero vector whose direction remains unchanged by that transformation. It may become longer, shorter, or reverse direction.

Its defining equation is:

```text
M*v = lambda*v
```

Here:
- `M` is the transformation matrix.
- `v` is an eigenvector.
- `lambda` is the corresponding eigenvalue.

Why does this matter for change of basis?

Imagine that we can choose a basis made from eigenvectors of a transformation.

In that basis, each basis vector is simply scaled by its corresponding eigenvalue.

If we have enough linearly independent eigenvectors to form a basis, the transformation matrix becomes diagonal.

A diagonal matrix is especially convenient because each coordinate can be scaled independently.

The change-of-basis formula tells us how to obtain that representation.

If the columns of `P` are a suitable set of eigenvectors, then:

```text
D = P^(-1) * M * P
```

where `D` is diagonal.

Equivalently:

```text
M = P * D * P^(-1)
```

This is called **diagonalization**.

Not every matrix can be diagonalized, but when it can, the right basis can turn a complicated transformation into a much simpler one.

That is a major reason change of basis matters beyond introductory linear algebra.

---

## 12. Connections to AI and Machine Learning

Let's connect this to your AI/ML learning path.

### A. Feature representations

In machine learning, data is often represented by vectors of numerical features.

For example:

```text
x = [age, income, experience]
```

These coordinates describe an example relative to a chosen feature representation.

Transforming those features into another coordinate system can sometimes make the underlying structure easier to work with.

However, be careful: not every feature transformation is literally a change of basis. A true change of basis is an invertible linear coordinate transformation within the same vector space.

Feature engineering may involve nonlinear transformations, adding or removing dimensions, and other operations that go beyond change of basis.

### B. Principal Component Analysis

Principal Component Analysis, or PCA, constructs new orthogonal directions that capture as much data variance as possible, in descending order.

In a centered dataset, these directions are eigenvectors of the covariance matrix.

Expressing the data in this new basis gives coordinates called principal component scores.

Why is that useful?

- The first principal component captures the largest possible variance along a single direction.
- The second captures the largest remaining variance while being orthogonal to the first.
- Further components capture progressively smaller amounts of remaining variance.

If we retain all components, PCA's rotation into an orthonormal eigenvector basis is an invertible coordinate transformation.

If we discard components, however, dimensionality is reduced and information may be lost. That is no longer an invertible change of basis.

This is a direct application of the relationship between basis choice and representation.

### C. Neural networks and internal representations

Neural networks repeatedly transform vectors from one representation to another.

A linear layer typically performs an operation of the form:

```text
y = W*x + b
```

Here, `W` transforms the input representation and `b` adds a bias.

A neural network's hidden layers learn useful representations of data. These learned representations are not automatically changes of basis in the strict mathematical sense, since the transformations may change dimensionality or include nonlinear activation functions.

Nevertheless, the central intuition carries over: **the representation used to describe information strongly affects how easily we can process it.**

### D. Eigenvalues and training dynamics

Eigenvalues and eigenvectors help us understand linear systems, covariance matrices, and aspects of optimization.

For example, the eigenvalues of a Hessian matrix describe curvature along particular directions near a point in parameter space.

Directions with very different curvature can make optimization harder. This is one reason conditioning and appropriate parameter scaling matter.

A suitable coordinate system can sometimes make a mathematical problem easier to analyze or solve.

### E. A practical lesson

Change of basis teaches a broader engineering principle:

**Choose a representation that makes the structure of your problem easier to work with, while being clear about what information is preserved.**

This idea appears in PCA, numerical linear algebra, signal processing, computer graphics, and many ML algorithms.

---

## 13. Common Misconceptions

### Misconception 1: Changing the basis changes the vector

Not necessarily.

The geometric vector remains the same. Only its coordinate description changes.

### Misconception 2: Coordinates are meaningful without knowing the basis

Coordinates require a reference basis.

The pair `[1, 0]` represents the first basis vector, whatever that vector happens to be.

### Misconception 3: Every basis must be perpendicular

No.

A basis must be linearly independent and span the space. Perpendicularity is not required.

An orthonormal basis is a particularly convenient special case, but it is not the only valid type of basis.

### Misconception 4: The basis matrix and its inverse do the same thing

They perform opposite coordinate conversions.

```text
Standard coordinates = B * Basis coordinates
```

```text
Basis coordinates = B^(-1) * Standard coordinates
```

### Misconception 5: The formula is `B*M*B^(-1)`

For the convention used in these notes, where the columns of `B` are the new basis vectors expressed in standard coordinates, the formula is:

```text
M_B = B^(-1) * M * B
```

Other formulas may appear when a different matrix convention is used or when solving for a different quantity. Always establish what each matrix represents before multiplying.

### Misconception 6: Different matrices must represent different transformations

No.

Similar matrices can represent the same transformation in different bases.

### Misconception 7: Every matrix can be diagonalized

No.

A matrix can be diagonalized when it has a basis of linearly independent eigenvectors. Some matrices do not have enough independent eigenvectors to form such a basis.

---

## 14. Quick Revision Sheet

| Topic | Essential idea |
|---|---|
| Basis | A linearly independent set that spans the space |
| Coordinates | Coefficients relative to a particular basis |
| Basis matrix | A matrix whose columns are the basis vectors in another coordinate system |
| New basis to standard | Multiply by `B` |
| Standard to new basis | Multiply by `B^(-1)` |
| Invertibility | A valid basis matrix must be invertible |
| Change of basis for a transformation | `M_B = B^(-1)*M*B` |
| Similar matrices | Different representations of the same transformation |
| Eigenvectors | Directions preserved by a transformation, up to scaling |
| Diagonalization | Representing a transformation by a diagonal matrix in a suitable eigenvector basis |

### The three formulas to remember

**1. Convert new-basis coordinates to standard coordinates**

```text
v = B*c
```

**2. Convert standard coordinates to new-basis coordinates**

```text
c = B^(-1)*v
```

**3. Represent a transformation in the new basis**

```text
M_B = B^(-1)*M*B
```

If these three equations make sense to you conceptually, you have grasped the mathematical heart of this chapter.

---

## 15. Self-Test

Try answering these before checking the solutions.

### Question 1: Change of coordinates

Suppose the new basis is:

```text
b1 = [1, 1]

b2 = [1, -1]
```

A vector has coordinates:

```text
c = [3, 2]
```

What are its standard coordinates?

### Question 2: Reverse the conversion

Using the same basis, a vector has standard coordinates:

```text
v = [5, 1]
```

Find its coordinates in the new basis.

### Question 3: Understand the formula

Why do we use the inverse basis matrix when converting standard coordinates into new-basis coordinates?

### Question 4: Transformation matrices

Suppose `M` represents a linear transformation in standard coordinates, and `B` contains the new basis vectors as columns.

What formula represents the same transformation in the new basis?

### Question 5: Conceptual understanding

Two similar matrices have different entries.

How can they still represent the same transformation?

---

## 16. Self-Test Answers

### Answer 1

Construct the basis matrix:

```text
B = [1   1]
    [1  -1]
```

Convert the new-basis coordinates to standard coordinates:

```text
v = B*c
```

Therefore:

```text
v = 3*[1, 1] + 2*[1, -1]

v = [3, 3] + [2, -2]

v = [5, 1]
```

**Answer:** `[5, 1]`

### Answer 2

We know:

```text
v = [5, 1]
```

The inverse basis matrix is:

```text
B^(-1) = [ 1/2   1/2 ]
         [ 1/2  -1/2 ]
```

Convert to the new basis:

```text
c = B^(-1)*v
```

Therefore:

```text
c1 = (1/2)*5 + (1/2)*1 = 3

c2 = (1/2)*5 - (1/2)*1 = 2
```

**Answer:** `[3, 2]`

### Answer 3

The basis matrix converts new-basis coordinates into standard coordinates. Its inverse performs the reverse operation, recovering the coefficients relative to the new basis.

### Answer 4

```text
M_B = B^(-1)*M*B
```

The matrix converts the input to standard coordinates, applies the transformation, and converts the output back to the new basis.

### Answer 5

The matrices describe the same underlying linear transformation using different coordinate systems. Their numerical entries differ because the basis vectors used to describe inputs and outputs differ.

---

## 17. Final Takeaway

The central idea of this chapter is simple, but it changes how you think about matrices.

**A matrix is not the transformation itself in isolation. It is a representation of that transformation relative to a choice of basis.**

For vectors, the basis determines what the coordinates mean.

For transformations, the basis determines how the transformation is represented numerically.

And when we choose a useful basis, we can sometimes turn a complicated mathematical problem into a much simpler one.

That is the bridge to eigenvectors, eigenvalues, and diagonalization, which are coming up next.

**Your checkpoint:** Make sure you can derive `v = B*c`, reverse it to `c = B^(-1)*v`, and explain why the transformation formula is `M_B = B^(-1)*M*B`. Do not just memorize the equations. Be able to explain what each matrix is doing.

Next up: **Chapter 14, Eigenvectors and Eigenvalues.**
