# Chapter 2: Functions, Probability, and Statistics

## 1. Functions describe relationships

A **function** is a rule that maps an input to an output. For example:

`f(x) = 2x + 1`

If `x = 3`, then `f(3) = 7`.

In Python:

```python
def f(x):
    return 2 * x + 1

print(f(3))
```

A simple model often behaves like a function: it receives input data and produces a prediction.

## 2. Parameters and features

A **feature** is an input measurement used by a model. A **parameter** is a value inside a model that controls its behaviour.

Consider:

`y = wx + b`

Here:
- `x` is the input feature.
- `y` is the output or prediction.
- `w` is the weight that scales the input.
- `b` is the bias that shifts the output.

If `w = 2`, `b = 1`, and `x = 3`, the output is 7. During training, a model adjusts parameters to make its predictions more useful.

## 3. Probability

**Probability** measures how likely an event is. It ranges from 0 to 1:
- 0 means impossible under the model.
- 1 means certain.
- 0.5 means a 50% chance.

For a fair six-sided die, the probability of rolling a 4 is `1/6`, because one of the six equally likely outcomes is a 4.

A model that predicts classes may output probabilities such as:
- cat: 0.70
- dog: 0.20
- bird: 0.10

These values sum to 1. The model's highest probability is its preferred class, but a probability is not a guarantee that the prediction is correct.

## 4. Averages and variation

The **mean** is the sum of values divided by the number of values.

For scores 60, 70, and 80:

`mean = (60 + 70 + 80) / 3 = 70`

The mean gives a measure of the centre of the data, but it does not tell us how spread out the values are.

**Variance** measures average squared distance from the mean. **Standard deviation** is the square root of variance and describes spread in the original units.

A set of values clustered near the mean has a smaller standard deviation than a set spread far away from it.

In Python:

```python
import numpy as np

scores = np.array([60, 70, 80])
print(scores.mean())
print(scores.std())
```

NumPy's default standard deviation uses the population convention. Statistical estimates from a sample may use a different convention.

## 5. Why statistics matter

Data can contain unusual values, missing measurements, or imbalanced categories. Averages alone can hide these issues. Before training a model, inspect the data:
- How many examples are there?
- What ranges do numerical values cover?
- Are some classes much more common than others?
- Are values missing or duplicated?

## Check your understanding

1. What does a function do?
2. In `y = wx + b`, which symbols are parameters?
3. What does a probability of 0.8 mean?
4. Calculate the mean of 4, 6, and 8.
5. What does standard deviation describe?
6. Why should you inspect a dataset before training?

## Practice

Create a NumPy array containing five test scores. Calculate its mean, minimum, maximum, and standard deviation. Write two sentences explaining what those numbers tell you and what they do not tell you.

**Next:** [Chapter 3 — Derivatives and gradients](03-derivatives-and-gradients.md)
