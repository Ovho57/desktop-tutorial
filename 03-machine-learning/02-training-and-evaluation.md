# Chapter 2: Training and Evaluating a Model

## 1. What does training mean?

A model contains parameters that control its predictions. During training, a learning algorithm compares predictions with the desired answers and adjusts parameters to reduce errors.

A **loss function** is a mathematical function that measures how poorly a model's prediction matches the target. Lower loss usually means a better fit for the examples being measured, but it does not guarantee good performance on new data.

## 2. Split the dataset

Do not judge a model only on the examples it learned from. Divide the dataset into separate parts:

- **Training set:** used to fit the model's parameters.
- **Validation set:** used while developing the model and comparing choices.
- **Test set:** held back for a final evaluation.

If the same examples appear in training and testing, the evaluation can be misleading. This is a form of **data leakage**: information from outside the intended training process influences the evaluation.

For time-based data, split chronologically when that better matches the real task. For grouped data, keep related records together where necessary.

## 3. Baselines

A **baseline** is a simple method used as a point of comparison. For a classification task, a baseline might always predict the most common class. A useful model should be compared against a sensible baseline, not just judged by whether it runs.

## 4. Evaluation metrics

For classification:
- **Accuracy** is the fraction of predictions that are correct.
- **Precision** asks: among examples predicted positive, how many were actually positive?
- **Recall** asks: among actual positive examples, how many did the model find?
- **F1 score** combines precision and recall using their harmonic mean.

Accuracy can be misleading when classes are imbalanced. If 99% of messages are not spam, a model that always says “not spam” gets 99% accuracy but finds no spam at all.

For regression:
- **Mean absolute error (MAE)** averages the absolute differences between predictions and targets.
- **Mean squared error (MSE)** averages squared differences, penalising large errors more strongly.

Choose metrics based on the real cost of mistakes.

## 5. Overfitting and underfitting

**Overfitting** happens when a model learns details of its training examples that do not generalise well to new examples. It may have very low training loss but much worse validation loss.

**Underfitting** happens when a model is too limited or insufficiently trained to capture useful patterns. It performs poorly even on training data.

A **generalisation** is the ability to perform well on new examples drawn from the intended task distribution.

## Check your understanding

1. What does a loss function measure?
2. Why keep a test set separate?
3. What is data leakage?
4. Why can accuracy be misleading with imbalanced classes?
5. Explain overfitting versus underfitting.
6. What does generalisation mean?

## Practice

Invent a classification example with 100 records: 90 negative and 10 positive. Calculate the accuracy of a model that always predicts negative. Explain why that score is not enough to claim the model is useful.

**Next:** [Chapter 3 — A first model with scikit-learn](03-your-first-model.md)
