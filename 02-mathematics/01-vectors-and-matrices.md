# Chapter 1: Vectors and Matrices

## Why mathematics matters in AI

A machine-learning model receives information, performs calculations, and produces an output. Mathematics gives us a precise language for describing those calculations. You do not need to memorise formulas without meaning; learn what each object represents and what operation does to it.

## 1. Numbers, coordinates, and datasets

A number can represent a measurement, such as temperature. A coordinate describes a position. On a two-dimensional graph, a point `(x, y)` means move `x` units along the horizontal axis and `y` units along the vertical axis.

A **dataset** is a collection of examples. Imagine recording hours studied and test scores:

| Hours (x) | Score (y) |
|---:|---:|
| 1 | 52 |
| 2 | 60 |
| 3 | 68 |
| 4 | 76 |

Each row is one observation. A graph may show that higher study hours are associated with higher scores in this small dataset. Association does not by itself prove cause and effect.

## 2. Vectors

A **vector** is an ordered list of numbers. It can represent a group of measurements or a point in a space.

`[1, 2, 3]` is a vector with three components. A single number such as 2 is called a **scalar**.

Vectors of the same length can be added component by component:

`[1, 2, 3] + [4, 5, 6] = [5, 7, 9]`

A scalar can multiply every component:

`2 × [1, 2, 3] = [2, 4, 6]`

The **dot product** multiplies corresponding components and adds the results:

`[1, 2, 3] · [4, 5, 6] = 1×4 + 2×5 + 3×6 = 32`

Dot products are important in machine learning because a model can combine input values with weights using this operation.

## 3. Matrices

A **matrix** is a rectangular arrangement of numbers in rows and columns.

```text
1  2  3
4  5  6
```

This matrix has 2 rows and 3 columns, so its shape is `(2, 3)`.

In NumPy:

```python
import numpy as np

A = np.array([[1, 2, 3],
              [4, 5, 6]])

print(A.shape)  # (2, 3)
```

A **transpose** swaps rows and columns:

```python
print(A.T)
```

The result has shape `(3, 2)`.

## 4. Matrix multiplication and shape

Matrix multiplication combines rows of the first matrix with columns of the second. The inner dimensions must match.

A matrix with shape `(2, 3)` can multiply one with shape `(3, 4)`. The result has shape `(2, 4)`.

The first matrix has 3 columns and the second has 3 rows, so the inner dimensions match. The output keeps the outer dimensions: 2 and 4.

In NumPy, use `@` for matrix multiplication:

```python
A = np.array([[1, 2, 3],
              [4, 5, 6]])

B = np.ones((3, 4))
C = A @ B

print(C.shape)  # (2, 4)
```

Do not confuse matrix multiplication with element-wise multiplication. They are different operations with different shape rules.

## Check your understanding

1. What is the difference between a scalar and a vector?
2. Calculate `[2, 1] + [3, 4]`.
3. Calculate the dot product of `[2, 3]` and `[4, 5]`.
4. What is the shape of a matrix with 5 rows and 2 columns?
5. What is the output shape of `(2, 3) @ (3, 4)`?
6. Why is a transpose useful?

## Practice

Create two NumPy vectors. Add them and calculate their dot product. Then create matrices with shapes `(2, 3)` and `(3, 2)`, multiply them, and print the result shape.

## Summary

Vectors represent ordered numerical information. Matrices organise values into rows and columns. Their shapes determine which operations are valid. These ideas appear throughout neural networks and transformer models.

**Next:** [Chapter 2 — Functions, probability, and statistics](02-functions-probability-and-statistics.md)
