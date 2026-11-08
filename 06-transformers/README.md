# 06 — Transformers & Attention

Transformers are neural-network architectures used in many modern language models. This module introduces the pieces in a careful order. It explains the words query, key, value, attention, and architecture before asking you to work with them.

**Prerequisites:** [04 — Neural Networks](../04-neural-networks/README.md) and [05 — NLP](../05-nlp/README.md). You should understand vectors, matrices, embeddings, layers, and token sequences.

[Back to course home](../README.md)

---

# Lesson 1 — Why sequence models need context

A sentence is a sequence of tokens. The meaning of a token often depends on other tokens around it.

Consider:
- “The animal did not cross the road because it was tired.”
- “The animal did not cross the road because it was busy.”

The word “it” refers to something in the earlier sentence. A language model needs a way to use information from other positions in the sequence.

Earlier sequence models processed tokens step by step. Transformers use **attention**, a method that lets a token representation combine information from other positions.

The key idea: instead of treating each token as isolated, attention lets the model decide which other tokens are useful for representing it.

### Checkpoint

1. Why does context matter in language?
2. What problem does attention help with?
3. Does attention mean every token is equally important to every other token?

---

# Lesson 2 — Embeddings and positional information

A transformer receives token IDs, but it needs vectors to perform its calculations. As you learned in NLP, an **embedding** maps a token ID to a learned vector.

A sequence of tokens becomes a sequence of vectors. But if the model only received token embeddings, it would not automatically know the order in which the tokens appeared.

Transformers therefore add **positional information** to token representations. A positional encoding or positional embedding gives the model information about where a token occurs in the sequence.

For example, the same word appearing at position 2 and position 8 needs to be distinguishable by position as well as token identity.

There are multiple ways to represent positions. Some transformer designs use fixed mathematical positional encodings; others learn positional embeddings or use relative-position methods. The important beginner idea is that token identity and sequence position are different kinds of information.

### Checkpoint

1. What does a token embedding represent?
2. Why is token order important?
3. What does positional information add?
4. Is positional information the same thing as a token embedding?

---

# Lesson 3 — Attention: the main idea

**Attention** is a calculation that lets a token gather information from other token representations. The model calculates scores that determine how much each position should contribute.

Imagine reading the sentence “The dog chased the ball because it was moving.” When processing “it”, information about “ball” may be more useful than information about “the”.

Attention does not use human-written rules for every sentence. It learns numerical transformations and patterns from training.

A useful analogy is looking up information:
- Decide what information you are looking for.
- Compare that request with available information.
- Combine the information that seems relevant.

This analogy leads to the three names used in attention: query, key, and value. These are not mysterious objects; they are vectors calculated from the input representations.

### Checkpoint

1. What does attention allow a token to do?
2. Why might one earlier token be more useful than another?
3. Does the model use fixed hand-written rules to decide every attention score?

---

# Lesson 4 — Queries, keys, and values

Each input token representation is transformed into three vectors:

- **Query (Q):** what this position is looking for.
- **Key (K):** what information this position offers for matching.
- **Value (V):** the information that can be passed along if this position is attended to.

These are learned linear transformations of the token representations. In a simplified form:

[
Q = XW_Q,\
K = XW_K,\
V = XW_V
]

Here, X is the matrix of input token vectors. The matrices (W_Q), (W_K), and (W_V) contain learned weights.

Think of a query as a search request, a key as a label used to compare against that request, and a value as the content to retrieve. This is an analogy to make the roles memorable; the actual computation is numerical.

### Checkpoint

1. What does a query represent in the attention calculation?
2. What does a key help calculate?
3. What does a value carry?
4. Are Q, K, and V usually learned from the input through weight matrices?

---

# Lesson 5 — Attention scores and weighted sums

The model compares queries with keys using dot products. A larger score means the query and key match more strongly according to the learned representation.

The scores are scaled and passed through **softmax**. Softmax converts a list of scores into non-negative values that sum to 1. These values are attention weights.

The output for a position is a weighted sum of the value vectors. A value with a larger attention weight contributes more to the result.

The scaled dot-product attention formula is:

[
Attention(Q,K,V) =
softmax\left(\frac{QK^T}{\sqrt{d_k}}\right)V
]

Read the formula in stages:
1. (QK^T) calculates query-key similarity scores.
2. Dividing by (sqrt{d_k}) scales the scores, where (d_k) is the key-vector dimension.
3. Softmax turns each score row into weights.
4. Multiplying by V combines the value vectors using those weights.

You do not need to derive the formula yet. Understand what each stage contributes.

### Checkpoint

1. What do attention scores compare?
2. What does softmax do to a row of scores?
3. What do attention weights control?
4. Why are value vectors combined?

---

# Lesson 6 — Self-attention and masking

**Self-attention** means queries, keys, and values are all calculated from the same input sequence. Each token can use information from other tokens in that sequence.

For language generation, a model must not look at future tokens when predicting the next token. A **causal mask** blocks attention to later positions. This preserves the left-to-right prediction rule.

A **padding mask** prevents padded positions from being treated as real content. Causal masking and padding masking solve different problems:
- Causal mask: do not look ahead at future tokens.
- Padding mask: ignore filler positions added to make sequences the same length.

### Checkpoint

1. What makes attention “self-attention”?
2. Why does next-token prediction use a causal mask?
3. What problem does a padding mask solve?
4. How are causal and padding masks different?

---

# Lesson 7 — Multi-head attention and transformer blocks

**Multi-head attention** runs several attention calculations in parallel. Each head has its own learned projections and can focus on different relationships. The results are combined and projected to form the layer output.

A transformer block commonly contains:
1. A multi-head attention sublayer.
2. A feed-forward network applied to each position.
3. Residual connections.
4. Layer normalisation.

A **feed-forward network** is a small neural network applied to each token representation. A **residual connection** adds a sublayer's input to its output, helping information and gradients move through deeper networks. **Layer normalisation** rescales and recentres values within a representation to help training.

The exact order and details vary between transformer designs. The arrangement of these parts is part of the model's architecture.

### Checkpoint

1. Why use multiple attention heads?
2. What does a feed-forward sublayer do?
3. What is a residual connection?
4. What does layer normalisation help with?

---

# Lesson 8 — From transformer blocks to text generation

A language model can stack multiple transformer blocks. The final token representations are projected to produce **logits**: raw numerical scores for possible next tokens.

A **softmax** can convert logits into a probability distribution. A decoding method then selects the next token.

Common decoding choices:
- **Greedy decoding:** choose the token with the highest score each time.
- **Sampling:** choose randomly according to the predicted probabilities.
- **Temperature:** adjust how sharp or flat the probability distribution is before sampling. Lower temperature generally makes choices more concentrated; higher temperature generally makes them more varied.

After choosing a token, append it to the sequence and run the model again to predict another token. This repeats until a stopping condition is met, such as an end token or a maximum length.

### Checkpoint

1. What are logits?
2. What does softmax produce from logits?
3. How does greedy decoding choose a token?
4. What effect does temperature have on sampling?
5. What is autoregressive generation?

---

## Module project — Trace a tiny attention calculation

Use a small example with two or three token vectors. You may use NumPy to:
1. Define a small matrix X.
2. Define small weight matrices for Q, K, and V.
3. Calculate Q, K, and V.
4. Calculate the query-key scores.
5. Apply a row-wise softmax.
6. Multiply the weights by V to obtain the attention output.

Use very small numbers so you can inspect every step. Label each matrix and write down its shape. If you implement causal masking, explain which future positions are blocked.

This project is for understanding the calculation, not for training a large language model.

## Vocabulary

| Term | Meaning |
|---|---|
| Transformer | A neural-network architecture built around attention |
| Attention | A method for combining information from sequence positions |
| Embedding | A learned vector representation |
| Positional information | Information describing a token's position in a sequence |
| Query | Vector used to seek relevant information |
| Key | Vector used to calculate how relevant a position is |
| Value | Vector containing information to combine |
| Attention score | Numerical query-key comparison |
| Softmax | Converts scores into values that sum to one |
| Attention weight | The contribution assigned to a value |
| Self-attention | Attention where Q, K, and V come from the same sequence |
| Causal mask | Prevents looking at future tokens |
| Padding mask | Prevents padded positions from being treated as real tokens |
| Multi-head attention | Several attention calculations run in parallel |
| Residual connection | Adds a sublayer input to its output |
| Layer normalisation | Normalises values within a representation |
| Logit | Raw score for a possible output token |
| Temperature | Sampling setting that changes probability sharpness |

## Continue

[Go to 07 — Train Your Own Small Model](../07-training-a-model/README.md)
