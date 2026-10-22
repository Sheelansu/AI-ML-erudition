# Essence of Linear Algebra, Chapter 10
## Cross Products

**Source:** [3Blue1Brown, Chapter 10](https://www.youtube.com/watch?v=eu6i7WJeinw)

## 1. The big idea

In the previous chapter, we learned about the dot product.

```text
v · w = |v| * |w| * cos(theta)
```

The dot product takes two vectors and returns a **scalar**. It tells us something about their alignment.

The cross product is a different operation. It takes two vectors in three-dimensional space and returns a **new vector**.

```text
v × w = a vector perpendicular to both v and w
```

Its magnitude is the area of the parallelogram spanned by the two input vectors.

```text
|v × w| = |v| * |w| * sin(theta)
```

So the two products reveal different geometric properties:

- **Dot product:** How aligned are the vectors?
- **Cross product:** What perpendicular direction do they define, and how much area do they span?

The cross product is especially useful in 3D geometry, physics, computer graphics, and robotics.

---

## 2. Start with area in two dimensions

Suppose we have two vectors in the plane:

```text
v = [vx]
    [vy]

w = [wx]
    [wy]
```

Place them tail-to-tail at the origin. Together, they form two sides of a parallelogram.

The area of that parallelogram is the base multiplied by the perpendicular height.

The cross product's 2D version captures this **signed area**.

The formula is:

```text
v × w = vx*wy - vy*wx
```

In 2D, this expression returns a scalar rather than a 3D vector.

More precisely, it is the signed area of the parallelogram formed by `v` and `w`.

### Example

Consider:

```text
v = [3]
    [1]

w = [1]
    [4]
```

The signed area is:

```text
v × w = (3*4) - (1*1)
      = 12 - 1
      = 11
```

The parallelogram has area 11 square units.

If the vectors were reversed, the result would change sign, but the geometric area would remain 11.

This sign is important because it records orientation.

### Why is the area formula a determinant?

Arrange the vector coordinates as columns:

```text
A = [vx  wx]
    [vy  wy]
```

The determinant is:

```text
det(A) = vx*wy - wx*vy
```

Since multiplication of real numbers is commutative:

```text
det(A) = vx*wy - vy*wx
```

That is exactly the 2D signed cross-product expression.

The connection to Chapter 6 is direct: the determinant measures signed area scaling, and this expression measures the signed area spanned by the two vectors.

---

## 3. Why does the sign matter?

Consider the standard basis vectors:

```text
i = [1]       j = [0]
    [0]           [1]
```

Their 2D signed cross product is:

```text
i × j = (1*1) - (0*0)
      = 1
```

Reverse their order:

```text
j × i = (0*0) - (1*1)
      = -1
```

The area has not changed, but the sign has.

This gives us the important rule:

```text
v × w = -(w × v)
```

Swapping the order of the vectors reverses orientation.

In two dimensions, a positive result means the ordered pair `(v, w)` has the standard positive orientation. A negative result means the opposite orientation.

The exact language of "clockwise" and "counterclockwise" depends on how the coordinate axes and viewing direction are defined. The algebraic sign is the reliable part.

### When is the 2D cross product zero?

```text
v × w = 0
```

This means the signed area is zero.

For two nonzero vectors, it means they are parallel or antiparallel. They lie on the same line through the origin, so the parallelogram collapses into a line segment.

If either vector is the zero vector, the result is also zero.

---

## 4. Moving into three dimensions

In 3D, the cross product returns a vector perpendicular to both inputs.

Suppose:

```text
v = [vx]
    [vy]
    [vz]

w = [wx]
    [wy]
    [wz]
```

The cross product is:

```text
v × w = [ vy*wz - vz*wy ]
        [ vz*wx - vx*wz ]
        [ vx*wy - vy*wx ]
```

The result has three coordinates, so it is itself a 3D vector.

Its direction is perpendicular to the plane containing `v` and `w`.

Its magnitude equals the area of the parallelogram formed by those vectors.

```text
|v × w| = |v| * |w| * sin(theta)
```

Here, `theta` is the angle between the vectors, usually taken between 0 and 180 degrees.

### Why sine?

The parallelogram's base can be taken as `|v|`.

The perpendicular height contributed by `w` is:

```text
height = |w| * sin(theta)
```

Therefore:

```text
area = base * height
     = |v| * |w| * sin(theta)
```

That is the magnitude of the cross product.

When the vectors are perpendicular, the area is largest for fixed lengths. When they are parallel, the area is zero.

---

## 5. A worked 3D example

Consider the vectors:

```text
v = [1]
    [2]
    [3]

w = [4]
    [5]
    [6]
```

Using the component formula:

```text
v × w = [ (2*6) - (3*5) ]
        [ (3*4) - (1*6) ]
        [ (1*5) - (2*4) ]
```

Calculate each coordinate:

```text
v × w = [12 - 15]
        [12 -  6]
        [ 5 -  8]
```

Therefore:

```text
v × w = [-3]
        [ 6]
        [-3]
```

The result is a vector perpendicular to both input vectors.

We can verify this using dot products.

For perpendicular vectors, the dot product should be zero.

First:

```text
(v × w) · v = (-3*1) + (6*2) + (-3*3)
            = -3 + 12 - 9
            = 0
```

Second:

```text
(v × w) · w = (-3*4) + (6*5) + (-3*6)
            = -12 + 30 - 18
            = 0
```

Both dot products are zero, confirming that the cross-product vector is perpendicular to both inputs.

Its magnitude is:

```text
|v × w| = sqrt((-3)^2 + 6^2 + (-3)^2)
        = sqrt(9 + 36 + 9)
        = sqrt(54)
        = 3*sqrt(6)
```

So the parallelogram spanned by `v` and `w` has area `3*sqrt(6)`.

---

## 6. The right-hand rule: choosing the direction

A plane in 3D has two perpendicular directions. If a vector is perpendicular to both `v` and `w`, then its opposite is also perpendicular to both.

So perpendicularity and magnitude alone are not enough to specify a unique cross product.

We need a convention for choosing between the two directions. That convention is the **right-hand rule**.

For `v × w`:

1. Point the fingers of your right hand in the direction of `v`.
2. Curl them toward `w` through the smaller angle.
3. Your thumb indicates the direction of `v × w`.

The order matters. If you reverse the input vectors, the output points in the opposite direction.

```text
v × w = -(w × v)
```

For the standard 3D basis vectors:

```text
i = [1]       j = [0]       k = [0]
    [0]           [1]           [0]
    [0]           [0]           [1]
```

The cross products are:

```text
i × j =  k
j × k =  i
k × i =  j
```

Reversing any pair negates the result:

```text
j × i = -k
k × j = -i
i × k = -j
```

A handy memory trick is to cycle through `i`, `j`, `k` in that order for positive results. Reversing the order introduces a negative sign.

---

## 7. Calculating the cross product using a determinant

The component formula works, but it is easy to lose track of signs.

A convenient computational method uses a 3 × 3 determinant.

Place the standard basis vectors in the first row and the two input vectors beneath them:

```text
v × w = det([ i   j   k  ])
            ([ vx  vy  vz ])
            ([ wx  wy  wz ])
```

Expanding along the first row gives:

```text
v × w = i*(vy*wz - vz*wy)
      - j*(vx*wz - vz*wx)
      + k*(vx*wy - vy*wx)
```

The middle term carries a minus sign because of the cofactor expansion of a determinant.

Writing the result as a vector:

```text
v × w = [ vy*wz - vz*wy ]
        [ vz*wx - vx*wz ]
        [ vx*wy - vy*wx ]
```

This is the same component formula from earlier.

### Important note about the determinant notation

This is a convenient mnemonic for calculating the cross product. It does not mean that an ordinary scalar determinant of a matrix is itself a vector.

The basis vectors `i`, `j`, and `k` in the first row indicate how the determinant expansion is assembled into a vector-valued result.

---

## 8. Cross product versus dot product

These operations have different jobs.

| Property | Dot product | Cross product |
|---|---|---|
| Inputs | Two vectors | Two vectors in 3D |
| Output | Scalar | Vector in 3D |
| Main geometric meaning | Alignment and projection | Perpendicular direction and area |
| Magnitude formula | `|v|*|w|*cos(theta)` | `|v|*|w|*sin(theta)` |
| Symmetry | `v · w = w · v` | `v × w = -(w × v)` |
| Zero for nonzero vectors when | They are perpendicular | They are parallel or antiparallel |

A useful way to remember the difference:

- The dot product is largest in magnitude when vectors align or oppose one another.
- The cross product is largest in magnitude when the vectors are perpendicular.

Both operations combine two vectors, but they extract different geometric information.

---

## 9. Special cases worth knowing

### Case A: parallel vectors

If the angle is 0 or 180 degrees:

```text
sin(theta) = 0
```

Therefore:

```text
v × w = 0
```

The vectors span no area.

### Case B: perpendicular vectors

If the angle is 90 degrees:

```text
sin(theta) = 1
```

Therefore:

```text
|v × w| = |v| * |w|
```

The parallelogram's area is the product of the two lengths.

### Case C: one vector is zero

```text
0 × v = 0
```

There is no direction or area to recover from the zero vector.

### Case D: swapping vectors

```text
w × v = -(v × w)
```

The magnitude remains the same, but the direction reverses.

### Case E: scaling a vector

For a scalar `c`:

```text
(c*v) × w = c*(v × w)
```

Similarly:

```text
v × (c*w) = c*(v × w)
```

Scaling either vector scales the cross product by the same factor. A negative scalar also reverses its direction.

---

## 10. Applications in physics, graphics, and machine learning

### A. Torque in physics

Torque describes the rotational effect of a force applied at a position relative to a pivot.

```text
torque = r × F
```

Here:

- `r` is the position vector from the pivot to the point where the force is applied.
- `F` is the force vector.

The magnitude is:

```text
|torque| = |r| * |F| * sin(theta)
```

A force directed along the position vector creates no torque about that pivot. A perpendicular force creates the largest torque for fixed magnitudes.

The cross product also gives the torque's axis direction.

### B. Surface normals in computer graphics

A surface normal is a vector perpendicular to a surface.

If two nonparallel vectors lie along a triangle's edges:

```text
normal = (B - A) × (C - A)
```

The resulting vector is perpendicular to the triangle's plane.

Its magnitude equals twice the triangle's area:

```text
triangle_area = |normal| / 2
```

Graphics engines use surface normals in lighting calculations, shading, collision detection, and geometric processing.

The order of the triangle vertices affects the normal's direction, which is important for front-face and back-face conventions.

### C. Angular momentum

Angular momentum for a particle about a chosen origin is:

```text
L = r × p
```

Here, `p` is linear momentum.

The cross product describes both the magnitude of the rotational quantity and its direction.

### D. Machine learning and 3D data

The cross product is not a core primitive in every neural network, but it is useful when working with 3D geometry.

Applications include:

- Computing normals for 3D meshes.
- Processing point clouds and geometric data.
- Building orientation features for robotics.
- Calculating torque and force features in physical simulation.
- Constructing coordinate frames for 3D perception.

In many machine learning systems, the dot product is more common for comparing learned feature vectors. The cross product is especially useful when the data has a meaningful 3D geometric interpretation.

---

## 11. Common misconceptions

**Misconception 1: The cross product works the same way in every dimension.**

The standard cross product of two vectors returning a perpendicular vector is a special operation in 3D. There is also a signed-area version in 2D, but its output is a scalar.

**Misconception 2: The cross product is commutative.**

It is anti-commutative:

```text
v × w = -(w × v)
```

Changing the order reverses the result.

**Misconception 3: The cross product's magnitude is always the product of the vector lengths.**

Only when the vectors are perpendicular. In general:

```text
|v × w| = |v|*|w|*sin(theta)
```

**Misconception 4: A vector perpendicular to both inputs is uniquely determined by perpendicularity alone.**

There are two opposite directions perpendicular to the same plane. The right-hand rule chooses the direction.

**Misconception 5: A zero cross product means the input vectors are perpendicular.**

The opposite is true for nonzero vectors: a zero cross product means they are parallel or antiparallel.

**Misconception 6: The determinant expansion is literally an ordinary scalar determinant returning a vector.**

The determinant notation is used as a computational mnemonic with basis vectors in the first row. The final result is a vector assembled from the cofactor expansion.

---

## 12. Quick revision sheet

| Concept | Key idea |
|---|---|
| 2D signed cross product | `vx*wy - vy*wx` |
| 2D geometric meaning | Signed parallelogram area |
| 3D cross product | Vector perpendicular to both inputs |
| Magnitude | Parallelogram area |
| Direction | Chosen by the right-hand rule |
| Order | Reversing vectors negates the result |
| Parallel inputs | Cross product is zero |
| Perpendicular inputs | Magnitude is the product of lengths |
| Determinant connection | The 2D signed area is a 2 × 2 determinant |
| Torque | `r × F` |
| Surface normal | Cross product of two surface directions |

### The five equations to remember

```text
2D signed cross product:

v × w = vx*wy - vy*wx
```

```text
3D cross product:

v × w = [ vy*wz - vz*wy ]
        [ vz*wx - vx*wz ]
        [ vx*wy - vy*wx ]
```

```text
Magnitude:

|v × w| = |v|*|w|*sin(theta)
```

```text
Order reversal:

v × w = -(w × v)
```

```text
Triangle area:

area = |(B - A) × (C - A)| / 2
```

---

## 13. Self-test

Try these before checking the answers.

**Q1.** What does the dot product return, and what does the 3D cross product return?

**Q2.** Calculate the 2D signed cross product of `(2, 1)` and `(1, 3)`.

**Q3.** What is `i × j` in the standard right-handed coordinate system?

**Q4.** If two nonzero vectors are parallel, what is their cross product?

**Q5.** If `|v| = 3`, `|w| = 4`, and the angle between them is 90 degrees, what is `|v × w|`?

**Q6.** Why does reversing the order of a cross product reverse its direction?

**Q7.** How can you calculate the area of a triangle using a cross product?

**Q8.** Why is the cross product useful for calculating a surface normal?

### Answers

**A1.** The dot product returns a scalar. The standard 3D cross product returns a vector perpendicular to both inputs.

**A2.**

```text
(2*3) - (1*1) = 6 - 1 = 5
```

The signed area is positive 5.

**A3.**

```text
i × j = k
```

**A4.** The zero vector, because parallel vectors span no area.

**A5.**

```text
|v × w| = 3*4*sin(90 degrees) = 12
```

**A6.** The operation is anti-commutative. Swapping the vectors preserves the magnitude but reverses the orientation and direction.

**A7.** Take half the magnitude of the cross product of two edge vectors from the same vertex.

**A8.** The cross product of two nonparallel vectors lying in the surface produces a vector perpendicular to both, which is normal to the surface.

---

## Final takeaway

The cross product takes two vectors and produces a vector that captures the area they span and the orientation of their plane.

The dot product asks, "How much do these vectors align?"

The cross product asks, "What perpendicular direction do these vectors define, and how much area do they span?"

The determinant connects the cross product to signed area, while the right-hand rule determines its direction in 3D.

Next up: **Chapter 11, “Cross Products in the Light of Linear Transformations.”** That chapter digs into why the cross-product formula works, tying together determinants, duality, and the transformations you've been studying.
