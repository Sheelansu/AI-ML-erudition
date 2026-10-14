# Essence of Linear Algebra: Chapter 1
## Video 1: Vectors | 3Blue1Brown

**Video:** [Vectors | Essence of Linear Algebra, Chapter 1](https://www.youtube.com/watch?v=fNk_zzaMoSs)

**Playlist:** [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

---

## 1. What Is a Vector?

A **vector is a fundamental building block of linear algebra**. It can be understood from three related perspectives.

### 1.1 Physics perspective

A vector is represented geometrically as an arrow with a magnitude (length) and direction.

Examples:
- Displacement: moving 3 units right and 2 units up.
- Velocity: the speed and direction of a moving object.
- Force: the magnitude and direction of a push or pull.

Two arrows represent the same vector if they have the same magnitude and direction, even when drawn at different positions.

**Important:** A vector describes a displacement or other directed quantity, not necessarily a fixed location.

### 1.2 Computer science perspective

A vector is represented as an ordered list of numbers.

Example:

```text
v = [3, 2]
```

This vector contains two components:
- First component: 3
- Second component: 2

The order matters. `[3, 2]` and `[2, 3]` are different vectors.

In data analysis, a vector might represent a house using two features:

```text
house = [2600, 300000]
```

Here:
- 2600 = area in square feet
- 300000 = price in dollars

This is a two-dimensional vector because it contains two numerical components.

### 1.3 Mathematical perspective

Mathematics generalizes both interpretations.

A vector is an object for which we can define operations such as:
- Vector addition
- Scalar multiplication

More abstract vector spaces can contain objects other than arrows or lists of numbers, provided they satisfy the required mathematical rules.

For now, focus on arrows and numerical lists. These concrete interpretations provide the foundation for understanding the abstract definition.

---

## 2. Two-Dimensional and Three-Dimensional Vectors

### 2.1 Two-dimensional vectors (2D)

A 2D vector has two components and can be visualized in a plane.

Example:

```text
v = [3, 2]
```

Geometrically, this represents:
- 3 units horizontally to the right
- 2 units vertically upward

The arrow starts at the origin `(0, 0)` and ends at `(3, 2)`.

### 2.2 Three-dimensional vectors (3D)

A 3D vector has three components.

Example:

```text
v = [3, 2, 4]
```

The components describe displacement along three independent axes:
- x-axis: 3 units
- y-axis: 2 units
- z-axis: 4 units

The third axis allows us to represent positions and displacements in three-dimensional space.

### 2.3 The general pattern

A vector can contain any number of components.

```text
v = [v1, v2, ..., vn]
```

This is an n-dimensional vector.

**Key takeaway:** In a coordinate representation, the dimension of a vector is the number of components it contains.

For example:
- `[3, 2]` is 2D.
- `[3, 2, 4]` is 3D.
- A list of 100 numbers represents a vector in 100-dimensional space.

We cannot directly visualize a 100-dimensional vector as an ordinary arrow in physical 3D space, but we can still represent and manipulate it mathematically.

---

## 3. Coordinates: Connecting Geometry and Numbers

Coordinates provide the bridge between a vector's geometric and numerical representations.

Consider:

```text
v = [3, 2]
```

The coordinates tell us how to travel from the origin to the arrow's tip:
- First coordinate: horizontal displacement.
- Second coordinate: vertical displacement.

### 3.1 Positive and negative coordinates

| Coordinate | Geometric meaning |
|---|---|
| Positive x | Move right |
| Negative x | Move left |
| Positive y | Move upward |
| Negative y | Move downward |

Examples:

```text
a = [-3, 2]
```

Move 3 units left and 2 units up.

```text
b = [3, -2]
```

Move 3 units right and 2 units down.

### 3.2 Points versus vectors

A point such as `(3, 2)` identifies a location in the coordinate plane.

A vector such as `[3, 2]` can represent the displacement from the origin to that point.

Although they are closely related, points and vectors are conceptually different:
- A point identifies a location.
- A vector represents a displacement or an element of a vector space.

In the usual geometric interpretation, an arrow can be moved parallel to itself without changing the vector it represents.

For example, arrows with the same displacement represent the same vector even if their tails are at different locations.

### 3.3 The one-to-one correspondence

In a standard coordinate system:
- Every pair of real numbers identifies one 2D vector.
- Every 2D vector has a unique pair of coordinates relative to the chosen coordinate system.

The same principle applies to 3D vectors and ordered triples of coordinates.

This correspondence allows us to switch between visual reasoning and numerical computation.

---

## 4. Vector Addition

Vector addition combines two displacements into one overall displacement.

Suppose we have:

```text
a = [1, 2]
b = [3, -1]
```

### 4.1 Geometric interpretation: Tip-to-tail method

To add two vectors:

1. Draw the first vector.
2. Move the second vector so that its tail begins at the tip of the first.
3. Draw a new arrow from the original starting point to the final tip.

The resulting arrow represents the sum.

Think of it as taking two consecutive steps. The sum represents the single displacement that takes you from the starting point to the same final destination.

### 4.2 Numerical interpretation: Add corresponding components

```text
a = [1, 2]
b = [3, -1]

a + b = [1 + 3, 2 + (-1)]
      = [4, 1]
```

The combined displacement is 4 units right and 1 unit up.

### 4.3 General formula

```text
a = [a1, a2, ..., an]
b = [b1, b2, ..., bn]

a + b = [a1 + b1, a2 + b2, ..., an + bn]
```

**Rule:** Add corresponding components.

Both vectors must have the same dimension for this standard addition operation to be defined.

### 4.4 Connection to ordinary number addition

Ordinary addition can be interpreted as movement along a number line.

```text
2 + 5 = 7
```

Start at 0, move 2 units right, and then move another 5 units right. The overall displacement is 7 units.

Vector addition extends this idea to multiple dimensions, where each component describes displacement along a different axis.

Adding corresponding coordinates combines the displacement along each axis.

---

## 5. Scalar Multiplication

A **scalar** is an ordinary number used to multiply a vector.

Scalar multiplication changes the magnitude of a vector and may reverse its direction.

Consider:

```text
v = [3, 2]
```

### 5.1 Multiplication by a positive scalar greater than 1

```text
2*v = [2*3, 2*2]
    = [6, 4]
```

The vector becomes twice as long while retaining its direction.

### 5.2 Multiplication by a fraction between 0 and 1

```text
(1/3)*v = [(1/3)*3, (1/3)*2]
        = [1, 2/3]
```

The vector becomes one-third as long, retaining its direction.

### 5.3 Multiplication by a negative scalar

```text
-2*v = [-2*3, -2*2]
     = [-6, -4]
```

Two things happen:
- The direction reverses.
- The magnitude doubles.

### 5.4 Multiplication by zero

```text
0*v = [0, 0]
```

The result is the zero vector, which has zero magnitude.

### 5.5 General formula

```text
v = [v1, v2, ..., vn]

c*v = [c*v1, c*v2, ..., c*vn]
```

Here, `c` is a scalar.

Multiply every component of the vector by the scalar.

### 5.6 Scalar multiplication at a glance

| Scalar | Effect on a nonzero vector |
|---|---|
| `c > 1` | Stretches the vector |
| `0 < c < 1` | Shrinks the vector |
| `c = 1` | Leaves it unchanged |
| `c = 0` | Produces the zero vector |
| `c < 0` | Reverses direction and scales magnitude |

**Important distinction:** Scalar multiplication does not generally rotate a vector by an arbitrary angle. A negative scalar reverses its direction, equivalent to a 180-degree turn in the geometric picture.

---

## 6. The Two Fundamental Operations of Linear Algebra

This first video introduces two fundamental operations.

### Operation 1: Vector addition

```text
a + b
```

Combines two vectors into a new vector.

### Operation 2: Scalar multiplication

```text
c*v
```

Scales a vector by a number.

Together, these operations let us construct **linear combinations** of vectors.

### 6.1 Linear combinations

A linear combination combines vectors after multiplying each by a scalar.

General form:

```text
result = alpha*a + beta*b
```

Example:

```text
a = [1, 2]
b = [3, 4]

2*a = [2, 4]
3*b = [9, 12]

2*a - 3*b = [2, 4] - [9, 12]
          = [-7, -8]
```

You can think of this as:
1. Scale the first vector.
2. Scale the second vector.
3. Add the resulting vectors.

Linear combinations become central to understanding span, basis vectors, linear independence, and matrix transformations in later chapters.

---

## 7. Why the Two Perspectives Matter

One of the most important lessons in the video is that linear algebra becomes much more intuitive when we translate between geometric and numerical representations.

### 7.1 Geometry to numbers

Suppose you visualize an arrow moving right and upward.

You can describe the displacement numerically using its coordinates.

This gives us a mathematical language for representing spatial relationships and manipulating them computationally.

### 7.2 Numbers to geometry

Suppose a computer stores the following vector:

```text
v = [3, 2]
```

Instead of seeing only a list, interpret it as an arrow.

You immediately gain a geometric understanding of its direction and magnitude.

Likewise, vector addition becomes a visual combination of movements rather than just arithmetic on lists.

### 7.3 Why this is useful

**For computer scientists and machine learning engineers:**
- Numerical data can be interpreted geometrically.
- Geometric reasoning can help reveal patterns and relationships in data.
- Mathematical operations on data gain intuitive interpretations.

**For physicists and computer graphics programmers:**
- Positions, movements, and spatial relationships can be represented numerically.
- Computers can calculate these representations and use the results to simulate physical systems or render graphics.

The real power lies in moving fluently between both views.

---

## 8. Connection to AI and Machine Learning

The video does not teach machine learning directly, but its concepts establish important foundations for it.

### 8.1 Representing data as vectors

A data point can be represented by a list of numerical features.

For example:

```text
x = [age, income, experience]
```

In an actual dataset, these entries would be numerical values.

Each component represents one feature, and the entire vector represents one data point.

### 8.2 Representing embeddings

AI systems often represent words, sentences, images, and other objects using vectors called **embeddings**.

An embedding might contain hundreds or thousands of numbers.

```text
embedding = [e1, e2, e3, ..., en]
```

These vectors can be processed mathematically. Their geometric relationships can sometimes reveal useful patterns in learned representations.

An embedding is not necessarily a physical arrow. It is a high-dimensional numerical representation whose geometry becomes meaningful through how the model learns and uses it.

### 8.3 Vector operations in AI

The ideas introduced in this video underpin more advanced operations:

- **Addition:** Combining vector representations or intermediate results.
- **Scalar multiplication:** Rescaling vector components.
- **Linear combinations:** Combining multiple vectors using numerical weights.
- **Geometric reasoning:** Understanding concepts such as similarity and direction in vector spaces.

Later, you will encounter dot products, matrices, linear transformations, and other operations that make these ideas more powerful.

---

## 9. Common Misconceptions to Avoid

1. **A vector is not merely an arrow.** An arrow is its geometric representation; an ordered list is its numerical representation.
2. **A vector is not an unordered collection of numbers.** Component order matters.
3. **Dimension is not magnitude.** A 3D vector has three components, but its length can be any nonnegative value.
4. **The drawing position does not determine a vector's identity.** In the usual geometric interpretation, arrows with the same displacement represent the same vector.
5. **Vector addition is not arbitrary list addition.** Corresponding components are added, and the vectors must have compatible dimensions.
6. **Scalar multiplication affects every component.** It scales the vector as a whole.
7. **A vector's dimension does not have to be 2 or 3.** Machine learning frequently uses vectors with hundreds or thousands of components.
8. **A vector is not automatically a physical quantity.** It can represent abstract data just as naturally as displacement or force.
9. **A point and a vector are not identical concepts.** A point represents a location, whereas a vector represents a displacement or an element of a vector space.

---

## 10. Quick Revision Sheet

| Concept | Definition |
|---|---|
| Vector | An object represented here as an arrow or ordered list of numbers |
| Component | One entry in a vector |
| 2D vector | A vector with two components |
| 3D vector | A vector with three components |
| Coordinates | Numbers describing a vector relative to chosen axes |
| Origin | The point where the coordinate axes intersect |
| Vector addition | Add corresponding components |
| Scalar | A number used to multiply a vector |
| Scalar multiplication | Multiply every component by the scalar |
| Zero vector | A vector whose components are all zero |
| Magnitude | The length of a geometric vector |
| Dimension | Number of components in the coordinate representation |
| Linear combination | A sum of vectors multiplied by scalars |

### Essential formulas

**Vector addition**

```text
a = [a1, a2, ..., an]
b = [b1, b2, ..., bn]

a + b = [a1+b1, a2+b2, ..., an+bn]
```

**Scalar multiplication**

```text
v = [v1, v2, ..., vn]

c*v = [c*v1, c*v2, ..., c*vn]
```

**Linear combination**

```text
result = alpha*a + beta*b
```

**Magnitude of a 2D vector**

For a vector `v = [x, y]`:

```text
|v| = sqrt(x^2 + y^2)
```

Example:

```text
v = [3, 4]

|v| = sqrt(3^2 + 4^2)
    = sqrt(9 + 16)
    = 5
```

Note: The magnitude formula is included as a useful supporting concept. The primary focus of this video is the meaning of vectors, vector addition, scalar multiplication, and the translation between geometric and numerical perspectives.

---

## 11. Self-Test

Try answering these questions without looking at the notes.

1. What are the three perspectives on vectors?
2. What does the vector `[-4, 3]` represent geometrically?
3. Calculate `[2, 5] + [3, -2]`.
4. Calculate `3*[-2, 4]`.
5. What happens geometrically when a vector is multiplied by `-1`?
6. Why do we add corresponding components when adding vectors?
7. Why is translating between geometric and numerical representations useful in computer science?
8. How can a high-dimensional vector represent a data point in machine learning?
9. What is the difference between a point and a vector?
10. What is a linear combination?

### Answers

1. Physics: arrows in space. Computer science: ordered lists of numbers. Mathematics: abstract objects supporting vector addition and scalar multiplication under the rules of a vector space.
2. Four units left and three units up.
3. `[5, 3]`.
4. `[-6, 12]`.
5. Its direction reverses while its magnitude remains unchanged.
6. Each component describes displacement along a particular coordinate axis, so adding corresponding components combines the displacement along each axis.
7. It lets us use visual intuition to understand numerical data and use numerical computation to manipulate geometric objects.
8. Each component can encode a numerical feature or a learned dimension of the representation.
9. A point identifies a location, whereas a vector represents a displacement or an element of a vector space.
10. A linear combination is a sum of vectors multiplied by scalars, such as `2*a - 3*b`.

---

## Final Takeaway

**A vector is the bridge between numbers and geometry.**

You can think of it as an arrow representing displacement or as an ordered list of numerical components.

- Vector addition combines displacements.
- Scalar multiplication stretches, shrinks, or reverses vectors.
- Coordinates translate geometric objects into numerical representations.
- The same ideas extend naturally to high-dimensional data used in AI and machine learning.

The most valuable habit to develop from this first video is to look at vectors in both ways: **visualize what the numbers mean geometrically, then understand how that geometry translates back into computation.**

That habit will serve you throughout linear algebra and deep learning.
