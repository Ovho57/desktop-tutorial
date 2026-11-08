# Chapter 2: Embeddings and Sequences

## 1. From token IDs to vectors

Token IDs let a program identify tokens, but their numeric values are arbitrary labels. A model should not assume token 8 is meaningfully larger than token 3.

An **embedding** is a learned vector associated with a token or another item. Instead of representing a token with one integer, the model looks up a list of numbers.

For example, a teaching-only embedding could be:

`embedding("cat") = [0.2, -0.1, 0.7]`

These numbers are not a hand-written definition of “cat”. During training, the model adjusts embedding values so they become useful for its task.

## 2. A sequence of embeddings

A sentence becomes a sequence of token IDs. Each ID is mapped to an embedding vector. The result is a sequence of vectors.

If a sentence has 5 tokens and each embedding has 8 numbers, the embedding sequence can be represented as a matrix with shape `(5, 8)`.

The first dimension represents token positions. The second represents the features in each embedding vector.

## 3. Context windows

A **sequence** is an ordered collection of tokens. A **context window** is the portion of the sequence available to a model when it makes a prediction.

A language model may receive earlier tokens and predict the next token. If the context is too short, important information may be missing. A longer context requires more computation and memory.

## 4. Padding and masks

When sequences in a batch have different lengths, they are sometimes padded to a common length. **Padding** adds special placeholder tokens so examples can fit into a rectangular tensor.

A **mask** identifies positions that should be ignored by a particular operation. For example, an attention mask can prevent a model from treating padding positions as meaningful content.

Padding tokens are a technical convenience; they are not words in the original sentence.

## Check your understanding

1. Why are token IDs not rich representations of meaning?
2. What is an embedding?
3. What does shape `(5, 8)` mean for a sequence of embeddings?
4. What is a context window?
5. Why might a batch need padding?
6. What does a mask identify?

## Practice

Create a tiny vocabulary and map three tokens to IDs. Then create a dictionary that maps those IDs to short vectors. Explain why the vector values should not be interpreted as a human-readable definition.

**Continue:** [Module 06 — Transformers and Attention](../06-transformers/README.md)
