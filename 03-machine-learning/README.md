# 03 — Machine Learning

Machine learning is a way to build programs that improve at a task by learning patterns from examples. This module explains the workflow before asking you to train models.

**Prerequisites:** [01 — Python](../01-python/README.md) and [02 — Math for AI](../02-mathematics/README.md). You should understand variables, functions, arrays, averages, and the basic idea of a parameter.

[Back to course home](../README.md)

## What you will build

A small program that learns to predict a numerical value from examples, then a classifier that chooses between categories.

---

# Lesson 1 — What does machine learning mean?

In ordinary programming, a developer writes the rules that transform inputs into outputs. In **machine learning**, we provide examples and a learning algorithm adjusts a model so it can make useful predictions on new inputs.

A **model** is the mathematical function or system that makes predictions. A **training example** is one example used to help the model learn. A dataset contains many examples.

Imagine examples of house sizes and sale prices. We want a model that predicts price from size. We give it examples where both size and known price are available. The model makes predictions, compares them with known answers, and adjusts its internal values.

Machine learning does not mean a computer understands the world like a person. It means a method has found patterns in data that may help with a task.

### Three broad learning settings

- **Supervised learning:** examples include the correct answer, called a label or target.
- **Unsupervised learning:** examples do not include a target; the method looks for structure such as groups.
- **Reinforcement learning:** an agent takes actions and receives rewards or penalties from an environment.

This course begins with supervised learning because it is a clear way to understand training.

### Checkpoint

1. What is a model?
2. What is a training example?
3. What makes supervised learning different from unsupervised learning?
4. Does machine learning guarantee that predictions are correct?

**Practice:** Give one example of a task where the training examples could include both an input and a known answer.

---

# Lesson 2 — Features, labels, and datasets

A **feature** is information supplied to a model as input. A **label** (also called a target) is the answer we want the model to predict.

For a house-price task:
- House size could be a feature.
- Sale price could be the label.

A row is one example. A column can represent one feature or the target.

```python
import numpy as np

# One feature: study hours
X = np.array([[1], [2], [3], [4], [5]])

# Target: observed scores
y = np.array([52, 58, 65, 71, 78])
```

Here, `X` contains input features and `y` contains target values. The capital letter X is commonly used for the feature data; y is commonly used for targets.

**Preprocessing** means preparing raw data so it can be used by a model. Examples include fixing missing values, converting text categories into numbers, and scaling numeric features. Do not change data blindly: a preprocessing choice should make sense for the task.

### Checkpoint

1. What is a feature?
2. What is a label?
3. In the example, how many training examples are there?
4. Why might data need preprocessing?

**Practice:** Design a tiny dataset for predicting whether a student passes. Name two possible features and the label.

---

# Lesson 3 — Splitting data fairly

We want to know whether a model works on examples it has not already seen. If we test it on the same examples used for learning, the result can look better than its real-world performance.

So we divide data into parts:

- **Training set:** used to fit the model.
- **Validation set:** used to compare choices and tune settings.
- **Test set:** held back until final evaluation.

A common split might be 70% training, 15% validation, and 15% test, but the best split depends on the dataset size and task.

**Data leakage** happens when information from outside the training process improperly influences model training or evaluation. For example, using test-set answers to make modelling decisions means the test set is no longer a fair final check.

For time-based data, random splitting can be inappropriate. You may need to train on earlier dates and test on later dates.

### Checkpoint

1. What is the training set used for?
2. Why keep a test set separate?
3. What is data leakage?
4. Why might random splitting be wrong for time-based data?

**Practice:** Explain why testing a model on the same 100 examples it learned from does not tell us how well it handles new examples.

---

# Lesson 4 — Regression: predicting numbers

**Regression** is a supervised-learning task where the target is a number, such as a temperature, price, or travel time.

A simple model is a straight line:

[
\hat y = wx + b
]

The symbol `ŷ` means predicted y. The input is x. The model parameters are w (weight) and b (bias). A weight controls how strongly the input affects the prediction; a bias shifts the prediction up or down.

For a model with `w = 3` and `b = 2`, an input `x = 4` gives:

[
\hat y = 3(4) + 2 = 14
]

The model's prediction is 14. It may not match the actual target.

A common regression loss is **mean squared error (MSE)**. For each example, calculate prediction minus actual value, square the difference, and average all squared differences:

[
MSE = \frac{1}{n}\sum_{i=1}^{n}(\hat y_i-y_i)^2
]

Squaring makes negative and positive errors positive and gives larger errors more influence.

### Checkpoint

1. What kind of target does regression predict?
2. What do w and b control in the line model?
3. Why does MSE square the errors?
4. If actual value is 10 and prediction is 13, what is the squared error?

**Practice:** Calculate MSE for actual values `[2, 4]` and predictions `[3, 2]`.

---

# Lesson 5 — Classification: predicting categories

**Classification** is a supervised-learning task where the target is a category. Examples include spam/not spam, cat/dog, or approved/rejected.

A **binary classification** task has two categories. A **multiclass classification** task has more than two.

A classifier may produce a score or probability for each category, then choose a category using a decision rule. A probability of 0.8 for “spam” means the model assigns an 80% estimated probability to that class; it does not guarantee that 80% of all such predictions will be correct unless the model is well calibrated.

A **threshold** is a cutoff used to turn a score into a decision. For a binary classifier with a spam score:
- score at least 0.5: predict spam
- score below 0.5: predict not spam

The threshold can be changed depending on the cost of false alarms and missed detections.

### Checkpoint

1. What kind of target does classification predict?
2. What is binary classification?
3. What is a threshold?
4. Why might a spam filter use a different threshold from a medical screening tool?

**Practice:** Propose two categories for a simple classifier and describe one feature that might help distinguish them.

---

# Lesson 6 — Evaluating predictions

A model should be evaluated using data it did not train on.

For classification, **accuracy** is the fraction of predictions that are correct. It can be misleading when classes are imbalanced. If 99 out of 100 examples are not spam, a model that always predicts “not spam” has 99% accuracy but catches no spam.

A **confusion matrix** counts:
- True positives: positive cases correctly predicted positive.
- True negatives: negative cases correctly predicted negative.
- False positives: negative cases incorrectly predicted positive.
- False negatives: positive cases incorrectly predicted negative.

**Precision** asks: among the examples predicted positive, how many really are positive?

[
Precision = \frac{TP}{TP+FP}
]

**Recall** asks: among all actual positive examples, how many did the model find?

[
Recall = \frac{TP}{TP+FN}
]

For regression, common metrics include MAE (mean absolute error) and MSE (mean squared error). MAE averages absolute differences; MSE averages squared differences.

### Checkpoint

1. What does accuracy measure?
2. What is a false positive?
3. What is the difference between precision and recall?
4. Why can accuracy be misleading with an imbalanced dataset?

**Practice:** A model predicts 10 messages as spam. Of those, 8 are truly spam. It misses 2 other spam messages. Calculate precision and recall.

---

# Lesson 7 — Overfitting and underfitting

**Overfitting** happens when a model learns the training examples too closely, including noise or accidental details. It performs well on training data but poorly on new data.

**Underfitting** happens when a model is too simple or has not learned enough to capture the useful pattern. It performs poorly on both training and new data.

A **generalisation** is the ability to perform well on new examples from the task's intended data distribution.

Ways to reduce overfitting include:
- Use more representative training data.
- Use a simpler model.
- Use regularisation, a method that discourages overly complex parameter values.
- Stop training when validation performance stops improving.
- Use data augmentation when appropriate to create valid variations of training examples.

Always keep the test set separate while making these choices.

### Checkpoint

1. What is overfitting?
2. What is underfitting?
3. What does generalisation mean?
4. Why is validation data useful?

**Practice:** Describe what you would expect to see if training error is very low but test error is high.

---

# Lesson 8 — A first model with scikit-learn

**scikit-learn** is a Python library containing common machine-learning tools. Install it in your active virtual environment:

```bash
python -m pip install scikit-learn
```

Here is a small regression example. The data is invented for learning, not for real decisions.

```python
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error

X = np.array([[1], [2], [3], [4], [5], [6], [7], [8]])
y = np.array([3, 5, 7, 9, 11, 13, 15, 17])

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.25, random_state=42
)

model = LinearRegression()
model.fit(X_train, y_train)

predictions = model.predict(X_test)
print("Predictions:", predictions)
print("Actual:", y_test)
print("MAE:", mean_absolute_error(y_test, predictions))
```

What each important line does:
- `train_test_split` separates training examples from test examples.
- `LinearRegression()` creates a linear regression model.
- `fit` learns model parameters from training data.
- `predict` uses the fitted model to produce predictions.
- `mean_absolute_error` measures average absolute prediction error.

The argument `test_size=0.25` means one quarter of the examples are placed in the test set. `random_state=42` makes the random split repeatable; 42 is simply a chosen seed value.

### Checkpoint

1. What does `fit` do?
2. What does `predict` do?
3. Why split the data?
4. What does MAE measure?

**Practice:** Change the example's values, run it again, and explain how the predictions and error change.

---

## Module project — Build and evaluate a small predictor

Choose a small, clean dataset. Define the feature and target. Split the data into training and test portions. Train a regression or classification model. Evaluate it with a metric that matches the task.

Your project report must include:
1. What are you predicting?
2. What are the features and target?
3. How did you split the data?
4. Which model did you use?
5. Which metric did you calculate?
6. What are one limitation and one possible improvement?

Do not use sensitive personal data. Do not present a classroom model as reliable for medical, financial, legal, or other high-impact decisions.

## Vocabulary

| Term | Meaning |
|---|---|
| Machine learning | Learning patterns from examples |
| Model | A system that makes predictions |
| Feature | Input information used by a model |
| Label / target | The answer the model is trained to predict |
| Supervised learning | Learning from examples with known answers |
| Unsupervised learning | Finding structure without supplied target answers |
| Training set | Data used to fit a model |
| Validation set | Data used to compare choices during development |
| Test set | Held-back data for final evaluation |
| Regression | Predicting a numerical value |
| Classification | Predicting a category |
| Loss / metric | A numerical way to measure model error or performance |
| Overfitting | Learning training details that do not generalise |
| Underfitting | Failing to learn the useful pattern |
| Generalisation | Performance on new examples |
| Data leakage | Improper use of information that makes evaluation unfair |

## Continue

[Go to 04 — Neural Networks](../04-neural-networks/README.md)
