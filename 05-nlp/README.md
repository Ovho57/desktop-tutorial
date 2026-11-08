# 05 — Natural Language Processing

Natural Language Processing (NLP) is the area of computing concerned with working with human language, such as written text. This module explains how text becomes numerical data that a model can process.

**Prerequisites:** [01 — Python](../01-python/README.md), [03 — Machine Learning](../03-machine-learning/README.md), and [04 — Neural Networks](../04-neural-networks/README.md).

[Back to course home](../README.md)

---

# Lesson 1 — Why text needs preparation

A computer program stores text as data, but most machine-learning models operate on numbers. NLP methods turn text into numerical representations.

Consider:

```text
I like building AI.
```

Before a model can process this sentence, a system needs a consistent way to break it into manageable pieces and map those pieces to numbers.

**Text preprocessing** means preparing text for a task. Possible steps include:
- Standardising certain characters or letter case.
- Removing unwanted markup.
- Handling extra spaces.
- Splitting text into pieces.
- Deciding how to handle punctuation.

Preprocessing choices depend on the task. Lowercasing may be useful for a simple search task, but it can remove information in tasks where capitalisation matters, such as names or abbreviations. Do not remove information automatically without considering its value.

### Checkpoint

1. Why do NLP systems convert text into numerical representations?
2. What is text preprocessing?
3. Why might lowercasing be harmful for some tasks?

**Practice:** Write a sentence and list two preparation steps you might apply before analysing it.

---

# Lesson 2 — Tokens and tokenization

A **token** is a unit of text used by a language-processing system. A token may be a whole word, part of a word, punctuation, or another text unit.

**Tokenization** is the process of splitting text into tokens.

A simple word-based example:

```python
sentence = "I like building AI."
tokens = sentence.split()
print(tokens)
```

Output:

```text
['I', 'like', 'building', 'AI.']
```

This is a basic split on spaces, not a sophisticated language tokenizer. Notice that punctuation remains attached to `AI.`.

Modern language models often use **subword tokenization**. This means common words may be stored as one token, while less common words may be divided into smaller pieces. Subword methods help handle unfamiliar words without requiring a separate token for every possible word.

A **vocabulary** is the set of tokens a tokenizer knows. Each token is assigned an integer ID so a model can work with it.

### Checkpoint

1. What is a token?
2. What is tokenization?
3. Why might a word be split into smaller subword pieces?
4. What is a vocabulary?

**Practice:** Run the simple Python split example. Explain why it is not the same as a modern subword tokenizer.

---

# Lesson 3 — Token IDs and unknown words

A tokenizer maps tokens to integer IDs. For a tiny made-up vocabulary:

| Token | ID |
|---|---:|
| I | 0 |
| like | 1 |
| AI | 2 |

The sentence “I like AI” becomes:

[
[0,1,2]
]

The IDs are labels, not measurements. ID 2 is not “twice as much” as ID 1. The numerical order does not express meaning.

A simple tokenizer:

```python
vocabulary = {"I": 0, "like": 1, "AI": 2}
tokens = ["I", "like", "AI"]
token_ids = [vocabulary[token] for token in tokens]
print(token_ids)
```

What happens when a token is not in the vocabulary? A basic word tokenizer might fail. Many tokenizers use an **unknown token** marker, while subword tokenizers can often represent an unfamiliar word using known pieces.

Real tokenizers also commonly use special tokens to mark boundaries or tasks. Their meaning depends on the model and tokenizer.

### Checkpoint

1. What does a token ID represent?
2. Does a larger token ID mean a word is more important?
3. Why does a tokenizer need a way to handle unfamiliar text?

**Practice:** Extend the tiny vocabulary with two words and encode a new sentence.

---

# Lesson 4 — Embeddings: numbers that represent tokens

Token IDs are arbitrary labels. A model needs a representation that can be used in calculations.

An **embedding** is a learned vector associated with a token or another item. Instead of representing a token with a single integer, an embedding represents it with a list of numbers.

For example, a teaching-only embedding might look like:

[
Embedding("cat") = [0.2, -0.1, 0.7]
]

These numbers are not hand-written definitions of “cat”. During model training, embedding values are adjusted so that the representations are useful for the model's task.

Embeddings allow models to work with numerical representations of tokens. Similarity between vectors can sometimes reflect useful relationships, but embeddings do not contain perfect human-readable definitions.

### Checkpoint

1. Why are token IDs alone not rich representations?
2. What is an embedding?
3. Are embedding values usually manually assigned meanings?

**Practice:** Explain the difference between a token ID and an embedding vector in your own words.

---

# Lesson 5 — Sequences, padding, and context

Text is a sequence: the order of tokens matters. “Dog bites person” and “person bites dog” contain similar words but have different meanings because the order changes.

A **sequence** is an ordered list of tokens or token IDs.

Models often process batches of sequences. A batch is easier to arrange when sequences have the same length. **Padding** adds special filler tokens to shorter sequences so they share a length.

For example:

```text
[12, 8, 4, 9]
[7, 3, PAD, PAD]
```

A **mask** can tell the model which positions are real tokens and which are padding. Without the correct handling, padding could affect calculations in unwanted ways.

**Context** is the surrounding information that helps interpret a token. In “bank of a river” and “bank account”, nearby words help distinguish the meaning of “bank”.

### Checkpoint

1. Why does word order matter?
2. What is padding?
3. What does a padding mask help a model do?
4. What is context?

**Practice:** Give two short sentences where the same word has different meanings depending on its surrounding words.

---

# Lesson 6 — A tiny text classifier

A **text classifier** takes text as input and predicts a category, such as positive or negative sentiment.

A simple traditional approach is a **bag of words**. It counts how often each vocabulary item appears, without preserving the full word order.

Suppose the vocabulary is `["good", "bad", "movie"]`. The sentence “good movie good” becomes the count vector:

[
[2,0,1]
]

The first position counts “good”, the second counts “bad”, and the third counts “movie”.

This representation is simple and useful for learning, but it loses word order and context. “not good” can be difficult to distinguish from “good” using basic word counts alone.

A library such as scikit-learn can build this representation:

```python
from sklearn.feature_extraction.text import CountVectorizer

texts = [
    "good movie",
    "bad movie",
    "good good story"
]

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(texts)

print(vectorizer.get_feature_names_out())
print(X.toarray())
```

`fit_transform` learns the vocabulary from the supplied training text and converts the texts into count vectors. In a real evaluation pipeline, fit the vectorizer on training text only, then use its `transform` method on validation and test text. This prevents test information from leaking into training.

### Checkpoint

1. What does a text classifier predict?
2. What does bag-of-words count?
3. What important information does basic bag-of-words lose?
4. Why should the vectorizer be fitted on training data only?

---

# Lesson 7 — Language models and next-token prediction

A **language model** learns patterns in sequences of tokens. One common objective is to predict the next token based on the tokens that came before it.

For example, after:

```text
The sun rises in the
```

a model might assign probabilities to possible next tokens such as “east”, “morning”, or others, depending on the training data.

The model does not simply store a list of memorised sentence completions. It learns numerical parameters that help it estimate likely continuations.

**Autoregressive generation** means generating one token at a time, then using the generated sequence as context for the next prediction.

The next module explains the transformer architecture, a widely used neural-network design for language models.

### Checkpoint

1. What does a language model learn to estimate?
2. What does next-token prediction mean?
3. What does autoregressive generation do?

**Practice:** Write a short sequence and suggest three possible next tokens. Explain why more than one continuation could make sense.

---

## Module project — Build a tiny text preprocessing tool

Create a Python program that:
1. Accepts a sentence from the user.
2. Converts it to lowercase.
3. Splits it into simple tokens.
4. Builds a vocabulary from the tokens.
5. Assigns an integer ID to each unique token.
6. Prints the tokens and IDs.

Then write down two limitations of your tool. For example, simple splitting does not handle punctuation or subword pieces in the way a production tokenizer does.

## Vocabulary

| Term | Meaning |
|---|---|
| NLP | Computing methods for working with human language |
| Preprocessing | Preparing raw text for a task |
| Token | A unit of text used by a model |
| Tokenization | Splitting text into tokens |
| Vocabulary | The set of tokens a tokenizer knows |
| Token ID | Integer label assigned to a token |
| Subword | A piece smaller than or equal to a word |
| Embedding | A learned numerical vector representation |
| Sequence | An ordered list of tokens |
| Padding | Filler tokens used to align sequence lengths |
| Mask | Information indicating which positions should be used |
| Context | Surrounding information that helps interpret a token |
| Bag of words | A representation based on token counts |
| Language model | A model that learns patterns in token sequences |
| Autoregressive | Generating the next item using previous items as context |

## Continue

[Go to 06 — Transformers & Attention](../06-transformers/README.md)
