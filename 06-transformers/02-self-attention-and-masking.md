# Chapter 2: Self-Attention and Causal Masking

## 1. What does “self” mean?

In **self-attention**, queries, keys, and values are all calculated from the same input sequence. Each position can compare its query with keys from other positions in that sequence.

This allows token representations to incorporate context from other tokens.

## 2. The scaled dot-product calculation

A common attention calculation is:

`Attention(Q, K, V) = softmax(QKᵀ / √dₖ)V`

Read it in stages:
1. Multiply queries by the transpose of keys to calculate similarity scores.
2. Divide by the square root of the key dimension to scale the scores.
3. Apply softmax to turn scores into weights.
4. Multiply the weights by the value matrix to combine information.

The symbol `dₖ` is the size of each key vector. Scaling helps keep scores in a useful range as dimensions grow.

## 3. Why causal masking is needed

A model trained to predict the next token should not see future target tokens while making an earlier prediction. If it could see the answer, training would be unfair and would not match generation.

A **causal mask** prevents a position from attending to future positions. In a simple sequence of four positions, position 1 can use position 1; position 2 can use positions 1 and 2; position 3 can use positions 1, 2, and 3; and position 4 can use all four.

Padding masks solve a different problem: they prevent padded positions from being treated as real content. Do not confuse causal masks with padding masks.

## 4. Multi-head attention

**Multi-head attention** runs several attention operations in parallel, using different learned projections. Each head can learn different patterns of relationships. Their results are combined and projected into an output representation.

More heads do not automatically mean better results. The number of heads, dimensions, and total model size are design choices that affect computation and capacity.

## Check your understanding

1. Why is it called self-attention?
2. What are the four stages of scaled dot-product attention?
3. Why divide scores by the square root of the key dimension?
4. What does a causal mask prevent?
5. How is a padding mask different?
6. What is the purpose of multiple attention heads?

## Practice

Draw a four-token sequence. For each token position, list which earlier or current positions it may attend to under a causal mask. Explain why it cannot use a later token during next-token prediction.

**Next:** [Chapter 3 — Transformer blocks and generation](03-transformer-blocks-and-generation.md)
