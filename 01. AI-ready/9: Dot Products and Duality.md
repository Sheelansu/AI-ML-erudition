# Essence of Linear Algebra, Chapter 9
## Dot Products and Duality

**Source:** [3Blue1Brown, Chapter 9](https://www.youtube.com/watch?v=LyGKycYT2v0)

## 1. The dot product: one operation, two vectors, one number

So far, we have worked with vectors as objects that have both magnitude and direction. We have added vectors, scaled them, and transformed them using matrices.

Now we introduce an operation that takes **two vectors and returns a single number**: the dot product.

The dot product is written using a centered dot:

```text
v · w
```

If two vectors have the same number of coordinates, multiply corresponding coordinates and add the results.

For example:

```text
v = [1]
    [2]

w = [3]
    [4]
```

Their dot product is:

```text
v · w = (1*3) + (2*4)
      = 3 + 8
      = 11
```

For vectors with `n` coordinates:

```text
v = [v1, v2, ..., vn]
w = [w1, w2, ..., wn]
```

the formula is:

```text
v · w = v1*w1 + v2*w2 + ... + vn*wn
```

This is the **algebraic definition** of the dot product.

But why should multiplying corresponding coordinates and adding them tell us something useful about the geometry of two vectors?

That is the real question of this chapter.

---

## 2. The geometric meaning: projection and alignment

Imagine two vectors, `v` and `w`, starting at the origin.

Draw a line through the origin in the direction of `v`. Now project `w` onto that line.

The projection tells you how much of `w` lies along the direction of `v`.

The dot product is the signed length of this projection multiplied by the length of `v`.

```text
v · w = |v| * signed_projection_length_of_w_onto_v
```

The word **signed** matters. The projection is positive if it points in the same direction as `v`, and negative if it points in the opposite direction.

This gives us a geometric interpretation of the dot product.

### Case 1: vectors point in similar directions

If `v` and `w` point in broadly the same direction, the projection of `w` onto `v` is positive.

```text
v · w > 0
```

The dot product is positive.

### Case 2: vectors are perpendicular

If `v` and `w` are perpendicular, the projection of one onto the other is zero.

```text
v · w = 0
```

The dot product is zero.

### Case 3: vectors point in opposing directions

If the projection of `w` onto `v` points opposite to `v`, its signed length is negative.

```text
v · w < 0
```

The dot product is negative.

### The angle formula

If `theta` is the angle between two nonzero vectors, then:

```text
v · w = |v| * |w| * cos(theta)
```

This formula connects the algebraic calculation to geometry.

Why cosine? Because the length of the projection of `w` onto `v` is:

```text
projection_length = |w| * cos(theta)
```

Multiplying that by `|v|` gives:

```text
v · w = |v| * |w| * cos(theta)
```

This is one of the most important formulas in introductory linear algebra.

### A few useful consequences

If the vectors point in exactly the same direction, the angle is zero and the cosine is 1.

```text
theta = 0 degrees
v · w = |v| * |w|
```

If they are perpendicular, the cosine is zero.

```text
theta = 90 degrees
v · w = 0
```

If they point in opposite directions, the cosine is -1.

```text
theta = 180 degrees
v · w = -|v| * |w|
```

**Important:** a zero dot product means perpendicular vectors only when using the standard Euclidean dot product and interpreting the vectors in that usual geometric setting. If either vector is the zero vector, its dot product with every vector is zero, but the zero vector has no defined direction.

---

## 3. Worked example: calculating alignment

Consider:

```text
v = [4]
    [6]

w = [-3]
    [ 2]
```

The dot product is:

```text
v · w = (4*(-3)) + (6*2)
      = -12 + 12
      = 0
```

The vectors are perpendicular.

Notice that their coordinates do not need to be zero, and neither vector needs to be horizontal or vertical. The dot product detects perpendicularity even when the vectors point in arbitrary directions.

Now consider:

```text
a = [1]
    [2]

b = [3]
    [4]
```

Then:

```text
a · b = (1*3) + (2*4)
      = 11
```

The positive result indicates that the vectors have a positive alignment.

However, the dot product alone does not tell us the angle unless we also know the magnitudes of both vectors.

To calculate the angle:

```text
cos(theta) = (v · w) / (|v|*|w|)
```

Then:

```text
theta = arccos((v · w) / (|v|*|w|))
```

This is a useful way to compare the directions of vectors independently of their lengths.

---

## 4. Why does the dot product scale linearly?

Consider multiplying `v` by 2.

```text
(2v) · w = 2(v · w)
```

The dot product doubles.

Why? Geometrically, the direction of `v` has not changed, but its length has doubled. The projection of `w` onto the direction of `v` stays the same, while the length multiplying that projection doubles.

The same applies if we scale `w` instead:

```text
v · (2w) = 2(v · w)
```

Both sides of the dot product behave symmetrically.

The dot product is also additive:

```text
(u + v) · w = (u · w) + (v · w)
```

And it is commutative:

```text
v · w = w · v
```

These properties follow from the coordinate formula and match its geometric interpretation.

The important distinction is that the dot product is not a vector-valued operation. It takes vectors as inputs but returns a scalar, meaning a single number.

---

## 5. The deeper puzzle: why does the coordinate formula match projection?

So far, we have two descriptions:

**Algebraically:** multiply matching coordinates and add.

```text
v · w = v1*w1 + v2*w2 + ... + vn*wn
```

**Geometrically:** multiply the length of one vector by the signed length of the projection of the other onto it.

```text
v · w = |v| * |w| * cos(theta)
```

Why are these the same operation?

The video approaches this question using linear transformations from a higher-dimensional space to the number line.

This is where the concept of **duality** enters.

---

## 6. Linear transformations from 2D to 1D

In Chapter 8, we learned that a rectangular matrix can transform a vector from one dimension to another.

A 1 × 2 matrix takes a 2D vector and produces a single number.

For example:

```text
A = [3  2]

x = [x]
    [y]
```

Multiplying them gives:

```text
A*x = 3x + 2y
```

This is a linear transformation from the plane to the number line.

```text
T: R^2 -> R
```

It takes a point `(x, y)` and assigns it a scalar.

The transformation is fully determined by where the two standard basis vectors land.

Recall:

```text
i = [1]       j = [0]
    [0]           [1]
```

Then:

```text
T(i) = 3
T(j) = 2
```

These two numbers become the entries of the 1 × 2 matrix.

This is a general principle: a linear transformation from `R^n` to `R` is completely determined by its values on the `n` standard basis vectors.

---

## 7. A geometric way to create a transformation to the number line

Imagine projecting every point in the plane onto a particular line through the origin.

Then interpret its position along that line as a single number.

As you move through the plane, each point receives a scalar output.

This creates a transformation:

```text
T: R^2 -> R
```

If the transformation is linear, it can be represented by a 1 × 2 matrix.

For instance:

```text
T([x]) = 3x + 2y
  ([y])
```

The output depends on how much of the input lies along the directions associated with the transformation.

There is a useful geometric picture here: the transformation groups points according to their scalar output. Every point with the same output lies on a line perpendicular to the direction that determines the projection.

For the example:

```text
T(x, y) = 3x + 2y
```

all points that produce the same number `c` satisfy:

```text
3x + 2y = c
```

These are parallel lines. The transformation assigns one scalar to each such line.

The set of points producing zero satisfies:

```text
3x + 2y = 0
```

This is the null space of the transformation, as introduced in Chapter 7.

---

## 8. The connection: a 1 × n matrix is a vector turned sideways

Consider a linear transformation:

```text
T: R^n -> R
```

It must be represented by a 1 × n matrix.

For example:

```text
A = [a1  a2  a3]
```

Apply it to a vector:

```text
w = [w1]
    [w2]
    [w3]
```

The output is:

```text
A*w = a1*w1 + a2*w2 + a3*w3
```

Now imagine turning the row of matrix entries into a column vector:

```text
v = [a1]
    [a2]
    [a3]
```

The multiplication above is exactly the dot product:

```text
v · w = a1*w1 + a2*w2 + a3*w3
```

Therefore:

```text
T(w) = v · w
```

This is the key connection.

Every linear transformation from a vector space of finite dimension `n` to the real numbers can be represented by taking the dot product with a particular vector.

That vector encodes the transformation.

**A vector can be understood not only as an arrow in space, but also as a machine that takes another vector and returns a number.**

This is the central insight of the chapter.

---

## 9. Duality: one mathematical object, two viewpoints

Duality is a broad mathematical idea in which two different types of objects correspond to each other in a natural and useful way.

In this chapter, the two types of objects are:

1. Vectors.
2. Linear transformations from vectors to scalars.

The dot product creates the connection.

Given a vector `v`, we can define a transformation:

```text
T_v(w) = v · w
```

This transformation accepts any compatible vector `w` and returns a scalar.

Conversely, every linear functional on a finite-dimensional real vector space equipped with the standard dot product can be represented by a unique vector in this way.

A **linear functional** is simply a linear transformation whose output is a scalar.

So, under the standard dot product, we can think of a vector and its associated linear functional as two representations of the same underlying mathematical information.

### Example

Let:

```text
v = [2]
    [5]
```

Define:

```text
T_v(w) = v · w
```

For:

```text
w = [3]
    [4]
```

we get:

```text
T_v(w) = (2*3) + (5*4)
       = 6 + 20
       = 26
```

The vector `(2, 5)` has defined a transformation that maps `(3, 4)` to the scalar `26`.

The same vector can be viewed in two ways:

- As an arrow pointing in the plane.
- As a rule that evaluates other vectors and returns numbers.

That is duality in action.

### A useful mathematical qualification

The correspondence between vectors and linear functionals depends on the chosen inner product or an equivalent identification. In ordinary Euclidean space with the standard dot product, the correspondence is especially natural. In more abstract vector spaces, vectors and linear functionals are distinct types of objects, even when they can be put into one-to-one correspondence.

---

## 10. Why this matters in AI and machine learning

The dot product is one of the most frequently used operations in machine learning.

### A. Neurons calculate weighted combinations

A simple artificial neuron computes something like:

```text
z = w1*x1 + w2*x2 + ... + wn*xn + b
```

This can be rewritten as:

```text
z = w · x + b
```

The weights form a vector. The input features form another vector. Their dot product produces a scalar, and the bias shifts that scalar.

An activation function may then transform the result:

```text
output = activation(w · x + b)
```

For example, a neuron might receive hundreds of input features and produce a single score.

This is precisely the kind of vector-to-scalar transformation discussed in this chapter.

### B. Similarity between embeddings

Suppose two words, images, or documents are represented by vectors.

Their dot product gives a measure of alignment that depends on both direction and magnitude.

```text
similarity_score = embedding_A · embedding_B
```

A larger positive dot product often indicates stronger alignment, but raw dot products are not automatically normalized similarity scores. Large vector magnitudes can produce large values even when the angle between vectors stays unchanged.

For a direction-focused comparison, cosine similarity is often used:

```text
cosine_similarity(A, B) =
    (A · B) / (|A| * |B|)
```

Cosine similarity ranges from -1 to 1 for nonzero real vectors.

- `1` means they point in the same direction.
- `0` means they are perpendicular.
- `-1` means they point in opposite directions.

In practical embedding systems, similarity scores also depend on how the embeddings were trained and what geometry the model learned.

### C. Attention in transformers

In transformer models, query and key vectors are compared using dot products.

A simplified attention score is:

```text
score = query · key
```

The score measures how strongly those vectors align under the learned representation.

In scaled dot-product attention, the score is divided by the square root of the key dimension:

```text
score = (query · key) / sqrt(d_k)
```

The scores are then typically passed through softmax to obtain attention weights.

This is a direct use of dot products as vector-to-scalar functions.

### D. Linear classifiers

A linear classifier can calculate:

```text
score = w · x + b
```

The sign or magnitude of the score helps determine the predicted class, depending on the classifier.

Geometrically, the decision boundary is:

```text
w · x + b = 0
```

In ordinary Euclidean geometry, this describes a hyperplane perpendicular to `w`.

The vector `w` therefore does more than represent a direction. It encodes a rule for evaluating points and separating regions of the input space.

---

## 11. Common misconceptions

**Misconception 1: A dot product returns another vector.**

No. A dot product returns a scalar.

**Misconception 2: A positive dot product means the vectors point in exactly the same direction.**

No. It means the angle between nonzero vectors is less than 90 degrees. The vectors can still point in noticeably different directions.

**Misconception 3: A zero dot product always means one vector is zero.**

No. Two nonzero vectors can have a zero dot product when they are perpendicular.

**Misconception 4: The dot product only makes sense as a coordinate calculation.**

The coordinate calculation is one way to compute it. Its geometric interpretation is about projection and alignment.

**Misconception 5: A vector and a linear functional are literally the same kind of object.**

They are different kinds of mathematical objects, but the standard dot product gives a natural correspondence between them in finite-dimensional Euclidean space.

**Misconception 6: A large dot product always means high similarity.**

Not necessarily. Dot products depend on vector magnitudes as well as angles. If you want to compare direction independently of magnitude, consider cosine similarity.

---

## 12. Quick revision sheet

| Concept | Key idea |
|---|---|
| Dot product | Multiply corresponding coordinates and add |
| Geometric meaning | Length of one vector times the signed projection of the other |
| Positive dot product | Nonzero vectors point at an angle smaller than 90 degrees |
| Zero dot product | Nonzero vectors are perpendicular |
| Negative dot product | Nonzero vectors point at an angle greater than 90 degrees |
| Angle formula | `v · w = |v|*|w|*cos(theta)` |
| Linear functional | A linear transformation that returns a scalar |
| 1 × n matrix | Represents a linear transformation from `R^n` to `R` |
| Duality | A vector corresponds to a linear functional through the dot product |
| Neural network neuron | Computes a weighted sum, commonly `w · x + b` |
| Cosine similarity | Normalizes the dot product by both vector magnitudes |

### The four equations to remember

```text
v · w = v1*w1 + v2*w2 + ... + vn*wn
```

The coordinate formula.

```text
v · w = |v|*|w|*cos(theta)
```

The geometric formula.

```text
T_v(w) = v · w
```

A vector defines a linear transformation from vectors to scalars.

```text
z = w · x + b
```

A common form of the weighted sum calculated by a neuron.

---

## 13. Self-test

**Q1.** Calculate the dot product of `(2, 3)` and `(4, -1)`.

**Q2.** What does a negative dot product tell you about two nonzero vectors?

**Q3.** Two nonzero vectors have a dot product of zero. What can you conclude?

**Q4.** A vector `v` has three coordinates. What shape of matrix represents the associated linear functional `T_v(w) = v · w`?

**Q5.** Why is a dot product useful for comparing embedding vectors?

**Q6.** What is the geometric interpretation of the equation `w · x + b = 0`?

**Q7.** Why can a large dot product be misleading as a similarity measure?

### Answers

**A1.**

```text
(2*4) + (3*(-1)) = 8 - 3 = 5
```

**A2.** The angle between them is greater than 90 degrees, so they have negative alignment.

**A3.** They are perpendicular under the standard Euclidean dot product.

**A4.** A 1 × 3 row matrix.

**A5.** It gives a scalar score that measures alignment while taking vector magnitudes into account. Cosine similarity can be used when magnitude-independent directional comparison is desired.

**A6.** It defines a hyperplane whose normal vector is `w`.

**A7.** The dot product depends on both direction and magnitude. Two vectors with the same angle can have very different dot products if their lengths differ.

---

## Final takeaway

The dot product starts as a simple arithmetic rule: multiply matching coordinates and add.

But its deeper meaning is geometric. It measures alignment through projection, and it can turn a vector into a linear transformation that evaluates other vectors.

That is the chapter's central insight:

**A vector is not only an arrow. Through the dot product, it can also represent a rule that converts vectors into numbers.**

This connection will be useful in neural networks, embedding similarity, attention mechanisms, and linear classification.

Next up: **Chapter 10, “Cross Products.”** We will move from measuring alignment with a scalar to constructing a vector perpendicular to two others.
