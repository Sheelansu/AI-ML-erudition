# Essence of Linear Algebra: Chapter 6
## The Determinant

**Video:** [The Determinant | 3Blue1Brown](https://www.youtube.com/watch?v=Ip3X9LOh2dk)

**Playlist:** [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

---

## 1. Recap: Linear Transformations Change Space

In the previous chapters, we learned that a matrix represents a linear transformation.

A transformation can stretch, compress, rotate, reflect, shear, or collapse space.

For example, consider this matrix:

```text
A = [3  0]
    [0  2]
```

It stretches the x-direction by a factor of 3 and the y-direction by a factor of 2.

The input vector:

```text
v = [x, y]
```

becomes:

```text
A*v = [3*x, 2*y]
```

But how much does this transformation stretch the entire plane?

To answer that, we need a number that describes the transformation's effect on area.

**That number is the determinant.**

The determinant is a single number associated with a square matrix that tells us how the corresponding linear transformation scales area in 2D or volume in 3D.

It also tells us whether the transformation reverses orientation or collapses space into a lower dimension.

---

## 2. What Is the Determinant?

The determinant measures the **signed scaling factor** of a linear transformation.

For a 2D transformation, it describes how signed area changes.

For a 3D transformation, it describes how signed volume changes.

Suppose a transformation has determinant:

```text
det(A) = 3
```

This means:
- Every region's area becomes 3 times its original area.
- The transformation preserves orientation because the determinant is positive.

If:

```text
det(A) = 1/2
```

Every region's area becomes half its original area, with orientation preserved.

If:

```text
det(A) = -2
```

Every region's area becomes twice its original area in magnitude, but the transformation reverses orientation.

If:

```text
det(A) = 0
```

The transformation collapses the plane into a lower-dimensional space, so every transformed region has zero area.

### 2.1 Why is it called a scaling factor?

Imagine a square with an area of 1 square unit.

After a linear transformation, the square may become a parallelogram.

If the parallelogram's area is 6 square units, the transformation scales area by a factor of 6.

If the parallelogram's area is 0.25 square units, the transformation scales area by a factor of 0.25.

The determinant captures this scaling factor for every region, not just the original square.

For area and volume, the magnitude of the determinant gives the scaling factor:

```text
Area scaling factor   = abs(det(A))   [in 2D]
Volume scaling factor = abs(det(A))   [in 3D]
```

The sign carries additional information about orientation.

---

## 3. Visualizing the Determinant Using a Unit Square

Consider the standard basis vectors:

```text
i = [1, 0]
j = [0, 1]
```

Together, they define a unit square with:
- Width = 1
- Height = 1
- Area = 1

Now apply a linear transformation.

The basis vectors move to new locations:

```text
A*i = first column of A
A*j = second column of A
```

The original unit square transforms into a parallelogram.

The two transformed basis vectors become its sides.

The determinant tells us the signed area of this parallelogram.

### 3.1 Example: Stretching the plane

Consider:

```text
A = [3  0]
    [0  2]
```

The basis vectors transform as follows:

```text
A*i = [3, 0]
A*j = [0, 2]
```

The unit square becomes a rectangle with:
- Width = 3
- Height = 2

Its area is:

```text
Area = 3*2 = 6
```

Therefore:

```text
det(A) = 6
```

Every region in the plane has its area multiplied by 6.

### 3.2 General principle

The transformed unit square tells us the area-scaling factor because its original area is 1.

If the transformed parallelogram has area 4, the determinant has magnitude 4.

If the transformed parallelogram has area 0.5, the determinant has magnitude 0.5.

This is the geometric intuition behind the determinant.

---

## 4. The Determinant Can Be Negative

Area itself cannot be negative. So why can a determinant be negative?

Because the determinant records orientation as well as area scaling.

### 4.1 Example: Reflection across the y-axis

Consider:

```text
A = [-1  0]
    [ 0  1]
```

This transformation maps:

```text
[x, y] -> [-x, y]
```

The x-coordinate changes sign, while the y-coordinate remains unchanged.

Geometrically, this reflects the plane across the y-axis.

The unit square still has area 1 after the transformation.

However, the orientation is reversed.

The determinant is:

```text
det(A) = (-1)*1 - 0*0
       = -1
```

Therefore:

```text
det(A) = -1
```

The magnitude tells us that area is unchanged. The negative sign tells us that orientation is reversed.

### 4.2 Positive, negative, and zero determinants

| Determinant | Geometric meaning |
|---|---|
| `det(A) > 1` | Area or volume increases, with orientation preserved |
| `det(A) = 1` | Area or volume is preserved, with orientation preserved |
| `0 < det(A) < 1` | Area or volume decreases, with orientation preserved |
| `det(A) < 0` | Orientation reverses; scaling is given by `abs(det(A))` |
| `det(A) = 0` | Space collapses into a lower dimension |

A negative determinant does not necessarily mean the transformation compresses space.

For example:

```text
det(A) = -3
```

means the area scaling factor is 3, and orientation is reversed.

---

## 5. What Happens When the Determinant Is Zero?

This is one of the most important cases.

Consider the transformation:

```text
A = [1  2]
    [2  4]
```

Its columns are:

```text
v = [1, 2]
w = [2, 4]
```

Notice that:

```text
w = 2*v
```

The columns point in the same direction. They do not provide two independent directions in the plane.

Now consider the output of the transformation:

```text
A*[x, y] = [x + 2*y, 2*x + 4*y]
```

The second output coordinate is always twice the first.

Therefore, every output lies on the line:

```text
second coordinate = 2*(first coordinate)
```

The entire 2D plane collapses onto a line.

The determinant is:

```text
det(A) = 1*4 - 2*2
       = 4 - 4
       = 0
```

Hence:

```text
det(A) = 0
```

### 5.1 Why does this matter?

The transformation has destroyed one dimension of the plane.

The original unit square becomes a line segment with zero area.

This gives us a powerful test:

**If the determinant of a square matrix is zero, its transformation is singular and collapses at least one dimension.**

For a square matrix, a zero determinant also means the matrix has no inverse.

We will explore this connection more deeply in Chapter 7.

### 5.2 Important distinction

A determinant of zero does not mean that every vector becomes the zero vector.

For example:

```text
A = [1  2]
    [2  4]

A*[1, 0] = [1, 2]
```

The output is not zero.

Instead, the transformation maps the entire plane into a line, and some nonzero input vectors are mapped to zero.

---

## 6. Calculating the Determinant of a 2x2 Matrix

The geometric interpretation is the most important idea, but we also need a formula for calculating the determinant.

Consider a general matrix:

```text
A = [a  b]
    [c  d]
```

Its determinant is:

```text
det(A) = a*d - b*c
```

This formula is worth remembering, but it becomes much more intuitive when connected to the transformed basis vectors.

### 6.1 Understanding the formula through columns

The columns of the matrix are:

```text
v = [a, c]
w = [b, d]
```

They represent the transformed basis vectors.

The parallelogram formed by these two vectors has signed area:

```text
det(A) = a*d - b*c
```

The absolute value gives the ordinary area:

```text
Parallelogram area = abs(a*d - b*c)
```

The sign tells us whether orientation is preserved or reversed.

### 6.2 Worked example

Consider:

```text
A = [2  1]
    [1  1]
```

Identify the entries:

```text
a = 2
b = 1
c = 1
d = 1
```

Apply the formula:

```text
det(A) = a*d - b*c
       = 2*1 - 1*1
       = 2 - 1
       = 1
```

Therefore:

```text
det(A) = 1
```

The transformation preserves area and orientation.

It may still change the shape of a region, its angles, and the lengths of its sides.

**Preserving area does not mean preserving the shape.**

---

## 7. Why the Formula Is `a*d - b*c`

Let's connect the calculation to geometry.

The columns of the matrix are:

```text
v = [a, c]
w = [b, d]
```

The parallelogram they form has a signed area determined by the horizontal and vertical components of the two vectors.

The expression:

```text
a*d - b*c
```

combines these components in a way that measures the signed area.

The subtraction is essential because orientation matters.

For example:

```text
A = [1  0]
    [0  1]
```

The determinant is:

```text
det(A) = 1*1 - 0*0
       = 1
```

The unit square keeps its area and orientation.

Now consider:

```text
A = [-1  0]
    [ 0  1]
```

The determinant is:

```text
det(A) = (-1)*1 - 0*0
       = -1
```

The area remains 1, but orientation reverses.

The determinant formula captures both properties in a single number.

---

## 8. Determinants in Three Dimensions

The determinant works similarly in 3D, except that we measure volume rather than area.

In 3D, the standard basis vectors are:

```text
i = [1, 0, 0]
j = [0, 1, 0]
k = [0, 0, 1]
```

They define a unit cube with volume 1.

After a linear transformation, this cube may become a parallelepiped, a 3D shape whose faces are parallelograms.

The determinant tells us the signed volume-scaling factor.

### 8.1 Example: Scaling a 3D space

Consider:

```text
A = [2  0  0]
    [0  3  0]
    [0  0  4]
```

The transformation scales:
- The x-direction by 2.
- The y-direction by 3.
- The z-direction by 4.

The unit cube becomes a rectangular box.

Its volume is:

```text
Volume = 2*3*4
       = 24
```

Therefore:

```text
det(A) = 24
```

Every volume in the space is multiplied by 24.

### 8.2 General principle

For a 3D transformation:

```text
Volume scaling factor = abs(det(A))
```

If:

```text
det(A) = -5
```

The volume scaling factor is 5, and orientation is reversed.

If:

```text
det(A) = 0
```

The transformed cube has zero volume.

The transformation has collapsed 3D space into a lower-dimensional space, such as a plane or a line.

### 8.3 Generalizing to higher dimensions

The same principle applies in any finite dimension.

- In 2D, the determinant measures signed area scaling.
- In 3D, it measures signed volume scaling.
- In higher dimensions, it measures the corresponding signed volume-scaling factor, often called the signed hypervolume factor.

The geometric visualization becomes difficult beyond three dimensions, but the mathematical definition remains valid.

---

## 9. Determinant and Linear Independence

The determinant is closely related to the linear independence of a matrix's columns.

Consider a 2x2 matrix:

```text
A = [a  b]
    [c  d]
```

Its columns are:

```text
v = [a, c]
w = [b, d]
```

### Case 1: Independent columns

If the columns point in genuinely different directions, they span the plane.

Their parallelogram has nonzero area.

```text
det(A) != 0
```

The matrix is invertible.

### Case 2: Dependent columns

If one column is a scalar multiple of the other, the columns span only a line, assuming at least one column is nonzero.

The parallelogram collapses into a line segment.

```text
det(A) = 0
```

The matrix is singular.

### 9.1 The general rule

For a square matrix:

```text
det(A) != 0
```

if and only if its columns are linearly independent.

Equivalently, the transformation preserves the full dimension of the space and is invertible.

If:

```text
det(A) = 0
```

the columns are linearly dependent, the transformation loses at least one dimension, and the matrix is not invertible.

This connection will be important in the next chapter, which studies inverse matrices, column space, and null space.

---

## 10. Connection to AI and Machine Learning

The determinant is not the main operation used in every machine learning model, but its geometric interpretation helps explain important properties of linear transformations.

### 10.1 Understanding whether information is lost

Suppose a square weight matrix transforms an input vector:

```text
y = W*x
```

If:

```text
det(W) = 0
```

then `W` is singular.

Different input vectors can map to the same output, meaning the transformation loses information about the original input.

For example:

```text
W = [1  2]
    [2  4]
```

This matrix maps every input into a line.

It cannot uniquely recover every original 2D input vector.

If:

```text
det(W) != 0
```

the square linear transformation is invertible, so every output uniquely determines its input.

This does not automatically mean the transformation is numerically stable or useful for a model, but it tells us that no dimensions are completely collapsed by the exact mathematical transformation.

### 10.2 Determinants and normalizing flows

Some generative models, particularly normalizing flows, use the determinant of a transformation's Jacobian.

The Jacobian describes how a possibly nonlinear function behaves locally.

Its determinant measures the local volume-scaling factor.

This matters when calculating how probability densities change under a transformation.

For a linear transformation:

```text
y = A*x
```

the Jacobian is simply `A`, so its volume-scaling factor is:

```text
abs(det(A))
```

For a nonlinear transformation, the Jacobian can vary from point to point, and its determinant describes local volume changes.

This is a more advanced application, but it shows why determinants matter beyond introductory geometry.

### 10.3 A caution about large determinants

A large absolute determinant indicates substantial area or volume expansion for a square linear transformation.

A small nonzero determinant indicates substantial compression of area or volume.

However, the determinant alone does not tell us whether the transformation is well-conditioned.

For example, one direction might be stretched enormously while another is compressed enormously, producing a determinant of 1.

Therefore, determinant and numerical stability are related to different questions and should not be confused.

---

## 11. Common Misconceptions to Avoid

1. **The determinant is not just an arbitrary calculation.** It measures the signed area or volume scaling of a linear transformation.
2. **A negative determinant does not mean negative physical area.** Its magnitude gives the area-scaling factor, while the sign indicates orientation reversal.
3. **A determinant of 1 does not mean nothing changed.** The transformation may change lengths, angles, and shape while preserving area or volume.
4. **A determinant of zero does not mean every vector maps to zero.** It means the transformation collapses at least one dimension.
5. **The determinant is defined for square matrices.** Rectangular matrices do not have an ordinary determinant.
6. **A nonzero determinant means a square matrix is invertible.** A zero determinant means it is singular.
7. **A determinant can be negative even when volume remains positive.** The sign records orientation, not negative physical volume.
8. **The determinant alone does not measure every kind of distortion.** It measures the overall area or volume scaling, not the individual stretch along every direction.
9. **Preserving area does not imply preserving lengths.** A shear can preserve area while changing lengths and angles.
10. **A determinant of 1 does not guarantee numerical stability.** The transformation may stretch some directions and compress others dramatically.

---

## 12. Quick Revision Sheet

| Concept | Meaning |
|---|---|
| Determinant | Signed area or volume scaling factor of a square linear transformation |
| Positive determinant | Orientation preserved |
| Negative determinant | Orientation reversed |
| Zero determinant | At least one dimension is collapsed |
| Absolute determinant | Area or volume scaling factor |
| Unit square | Used to visualize 2D area scaling |
| Unit cube | Used to visualize 3D volume scaling |
| Independent columns | Columns span the full space for a square matrix |
| Dependent columns | Columns fail to span the full space |
| Invertible matrix | A square matrix with nonzero determinant |
| Singular matrix | A square matrix with zero determinant |

### Essential formulas

**Determinant of a 2x2 matrix**

```text
A = [a  b]
    [c  d]

det(A) = a*d - b*c
```

**Area scaling in 2D**

```text
Area scaling factor = abs(det(A))
```

**Volume scaling in 3D**

```text
Volume scaling factor = abs(det(A))
```

**Invertibility test for a square matrix**

```text
det(A) != 0  -> A is invertible

det(A) = 0   -> A is singular
```

**Linear independence test for the columns of a square matrix**

```text
det(A) != 0  -> columns are linearly independent

det(A) = 0   -> columns are linearly dependent
```

---

## 13. Self-Test

Try answering these questions without looking at the notes.

1. What does the determinant measure geometrically?
2. If `det(A) = 4`, what happens to the area under the transformation?
3. If `det(A) = -2`, what is the area-scaling factor, and what happens to orientation?
4. Calculate the determinant of `A = [[3, 0], [0, 2]]`.
5. Calculate the determinant of `A = [[1, 2], [2, 4]]`.
6. Why does a zero determinant imply that a square matrix is not invertible?
7. Can a transformation preserve area while changing the shape of a region?
8. What does the determinant measure in 3D?
9. Why is the determinant useful when studying whether information is lost by a square linear transformation?
10. Does a determinant of 1 guarantee that a transformation preserves lengths and angles?

### Answers

1. The signed area or volume scaling factor of the transformation.
2. Every region's area is multiplied by 4, with orientation preserved.
3. The area-scaling factor is 2, and orientation is reversed.
4. `det(A) = 3*2 - 0*0 = 6`.
5. `det(A) = 1*4 - 2*2 = 0`.
6. It means the transformation collapses at least one dimension, so distinct inputs cannot always be uniquely recovered.
7. Yes. A shear can preserve area while changing angles and lengths.
8. The signed volume-scaling factor.
9. A singular square transformation maps distinct inputs to the same output, so the original input cannot always be recovered.
10. No. It preserves area or volume, but individual lengths and angles may change.

---

## Final Takeaway

The determinant gives us a geometric measurement of a linear transformation.

Its absolute value tells us how much the transformation scales area or volume. Its sign tells us whether orientation is preserved or reversed. A zero determinant tells us that the transformation collapses at least one dimension.

Remember these three ideas:

- **Magnitude:** How much area or volume changes.
- **Sign:** Whether orientation reverses.
- **Zero:** Whether the transformation loses a dimension and becomes non-invertible.

Most importantly, the determinant connects geometry to algebra. A single number tells us something profound about how a matrix changes space.

That intuition will lead directly into the next chapter, where inverse matrices, column space, and null space explain what happens when a transformation can or cannot be reversed.
