# Chapter 3: Transformer Blocks and Text Generation

## 1. A transformer block

A transformer is built by stacking blocks of operations. A common transformer block contains:
- An attention sublayer.
- A feed-forward network.
- Residual connections.
- Normalisation.

Exact arrangements differ between model designs.

A **feed-forward network** applies learned transformations independently at each sequence position. A **residual connection** adds an earlier representation to a later result, helping information and gradients move through deep networks. **Layer normalisation** helps keep activations in a stable range.

## 2. From tokens to output scores

A decoder-style language model receives token IDs, looks up embeddings, adds positional information, and passes the sequence through transformer blocks.

At the output, a final projection produces **logits**: raw numerical scores for possible next tokens. Softmax can convert logits into probabilities.

The model can then choose a next token according to a decoding strategy.

## 3. Generating text

A basic generation loop works like this:
1. Start with a prompt represented as token IDs.
2. Run the model to obtain next-token scores.
3. Choose a token.
4. Append that token to the sequence.
5. Repeat until a stopping condition is met.

A **greedy decoding** strategy chooses the highest-scoring token each time. Sampling chooses probabilistically and can produce more varied text.

**Temperature** changes how concentrated the probability distribution is before sampling. Lower temperature makes high-scoring choices more dominant; higher temperature makes the distribution flatter. Temperature does not add knowledge or fix a poorly trained model.

## 4. Limits and responsible use

A transformer predicts patterns based on training. Fluent output can still be incorrect. Evaluate outputs against the task, protect private data, and avoid presenting uncertain generated text as verified fact.

## Check your understanding

1. What operations may appear in a transformer block?
2. What is a residual connection?
3. What are logits?
4. Describe the next-token generation loop.
5. How does greedy decoding differ from sampling?
6. What does temperature change?

## Practice

Write pseudocode for a loop that starts with a prompt, chooses one token at a time, and stops after a maximum number of tokens or an end token. Label the point where the model calculates logits and the point where the decoding strategy selects a token.

**Continue:** [Module 07 — Train a Small Model](../07-training-a-model/README.md)
