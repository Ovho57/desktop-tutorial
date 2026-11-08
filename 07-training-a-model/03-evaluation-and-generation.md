# Chapter 3: Evaluation and Generation

## 1. Evaluate on held-back text

Training loss measures how well the model fits training examples. Validation loss measures performance on held-back examples used during development. Test loss is reserved for a final evaluation.

If the model performs much better on training data than validation data, it may be memorising patterns that do not generalise.

Do not repeatedly adjust a model based on the test set. Doing so gradually turns the test set into part of the development process.

## 2. Generate a continuation

Generation repeatedly predicts and appends one token:
1. Encode the prompt.
2. Run the model.
3. Read the logits for the next position.
4. Convert scores to probabilities or choose the highest score.
5. Select a token.
6. Append it and repeat.

Stop when you reach an end token or a chosen maximum length. If you use a character-level model, the generated output may look like plausible character patterns without forming meaningful words. That is still a useful result for learning the mechanics.

## 3. Inspect quality honestly

A generated sample can look fluent and still be wrong. For a tiny model, inspect:
- Whether it produces valid token IDs.
- Whether output length is controlled.
- Whether it repeats the same fragments.
- Whether it resembles the training data too closely.
- Whether it performs differently on unseen prompts.

Do not claim the model understands a topic just because it produces a sentence about it.

## 4. Save the experiment

Save the model state, tokenizer vocabulary, configuration, and notes about the dataset. The tokenizer is part of the model pipeline: without the matching token-to-ID mapping, the saved weights may not process text correctly.

Record limitations and failed experiments as well as successful ones. Reproducibility means another person can understand how the result was produced.

## Check your understanding

1. Why evaluate on held-back text?
2. Why should the test set not guide every development choice?
3. What are the stages of generation?
4. Why can a character-level model produce weak-looking text?
5. Why must the tokenizer mapping be saved with the model?

## Final project

Train a tiny next-character model on a small, permitted text file. Your project report must include:
- Where the text came from and its licence.
- How you cleaned and split the data.
- How token IDs were created.
- Model architecture and context length.
- Training settings and loss curves or logs.
- At least three generated samples.
- A discussion of failures and limitations.

**Continue:** [Module 08 — Engineering and Deployment](../08-engineering-deployment/README.md)
