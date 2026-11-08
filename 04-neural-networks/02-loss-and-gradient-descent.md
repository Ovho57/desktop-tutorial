# Chapter 2: Loss and Gradient Descent

## 1. Predictions need a measure of error

A neural network produces a prediction. During supervised training, we compare that prediction with the target answer.

A **loss function** turns the difference between prediction and target into a numerical score. The training process aims to reduce this score.

For a numerical prediction, mean squared error is one possible loss:

`MSE = average((prediction - target)²)`

Squaring makes errors positive and penalises large differences more strongly. Other tasks use other loss functions.

## 2. Parameters are adjusted during training

Weights and biases are **parameters**. Training changes these values so the network's predictions become more useful.

A **gradient** tells us how the loss changes with respect to each parameter. Gradient descent updates parameters in the direction opposite the gradient.

`new weight = old weight - learning rate × gradient`

The **learning rate** controls the update size. If too large, updates can overshoot useful values. If too small, learning can take a long time.

## 3. The training loop

A simplified training loop follows this sequence:
1. Pass input examples through the network.
2. Calculate predictions.
3. Compare predictions with targets using a loss function.
4. Calculate gradients.
5. Update the parameters.
6. Repeat over many batches.

A complete pass through the training dataset is called an **epoch**. A **batch** is a subset of examples processed together before an update.

## 4. Backpropagation

**Backpropagation** is the method used to calculate how the loss depends on parameters throughout the network. It applies the chain rule from calculus, moving backward through the operations that produced the prediction.

Backpropagation calculates gradients; an optimiser uses those gradients to update parameters. They are related but not identical jobs.

## 5. Optimisers

An **optimiser** is the algorithm that updates model parameters using gradients. Basic gradient descent uses the gradient directly. More advanced optimisers, such as Adam, adapt update sizes using running information from previous gradients.

An optimiser does not magically know the correct answer. It follows a numerical update rule.

## Check your understanding

1. What does a loss function measure?
2. What are weights and biases?
3. What does the learning rate control?
4. What is an epoch?
5. What does backpropagation calculate?
6. How is an optimiser different from backpropagation?

## Practice

Write out the six stages of the training loop in your own words. Then calculate a gradient-descent update for a parameter whose current value is 2, gradient is -0.5, and learning rate is 0.1.

**Next:** [Chapter 3 — Build a tiny neural network](03-build-a-tiny-network.md)
