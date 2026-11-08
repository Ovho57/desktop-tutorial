# Chapter 1: Attention and Context

## 1. Why context matters

The meaning of a token often depends on other tokens. Consider:

- “The animal crossed the road because it was hungry.”
- “The animal crossed the road because it was frightened.”

The word “it” refers to something earlier in the sentence. A language model needs a way to use information from other positions in the sequence.

Earlier sequence models often processed tokens one step at a time. Transformers use **attention**, a calculation that lets a token representation gather information from other positions.

## 2. What attention does

Attention assigns numerical weights to information from different positions. A token can give more influence to some positions and less to others.

Imagine looking up a detail in a book. You have a question, you compare it with possible references, and you use the information from the most relevant places. This is only an analogy; attention itself is a mathematical operation.

Attention does not guarantee human-like understanding. It provides a learned mechanism for combining information across a sequence.

## 3. Queries, keys, and values

Attention uses three vectors:
- **Query (Q):** represents what a position is looking for.
- **Key (K):** represents what a position offers for matching.
- **Value (V):** contains the information that can be passed along.

These vectors are calculated from the input representations using learned transformations.

```text
Q = X × Wq
K = X × Wk
V = X × Wv
```

Here, X is the matrix of input token vectors. Wq, Wk, and Wv are learned weight matrices.

## 4. Scores and weighted information

The model compares queries with keys, often using dot products. These comparisons produce attention scores. A softmax operation converts scores into weights that sum to 1 across the positions being considered.

The output is a weighted combination of the value vectors. A position with a larger attention weight contributes more to the result.

## Check your understanding

1. Why does a language model need context?
2. What does attention allow a token representation to do?
3. What is the role of a query?
4. What does a key help determine?
5. What information does a value carry?
6. Why are attention weights useful?

## Practice

Explain attention using your own analogy. Then explain where the analogy stops being accurate. Define query, key, and value without using the word “attention” in each definition.

**Next:** [Chapter 2 — Self-attention and causal masking](02-self-attention-and-masking.md)
