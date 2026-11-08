# Chapter 1: Data and Tokenization

## 1. Set a realistic goal

A small language model is a learning experiment, not a competitor to a large commercial assistant. The goal is to understand the training pipeline: prepare text, tokenize it, build sequences, train a predictor, evaluate it, and generate a short continuation.

A **language model** learns patterns in sequences of tokens. A next-token language model estimates which token is likely to come next given the preceding context.

## 2. Choose data responsibly

A **dataset** is the collection of examples used for training and evaluation. Choose text that you have permission to use. Check its licence and usage conditions.

A responsible preparation process:
1. Keep a copy of the original source.
2. Remove corrupted or irrelevant records when justified.
3. Check for duplicates.
4. Avoid private messages, passwords, personal records, and other sensitive information.
5. Split data into training, validation, and test sets.

The training set fits parameters. The validation set helps compare settings during development. The test set is reserved for a final check.

For text, split by document when necessary. Randomly splitting neighbouring chunks can place nearly identical content in both training and test data, making evaluation look better than it should.

## 3. Build a character-level tokenizer

For a first experiment, a character-level tokenizer is easy to understand. Each unique character receives an integer ID.

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

`set(text)` finds unique characters. `sorted()` gives a stable order. `stoi` maps strings to integers; `itos` maps integers back to strings.

Character-level tokenization is simple, but it creates long sequences and treats each character as a separate prediction unit. Modern language models often use subword tokenizers.

## 4. Create input and target sequences

A language model learns to predict the next token. Suppose the text is:

`hello`

With a context length of 3:
- Input: `hel`
- Target: `ell`

Each input position is trained to predict the token immediately after it. The target is therefore shifted one position relative to the input.

A **context length** is the number of earlier tokens available to the model for a prediction.

## Check your understanding

1. What is the goal of this small model project?
2. Why check a dataset's licence?
3. Why keep a test set separate?
4. What do `stoi` and `itos` mean?
5. Why is the target sequence shifted?
6. What does context length measure?

## Practice

Use the character tokenizer above on a short sentence of your own. Encode it, decode it, and confirm that the decoded string matches the original. Then create one input/target example with context length 4.

**Next:** [Chapter 2 — Batches and the training loop](02-batches-and-training.md)
