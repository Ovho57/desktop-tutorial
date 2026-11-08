# Chapter 2: Batches and the Training Loop

## 1. What is a batch?

A **batch** is a group of training examples processed together. Batching makes training more efficient and gives the optimiser several examples from which to calculate a gradient.

For a context length of four, one input might represent the characters `hell` and its target might represent `ello`. A batch contains multiple such input and target sequences.

Inspect a batch before training:
- Do inputs and targets have the expected shapes?
- Does each target really represent the next token?
- Are all token IDs inside the vocabulary range?
- Do examples come from the intended dataset split?

## 2. Logits and loss

The model produces **logits**, which are raw scores for each possible next token. A loss function compares those scores with the correct target token IDs.

For next-token classification, a common choice is cross-entropy loss. Lower cross-entropy means the model assigns higher probability to the correct targets on average.

A loss number is useful, but it is not a complete evaluation. Inspect generated samples and evaluate on data that was not used for parameter updates.

## 3. A training step

A typical PyTorch training step follows this pattern:

```python
optimizer.zero_grad()
logits = model(inputs)
loss = loss_function(logits, targets)
loss.backward()
optimizer.step()
```

Each line has a job:
- `zero_grad()` clears gradients from the previous update.
- The model calculates logits.
- The loss function measures prediction error.
- `backward()` calculates gradients through backpropagation.
- `step()` updates parameters using the optimiser.

The exact tensor shapes and loss-function inputs depend on the model implementation. Make sure the model output and target dimensions match the framework's expected format.

## 4. Epochs and checkpoints

An **epoch** is one pass through the training dataset. Training for more epochs does not guarantee improvement on new data; the model may overfit.

A **checkpoint** is a saved state of the model and often the optimiser and training progress. Checkpoints let you resume training or compare model versions. Store them with clear names and keep track of the data and settings used.

## 5. Monitor training

Record training loss and validation loss. If training loss continues to fall while validation loss rises, the model may be overfitting.

Keep a record of:
- Dataset and licence.
- Tokenizer and vocabulary size.
- Context length.
- Model size.
- Learning rate and optimiser.
- Number of epochs.
- Training and validation results.

## Check your understanding

1. What is a batch?
2. What are logits?
3. What does cross-entropy loss measure?
4. Why clear gradients before a new update?
5. What does `backward()` calculate?
6. What is a checkpoint?
7. What pattern may indicate overfitting?

## Practice

Write pseudocode for one complete training step. For each line, explain what information enters and what changes. Then describe what you would save in a training log so another person could reproduce the experiment.

**Next:** [Chapter 3 — Evaluation and generation](03-evaluation-and-generation.md)
