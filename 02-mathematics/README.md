# 02 — Math for AI

This module teaches the mathematical ideas that appear in machine learning and neural networks. You do not need to be a mathematician. The goal is to understand what the calculations mean and why AI uses them.

**Prerequisite:** [01 — Python Foundations](../01-python/README.md), especially variables, functions, and basic NumPy arrays.

[Back to course home](../README.md)

## Learning goals

You will learn numbers and graphs as data, vectors, matrices, functions, probability, averages and variation, derivatives, and gradients. Each topic is introduced before it is used in a later lesson.

---

# Lesson 1 — Numbers, coordinates, and graphs

A number can describe a quantity, such as a temperature or a price. A **coordinate** describes a position. On a simple graph, a point is written as `(x, y)`: first move along the horizontal x-axis, then along the vertical y-axis.

For example, the point `(2, 3)` is two units right and three units up from the origin `(0, 0)`.

A **dataset** is a collection of examples. Imagine recording hours studied and test scores:

| Hours studied (x) | Score (y) |
|---:|---:|
| 1 | 52 |
| 2 | 60 |
| 3 | 68 |
| 4 | 76 |

Each row is one observation. A graph of these points may show a relationship: in this small example, more study hours are associated with higher scores. Association alone does not prove that one thing caused the other.

### Checkpoint

1. What does a coordinate `(x, y)` represent?
2. What is a dataset?
3. Does a relationship in a dataset automatically prove cause and effect?

**Practice:** Write down three pairs of values, such as hours practised and a score. Identify which value is x and which is y.

---

# Lesson 2 — Vectors

A **vector** is an ordered list of numbers. It can represent measurements or a point in a space.

```python
import numpy as np

hours = np.array([1, 2, 3, 4])
scores = np.array([52, 60, 68, 76])
```

The vector `hours` contains four measurements. The first value in `hours` corresponds to the first value in `scores`, and so on.

Vectors of the same length can be added element by element:

[
[1,2,3] + [4,5,6] = [5,7,9]
]

They can also be multiplied by a number called a **scalar**:

[
2[1,2,3] = [2,4,6]
]

A scalar is just one number, as opposed to a vector containing multiple numbers.

The **dot product** combines two same-length vectors by multiplying corresponding values and adding the results:

[
[1,2,3]cdot[4,5,6] = 1(4)+2(5)+3(6)=32
]

Dot products are important in machine learning because they let a model combine input values with learned weights.

### Checkpoint

1. What is a vector?
2. What is a scalar?
3. Calculate `[2, 1] + [3, 4]`.
4. Calculate the dot product of `[2, 3]` and `[4, 5]`.

**Practice:** Use NumPy to create two vectors and calculate their sum and dot product.

---

# Lesson 3 — Matrices and shapes

A **matrix** is a rectangular arrangement of numbers in rows and columns.

[
A =
egin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
end{bmatrix}
]

This matrix has 2 rows and 3 columns, so its **shape** is `(2, 3)`.

In NumPy:

```python
import numpy as np

A = np.array([[1, 2, 3],
              [4, 5, 6]])

print(A.shape)  # (2, 3)
```

A **transpose** swaps rows and columns:

[
A^T =
egin{bmatrix}
1 & 4 \\
2 & 5 \\
3 & 6
end{bmatrix}
]

Matrix multiplication combines rows from the first matrix with columns from the second. The inside dimensions must match. A matrix with shape `(2, 3)` can multiply a matrix with shape `(3, 4)`; the result has shape `(2, 4)`.

This shape rule is crucial. If the inner dimensions do not match, the multiplication is not defined.

### Checkpoint

1. How many rows and columns are in a `(2, 3)` matrix?
2. What does a transpose do?
3. What is the result shape of `(2, 3) @ (3, 4)`?
4. Why do dimensions matter in matrix multiplication?

**Practice:** Create a 2-by-3 NumPy matrix. Print its shape and transpose.

---

# Lesson 4 — Functions and relationships

A **function** describes a rule that maps an input to an output. For example:

[
f(x) = 2x + 1
]

If the input `x` is 3, the output is 7. The input is the independent variable; the output depends on it.

In Python:

```python
def f(x):
    return 2 * x + 1

print(f(3))
```

A simple machine-learning model often uses a function to turn input features into a prediction. A **feature** is an input measurement the model uses. For example, house size could be a feature used to predict a house price.

A **parameter** in a mathematical model is a value that controls the model's behaviour. In the line:

[
y = wx + b
]

`w` and `b` are parameters. `x` is the input and `y` is the output. Later, you will learn how a model can adjust its parameters using training data. For now, understand the roles: input goes in, parameters control the rule, prediction comes out.

### Checkpoint

1. What does a function do?
2. For `f(x) = 2x + 1`, what is `f(4)`?
3. In `y = wx + b`, which symbols are parameters?
4. What is a feature?

**Practice:** Write a Python function for `y = 3x + 2`. Test it with three different values of x.

---

# Lesson 5 — Probability

**Probability** measures how likely an event is. It ranges from 0 to 1:
- 0 means impossible.
- 1 means certain.
- 0.5 means a 50% chance.

For a fair six-sided die, each side has probability `1/6`. The probability of rolling an even number is `3/6 = 0.5`, because three of the six possible outcomes are even.

A **random variable** is a number whose value depends on the outcome of a random process. For example, the number shown on a die is a random variable.

A **distribution** describes the probabilities of possible values. A fair die has a uniform distribution because each side is equally likely.

In AI, probability helps describe uncertainty. A classifier might output estimated probabilities for possible categories. These values can help express how strongly the model favours each category, though they are not automatically guaranteed to be well-calibrated.

### Checkpoint

1. What does a probability of 0 mean?
2. What is the chance of rolling an even number on a fair six-sided die?
3. What does a probability distribution describe?

**Practice:** A bag has 3 red balls and 1 blue ball. What is the probability of selecting a red ball at random? Show your calculation.

---

# Lesson 6 — Average, spread, and data summaries

The **mean** is the arithmetic average: add the values and divide by the number of values.

For `2, 4, 6`, the mean is `(2 + 4 + 6) / 3 = 4`.

The **median** is the middle value after sorting. For `2, 4, 100`, the median is 4. The median is less affected by an extreme value than the mean.

The **range** is the maximum minus the minimum. It gives a simple measure of spread.

**Variance** measures how far values tend to be from the mean by averaging squared differences from the mean. **Standard deviation** is the square root of variance, expressed in the same units as the original values.

Use NumPy:

```python
import numpy as np

scores = np.array([60, 70, 80, 90])
print("Mean:", scores.mean())
print("Median:", np.median(scores))
print("Standard deviation:", scores.std())
```

These summaries help us understand a dataset before training a model.

### Checkpoint

1. How do you calculate the mean?
2. What is the median of `1, 5, 9`?
3. What does standard deviation tell us in general?
4. Why can the median be useful when a dataset contains an extreme value?

**Practice:** Calculate the mean, median, and range of `3, 5, 5, 7, 20`.

---

# Lesson 7 — Slopes and derivatives

A **slope** describes how much one value changes compared with another. For a straight line, slope is:

[
m = \frac{\text{change in } y}{\text{change in } x}
]

For example, if y increases from 2 to 8 while x increases from 1 to 3, the slope is `(8 - 2) / (3 - 1) = 3`.

A **derivative** extends the idea of slope to a curve. It describes the rate at which a function's output changes at a particular input.

For the function:

[
f(x) = x^2
]

the derivative is:

[
f'(x) = 2x
]

At `x = 3`, the derivative is 6. This means the curve's slope at that point is 6.

You do not need to memorise many derivative rules yet. The key idea is that a derivative tells us how sensitive an output is to a small change in an input.

### Checkpoint

1. What does slope measure?
2. What does a derivative tell us?
3. If `f'(x) = 2x`, what is the derivative at `x = 4`?

**Practice:** For `f(x) = x^2`, calculate the derivative formula shown above at x = 1, 2, and 5.

---

# Lesson 8 — Gradients and learning

A **gradient** is a collection of derivatives for a function with multiple inputs. It tells us how the output changes when each input changes.

In machine learning, we often define a **loss function**: a number that measures how wrong a model's predictions are. A lower loss generally means predictions are closer to the target values according to that loss measure.

Imagine a simple loss curve depending on one parameter. The derivative tells us which direction makes the loss increase. To reduce the loss, we can move the parameter in the opposite direction.

This idea leads to **gradient descent**:

1. Start with parameter values.
2. Calculate the loss.
3. Calculate the gradient of the loss.
4. Move parameters a little in the direction that reduces the loss.
5. Repeat.

The **learning rate** controls how large each update is. If it is too large, updates may jump around or fail to settle. If it is too small, learning may be very slow.

You will implement this process in the neural-network module. Here, focus on the idea: use the slope of the loss to decide how to adjust parameters.

### Checkpoint

1. What does a loss function measure?
2. What information does a gradient provide?
3. In gradient descent, why do we move opposite the gradient?
4. What does the learning rate control?

**Practice:** Explain gradient descent using a hill analogy. Identify what represents the height, the direction downhill, and the size of each step.

---

## Module project — Explore a tiny dataset

Use NumPy to:
1. Create an array of five study-hour values.
2. Create an array of five matching test scores.
3. Calculate the mean score.
4. Calculate the dot product of a vector you choose and explain what it computes.
5. Write a function `predict(hours, weight, bias)` that returns `weight * hours + bias`.
6. Try several weights and biases and observe how predictions change.

Do not claim this simple line is a good predictive model yet. In Module 03, you will learn how to fit and evaluate a model using data.

## Vocabulary

| Term | Meaning |
|---|---|
| Coordinate | A value describing a position |
| Dataset | A collection of examples |
| Vector | An ordered list of numbers |
| Scalar | A single number |
| Dot product | Multiply matching vector values and add the results |
| Matrix | A rectangular grid of numbers |
| Shape | The number of entries along each array dimension |
| Transpose | Swap rows and columns |
| Function | A rule mapping inputs to outputs |
| Feature | An input measurement used by a model |
| Parameter | A value controlling a model's behaviour |
| Probability | A measure of how likely an event is |
| Mean | Arithmetic average |
| Median | Middle value in sorted data |
| Variance | Average squared distance from the mean |
| Derivative | Rate of change at a point |
| Gradient | Derivatives for a function with multiple inputs |
| Loss | A number measuring prediction error |
| Learning rate | Size of a parameter update |

## Continue

[Go to 03 — Machine Learning](../03-machine-learning/README.md)
