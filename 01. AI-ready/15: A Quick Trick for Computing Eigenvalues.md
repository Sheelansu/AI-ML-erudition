# Essence of Linear Algebra, Chapter 15: A Quick Trick for Computing Eigenvalues

**Video:** [A Quick Trick for Computing Eigenvalues | 3Blue1Brown](https://www.youtube.com/watch?v=e50Bj7jn9IQ)

**Main question:** How can we calculate the eigenvalues of a 2×2 matrix quickly by looking at its entries?

---

## 1. The Big Idea

In the previous chapter, we learned that an eigenvector is a nonzero vector whose direction remains along the same line after a linear transformation.

The defining equation is:

```text
A*v = lambda*v
```

Here:
- `A` is the transformation matrix.
- `v` is a nonzero eigenvector.
- `lambda` is its eigenvalue.

We also learned that eigenvalues can be found by solving the characteristic equation:

```text
det(A - lambda*I) = 0
```

For a 2×2 matrix, this usually produces a quadratic equation. We then solve it using the quadratic formula.

That works perfectly well, but there is a quicker approach.

**The shortcut uses the trace and determinant to find the mean and product of the two eigenvalues.**

Once we know the mean and product, we can recover the eigenvalues directly.

---

## 2. First, Understand the Trace

Consider a general 2×2 matrix:

```text
A = [a  b]
    [c  d]
```

The **trace** is the sum of the diagonal entries.

```text
tr(A) = a + d
```

For example:

```text
A = [3  1]
    [4  1]
```

Its trace is:

```text
tr(A) = 3 + 1 = 4
```

The trace is easy to calculate because we only need the diagonal entries.

### The important property

For a square matrix, the trace equals the sum of its eigenvalues, counting their algebraic multiplicities.

For a 2×2 matrix with eigenvalues `lambda1` and `lambda2`:

```text
tr(A) = lambda1 + lambda2
```

Therefore:

```text
lambda1 + lambda2 = a + d
```

Dividing both sides by 2 gives:

```text
(lambda1 + lambda2)/2 = (a + d)/2
```

The mean of the eigenvalues is therefore:

```text
m = (a + d)/2
```

**First key result: The mean of the two eigenvalues is half the trace.**

Notice that we have already learned something about both eigenvalues without finding either one individually.

---

## 3. Why Does the Trace Equal the Sum of the Eigenvalues?

Let's connect this to the characteristic polynomial from Chapter 14.

For:

```text
A = [a  b]
    [c  d]
```

subtract `lambda*I`:

```text
A - lambda*I = [a-lambda  b]
               [c        d-lambda]
```

Calculate the determinant:

```text
det(A - lambda*I)
    = (a-lambda)*(d-lambda) - b*c
```

Expand:

```text
= a*d - a*lambda - d*lambda + lambda^2 - b*c
```

Collect the terms:

```text
= lambda^2 - (a+d)*lambda + (a*d-b*c)
```

The characteristic equation is:

```text
lambda^2 - (a+d)*lambda + (a*d-b*c) = 0
```

Suppose the two roots are `lambda1` and `lambda2`.

A quadratic with those roots can be written as:

```text
(lambda-lambda1)*(lambda-lambda2) = 0
```

Expanding:

```text
lambda^2 - (lambda1+lambda2)*lambda
        + lambda1*lambda2 = 0
```

Compare the two expressions.

The coefficients of `lambda` must match:

```text
lambda1 + lambda2 = a + d
```

But `a+d` is precisely the trace.

Therefore:

```text
tr(A) = lambda1 + lambda2
```

This is not a coincidence. It follows directly from the characteristic polynomial.

---

## 4. Next, Understand the Determinant

For a 2×2 matrix:

```text
A = [a  b]
    [c  d]
```

the determinant is:

```text
det(A) = a*d - b*c
```

For example:

```text
A = [3  1]
    [4  1]
```

Its determinant is:

```text
det(A) = (3*1) - (1*4)

det(A) = -1
```

The determinant describes the signed area-scaling factor of a 2D linear transformation. In higher dimensions, it describes the corresponding signed volume-scaling factor.

In Chapter 6, we learned that:
- A determinant with magnitude greater than 1 means areas are scaled up.
- A determinant with magnitude between 0 and 1 means areas are scaled down.
- A negative determinant indicates an orientation reversal.
- A zero determinant means the transformation collapses the space into a lower-dimensional space.

Now comes the second important property.

For a square matrix, the determinant equals the product of its eigenvalues, counting algebraic multiplicities.

For a 2×2 matrix:

```text
det(A) = lambda1*lambda2
```

Therefore:

```text
lambda1*lambda2 = a*d - b*c
```

**Second key result: The determinant gives us the product of the two eigenvalues.**

We now know:
1. Their sum.
2. Their product.

Can we recover the two eigenvalues from those facts alone?

Yes.

---

## 5. The Mean-Product Formula

Suppose two numbers have:
- Mean `m`.
- Product `p`.

We want to find the two numbers.

If their mean is `m`, they must be equally spaced around `m`.

We can write them as:

```text
number1 = m + r

number2 = m - r
```

Here, `r` is the distance between either number and the mean.

Their product is:

```text
p = (m+r)*(m-r)
```

Using the difference-of-squares identity:

```text
p = m^2 - r^2
```

Rearrange:

```text
r^2 = m^2 - p
```

Taking square roots:

```text
r = sqrt(m^2-p)
```

The two numbers are therefore:

```text
number1 = m + sqrt(m^2-p)

number2 = m - sqrt(m^2-p)
```

This is the **mean-product formula**.

For a 2×2 matrix, substitute:
- `m = tr(A)/2`.
- `p = det(A)`.

We obtain the shortcut for eigenvalues.

### The key formula

For:

```text
A = [a  b]
    [c  d]
```

the eigenvalues are:

```text
lambda1, lambda2
    = m +/- sqrt(m^2-p)
```

where:

```text
m = (a+d)/2
```

and:

```text
p = a*d-b*c
```

Therefore:

```text
lambda1, lambda2
    = (a+d)/2 +/- sqrt(((a+d)/2)^2 - (a*d-b*c))
```

You do not need to memorize this expanded expression. The version using the trace and determinant is easier to remember and understand.

---

## 6. The Shortcut: Four Steps

Given any 2×2 matrix:

```text
A = [a  b]
    [c  d]
```

### Step 1: Calculate the mean

Average the diagonal entries:

```text
m = (a+d)/2
```

### Step 2: Calculate the determinant

```text
p = a*d-b*c
```

### Step 3: Apply the mean-product formula

```text
lambda1, lambda2 = m +/- sqrt(m^2-p)
```

### Step 4: Simplify

Calculate the two values.

That's it!

No need to expand the characteristic polynomial and then separately apply the quadratic formula.

---

## 7. Worked Example 1: A Matrix from the Video

Consider:

```text
A = [3  1]
    [4  1]
```

We want to find its eigenvalues.

### Step 1: Find the mean

The diagonal entries are 3 and 1.

```text
m = (3+1)/2

m = 2
```

### Step 2: Find the determinant

```text
p = (3*1)-(1*4)

p = -1
```

### Step 3: Apply the formula

```text
lambda1, lambda2 = 2 +/- sqrt(2^2-(-1))
```

Simplify:

```text
lambda1, lambda2 = 2 +/- sqrt(5)
```

Therefore:

```text
lambda1 = 2 + sqrt(5)

lambda2 = 2 - sqrt(5)
```

Approximately:

```text
lambda1 = 4.236

lambda2 = -0.236
```

We have obtained the eigenvalues without explicitly expanding the characteristic polynomial.

### Verify using the trace

The sum should equal the trace:

```text
(2+sqrt(5)) + (2-sqrt(5)) = 4
```

The trace is:

```text
tr(A) = 3+1 = 4
```

Correct.

### Verify using the determinant

The product should equal the determinant:

```text
(2+sqrt(5))*(2-sqrt(5))
    = 4-5
    = -1
```

The determinant is also `-1`.

Everything checks out.

---

## 8. Worked Example 2: Beautifully Simple Eigenvalues

Consider:

```text
A = [2  7]
    [1  8]
```

### Step 1: Calculate the mean

```text
m = (2+8)/2

m = 5
```

### Step 2: Calculate the determinant

```text
p = (2*8)-(7*1)

p = 16-7

p = 9
```

### Step 3: Apply the formula

```text
lambda1, lambda2 = 5 +/- sqrt(5^2-9)
```

Simplify:

```text
lambda1, lambda2 = 5 +/- sqrt(16)
```

Therefore:

```text
lambda1, lambda2 = 5 +/- 4
```

The eigenvalues are:

```text
lambda1 = 9

lambda2 = 1
```

Notice how quickly we obtained the answer.

### Why this is useful

The trace immediately tells us that the eigenvalues average to 5.

The determinant tells us that their product is 9.

The only two numbers with mean 5 and product 9 are 9 and 1.

The formula simply turns that intuition into a reliable calculation.

---

## 9. Worked Example 3: Eigenvalues of 2 and 8

Suppose:

```text
A = [3  5]
    [5  7]
```

Find the eigenvalues.

### Step 1: Calculate the mean

```text
m = (3+7)/2

m = 5
```

### Step 2: Calculate the determinant

```text
p = (3*7)-(5*5)

p = 21-25

p = -4
```

### Step 3: Apply the formula

```text
lambda1, lambda2 = 5 +/- sqrt(5^2-(-4))
```

Simplify:

```text
lambda1, lambda2 = 5 +/- sqrt(29)
```

Therefore:

```text
lambda1 = 5 + sqrt(29)

lambda2 = 5 - sqrt(29)
```

These are not 2 and 8. The mean is 5, but the product is `-4`, not 16.

This example highlights why both pieces of information matter. Knowing the mean alone does not determine the eigenvalues.

---

## 10. What If the Square Root Is Negative?

The formula contains:

```text
sqrt(m^2-p)
```

What happens when:

```text
m^2-p < 0
```

The eigenvalues are then complex conjugates if the matrix has real entries.

For example, consider a 90-degree rotation:

```text
A = [0 -1]
    [1  0]
```

### Step 1: Calculate the mean

```text
m = (0+0)/2

m = 0
```

### Step 2: Calculate the determinant

```text
p = (0*0)-((-1)*1)

p = 1
```

### Step 3: Apply the formula

```text
lambda1, lambda2 = 0 +/- sqrt(0^2-1)
```

Therefore:

```text
lambda1, lambda2 = +/- sqrt(-1)
```

So:

```text
lambda1 = i

lambda2 = -i
```

These are complex eigenvalues.

Geometrically, the rotation has no real eigenvectors because it turns every nonzero real vector by 90 degrees.

The shortcut is still valid, provided we allow complex numbers.

### Three possible cases

| Value of `m^2-p` | Eigenvalues |
|---|---|
| Greater than zero | Two distinct real eigenvalues |
| Equal to zero | A repeated real eigenvalue |
| Less than zero | A complex-conjugate pair, for a real matrix |

This quantity is closely related to the discriminant of the characteristic polynomial.

---

## 11. Repeated Eigenvalues

Consider a matrix that scales every vector by 2:

```text
A = [2  0]
    [0  2]
```

### Step 1: Calculate the mean

```text
m = (2+2)/2

m = 2
```

### Step 2: Calculate the determinant

```text
p = (2*2)-(0*0)

p = 4
```

### Step 3: Apply the formula

```text
lambda1, lambda2 = 2 +/- sqrt(2^2-4)
```

Therefore:

```text
lambda1, lambda2 = 2 +/- sqrt(0)
```

Both eigenvalues are:

```text
lambda1 = 2

lambda2 = 2
```

This is a repeated eigenvalue.

However, remember from the previous chapter that repeated eigenvalues do not necessarily mean there is only one eigenvector direction.

For this particular matrix, every nonzero vector is an eigenvector with eigenvalue 2.

The eigenvalue is repeated, but the eigenspace is the entire 2D space.

---

## 12. Why Trace and Determinant Are Geometrically Meaningful

The shortcut is more than an arithmetic trick.

It brings together two important properties of linear transformations.

### Trace: The sum of the eigenvalues

For a 2×2 matrix:

```text
tr(A) = lambda1+lambda2
```

The trace describes the sum of the eigenvalues, even though the eigenvalues themselves may not be visible directly in the original matrix.

It is invariant under a change of basis.

That means similar matrices representing the same transformation have the same trace.

### Determinant: The product of the eigenvalues

For a 2×2 matrix:

```text
det(A) = lambda1*lambda2
```

The determinant measures the signed area-scaling factor of the transformation.

The eigenvalues describe the scaling along eigenvector directions when those directions are available.

Their product equals the determinant.

For a matrix that can be diagonalized, this is easy to see. In an eigenvector basis, the transformation scales one direction by `lambda1` and the other by `lambda2`. The signed area scales by their product.

The identity remains true even for matrices that cannot be diagonalized.

### The deeper connection

The trace and determinant summarize two important features of the eigenvalues:

- Their sum.
- Their product.

For a 2×2 matrix, those two values are enough to recover the eigenvalues, up to their ordering.

---

## 13. Connection to the Quadratic Formula

The shortcut is closely related to the ordinary quadratic formula.

Suppose a quadratic polynomial is:

```text
x^2 - s*x + p = 0
```

Let its roots be `x1` and `x2`.

Then:

```text
x1+x2 = s

x1*x2 = p
```

Their mean is:

```text
m = s/2
```

Using the mean-product formula:

```text
x1, x2 = m +/- sqrt(m^2-p)
```

Substitute `m = s/2`:

```text
x1, x2 = s/2 +/- sqrt((s/2)^2-p)
```

This is equivalent to the quadratic formula for this particular form of a quadratic.

For a 2×2 matrix, the characteristic polynomial is:

```text
lambda^2 - tr(A)*lambda + det(A) = 0
```

Thus:

```text
lambda1+lambda2 = tr(A)

lambda1*lambda2 = det(A)
```

The mean-product formula is simply the quadratic formula expressed in terms of meaningful matrix properties.

**The real benefit is not that it is a different mathematical method. It is that the relevant values can be read directly from the matrix.**

---

## 14. A Glimpse at Quantum Mechanics: Pauli Matrices

The video briefly explores a family of matrices used in quantum mechanics, called the Pauli matrices.

One of them is:

```text
sigma_x = [0  1]
          [1  0]
```

Its trace is:

```text
tr(sigma_x) = 0
```

Its determinant is:

```text
det(sigma_x) = (0*0)-(1*1)

det(sigma_x) = -1
```

Therefore, the mean of the eigenvalues is zero, and their product is negative one.

Using the mean-product formula:

```text
lambda1, lambda2 = 0 +/- sqrt(0^2-(-1))
```

So:

```text
lambda1, lambda2 = +/- 1
```

The eigenvalues are:

```text
lambda1 = 1

lambda2 = -1
```

The other two Pauli matrices also have eigenvalues `+1` and `-1`.

These matrices are important in quantum mechanics because they represent spin observables along different axes. The eigenvalues correspond to the possible measurement outcomes under the usual normalization convention.

The key point for this chapter is that trace and determinant can make the eigenvalues easy to identify even in applications that look quite different from ordinary geometry.

---

## 15. Connections to AI and Machine Learning

This chapter focuses on 2×2 matrices, but the underlying properties extend to larger square matrices.

### A. PCA and covariance matrices

In Principal Component Analysis, eigenvalues of the covariance matrix tell us how much variance lies along the corresponding principal directions.

The trace of a covariance matrix equals the sum of its eigenvalues.

It also equals the sum of the variances of the original features, because those variances occupy the diagonal of the covariance matrix.

For example, suppose a covariance matrix has two eigenvalues:

```text
lambda1 = 8

lambda2 = 2
```

The total variance is:

```text
Total variance = 8+2 = 10
```

The first principal component accounts for:

```text
8/10 = 80%
```

of the total variance.

This is an important connection to dimensionality reduction.

### B. Understanding linear systems

The determinant tells us whether a square matrix is invertible.

For a 2×2 matrix:

```text
det(A) = lambda1*lambda2
```

If the determinant is zero, at least one eigenvalue must be zero.

A zero eigenvalue means the matrix maps some nonzero vector to zero.

That is associated with a loss of information along at least one direction and a failure of invertibility.

In ML, rank-deficient matrices can appear when features are redundant or when data lies in a lower-dimensional subspace.

### C. Repeated transformations

If a linear system evolves according to:

```text
x_(t+1) = A*x_t
```

then after `t` steps:

```text
x_t = A^t*x_0
```

Eigenvalues help describe how different directions grow, shrink, or oscillate under repeated application.

The trace and determinant do not tell us everything about the system, but they summarize useful information about its eigenvalues.

### D. An important limitation

This shortcut directly finds eigenvalues only for 2×2 matrices.

For larger matrices, the trace still equals the sum of the eigenvalues, and the determinant still equals their product, counting algebraic multiplicities.

But those two quantities alone are generally insufficient to determine all the eigenvalues of a matrix of dimension 3 or higher.

For larger matrices, we usually need the characteristic polynomial or numerical eigenvalue algorithms.

---

## 16. Common Misconceptions

### Misconception 1: The trace is the product of the eigenvalues

No.

```text
Trace = Sum of eigenvalues
```

```text
Determinant = Product of eigenvalues
```

### Misconception 2: The shortcut is unrelated to the quadratic formula

It is equivalent to the quadratic formula applied to the characteristic polynomial of a 2×2 matrix.

The advantage is that the trace and determinant provide the sum and product directly.

### Misconception 3: A negative determinant means both eigenvalues are negative

Not for a real 2×2 matrix with real eigenvalues.

If the determinant is negative, the eigenvalues have opposite signs.

If the eigenvalues are complex, their product is nonnegative because they occur as a complex-conjugate pair.

### Misconception 4: A repeated eigenvalue means there is only one eigenvector

No.

The number of independent eigenvectors depends on the matrix, not just on whether the eigenvalue is repeated.

### Misconception 5: The formula works only when the eigenvalues are real

The formula also works over the complex numbers.

A negative value inside the square root gives complex eigenvalues.

### Misconception 6: The shortcut finds eigenvectors too

No.

It finds the eigenvalues. To find the corresponding eigenvectors, solve:

```text
(A-lambda*I)*v = 0
```

for each eigenvalue.

---

## 17. Quick Revision Sheet

| Concept | Formula or fact |
|---|---|
| Trace | `tr(A) = a+d` |
| Determinant | `det(A) = a*d-b*c` |
| Sum of eigenvalues | `lambda1+lambda2 = tr(A)` |
| Product of eigenvalues | `lambda1*lambda2 = det(A)` |
| Mean of eigenvalues | `m = tr(A)/2` |
| Product of eigenvalues | `p = det(A)` |
| Mean-product formula | `lambda1,lambda2 = m +/- sqrt(m^2-p)` |
| Characteristic equation | `det(A-lambda*I) = 0` |

### The one formula worth remembering

For a 2×2 matrix:

```text
A = [a  b]
    [c  d]
```

calculate:

```text
m = (a+d)/2

p = a*d-b*c
```

Then:

```text
lambda1, lambda2 = m +/- sqrt(m^2-p)
```

This is the entire shortcut.

---

## 18. Self-Test

Try to solve these without looking at the answers.

### Question 1

Find the eigenvalues of:

```text
A = [4  0]
    [0  6]
```

### Question 2

Find the eigenvalues of:

```text
A = [3  1]
    [2  4]
```

### Question 3

Find the eigenvalues of:

```text
A = [2  1]
    [1  2]
```

### Question 4

A 2×2 matrix has trace 10 and determinant 21.

What are its eigenvalues?

### Question 5

A 2×2 matrix has trace 0 and determinant 9.

What can you conclude about its eigenvalues?

### Question 6

A 2×2 matrix has eigenvalues 3 and 7.

What are its trace and determinant?

### Question 7

Can you determine the eigenvalues of every 3×3 matrix from its trace and determinant alone?

Explain why or why not.

---

## 19. Self-Test Answers

### Answer 1

The matrix is diagonal, so the eigenvalues are its diagonal entries:

```text
lambda1 = 4

lambda2 = 6
```

Using the shortcut gives the same result:

```text
m = (4+6)/2 = 5

p = 4*6 = 24
```

Therefore:

```text
lambda1, lambda2 = 5 +/- sqrt(25-24)

lambda1, lambda2 = 5 +/- 1
```

So the eigenvalues are 6 and 4.

### Answer 2

For:

```text
A = [3  1]
    [2  4]
```

Calculate the mean:

```text
m = (3+4)/2

m = 3.5
```

Calculate the determinant:

```text
p = (3*4)-(1*2)

p = 10
```

Apply the formula:

```text
lambda1, lambda2 = 3.5 +/- sqrt(3.5^2-10)
```

Simplify:

```text
lambda1, lambda2 = 3.5 +/- sqrt(2.25)
```

Therefore:

```text
lambda1 = 5

lambda2 = 2
```

### Answer 3

For:

```text
A = [2  1]
    [1  2]
```

Calculate:

```text
m = (2+2)/2 = 2

p = (2*2)-(1*1) = 3
```

Then:

```text
lambda1, lambda2 = 2 +/- sqrt(4-3)
```

Therefore:

```text
lambda1 = 3

lambda2 = 1
```

### Answer 4

The mean is:

```text
m = 10/2 = 5
```

The product is:

```text
p = 21
```

Therefore:

```text
lambda1, lambda2 = 5 +/- sqrt(25-21)
```

So:

```text
lambda1, lambda2 = 5 +/- 2
```

The eigenvalues are 7 and 3.

### Answer 5

The mean is zero, and the product is 9.

```text
lambda1, lambda2 = 0 +/- sqrt(0-9)
```

Therefore:

```text
lambda1 = 3i

lambda2 = -3i
```

The eigenvalues are complex conjugates.

### Answer 6

The trace equals the sum:

```text
tr(A) = 3+7 = 10
```

The determinant equals the product:

```text
det(A) = 3*7 = 21
```

### Answer 7

No.

For a 3×3 matrix, the trace gives the sum of three eigenvalues, and the determinant gives their product.

Those two constraints generally do not uniquely determine three unknown eigenvalues.

Additional information, such as the characteristic polynomial's remaining coefficient, is needed.

---

## 20. Final Takeaway

This chapter gives you a shortcut, but the real lesson is the connection between different mathematical descriptions of a matrix.

For a 2×2 matrix:

- The trace tells you the sum of the eigenvalues.
- The determinant tells you their product.
- The mean-product formula recovers the two eigenvalues.

Instead of calculating the characteristic polynomial every time, you can often read the answer almost directly from the matrix.

**Your checkpoint:** Given a 2×2 matrix, you should now be able to calculate its eigenvalues quickly, explain why the trace gives their sum, and explain why the determinant gives their product.

Next up: **Chapter 16, Abstract Vector Spaces**, the final chapter of the series. It generalizes the ideas you've learned beyond the familiar world of arrows and coordinate grids.
