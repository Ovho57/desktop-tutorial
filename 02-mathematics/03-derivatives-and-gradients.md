# Chapter 3: Derivatives and Gradients

## 1. Why do models need derivatives?

A model has parameters. Training tries to find parameter values that make its predictions better. To improve a parameter systematically, we need to know how changing it affects the error.

A **derivative** measures how quickly a function's output changes when its input changes. It is the slope of a function at a point.

For the function `f(x) = x²`, the derivative is `f'(x) = 2x`. At `x = 3`, the slope is 6. This means that near 3, a small increase in x produces approximately six times that small change in the function's output.

## 2. A simple numerical intuition

Imagine a hill. If you are standing on a steep slope, a small step changes your height a lot. If you are on flat ground, the same step changes your height only a little.

The derivative describes this local steepness. A positive derivative means the function rises as x increases. A negative derivative means it falls. A derivative near zero means the function is locally flat.

## 3. Partial derivatives

A model often has many parameters. A **partial derivative** measures how the output changes when one parameter changes while the others are held fixed.

For a function of two variables, `L(w, b)`, we can ask:
- How does the loss change when w changes?
- How does the loss change when b changes?

Each answer is a partial derivative.

## 4. Gradients

A **gradient** is a collection of partial derivatives. It points in the direction of the steepest increase of a function.

If we want to reduce a loss function, we move in the opposite direction of the gradient. This is the central idea behind **gradient descent**.

A simplified update is:

`new parameter = old parameter - learning rate × gradient`

The **learning rate** controls the size of each update. If it is too large, training may jump around or diverge. If it is too small, learning may be very slow.

## 5. A tiny numerical example

Suppose the loss is `L(w) = (w - 3)²`. Its derivative is `2(w - 3)`.

If `w = 1`, the derivative is -4. With a learning rate of 0.1:

`new w = 1 - 0.1 × (-4) = 1.4`

The parameter moves closer to 3, where this simple loss reaches zero.

This example is deliberately small. Real neural networks have many parameters and use automatic differentiation to calculate gradients efficiently.

## 6. What automatic differentiation does

Frameworks such as PyTorch and JAX can track mathematical operations and calculate derivatives automatically. This is called **automatic differentiation**. It applies the chain rule to the sequence of operations that produced a result.

You do not need to implement a full differentiation engine before training a model, but you should understand what the calculated gradients mean.

## Check your understanding

1. What does a derivative measure?
2. What does a negative derivative tell you?
3. What is a partial derivative?
4. What information does a gradient contain?
5. Why does gradient descent move opposite the gradient?
6. What can happen if the learning rate is too high?

## Practice

For `L(w) = (w - 5)²`, use the derivative `2(w - 5)`. Start at `w = 1` and use learning rate 0.1. Calculate one update by hand. Then write a short Python loop that performs ten updates and prints the value of w after each step.

## Summary

Derivatives measure local change. Gradients collect derivatives for all parameters. Gradient descent uses those gradients to update parameters in a direction intended to reduce loss.

**Continue:** [Module 03 — Machine Learning](../03-machine-learning/README.md)
