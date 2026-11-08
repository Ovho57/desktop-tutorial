# Chapter 3: Build a Tiny Neural Network

## 1. Install PyTorch

PyTorch is a machine-learning framework. It provides tensors, automatic differentiation, neural-network layers, and optimisers.

Install the version appropriate for your computer by following the official PyTorch installation selector. A basic CPU installation can be enough for this small lesson.

## 2. Tensors

A **tensor** is a general numerical container. A scalar is a tensor with no dimensions, a vector has one dimension, and a matrix has two dimensions. Higher-dimensional tensors can represent batches, images, and sequences.

```python
import torch

x = torch.tensor([[1.0, 2.0],
                  [3.0, 4.0]])

print(x.shape)
```

The shape is `(2, 2)`: two rows and two columns.

## 3. Define a network

```python
import torch
from torch import nn

model = nn.Sequential(
    nn.Linear(2, 4),
    nn.ReLU(),
    nn.Linear(4, 1)
)

sample = torch.tensor([[0.5, 1.0]])
prediction = model(sample)
print(prediction)
```

The first linear layer accepts two input features and produces four values. ReLU applies a nonlinear activation. The final linear layer produces one output.

The numbers in the linear layers are trainable parameters. PyTorch creates them and tracks operations so gradients can be calculated.

## 4. Inspect parameters

```python
for name, parameter in model.named_parameters():
    print(name, parameter.shape)
```

The shapes show how the parameters connect inputs, hidden units, and outputs. The exact initial values are normally random.

## 5. Training comes next

Defining a network does not train it. To train it, you still need:
- Input examples.
- Target values.
- A loss function.
- An optimiser.
- A loop that calculates predictions, loss, gradients, and updates.

The next module brings these pieces together for a small language-model experiment.

## Check your understanding

1. What is a tensor?
2. What does `nn.Linear(2, 4)` mean?
3. Why is ReLU included between the linear layers?
4. Does defining a model automatically train it?
5. What else is required to train a network?

## Practice

Change the hidden layer size from 4 to 8. Print the parameter shapes again. Explain which dimensions changed and why.

**Continue:** [Module 05 — Natural Language Processing](../05-nlp/README.md)
