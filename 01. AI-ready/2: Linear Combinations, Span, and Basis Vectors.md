# Essence of Linear Algebra: Chapter 2
## Linear Combinations, Span, and Basis Vectors

**Video:** [Linear combinations, span, and basis vectors | 3Blue1Brown](https://www.youtube.com/watch?v=k7RM-ot2NWY)

**Playlist:** [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

---

## 1. Recap: Building on Chapter 1

In the previous chapter, we learned that a vector can be interpreted geometrically as an arrow or numerically as an ordered list of numbers.

We also learned two fundamental operations:

1. Vector addition
2. Scalar multiplication

These two operations are the foundation of this chapter.

The central question now becomes:

**If we are given a collection of vectors, what other vectors can we create using only addition and scalar multiplication?**

To answer this question, we need to understand linear combinations, span, and basis vectors.

---

## 2. Basis Vectors and Coordinates

### 2.1 Standard basis vectors

In the standard 2D coordinate system, we use two special vectors:

```text
i = [1, 0]
j = [0, 1]
```

These are called the standard basis vectors.

- `i` points one unit along the x-axis.
- `j` points one unit along the y-axis.

Each vector has length 1, and they point in perpendicular directions.

### 2.2 Representing any 2D vector using basis vectors

Consider:

```text
v = [3, 2]
```

This vector can be constructed by taking three copies of `i` and two copies of `j`.

```text
v = 3*i + 2*j
```

Expanding the expression:

```text
v = 3*[1, 0] + 2*[0, 1]

  = [3, 0] + [0, 2]

  = [3, 2]
```

This gives us a new interpretation of coordinates.

**The coordinates of a vector tell us how much to scale each standard basis vector before adding them together.**

For example:

```text
v = [5, -3]

v = 5*i - 3*j
```

This means five units along the x-axis and three units in the negative y-direction.

### 2.3 Why this matters

Previously, we treated coordinates as numbers that directly describe a vector's displacement.

Now we can interpret those same numbers as coefficients that scale special vectors.

These are two ways of describing the same construction.

This idea becomes especially important when we move beyond the standard coordinate system and start using different basis vectors.

---

## 3. Linear Combinations

### 3.1 Definition

A linear combination is an expression formed by multiplying vectors by scalars and then adding the results.

For two vectors:

```text
result = a*v + b*w
```

Here:
- `v` and `w` are vectors.
- `a` and `b` are scalars.
- `a*v` and `b*w` are scaled vectors.
- Their sum is the resulting vector.

The scalars can be positive, negative, or zero.

### 3.2 Example

Suppose:

```text
v = [2, 1]
w = [1, 3]
```

Consider the linear combination:

```text
result = 2*v + 3*w
```

First, scale each vector:

```text
2*v = [4, 2]
3*w = [3, 9]
```

Then add them:

```text
result = [4, 2] + [3, 9]
       = [7, 11]
```

Therefore:

```text
2*[2, 1] + 3*[1, 3] = [7, 11]
```

### 3.3 Geometric interpretation

Imagine two arrows originating at the same point.

You can:
1. Stretch or shrink the first arrow.
2. Stretch or shrink the second arrow.
3. Reverse either arrow by multiplying it by a negative scalar.
4. Add the resulting arrows.

The final arrow is the linear combination.

By changing the scalars, you can generate different vectors from the same starting pair.

### 3.4 What happens when a coefficient is zero?

Suppose:

```text
result = 0*v + 2*w
```

Since `0*v` is the zero vector:

```text
result = 2*w
```

The vector `v` contributes nothing.

This is useful because it means a linear combination does not have to use every available vector with a nonzero coefficient.

### 3.5 Linear combinations of more than two vectors

The same idea extends to any finite number of vectors.

```text
result = a*v1 + b*v2 + c*v3
```

More generally:

```text
result = c1*v1 + c2*v2 + ... + cn*vn
```

This is one of the most important patterns in linear algebra.

Many operations involving vectors and matrices can be understood through combinations of scaled vectors.

---

## 4. Span: What Can a Collection of Vectors Generate?

### 4.1 Definition

The **span** of a collection of vectors is the set of all vectors that can be produced by taking their linear combinations.

For two vectors:

```text
span(v, w) = all vectors of the form a*v + b*w
```

The scalars `a` and `b` can take any real values.

In plain English:

**Span asks: What destinations can I reach if I can scale these vectors and add them together?**

The answer depends on the directions of the supplied vectors.

### 4.2 Case 1: Two non-collinear vectors in 2D

Consider:

```text
v = [1, 0]
w = [0, 1]
```

These vectors point in different, perpendicular directions.

Any 2D vector can be constructed using them:

```text
target = [x, y]

target = x*v + y*w
```

For example:

```text
target = [4, -2]

target = 4*[1, 0] - 2*[0, 1]

       = [4, 0] + [0, -2]

       = [4, -2]
```

In fact, any two non-collinear vectors in 2D span the entire 2D plane.

The standard basis vectors are just one particularly convenient example.

### 4.3 Case 2: Two collinear vectors

Consider:

```text
v = [2, 3]
w = [4, 6]
```

Notice:

```text
w = 2*v
```

The vectors point in the same direction, and one is a scalar multiple of the other.

Any linear combination has the form:

```text
a*v + b*w
```

Substitute `w = 2*v`:

```text
a*v + b*(2*v)
= (a + 2*b)*v
```

The result is always a scalar multiple of `v`.

Therefore, every possible result lies on the same line through the origin.

These two vectors cannot generate an arbitrary point in the 2D plane.

Their span is a line, not the entire plane.

### 4.4 Case 3: A single nonzero vector

Suppose:

```text
v = [2, 3]
```

The span of this vector is:

```text
span(v) = all vectors of the form c*v
```

Examples:

```text
0*v  = [0, 0]
1*v  = [2, 3]
2*v  = [4, 6]
-1*v = [-2, -3]
```

All these vectors lie on the same line through the origin.

Thus, one nonzero vector in 2D spans a line.

### 4.5 Case 4: The zero vector

Suppose the only available vector is:

```text
z = [0, 0]
```

Every scalar multiple of it is still the zero vector.

```text
c*z = [0, 0]
```

Therefore, its span contains only the zero vector.

This is a useful distinction: the zero vector cannot generate a line or plane by itself.

### 4.6 Summary of span in 2D

| Available vectors | Their span |
|---|---|
| One nonzero vector | A line through the origin |
| Two nonzero collinear vectors | A line through the origin |
| Two non-collinear vectors | The entire 2D plane |
| Only the zero vector | Only the zero vector |

The key factor is not merely the number of vectors. It is whether their directions provide independent ways to reach new destinations.

---

## 5. Span in Three Dimensions

The same reasoning applies to 3D vectors, but there is another possible outcome: a plane.

### 5.1 One nonzero vector

One nonzero vector can generate a line through the origin.

```text
v = [1, 2, 3]
```

Every scalar multiple has the form:

```text
c*v = [c, 2*c, 3*c]
```

All these vectors lie along one line.

### 5.2 Two non-collinear vectors

Two non-collinear vectors in 3D generally span a plane through the origin.

For example:

```text
v = [1, 0, 0]
w = [0, 1, 0]
```

Their linear combinations are:

```text
a*v + b*w = [a, b, 0]
```

The third coordinate is always zero.

Therefore, these vectors generate the xy-plane, but they cannot generate vectors with a nonzero z-coordinate.

### 5.3 Three independent vectors

Consider the standard 3D basis vectors:

```text
i = [1, 0, 0]
j = [0, 1, 0]
k = [0, 0, 1]
```

Every 3D vector can be represented as:

```text
v = [x, y, z]

v = x*i + y*j + z*k
```

For example:

```text
v = [3, -2, 5]

v = 3*i - 2*j + 5*k
```

These three independent directions let us reach every point in 3D space.

### 5.4 The important pattern

For standard coordinate spaces:

- One independent direction spans a line.
- Two independent directions span a plane.
- Three independent directions span 3D space.

More generally, `n` independent directions can span an `n`-dimensional vector space when the vectors belong to that space.

The phrase **independent directions** is crucial. Simply adding more vectors does not necessarily increase the span.

---

## 6. Linear Dependence and Linear Independence

These concepts explain why some vectors provide new directions while others do not.

### 6.1 Linearly dependent vectors

A collection of vectors is linearly dependent if at least one vector can be expressed as a linear combination of the others.

For two vectors, a simple example is:

```text
v = [2, 3]
w = [4, 6]
```

Since:

```text
w = 2*v
```

The second vector does not introduce a new direction.

It is redundant when the goal is to span the same line.

For two vectors, if one is a scalar multiple of the other, they are linearly dependent.

### 6.2 Linearly independent vectors

A collection is linearly independent if none of its vectors can be expressed as a linear combination of the others.

For example:

```text
v = [1, 0]
w = [0, 1]
```

Neither vector is a scalar multiple of the other.

Each supplies a direction that the other cannot generate by itself.

Together, they span the entire 2D plane.

### 6.3 A formal test for independence

A collection of vectors is linearly independent if the equation below has only the trivial solution, where every coefficient is zero.

```text
c1*v1 + c2*v2 + ... + cn*vn = [0, 0, ..., 0]
```

The trivial solution is:

```text
c1 = c2 = ... = cn = 0
```

If there is another solution in which at least one coefficient is nonzero, the vectors are linearly dependent.

This formal test will become especially useful when studying systems of equations and matrices.

### 6.4 Why dependence matters

Imagine having three vectors, where the third is the sum of the first two.

```text
v3 = v1 + v2
```

The third vector can already be generated using the first two.

It adds no new direction to their span.

This does not mean the third vector is useless for every application. It means that, for generating the same set of vectors, it is redundant.

---

## 7. Basis Vectors

### 7.1 Definition

A basis is a collection of linearly independent vectors that spans the vector space under consideration.

A basis must satisfy two conditions:

1. The vectors span the space.
2. The vectors are linearly independent.

Both conditions matter.

### 7.2 Standard basis for 2D space

```text
i = [1, 0]
j = [0, 1]
```

These vectors:
- Are linearly independent.
- Span the entire 2D plane.

Therefore, they form a basis for 2D space.

Every 2D vector can be expressed uniquely as a linear combination of these basis vectors.

For example:

```text
v = [5, 3]

v = 5*i + 3*j
```

### 7.3 Standard basis for 3D space

```text
i = [1, 0, 0]
j = [0, 1, 0]
k = [0, 0, 1]
```

These vectors form a basis for 3D space.

Any 3D vector can be written as:

```text
v = [x, y, z]

v = x*i + y*j + z*k
```

### 7.4 Can there be different bases for the same space?

Yes.

The standard basis is convenient, but it is not the only possible basis.

Consider these two vectors:

```text
u = [1, 1]
v = [1, -1]
```

They are not scalar multiples of one another, so they are linearly independent.

Since they are two independent vectors in 2D space, they span the entire plane and form another basis.

Now consider:

```text
target = [4, 2]
```

We want to find scalars `a` and `b` such that:

```text
target = a*u + b*v
```

Expanding:

```text
[4, 2] = a*[1, 1] + b*[1, -1]

[4, 2] = [a + b, a - b]
```

This produces two equations:

```text
a + b = 4
a - b = 2
```

Adding the equations:

```text
2*a = 6
a = 3
```

Substituting into the first equation:

```text
3 + b = 4
b = 1
```

Therefore:

```text
[4, 2] = 3*u + 1*v
```

The same vector can have different coordinates depending on the chosen basis.

**Important:** A vector does not change merely because we choose a different basis. Its coordinate representation changes.

---

## 8. Connecting Basis Vectors to Coordinates

This is one of the most important conceptual lessons in the video.

Coordinates are not inherently tied to one particular set of axes. They depend on the basis used to represent a vector.

### 8.1 Standard coordinates

Using the standard basis:

```text
i = [1, 0]
j = [0, 1]

target = [4, 2]

target = 4*i + 2*j
```

The coordinates are `[4, 2]`.

### 8.2 Coordinates in another basis

Using the alternative basis:

```text
u = [1, 1]
v = [1, -1]
```

We found:

```text
target = 3*u + 1*v
```

Its coordinates relative to this basis are `[3, 1]`.

The geometric vector is still `[4, 2]` in standard coordinates. Only its representation relative to the selected basis has changed.

This is similar to describing the same journey using different reference directions.

### 8.3 Why this is useful

Different bases can make a mathematical problem easier to understand or solve.

In more advanced linear algebra, choosing a suitable basis can simplify transformations, equations, and data representations.

The idea of changing basis becomes important in:
- Matrix diagonalization.
- Eigenvectors and eigenvalues.
- Dimensionality reduction.
- Principal Component Analysis (PCA).
- Understanding transformations in machine learning.

These are later topics, but the conceptual foundation begins here.

---

## 9. Connection to AI and Machine Learning

The ideas in this chapter help explain how numerical representations are constructed and combined in AI systems.

### 9.1 Feature vectors

A data point can be represented as a vector of features.

```text
x = [age, income, experience]
```

A model may transform or combine these features to make predictions.

The vector perspective helps us understand the data as a point in a numerical space.

### 9.2 Weighted combinations

Many machine learning calculations involve weighted combinations of inputs.

For example:

```text
score = w1*x1 + w2*x2 + w3*x3
```

Here:
- `x1`, `x2`, and `x3` are input features.
- `w1`, `w2`, and `w3` are weights.
- The score is a weighted sum of those features.

This is a scalar-valued weighted combination. In neural networks, related operations are applied repeatedly to vectors and matrices.

### 9.3 Embeddings and representation spaces

An embedding represents an object using a vector.

```text
embedding = [e1, e2, e3, ..., en]
```

The embedding lives in an `n`-dimensional numerical space.

Linear combinations and basis concepts help build intuition for how vectors can be represented and combined in such spaces.

However, learned embeddings do not necessarily use an interpretable basis in which each coordinate corresponds to a clear human concept.

### 9.4 Dimensionality and redundant information

If a collection of feature vectors is linearly dependent, some vectors can be represented using combinations of others.

This is one reason linear dependence is relevant to data analysis.

It can reveal redundancy in linear representations, although real-world data may also contain nonlinear relationships that ordinary linear dependence does not capture.

---

## 10. Common Misconceptions to Avoid

1. **A linear combination is more than vector addition.** It allows scalar multiplication before addition.
2. **Span is not the same as the list of given vectors.** It includes every vector obtainable through their linear combinations.
3. **More vectors do not necessarily mean a larger span.** A new vector might be a combination of existing vectors.
4. **Two vectors in 2D do not always span the entire plane.** If they are collinear, their span is a line, assuming at least one is nonzero.
5. **A basis must satisfy two conditions.** It must span the space and be linearly independent.
6. **A basis is not unique.** A vector space can have many different bases.
7. **Coordinates depend on the chosen basis.** The underlying vector remains the same.
8. **Linear dependence does not mean two vectors must be identical.** One can be a scalar multiple of the other, or a vector can be a combination of several others.
9. **A zero vector cannot provide a new direction.** Including it in a collection makes that collection linearly dependent.
10. **The number of vectors alone does not determine the span.** Their relationships and directions matter.

---

## 11. Quick Revision Sheet

| Concept | Meaning |
|---|---|
| Standard basis vectors | The usual unit vectors along the coordinate axes |
| Linear combination | Scaled vectors added together |
| Span | All vectors obtainable through linear combinations |
| Collinear vectors | Vectors lying along the same line through the origin |
| Linear dependence | At least one vector can be generated from the others |
| Linear independence | No vector can be generated from the others |
| Basis | A linearly independent collection that spans the space |
| Coordinates | Coefficients expressing a vector relative to a chosen basis |
| Redundant vector | A vector that adds no new direction to an existing span |

### Essential formulas

**Linear combination**

```text
result = a*v + b*w
```

**Span of two vectors**

```text
span(v, w) = {a*v + b*w : a and b are real numbers}
```

**Linear dependence test**

```text
c1*v1 + c2*v2 + ... + cn*vn = zero_vector
```

If there is a solution with at least one nonzero coefficient, the vectors are linearly dependent.

**Basis representation**

```text
target = c1*v1 + c2*v2 + ... + cn*vn
```

For a basis, every vector in the space has exactly one such representation.

---

## 12. Self-Test

Try answering these without looking at the notes.

1. What is a linear combination?
2. What is the span of a set of vectors?
3. What is the difference between linearly dependent and linearly independent vectors?
4. Do `[2, 3]` and `[4, 6]` span the entire 2D plane? Why?
5. Do `[1, 0]` and `[0, 1]` span the entire 2D plane? Why?
6. What two conditions must a basis satisfy?
7. Can a vector have different coordinates in different bases?
8. Can three vectors in 3D be linearly dependent even if all three are nonzero?
9. Why can redundant vectors be removed from a basis?
10. How are weighted sums related to linear combinations in machine learning?

### Answers

1. A sum of vectors multiplied by scalar coefficients.
2. The set of all vectors obtainable from linear combinations of the supplied vectors.
3. Dependent vectors have a nontrivial linear relationship; independent vectors do not.
4. No. The second vector is twice the first, so their span is only a line through the origin.
5. Yes. They provide two independent directions and can generate any 2D vector.
6. The vectors must span the space and be linearly independent.
7. Yes. The coordinates depend on the chosen basis, although the underlying vector remains unchanged.
8. Yes. For example, the third vector could be the sum of the first two.
9. A basis must be independent. A vector that can be generated from the others is redundant.
10. Weighted sums combine inputs using scalar coefficients, following the same fundamental pattern as linear combinations.

---

## Final Takeaway

This chapter builds on vector addition and scalar multiplication to introduce three powerful ideas:

- **Linear combination:** Scale vectors and add them together.
- **Span:** Understand every vector that a collection can generate.
- **Basis:** Find a minimal independent set of directions that can represent every vector in a space.

The deeper insight is that **coordinates describe how much of each basis vector is needed to construct a target vector**.

Once this clicks, coordinates stop being merely numbers attached to an arrow. They become instructions for building a vector from a chosen set of directions.

That perspective is a key stepping stone toward matrices, linear transformations, eigenvectors, and machine learning.
