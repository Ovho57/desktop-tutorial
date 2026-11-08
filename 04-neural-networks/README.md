# 04 — Neural Networks

A neural network is a model made from connected mathematical units. This module builds the idea from a single calculation toward a small trainable network.

**Prerequisites:** [02 — Math for AI](../02-mathematics/README.md) and [03 — Machine Learning](../03-machine-learning/README.md). You should know vectors, functions, parameters, loss, and the difference between training and test data.

[Back to course home](../README.md)

---

# Lesson 1 — From a line to a neuron

You have already seen a simple model:

[
y = wx + b
]

A **neuron** (also called a unit) performs a weighted sum of its inputs and usually passes the result through an activation function.

With several inputs:

[
z = w_1x_1 + w_2x_2 + b
]

Here:
- `x1` and `x2` are input values.
- `w1` and `w2` are weights.
- `b` is a bias.
- `z` is the calculated weighted sum.

A weight controls how strongly an input affects the result. A bias shifts the result. These are **parameters** because training can adjust them.

For example, if `x1=2`, `x2=3`, `w1=0.5`, `w2=1`, and `b=1`, then `z = 0.5(2) + 1(3) + 1 = 5`.

### Checkpoint

1. What does a neuron calculate before activation?
2. What is a weight?
3. What is a bias?
4. Calculate z when x1=1, x2=2, w1=2, w2=3, and b=1.

---

# Lesson 2 — Activation functions

If every layer only performed linear calculations, stacking layers would still produce a linear function. Neural networks need **nonlinear** operations to learn more complex patterns.

An **activation function** transforms a neuron's calculated value before passing it onward.

Three common examples:

**ReLU** (Rectified Linear Unit):

[
ReLU(z) = \max(0,z)
]

It returns zero for negative inputs and returns the input for positive inputs.

**Sigmoid** maps any real number to a value between 0 and 1:

[
\sigma(z) = \frac{1}{1+e^{-z}}
]

It is often used to produce a binary classification score at an output layer.

**Tanh** maps values between -1 and 1.

You do not need to memorise every formula immediately. Understand that activation functions add nonlinearity, which lets networks represent more than simple straight-line relationships.

### Checkpoint

1. Why do networks use nonlinear activation functions?
2. What does ReLU return for z = -3?
3. What does ReLU return for z = 4?
4. What range does sigmoid produce?

**Practice:** Calculate ReLU for `[-2, 0, 3]`.

---

# Lesson 3 — Layers and a network

A **layer** is a group of neurons that perform calculations at the same stage. A basic feed-forward network has:
- An input layer, which receives the data.
- One or more hidden layers, which transform it.
- An output layer, which produces the prediction.

A **hidden layer** is called hidden because its values are internal to the model rather than the final answer shown to the user.

A network passes information from one layer to the next. This is called a **forward pass**.

For a layer, the calculation can be written compactly as:

[
z = Wx + b
]

Here, `x` is a vector of inputs, `W` is a matrix of weights, and `b` is a vector of biases. The dimensions must line up for the matrix multiplication to work. The activation function is then applied to z.

The word **architecture** means the design or arrangement of a network: how many layers it has, how many neurons each layer contains, and how they connect. Architecture is a design choice; weights and biases are numerical parameters learned during training.

### Checkpoint

1. What is a hidden layer?
2. What is a forward pass?
3. What does architecture describe?
4. Are weights and biases architecture or parameters?

**Practice:** Draw a network with two input values, one hidden layer containing three neurons, and one output neuron. Label the input, hidden, and output layers.

---

# Lesson 4 — Predictions and loss

A network's output is its prediction. During supervised training, we compare the prediction with the known target.

A **loss function** turns the difference between prediction and target into a number. The training process tries to reduce this number.

For a simple numerical example, squared error is:

[
L = (\hat y-y)^2
]

If the actual value is 5 and the prediction is 7, the squared error is 4.

Different tasks use different loss functions. Mean squared error is common for regression. Cross-entropy loss is common for classification. The choice should match the task and output representation.

A loss value by itself does not tell the whole story. We also evaluate the model on held-back data and choose meaningful metrics.

### Checkpoint

1. What does a loss function measure?
2. Calculate squared error when the target is 8 and prediction is 6.
3. Why should the loss match the task?
4. Why do we still need test data?

---

# Lesson 5 — How a network learns: gradient descent

A neural network starts with weights and biases that usually do not give good predictions. Training adjusts these parameters.

**Gradient descent** is an optimisation method: a procedure for choosing parameter updates that reduce a loss function.

For one parameter `w`, a gradient descent update is:

[
w_{new} = w_{old} - \eta \frac{dL}{dw}
]

The symbol `η` (eta) is the **learning rate**. The derivative tells us how the loss changes as w changes. Subtracting the derivative moves in the direction that locally reduces loss.

If the learning rate is too high, updates may overshoot. If it is too low, training may take a long time.

### Checkpoint

1. What is gradient descent trying to reduce?
2. What does the derivative tell us?
3. What does the learning rate control?
4. What can happen if the learning rate is too large?

---

# Lesson 6 — Backpropagation

A network may have thousands or millions of parameters. We need an efficient way to calculate how each parameter contributed to the loss.

**Backpropagation** is an algorithm for calculating gradients through the network. It applies the chain rule from calculus, working backward from the loss through the output and earlier layers.

The high-level training cycle is:

1. **Forward pass:** calculate a prediction.
2. **Loss calculation:** compare prediction with target.
3. **Backward pass:** calculate gradients for parameters.
4. **Update:** use an optimiser such as gradient descent to adjust parameters.
5. Repeat with more examples.

Backpropagation calculates gradients; it does not itself decide every training setting or guarantee that the model will learn well. The optimiser uses those gradients to update parameters.

### Checkpoint

1. What is the purpose of backpropagation?
2. Does backpropagation calculate predictions or gradients?
3. What happens in the forward pass?
4. What uses the gradients to update the parameters?

**Practice:** Write the five training-cycle steps in your own words. Do not worry about deriving the chain rule yet; focus on what flows forward and what is calculated backward.

---

# Lesson 7 — Batches, epochs, and optimisers

Training on every example at once can be slow or use too much memory. A **batch** is a smaller group of training examples processed together.

An **epoch** is one complete pass through the training dataset. If a dataset has 1,000 examples and batch size is 100, one epoch contains 10 batches (assuming the data divides evenly).

An **optimiser** is the method that applies parameter updates using gradients. Stochastic gradient descent (SGD) and Adam are common optimisers. Adam adjusts update sizes using running estimates of gradient statistics; it is often a practical starting point, but not always best.

Training logs often show **training loss** and **validation loss**. If training loss keeps falling while validation loss starts rising, the model may be overfitting.

### Checkpoint

1. What is a batch?
2. What is an epoch?
3. How many batches are there for 600 examples with batch size 100?
4. What is an optimiser?
5. What might rising validation loss indicate?

---

# Lesson 8 — Build a small neural network with PyTorch

**PyTorch** is a Python library for tensor calculations and neural-network training. A **tensor** is a multi-dimensional array, similar in spirit to a NumPy array, with additional support for automatic gradient calculation and hardware acceleration.

Install PyTorch using the official selector because the correct command depends on your operating system and hardware:

[Official PyTorch installation guide](https://pytorch.org/get-started/locally/)

A small example:

```python
import torch
from torch import nn

# Four examples, each with two numerical input features.
X = torch.tensor([
    [0.0, 0.0],
    [0.0, 1.0],
    [1.0, 0.0],
    [1.0, 1.0]
])

# One target value per example.
y = torch.tensor([[0.0], [1.0], [1.0], [0.0]])

model = nn.Sequential(
    nn.Linear(2, 4),
    nn.ReLU(),
    nn.Linear(4, 1),
    nn.Sigmoid()
)

loss_fn = nn.BCELoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.01)

for epoch in range(1000):
    predictions = model(X)
    loss = loss_fn(predictions, y)

    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

print("Predictions:")
print(model(X).detach())
```

Read the example carefully:
- `nn.Linear(2, 4)` creates a layer that receives two input numbers and produces four outputs.
- `nn.ReLU()` applies the ReLU activation.
- `nn.Linear(4, 1)` maps four values to one output.
- `nn.Sigmoid()` maps that output between 0 and 1.
- `BCELoss` compares predicted probabilities with binary targets.
- `zero_grad()` clears gradients from the previous update.
- `backward()` calculates gradients.
- `step()` updates the parameters.

This tiny dataset is a demonstration, not a useful real-world model. The example also uses a small, fixed dataset repeatedly; later modules will teach proper data splitting and more robust training.

### Checkpoint

1. What does `nn.Linear(2, 4)` mean?
2. What does `loss.backward()` calculate?
3. Why call `optimizer.zero_grad()` before backpropagation?
4. What does `optimizer.step()` do?

---

## Module project — Train and inspect a small network

Choose a small public or synthetic dataset for a simple classification task. Define the inputs and targets. Split the data into training and test sets. Build a network with at least one hidden layer. Train it, record training and validation loss, and evaluate it on held-back data.

Your report must explain:
- The input features and target.
- The network architecture in plain language.
- What its parameters are.
- Which activation and loss functions you chose, and why.
- What one training epoch means in your implementation.
- How you evaluated generalisation.

Do not use a network for high-impact decisions or claim that a small teaching experiment is production-ready.

## Vocabulary

| Term | Meaning |
|---|---|
| Neuron / unit | A calculation that combines inputs with weights and a bias |
| Weight | A learned value controlling an input's influence |
| Bias | A learned value that shifts a calculation |
| Parameter | A numerical value learned or adjusted during training |
| Activation | A function applied to a neuron's output |
| Layer | A stage containing one or more units |
| Architecture | The arrangement of layers and connections |
| Forward pass | Calculating a prediction through the network |
| Loss function | A number measuring prediction error |
| Gradient descent | An optimisation method that updates parameters |
| Backpropagation | Calculating gradients through a network |
| Batch | A group of training examples processed together |
| Epoch | One complete pass through the training set |
| Optimiser | A method that uses gradients to update parameters |
| Tensor | A multi-dimensional numerical array |

## Continue

[Go to 05 — Natural Language Processing](../05-nlp/README.md)
