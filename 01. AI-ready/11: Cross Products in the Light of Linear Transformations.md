# Essence of Linear Algebra, Chapter 11
## Cross Products in the Light of Linear Transformations

**Source:** [3Blue1Brown, Chapter 11](https://www.youtube.com/watch?v=BaM7OCEm3G0)

## 1. The puzzle: why does the cross-product formula work?

In Chapter 10, we learned how to calculate the cross product of two 3D vectors.

For vectors `v` and `w`:

```text
v = [v1]
    [v2]
    [v3]

w = [w1]
    [w2]
    [w3]
```

The cross product is:

```text
v × w = [v2*w3 - v3*w2]
        [v3*w1 - v1*w3]
        [v1*w2 - v2*w1]
```

We know what this result means geometrically:

- It is perpendicular to both `v` and `w`.
- Its magnitude is the area of the parallelogram spanned by `v` and `w`.
- Its direction follows the right-hand rule.

But look at the formula. Why these particular combinations of coordinates? Why do the terms alternate in this way? Why does the determinant appear?

The formula seems almost suspiciously specific.

This chapter answers those questions by connecting the cross product to two earlier ideas:

1. **Determinants:** a determinant measures signed area or volume scaling.
2. **Duality:** a vector can represent a linear transformation from vectors to scalars through the dot product.

The plan is to construct a linear transformation whose output is the signed volume of a parallelepiped. Then we will discover that the vector representing that transformation is exactly the cross product.

---

## 2. Recall duality from Chapter 9

A linear transformation from a vector space to the real numbers is called a **linear functional**.

For example, consider:

```text
T(x, y, z) = 2x + 3y - z
```

This can be represented by a row matrix:

```text
T([x]) = [2  3  -1] [x]
  ([y])               [y]
  ([z])               [z]
```

The output is a single number.

Now turn the row of coefficients into a column vector:

```text
p = [ 2]
    [ 3]
    [-1]
```

The transformation becomes a dot product:

```text
T(u) = p · u
```

where:

```text
u = [x]
    [y]
    [z]
```

Indeed:

```text
p · u = 2x + 3y - z
```

This is the central idea of duality from Chapter 9:

**Every linear functional on a finite-dimensional real vector space with the standard dot product can be represented by taking the dot product with a unique vector.**

We call that vector the *dual vector* associated with the functional.

Chapter 11 uses exactly this idea, but the linear functional will be defined using a determinant.

---

## 3. Build a transformation using a determinant

Choose two fixed 3D vectors, `v` and `w`.

For now, these vectors do not change.

Now let `u` be a variable 3D vector:

```text
u = [u1]
    [u2]
    [u3]
```

Define a function `f` that takes `u` and returns the determinant of a matrix whose columns are `u`, `v`, and `w`.

```text
f(u) = det([u1  v1  w1])
           ([u2  v2  w2])
           ([u3  v3  w3])
```

The inputs `v` and `w` stay fixed. Only `u` changes.

Because a determinant returns a scalar, `f` maps 3D vectors to real numbers:

```text
f: R^3 -> R
```

This is a transformation from three dimensions to one dimension.

The surprising part is that this transformation is linear in `u`.

### Why is it linear?

A determinant is linear in each individual column when the other columns are fixed.

Therefore, with `v` and `w` held constant:

```text
f(a*u1 + b*u2) = a*f(u1) + b*f(u2)
```

Here, `u1` and `u2` represent arbitrary vectors, not individual coordinates.

More clearly, for vectors `u` and `q` and scalars `a` and `b`:

```text
f(a*u + b*q) = a*f(u) + b*f(q)
```

This is the defining property of a linear transformation.

So we have constructed a linear functional using a determinant.

That means the duality idea from Chapter 9 should apply.

There must be a vector `p` such that:

```text
f(u) = p · u
```

Our next job is to discover what `p` is.

---

## 4. The determinant has a geometric meaning: signed volume

Remember Chapter 6.

For a 3 × 3 matrix, the absolute value of its determinant measures the volume of the parallelepiped formed by its columns.

So our function:

```text
f(u) = det([u  v  w])
```

returns the signed volume of the parallelepiped formed by `u`, `v`, and `w`.

The sign records orientation. Reversing the order of two columns reverses the sign.

Geometrically, we can calculate this volume in another way.

Take the parallelogram spanned by `v` and `w`.

Its area is:

```text
area = |v × w|
```

Now use `u` as the third direction. The volume is the area of the base multiplied by the perpendicular height.

But the height is not generally the full length of `u`. It is the magnitude of the component of `u` perpendicular to the plane spanned by `v` and `w`.

Thus:

```text
volume_magnitude =
    area_of_base * perpendicular_height
```

Substitute the base area:

```text
volume_magnitude =
    |v × w| * perpendicular_height
```

If we include orientation, the signed volume can be expressed as:

```text
f(u) = signed_perpendicular_component_of_u
       * area_of_parallelogram_spanned_by_v_and_w
```

This is the geometric key to the entire chapter.

The function measures only the component of `u` perpendicular to the plane of `v` and `w`. Any component of `u` lying inside that plane contributes no extra height and therefore no volume.

---

## 5. Which vector produces this signed volume through a dot product?

We already know from duality that there must be some vector `p` satisfying:

```text
f(u) = p · u
```

The dot product has a geometric interpretation too:

```text
p · u = |p| * signed_projection_of_u_onto_p
```

Compare the two interpretations.

The signed-volume function takes `u`, projects it onto the direction perpendicular to the plane of `v` and `w`, and multiplies that signed component by the area of the parallelogram spanned by `v` and `w`.

The dot product with `p` does the same kind of operation:

- Project `u` onto the direction of `p`.
- Multiply the signed projection by `|p|`.

For the two expressions to agree for every possible `u`, the vector `p` must satisfy two conditions.

**Condition 1: Direction**

`p` must be perpendicular to both `v` and `w`.

Otherwise, projecting `u` onto `p` would measure a different component of `u` than the one controlling the volume.

**Condition 2: Magnitude**

The length of `p` must equal the area of the parallelogram spanned by `v` and `w`.

Otherwise, the dot product would scale the projection by the wrong amount.

Therefore:

```text
|p| = area_of_parallelogram_spanned_by_v_and_w
```

And:

```text
p is perpendicular to v and w
```

There are two opposite directions perpendicular to that plane. The signed-volume convention chooses the correct one using the right-hand rule.

But these are precisely the defining geometric properties of the cross product!

So the dual vector must be:

```text
p = v × w
```

Consequently:

```text
f(u) = (v × w) · u
```

This is the central result of Chapter 11.

**The cross product is the vector that represents the signed-volume linear functional through the dot product.**

---

## 6. Deriving the familiar cross-product formula

We have discovered the cross product geometrically. Now let's recover its coordinate formula.

Let:

```text
u = [x]
    [y]
    [z]

v = [v1]
    [v2]
    [v3]

w = [w1]
    [w2]
    [w3]
```

Our transformation is:

```text
f(u) = det([x  v1  w1])
           ([y  v2  w2])
           ([z  v3  w3])
```

Expand the determinant along the first column:

```text
f(u) = x*(v2*w3 - v3*w2)
     - y*(v1*w3 - v3*w1)
     + z*(v1*w2 - v2*w1)
```

Rewrite the middle coefficient:

```text
f(u) = x*(v2*w3 - v3*w2)
     + y*(v3*w1 - v1*w3)
     + z*(v1*w2 - v2*w1)
```

Now compare this with the general dot product:

```text
p · u = p1*x + p2*y + p3*z
```

Matching the coefficients gives:

```text
p1 = v2*w3 - v3*w2

p2 = v3*w1 - v1*w3

p3 = v1*w2 - v2*w1
```

Therefore:

```text
p = [v2*w3 - v3*w2]
    [v3*w1 - v1*w3]
    [v1*w2 - v2*w1]
```

But we already established geometrically that `p = v × w`.

Hence:

```text
v × w = [v2*w3 - v3*w2]
        [v3*w1 - v1*w3]
        [v1*w2 - v2*w1]
```

We have derived the standard cross-product formula rather than simply memorizing it.

The coordinate formula is not a lucky coincidence. It is forced by the determinant and dot-product interpretations of the same linear transformation.

---

## 7. Why the determinant notation works

In Chapter 10, we used a determinant-like mnemonic:

```text
v × w = det([ i   j   k  ])
            ([v1  v2  v3 ])
            ([w1  w2  w3 ])
```

Here, `i`, `j`, and `k` are the standard basis vectors.

Expanding along the first row gives:

```text
v × w = i*(v2*w3 - v3*w2)
      - j*(v1*w3 - v3*w1)
      + k*(v1*w2 - v2*w1)
```

Rearranging the middle term:

```text
v × w = i*(v2*w3 - v3*w2)
      + j*(v3*w1 - v1*w3)
      + k*(v1*w2 - v2*w1)
```

This is exactly the formula derived in the previous section.

The notation is useful for calculation, but it is not an ordinary scalar determinant that somehow returns a vector. The basis vectors in the first row make the cofactor expansion vector-valued.

The deeper derivation explains why those basis vectors appear in the mnemonic at all: they encode the coefficients of the linear functional defined by the signed-volume determinant.

---

## 8. A complete numerical example

Let:

```text
v = [1]
    [2]
    [3]

w = [4]
    [5]
    [6]
```

First, calculate the cross product:

```text
v × w = [(2*6) - (3*5)]
        [(3*4) - (1*6)]
        [(1*5) - (2*4)]
```

Simplify:

```text
v × w = [-3]
        [ 6]
        [-3]
```

Now define the signed-volume transformation:

```text
f(u) = det([u1  1  4])
           ([u2  2  5])
           ([u3  3  6])
```

From our result, this transformation must equal:

```text
f(u) = (v × w) · u
```

Therefore:

```text
f(u) = -3*u1 + 6*u2 - 3*u3
```

Let's verify it for a particular vector:

```text
u = [2]
    [0]
    [1]
```

Using the dot product:

```text
f(u) = (-3*2) + (6*0) + (-3*1)
     = -6 + 0 - 3
     = -9
```

Using the determinant:

```text
f(u) = det([2  1  4])
           ([0  2  5])
           ([1  3  6])
```

Expanding along the first column:

```text
f(u) = 2*(2*6 - 5*3)
     - 0*(1*6 - 5*4)
     + 1*(1*5 - 2*4)

     = 2*(12 - 15) + (5 - 8)

     = -6 - 3

     = -9
```

Both methods return the same signed volume.

This illustrates the entire chapter in one example:

```text
det([u  v  w]) = (v × w) · u
```

---

## 9. What does this tell us about the cross product?

The derivation gives us a deeper interpretation of the cross product than its coordinate formula alone.

### A. It is a normal vector with a specific magnitude

The cross product is perpendicular to both input vectors, and its magnitude equals the area of their parallelogram.

That is why it can serve as the vector representing the signed-volume transformation.

### B. It encodes an entire linear functional

Once `v` and `w` are fixed, the vector `v × w` tells us how to calculate the signed volume for every possible third vector `u`.

Instead of computing a separate determinant for every `u`, we can calculate the cross product once and then use a dot product:

```text
f(u) = (v × w) · u
```

### C. Its direction records orientation

The sign of the determinant changes if we swap two columns. Correspondingly:

```text
w × v = -(v × w)
```

The cross product's direction is therefore connected to the orientation convention for signed volume.

### D. A zero cross product means the base has zero area

If `v` and `w` are parallel, their parallelogram has zero area.

Then:

```text
v × w = 0
```

The signed-volume transformation is zero for every `u`, because the three vectors can never span a nonzero volume.

This is another connection to the determinant: linearly dependent columns produce a zero determinant.

---

## 10. Connections to AI, machine learning, and computation

This chapter is primarily about geometric reasoning, but the underlying concepts also appear in technical applications.

### A. Dot products turn vectors into scores

The key identity:

```text
f(u) = (v × w) · u
```

shows how a vector can encode a linear rule that produces a scalar.

The same general pattern appears in machine learning:

```text
score = weights · features + bias
```

A learned weight vector represents a function that maps an input representation to a number.

The cross-product chapter adds a geometric example of why this correspondence between vectors and scalar-valued linear functions is so natural.

### B. 3D geometry and computer vision

Suppose a computer vision system estimates two directions on a surface.

Their cross product gives a normal vector:

```text
normal = v × w
```

That normal can then be used in lighting calculations, surface orientation, and geometric reasoning.

The signed-volume identity can also help reason about the relative orientation of points in 3D.

### C. Robotics and physics

In robotics, vectors describe position, velocity, force, and orientation.

Cross products appear in expressions such as:

```text
torque = r × F
```

The geometric interpretation matters because the output direction represents the axis of rotation, while the magnitude describes the rotational effect.

The chapter's determinant viewpoint explains how the cross product's orientation and magnitude fit into a coherent mathematical structure.

### D. Numerical computation

The identity:

```text
det([u  v  w]) = (v × w) · u
```

provides two ways to calculate the same quantity.

Depending on the problem, one formulation may be more convenient than the other. In numerical applications, however, nearly parallel vectors can make cross products and determinant-based calculations sensitive to floating-point errors.

Understanding the geometry helps interpret those results rather than treating the output as a mysterious collection of numbers.

---

## 11. Common misconceptions

**Misconception 1: The cross-product formula is just a trick for remembering signs.**

The determinant expansion gives the formula because the cross product represents a signed-volume linear functional through the dot product.

**Misconception 2: The cross product is defined only by perpendicularity.**

Perpendicularity alone does not determine a unique vector. The magnitude and orientation conventions are also essential.

**Misconception 3: The determinant and cross product are unrelated operations.**

The determinant gives signed volume, while the cross product produces the vector that converts the signed-volume function into a dot product.

**Misconception 4: Duality means vectors and linear functionals are always literally the same object.**

They are different mathematical objects. The standard dot product establishes a natural correspondence between them in finite-dimensional Euclidean space.

**Misconception 5: The vector `u` in the determinant must have a special direction.**

No. It is an arbitrary input vector. The identity works for every `u`, which is exactly why it identifies a linear transformation.

**Misconception 6: A zero cross product means the inputs are perpendicular.**

For nonzero inputs, a zero cross product means they are parallel or antiparallel. Their parallelogram has zero area.

---

## 12. Quick revision sheet

| Concept | Key idea |
|---|---|
| Linear functional | A linear transformation from vectors to scalars |
| Duality | A vector represents a linear functional through the dot product |
| Signed-volume function | `f(u) = det([u v w])` |
| Geometric meaning | Signed volume of a parallelepiped |
| Linear transformation | With `v` and `w` fixed, `f` is linear in `u` |
| Dual vector | The vector `p` satisfying `f(u) = p · u` |
| Cross product identity | `p = v × w` |
| Main equation | `det([u v w]) = (v × w) · u` |
| Cross-product magnitude | Area of the parallelogram spanned by `v` and `w` |
| Orientation | Encoded by the sign of the determinant and the right-hand rule |

### The four equations to remember

```text
1. Define the linear functional:

f(u) = det([u  v  w])
```

```text
2. Use duality:

f(u) = p · u
```

```text
3. Identify the dual vector:

p = v × w
```

```text
4. The central identity:

det([u  v  w]) = (v × w) · u
```

The last equation is the chapter in miniature.

---

## 13. Self-test

**Q1.** If `v` and `w` are fixed, what does the function `f(u) = det([u v w])` return?

**Q2.** Why is `f` a linear transformation in `u`?

**Q3.** According to duality, what must exist for this linear functional?

**Q4.** Geometrically, what must the dual vector's direction be?

**Q5.** What determines the magnitude of the dual vector?

**Q6.** Complete the identity:

```text
det([u  v  w]) = ______
```

**Q7.** Why does swapping `v` and `w` reverse the cross product's direction?

**Q8.** What is the deeper reason the standard cross-product coordinate formula works?

### Answers

**A1.** The signed volume of the parallelepiped formed by `u`, `v`, and `w`.

**A2.** The determinant is linear in each column when the other columns are fixed, so it is linear in `u`.

**A3.** A vector `p` such that `f(u) = p · u` for every input vector `u`.

**A4.** It must be perpendicular to both `v` and `w`.

**A5.** Its magnitude must equal the area of the parallelogram spanned by `v` and `w`.

**A6.**

```text
(v × w) · u
```

**A7.** Swapping two columns reverses the sign of a determinant, so the corresponding dual vector must reverse direction.

**A8.** The cross product is the dual vector representing the signed-volume linear functional. Expanding the determinant gives the coordinates of that vector, which are exactly the familiar cross-product formula.

---

## Final takeaway

Chapter 10 taught us how to calculate the cross product. Chapter 11 explains why that calculation makes sense.

Fix two vectors, `v` and `w`. Use a determinant to define a linear transformation that measures the signed volume created by any third vector `u`. By duality, this transformation must be expressible as a dot product with some vector.

Geometry tells us that this vector must be perpendicular to `v` and `w`, have magnitude equal to their parallelogram's area, and point in the direction prescribed by orientation.

That vector is the cross product.

**The cross product formula is not an arbitrary recipe. It is the coordinate expression of a geometric fact about signed volume and linear transformations.**

Next up: **Chapter 12, “Cramer's Rule, Explained Geometrically.”** We'll use determinants to understand how to solve systems of linear equations and why the determinant appears in the formulas for their solutions.
