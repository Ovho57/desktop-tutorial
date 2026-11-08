# 07 — Train Your Own Small Model

This module connects the earlier lessons into a complete small language-model experiment. The goal is learning the training process—not building a system that competes with large commercial models.

**Prerequisites:** [01 — Python](../01-python/README.md), [02 — Math](../02-mathematics/README.md), [04 — Neural Networks](../04-neural-networks/README.md), [05 — NLP](../05-nlp/README.md), and [06 — Transformers](../06-transformers/README.md).

[Back to course home](../README.md)

---

# Lesson 1 — Set a realistic goal

A **language model** learns statistical patterns in sequences of tokens. A small model trained on a small dataset can learn simple patterns and generate short continuations. It will not have the broad knowledge, reliability, or capabilities of a large pretrained model.

For this project, aim to:
- Prepare a small text dataset.
- Train a tokenizer or use a simple existing tokenizer.
- Turn text into token sequences.
- Train a small next-token predictor.
- Measure loss on held-back text.
- Generate a short continuation.
- Record what worked and what failed.

Choose public-domain or appropriately licensed text. Check the licence and usage conditions before using a dataset. Do not place private messages, passwords, personal records, or other sensitive information into a training dataset.

### Checkpoint

1. What is a language model trained to learn?
2. Why should the first model be small?
3. Why must you check the dataset's licence?
4. Why is a small teaching model not equivalent to a large assistant?

---

# Lesson 2 — Prepare the text dataset

A **dataset** is the collection of examples used for training and evaluation. For a language model, the dataset is text that will be converted into token sequences.

A responsible preparation process:
1. Choose a small, permitted text collection.
2. Read the source and licence information.
3. Remove irrelevant markup or corrupted records where appropriate.
4. Remove duplicate documents if they would distort the experiment.
5. Keep a copy of the original data.
6. Split the data into training, validation, and test sets before fitting data-dependent preprocessing.

The training set is used to fit model parameters. The validation set helps compare settings while developing. The test set is reserved for a final check.

For text, it is important to avoid leakage across splits. If multiple passages come from the same document, splitting random chunks may place near-duplicate content in both training and test sets. Splitting by document can be safer.

### Checkpoint

1. What does the training set do?
2. Why keep a test set separate?
3. Why can splitting neighbouring chunks randomly cause leakage?
4. What should you check before using a text dataset?

---

# Lesson 3 — Tokenize text and build sequences

A tokenizer converts text into token IDs. For a first toy experiment, a character-level tokenizer is easy to understand: each unique character receives an integer ID.

```python
text = "hello world"

vocabulary = sorted(set(text))
stoi = {character: index for index, character in enumerate(vocabulary)}
itos = {index: character for character, index in stoi.items()}

encoded = [stoi[character] for character in text]
decoded = "".join(itos[index] for index in encoded)

print(vocabulary)
print(encoded)
print(decoded)
```

`set(text)` finds the unique characters. `sorted` gives them a stable order. `stoi` maps characters to IDs; `itos` maps IDs back to characters.

A **sequence length** is the number of tokens in a training example. A language model can receive a context window of earlier tokens and learn to predict the next token.

For example, with text “hello” and context length 3:
- Input: “hel”
- Target: “ell”

For next-token training, the target sequence is often the input sequence shifted one position to the left. Each input position is trained to predict the next token.

### Checkpoint

1. What does a tokenizer do?
2. What do `stoi` and `itos` represent?
3. Why does a next-token target shift relative to the input?
4. What is a context length?

---

# Lesson 4 — Create batches

A **batch** is a group of training sequences processed together. Batching makes training more efficient and gives the optimiser a group of examples from which to calculate a gradient.

For a character-level example, if the context length is 4, one input might be the IDs for “hell” and its target might be the IDs for “ello”. Each input position has a next-character target.

A batch of inputs can be represented as a matrix:
- Rows: separate examples.
- Columns: token positions within each example.

The target matrix has the same sequence dimensions, but each position contains the next token's ID.

Before training, inspect a batch:
- Are input and target shapes what you expect?
- Does each target really represent the next token?
- Are all IDs within the vocabulary range?
- Are sequences drawn only from the intended split?

### Checkpoint

1. What is a batch?
2. What do rows and columns represent in a batch of token sequences?
3. Why inspect the input and target before training?

---

# Lesson 5 — Define the model

A first language model can be much simpler than a transformer. A basic baseline might use an embedding table and a linear output layer. It learns token representations and predicts the next token from the current token, but it has little or no context.

A more useful small model can use a context window and a neural network, or a small transformer from Module 06.

Important design choices include:
- Vocabulary size: number of distinct token IDs.
- Context length: how many previous tokens the model can use.
- Embedding dimension: number of values in each token vector.
- Number of layers: how many processing blocks are stacked.
- Number of attention heads: how many attention calculations run in parallel in each attention layer.
- Hidden dimension: size of the internal feed-forward representation.

These choices are part of the model's **architecture**. The numerical weights and biases inside the model are its **parameters**. Architecture describes the design; parameters are the values the training process adjusts.

Start small. A larger model needs more memory and data and may be harder to train.

### Checkpoint

1. What is vocabulary size?
2. What does context length control?
3. What is the difference between architecture and parameters?
4. Why should the first model be small?

---

# Lesson 6 — Train the model

Training is the repeated process of making predictions, measuring errors, calculating gradients, and updating parameters.

A typical training iteration:
1. Fetch a batch.
2. Run the model to produce logits.
3. Calculate the loss against target token IDs.
4. Clear old gradients.
5. Calculate new gradients with backpropagation.
6. Update parameters with the optimiser.

For next-token prediction with multiple possible tokens, **cross-entropy loss** is commonly used. It measures how well the predicted probability distribution assigns probability to the correct next token.

A PyTorch training-step pattern looks like this:

```python
logits = model(inputs)
loss = loss_fn(logits.view(-1, vocab_size), targets.view(-1))

optimizer.zero_grad()
loss.backward()
optimizer.step()
```

This snippet assumes that:
- `model(inputs)` returns logits for each position.
- `targets` contains the correct next-token IDs.
- `loss_fn` is configured for integer class targets, such as `torch.nn.CrossEntropyLoss()`.
- The shapes are arranged so each prediction corresponds to one target.

Do not paste this snippet into a program without defining the model, inputs, targets, vocabulary size, loss function, and optimiser. Those pieces must fit together.

### Checkpoint

1. What does the model produce before softmax in this training setup?
2. What does cross-entropy compare?
3. Why clear gradients before calculating a new batch's gradients?
4. What does the optimiser update?

---

# Lesson 7 — Monitor training and evaluate

A model can memorise training examples without learning patterns that transfer to new text. Record both training and validation loss.

- Training loss measures error on training examples.
- Validation loss measures error on held-back examples used during development.

If training loss decreases but validation loss rises, overfitting may be occurring. If both remain high, the model may be too small, the data may be unsuitable, or the training process may need adjustment.

After development is complete, evaluate on the test set once for a final estimate. Avoid repeatedly tuning against the test set; doing so turns it into another validation set.

For a language model, lower cross-entropy generally means the model assigns more probability to the correct next tokens. It does not guarantee that generated text is factual, safe, or useful.

### Checkpoint

1. Why track validation loss?
2. What pattern might indicate overfitting?
3. Why should the test set not be used repeatedly for tuning?
4. Does low test loss guarantee factually correct generated text?

---

# Lesson 8 — Save checkpoints and generate text

A **checkpoint** is a saved copy of model state, usually including parameters and sometimes optimiser state. It lets you resume training or use the trained model later.

In PyTorch, a simple parameter save looks like:

```python
import torch

torch.save(model.state_dict(), "model_weights.pth")
```

To load those weights into the same model architecture:

```python
model.load_state_dict(torch.load("model_weights.pth", map_location="cpu"))
model.eval()
```

The architecture must be created with the same compatible structure before loading the weights. Saving only a state dictionary does not save the Python code that defines the model.

For generation:
1. Start with a prompt encoded as token IDs.
2. Ask the model for next-token logits.
3. Select a next token.
4. Append that token to the context.
5. Repeat until you reach a stopping condition.

A generated continuation is a model output, not a verified fact. Small models may repeat themselves, produce broken text, or imitate patterns from their training data.

### Checkpoint

1. What is a checkpoint?
2. What does `state_dict()` save?
3. Why must the model architecture match when loading weights?
4. Why should generated text not automatically be treated as factual?

---

## Module project — Train a tiny next-character model

Complete an end-to-end experiment using a small permitted text dataset.

Deliver:
- A note describing the source and licence.
- A tokenizer and vocabulary.
- A documented train/validation/test split.
- A batch-generation function.
- A small model.
- A training loop that reports loss.
- A saved checkpoint.
- A short generated sample.
- A short evaluation report with limitations.

Start with a simple baseline before attempting a transformer. If the baseline does not work, debug the data and training loop before making the architecture larger.

## Vocabulary

| Term | Meaning |
|---|---|
| Dataset | Collection of training and evaluation examples |
| Tokenizer | Converts text into token IDs |
| Vocabulary | Set of tokens understood by the tokenizer |
| Context window | Previous tokens available to the model |
| Batch | Group of examples processed together |
| Logits | Raw scores for possible next tokens |
| Cross-entropy | Common loss for predicting a correct token class |
| Training iteration | One batch's forward, loss, backward, and update cycle |
| Checkpoint | Saved model state |
| Validation loss | Error on held-back development data |
| Test set | Data reserved for final evaluation |
| Generation | Producing new tokens from a prompt |
| Architecture | The design and arrangement of model components |
| Parameters | Numerical weights and biases adjusted during training |

## Continue

[Go to 08 — Engineering & Deployment](../08-engineering-deployment/README.md)
