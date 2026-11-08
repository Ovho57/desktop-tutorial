# Chapter 1: Neurons and Layers

## 1. Why neural networks?

A neural network is a model made from connected mathematical operations. It can learn complex relationships by adjusting numerical parameters during training.

The name comes from a loose inspiration from biological nervous systems. An artificial neuron is a mathematical unit, not a realistic simulation of a human brain cell.

## 2. The artificial neuron

A simple neuron receives input values, multiplies them by weights, adds a bias, and applies an activation function.

`z = w₁x₁ + w₂x₂ + b`

Here:
- `x₁` and `x₂` are input features.
- `w₁` and `w₂` are weights.
- `b` is a bias.
- `z` is the weighted sum before activation.

A **weight** controls how strongly an input contributes. A **bias** shifts the weighted sum.

For example, if `x₁ = 2`, `x₂ = 3`, `w₁ = 0.5`, `w₂ = 1`, and `b = -1`, then:

`z = 0.5×2 + 1×3 - 1 = 3`

## 3. Activation functions

An **activation function** transforms a neuron's weighted sum. Without nonlinear activations, stacking ordinary linear layers would still produce a linear function overall.

A common activation is ReLU:

`ReLU(z) = max(0, z)`

If `z = 3`, ReLU returns 3. If `z = -2`, it returns 0.

Another activation is sigmoid, which maps a real number to a value between 0 and 1. It is often used to represent a binary probability at an output.

## 4. Layers

A **layer** is a group of neurons or a group of operations at one stage of a network. A simple feed-forward network may contain:
- An input layer that receives features.
- One or more hidden layers that transform representations.
- An output layer that produces predictions.

A **hidden layer** is an intermediate layer between input and output. Its internal values are not usually the final answer presented to a user.

## Check your understanding

1. What does a weight control?
2. What is the purpose of a bias?
3. What does an activation function do?
4. Why are nonlinear activations important?
5. What is a hidden layer?

## Practice

Calculate a neuron's weighted sum using `x₁=4`, `x₂=2`, `w₁=0.5`, `w₂=-1`, and `b=2`. Then apply ReLU. Show every step.

**Next:** [Chapter 2 — Loss and gradient descent](02-loss-and-gradient-descent.md)
