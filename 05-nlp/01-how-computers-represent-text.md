# Chapter 1: How Computers Represent Text

## 1. Text is information, but models calculate with numbers

A sentence is meaningful to a person, but a neural network performs numerical operations. Natural Language Processing (NLP) is the area of computing concerned with working with human language.

An NLP system must convert text into a form that can be processed mathematically. The exact preparation depends on the task. A search engine, a sentiment classifier, and a language model may prepare text differently.

## 2. Text preprocessing

**Text preprocessing** means preparing text before using it. Possible steps include:
- Standardising certain characters or letter case.
- Removing unwanted markup.
- Handling extra spaces.
- Splitting text into smaller units.
- Filtering irrelevant records.

Do not remove information automatically. Lowercasing may help a simple search task, but capitalisation can matter for names and abbreviations. Removing punctuation can also change meaning.

## 3. Tokens and tokenization

A **token** is a unit of text used by a language-processing system. It may be a whole word, part of a word, punctuation, or another unit.

**Tokenization** is the process of splitting text into tokens.

```python
sentence = "I like building AI."
tokens = sentence.split()
print(tokens)
```

This simple example splits on spaces. It produces `AI.` with the punctuation still attached. It is not a modern language-model tokenizer.

Modern models often use **subword tokenization**. Common words may be one token, while less common words can be split into smaller pieces. This helps a tokenizer represent words it did not see as complete units during its construction.

## 4. Vocabularies and token IDs

A **vocabulary** is the set of tokens known to a tokenizer. Each token is mapped to an integer called a **token ID**.

For a tiny made-up vocabulary:

| Token | ID |
|---|---:|
| I | 0 |
| like | 1 |
| AI | 2 |

The sentence “I like AI” becomes `[0, 1, 2]`.

Token IDs are labels, not measurements. ID 2 does not mean that token is twice as important as token 1.

## Check your understanding

1. Why do NLP systems convert text into numerical representations?
2. What is preprocessing?
3. What is a token?
4. Why use subword tokenization?
5. What is a vocabulary?
6. Do token IDs represent importance?

## Practice

Write a short sentence. Split it with Python's `split()` method. Explain one limitation of that approach and how punctuation might be handled differently.

**Next:** [Chapter 2 — Embeddings and sequences](02-embeddings-and-sequences.md)
