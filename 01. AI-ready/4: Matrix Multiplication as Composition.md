# Essence of Linear Algebra: Chapter 4
## Matrix Multiplication as Composition

**Video:** [Matrix Multiplication as Composition | 3Blue1Brown](https://www.youtube.com/watch?v=XkY2DOUCWMU)

**Playlist:** [Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

---

## 1. Recap: Matrices Represent Transformations

In Chapter 3, we learned that a matrix represents a linear transformation.

A transformation changes an input vector into an output vector.

For example, consider the matrix:

```text
A = [1  2]
    [0  1]
```

For an input vector:

```text
v = [x, y]
```

The transformation produces:

```text
A*v = [x + 2*y, y]
```

The matrix tells us how every vector in the plane changes.

We also learned that the columns of a transformation matrix tell us where the standard basis vectors end up.

```text
i = [1, 0]
j = [0, 1]
```

For the matrix `A` above:

```text
A*i = [1, 0]
A*j = [2, 1]
```

These transformed basis vectors form the columns of `A`.

### The question in this chapter

What if we want to apply one transformation and then another?

For example:

1. Rotate a vector.
2. Apply a shear transformation to the rotated vector.

Can we represent both operations as a single matrix?

**Yes. Matrix multiplication combines successive linear transformations into one transformation.** This is the central idea of the video. <Cite refs={["turn695285search0","turn695285search3"]}/>

---

## 2. Composition of Transformations

### 2.1 What is composition?

Composition means applying one function after another.

Suppose:
- `R` represents a rotation.
- `S` represents a shear.

If we rotate a vector first and then apply the shear, the overall transformation is:

```text
result = S*(R*v)
```

The vector passes through two stages:

```text
Original vector
      |
      v
Rotation: R*v
      |
      v
Shear: S*(R*v)
      |
      v
Final vector
```

Instead of performing two separate operations every time, we would like to find one matrix that produces the same final result.

Call that matrix `C`.

```text
C*v = S*(R*v)
```

Since this equality must hold for every input vector:

```text
C = S*R
```

Therefore, the composition of two linear transformations is itself a linear transformation, represented by the product of their matrices.

### 2.2 Why is this useful?

Suppose a graphics application needs to rotate, scale, and translate an object repeatedly.

Rather than treating each transformation as an isolated operation, we can combine compatible transformations into a single matrix operation.

The same principle appears in:
- Computer graphics.
- Robotics.
- Physics simulations.
- Neural network computations.
- Coordinate transformations.

The key insight is that a sequence of linear transformations can be represented by a single linear transformation.

**Important:** A nonzero translation is an affine transformation, not a linear transformation. Translations can still be combined with other transformations, but they require an affine or homogeneous-coordinate representation rather than an ordinary linear matrix acting on the original coordinates.

---

## 3. A Worked Example: Rotate, Then Shear

Let's work through a concrete example.

We will use two matrices:

**Rotation by 90 degrees counterclockwise**

```text
R = [0  -1]
    [1   0]
```

**Shear transformation**

```text
S = [1  1]
    [0  1]
```

The rotation acts first, followed by the shear.

Therefore:

```text
C = S*R
```

Remember that the matrix on the right is applied first.

### 3.1 Transform the first basis vector

The first standard basis vector is:

```text
i = [1, 0]
```

Apply the rotation:

```text
R*i = [0, 1]
```

Now apply the shear to the result:

```text
S*[0, 1] = [1, 1]
```

Therefore:

```text
C*i = [1, 1]
```

This becomes the first column of the composition matrix.

### 3.2 Transform the second basis vector

The second standard basis vector is:

```text
j = [0, 1]
```

Apply the rotation:

```text
R*j = [-1, 0]
```

Now apply the shear:

```text
S*[-1, 0] = [-1, 0]
```

Therefore:

```text
C*j = [-1, 0]
```

This becomes the second column of the composition matrix.

### 3.3 Construct the final matrix

The columns are the transformed basis vectors:

```text
First column  = [1, 1]
Second column = [-1, 0]
```

Thus:

```text
C = [1  -1]
    [1   0]
```

The entire sequence of rotating and then shearing can now be performed using one matrix.

```text
C = S*R

  = [1  1] * [0  -1]
    [0  1]   [1   0]

  = [1  -1]
    [1   0]
```

This is matrix multiplication understood geometrically: the product matrix captures the combined effect of both transformations. <Cite refs={["turn695285search0","turn695285search3"]}/>

---

## 4. Applying the Composition Matrix to an Arbitrary Vector

We have found:

```text
C = [1  -1]
    [1   0]
```

Suppose our input vector is:

```text
v = [2, 3]
```

Let's apply the transformations separately first.

### Step 1: Apply the rotation

```text
R*v = [0  -1] * [2]
      [1   0]   [3]
```

Calculating:

```text
R*v = [-3, 2]
```

### Step 2: Apply the shear

```text
S*[-3, 2] = [-3 + 2, 2]
           = [-1, 2]
```

The final result is:

```text
S*(R*v) = [-1, 2]
```

Now apply the composition matrix directly:

```text
C*v = [1  -1] * [2]
      [1   0]   [3]
```

Calculating:

```text
C*v = [2 - 3, 2]
    = [-1, 2]
```

Both methods give the same result.

```text
S*(R*v) = (S*R)*v
```

This confirms that the composition matrix produces the same output as the two successive transformations.

---

## 5. Why Matrix Multiplication Works

We know that a linear transformation is determined by where it sends the standard basis vectors.

For a 2D transformation matrix:

```text
A = [a  b]
    [c  d]
```

Its columns represent:

```text
A*i = [a, c]
A*j = [b, d]
```

Now suppose we have two transformation matrices:
- `R`, applied first.
- `S`, applied second.

The combined transformation is:

```text
C = S*R
```

To find the first column of `C`, track where `i` goes.

```text
i
|
v
R*i
|
v
S*(R*i)
```

The resulting vector is:

```text
C*i = S*(R*i)
```

Similarly, for the second basis vector:

```text
C*j = S*(R*j)
```

Therefore, the two columns of the composition matrix are:

```text
C = [ S*(R*i)  S*(R*j) ]
```

Here, each expression represents one column vector.

**This is the geometric explanation of matrix multiplication:** transform the basis vectors through both operations, then use their final positions as the columns of the combined matrix.

---

## 6. The Numerical Rule for Matrix Multiplication

The geometric explanation tells us what matrix multiplication means. Now let's understand how to calculate it.

Consider two matrices:

```text
A = [a  b]
    [c  d]

B = [e  f]
    [g  h]
```

We want to calculate:

```text
C = A*B
```

### 6.1 Calculate the first column

The first column of `B` is:

```text
[e, g]
```

Applying `A` to this vector gives:

```text
A*[e, g] = [a*e + b*g, c*e + d*g]
```

This becomes the first column of `C`.

### 6.2 Calculate the second column

The second column of `B` is:

```text
[f, h]
```

Applying `A` to this vector gives:

```text
A*[f, h] = [a*f + b*h, c*f + d*h]
```

This becomes the second column of `C`.

### 6.3 Assemble the product

```text
A*B = [a*e + b*g    a*f + b*h]
      [c*e + d*g    c*f + d*h]
```

Each column of the product is obtained by applying the left matrix to the corresponding column of the right matrix.

This follows directly from the geometric meaning of composition.

### 6.4 A practical example

Let:

```text
A = [1  2]
    [3  4]

B = [5  6]
    [7  8]
```

Calculate the first column:

```text
A*[5, 7] = [1*5 + 2*7, 3*5 + 4*7]
         = [19, 43]
```

Calculate the second column:

```text
A*[6, 8] = [1*6 + 2*8, 3*6 + 4*8]
         = [22, 50]
```

Assemble the columns:

```text
A*B = [19  22]
      [43  50]
```

The familiar arithmetic rule is simply a convenient way to compute the composition of two transformations.

---

## 7. Matrix Multiplication Is Not Commutative

One of the most important properties of matrix multiplication is that the order generally matters.

In ordinary arithmetic:

```text
2*3 = 3*2
```

But for matrices, in general:

```text
A*B != B*A
```

This is called **non-commutativity**.

### 7.1 Why does order matter?

Imagine rotating an object and then shearing it.

Compare that with shearing the object first and rotating it afterward.

These two sequences generally produce different results.

The first operation changes the vector that the second operation receives. Reversing the order changes the intermediate vector and therefore can change the final result.

### 7.2 Demonstration using the rotation and shear matrices

Recall:

```text
R = [0  -1]
    [1   0]

S = [1  1]
    [0  1]
```

We already calculated rotation followed by shear:

```text
S*R = [1  -1]
      [1   0]
```

Now reverse the order.

First apply the shear, then the rotation:

```text
R*S = [0  -1] * [1  1]
      [1   0]   [0  1]
```

Calculate each entry:

```text
R*S = [0  -1]
      [1   1]
```

Compare the results:

```text
S*R = [1  -1]
      [1   0]

R*S = [0  -1]
      [1   1]
```

They are different matrices.

Therefore, the order of transformations matters.

### 7.3 When can matrices commute?

Some pairs of matrices do commute. For example, two scalar multiples of the identity matrix commute.

However, this is not guaranteed for arbitrary matrices.

The safe rule is:

**Never reverse the order of matrix multiplication unless you have established that the matrices commute.**

---

## 8. Why Matrix Products Are Read Right to Left

Consider:

```text
C = S*R
```

The rightmost matrix `R` acts first, followed by `S`.

When applied to a vector:

```text
C*v = S*(R*v)
```

Read it from the innermost operation outward:

1. Compute `R*v`.
2. Apply `S` to that result.

This is the same convention used in function composition.

For functions:

```text
f(g(x))
```

The function `g` acts on `x` first. Then `f` acts on the result.

Matrix multiplication follows the same pattern.

### Memory aid

```text
A*B*v
```

Starting from the vector `v`:
1. Apply `B`.
2. Apply `A`.

The rightmost transformation acts first.

This convention may initially feel backward, but it is consistent with ordinary function notation.

---

## 9. Associativity: Grouping Does Not Matter

Matrix multiplication is associative.

For compatible matrices:

```text
(A*B)*C = A*(B*C)
```

This means that when multiplying three matrices, changing the grouping does not change the final product.

### 9.1 Geometric interpretation

Suppose we apply three transformations:

1. `C`
2. `B`
3. `A`

The overall transformation is:

```text
A*B*C
```

We can first combine `B` and `C`:

```text
A*(B*C)
```

Or first combine `A` and `B`:

```text
(A*B)*C
```

Both represent the same sequence of transformations.

The intermediate grouping changes, but the final effect does not.

### 9.2 Why this matters computationally

For large matrices, multiplication can be expensive.

Associativity allows us to choose how to group a sequence of products. Depending on the matrix dimensions, some groupings can require much less computation than others.

For example, if the matrices have different dimensions, multiplying a smaller intermediate pair first can reduce the number of arithmetic operations.

However, associativity does not mean that multiplication can be reordered arbitrarily.

```text
(A*B)*C = A*(B*C)
```

does not imply:

```text
A*B*C = A*C*B
```

Grouping can change. Order generally cannot.

---

## 10. Matrix Multiplication and AI/ML

Matrix multiplication is one of the main computational building blocks of machine learning.

### 10.1 Combining multiple transformations

A model may apply several linear transformations in sequence.

```text
x
|
v
A*x
|
v
B*(A*x)
|
v
C*(B*(A*x))
```

The combined transformation can be represented as:

```text
combined = C*B*A
```

Therefore:

```text
combined*x = C*(B*(A*x))
```

This is the same composition principle introduced in this chapter.

### 10.2 Neural networks

A typical neural network layer computes something like:

```text
y = W*x + b
```

Here:
- `x` is the input vector.
- `W` is a learned weight matrix.
- `b` is a bias vector.
- `y` is the output before the activation function.

A sequence of purely linear layers without intervening nonlinearities can be combined into a single linear transformation.

For example:

```text
h = W1*x
y = W2*h
```

Substituting the first equation into the second:

```text
y = W2*(W1*x)
  = (W2*W1)*x
```

The two matrix multiplications combine into one matrix product.

### 10.3 Why neural networks need nonlinear activation functions

If we stack only linear transformations, the result is still linear.

For example:

```text
y = W2*(W1*x)
```

can be rewritten as:

```text
y = W*x
```

where:

```text
W = W2*W1
```

Adding more purely linear layers does not, by itself, make the overall function more expressive than one linear transformation.

Neural networks therefore typically use nonlinear activation functions between layers.

For example:

```text
h = ReLU(W1*x + b1)
y = W2*h + b2
```

Because of the ReLU operation, the overall mapping is generally nonlinear.

This distinction helps explain why deep learning architectures combine matrix multiplication with nonlinear operations.

### 10.4 Large-scale computation

Modern AI systems perform enormous numbers of matrix multiplications.

These operations are highly optimized on GPUs and other accelerators because they can be expressed as structured numerical computations.

Understanding matrix multiplication as transformation composition gives you a geometric interpretation of the operation. Understanding its numerical rules helps you implement and optimize it.

Both perspectives matter.

---

## 11. Common Misconceptions to Avoid

1. **Matrix multiplication represents composition.** It combines transformations into one operation.
2. **The rightmost matrix acts first.** In `A*B*v`, apply `B` before `A`.
3. **Matrix multiplication is generally not commutative.** Reversing the order can change the result.
4. **Matrix multiplication is associative.** Compatible products can be regrouped without changing the result.
5. **The columns of a product matrix have meaning.** Each column is the final destination of a standard basis vector after all transformations.
6. **The product matrix captures the entire sequence.** It works for every input vector, not just one example.
7. **Linear layers without nonlinearities remain linear when composed.** Stacking them alone does not create nonlinear behavior.
8. **Matrix dimensions must be compatible.** The number of columns in the left matrix must equal the number of rows in the right matrix.
9. **Associativity is not commutativity.** Changing grouping is different from changing order.
10. **Affine transformations require care.** Nonzero translations cannot be represented as ordinary linear transformations on the original coordinates, although homogeneous coordinates let us incorporate them into matrix multiplication.

---

## 12. Quick Revision Sheet

| Concept | Meaning |
|---|---|
| Composition | Applying one transformation after another |
| Matrix product | Matrix representing the combined transformation |
| Rightmost matrix | Transformation applied first |
| Non-commutativity | Reversing matrix order generally changes the result |
| Associativity | Changing grouping does not change the product |
| Product columns | Final destinations of the basis vectors |
| Linear layers | Composable transformations represented by matrix products |
| Nonlinear activation | An operation that prevents a network from collapsing into one linear transformation |

### Essential formulas

**Composition**

```text
C = B*A
```

This means apply `A` first and `B` second.

**Applying the composition to a vector**

```text
C*v = B*(A*v)
```

**General 2x2 matrix multiplication**

```text
A = [a  b]
    [c  d]

B = [e  f]
    [g  h]

A*B = [a*e + b*g    a*f + b*h]
      [c*e + d*g    c*f + d*h]
```

**Non-commutativity**

```text
A*B != B*A     (in general)
```

**Associativity**

```text
(A*B)*C = A*(B*C)
```

**Combining two linear layers**

```text
h = W1*x
y = W2*h

y = (W2*W1)*x
```

---

## 13. Self-Test

Try answering these questions without looking at the notes.

1. What does composition of transformations mean?
2. If a vector is rotated and then sheared, which transformation matrix appears on the right?
3. Why can two successive linear transformations be represented by a single matrix?
4. If `C = S*R`, which transformation is applied first?
5. What is the geometric meaning of each column of the composition matrix?
6. Why is matrix multiplication generally not commutative?
7. What is the difference between associativity and commutativity?
8. If two linear transformations are represented by `A` and `B`, how do you represent applying `A` first and `B` second?
9. Why can multiple purely linear neural network layers be combined into one linear transformation?
10. Why do neural networks use nonlinear activation functions?

### Answers

1. Applying one transformation and then another.
2. The rotation matrix appears on the right.
3. The composition is itself a linear transformation, so it has a matrix representation.
4. `R` is applied first, followed by `S`.
5. Each column gives the final destination of one standard basis vector after both transformations.
6. Because the order of transformations generally changes the intermediate vectors and the final result.
7. Associativity permits regrouping; commutativity permits swapping order.
8. `B*A`.
9. Their product is another matrix that represents the same combined linear transformation.
10. Nonlinear activation functions allow the network to represent nonlinear mappings that cannot generally be reduced to a single linear transformation.

---

## Final Takeaway

The big idea of Chapter 4 is:

**Matrix multiplication is the mathematical language of composing linear transformations.**

The reasoning chain is:

1. A matrix represents a linear transformation.
2. Multiple transformations can be applied sequentially.
3. Their combined effect is another linear transformation.
4. The matrix of that combined transformation is the product of the original matrices.
5. The rightmost matrix acts first.
6. The order generally matters, although the grouping of a product can change.

Once you understand this, matrix multiplication stops being a memorized grid of arithmetic rules. It becomes a way to combine transformations into a single operation.

That is a powerful foundation for understanding neural networks, computer graphics, robotics, and more advanced linear algebra.
