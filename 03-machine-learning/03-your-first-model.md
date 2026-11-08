# Chapter 3: Build Your First Machine-Learning Model

## 1. Use a small, known dataset

The scikit-learn library provides tools for classical machine learning. It also includes small datasets for practice. We will use the Iris dataset, which contains measurements of flowers and a species label.

Install the package in your active virtual environment:

```bash
python -m pip install scikit-learn
```

## 2. Load data and inspect its shape

```python
from sklearn.datasets import load_iris

iris = load_iris()
X = iris.data
y = iris.target

print(X.shape)
print(y.shape)
print(iris.feature_names)
print(iris.target_names)
```

Here, `X` contains features and `y` contains labels. The shape of `X` tells you the number of examples and the number of features. Never assume the shape; inspect it.

## 3. Split before training

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)
```

The test set is held back for evaluation. `stratify=y` aims to preserve class proportions in both splits. The random state makes this split repeatable.

For a real project, you may also need a validation set and preprocessing fitted only on training data.

## 4. Fit a model

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=500)
model.fit(X_train, y_train)
```

The `fit()` method trains the model using the training features and labels. Logistic regression is a classification algorithm despite its name.

## 5. Predict and evaluate

```python
from sklearn.metrics import accuracy_score, classification_report

predictions = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, predictions))
print(classification_report(y_test, predictions, target_names=iris.target_names))
```

The model predicts labels for test examples. The metrics compare predictions with the known test labels.

Do not treat one accuracy score as the whole story. Inspect per-class precision and recall, and consider whether the test set represents the data you expect in real use.

## 6. What did the computer learn?

The model fitted numerical parameters from the training data. It did not memorise a human-written description of each flower. It found patterns in measurements that help separate the training classes.

This is a small educational example. Real deployments require stronger data checks, monitoring, privacy protections, and testing against distribution changes.

## Check your understanding

1. What information is stored in `X` and `y`?
2. Why split data before fitting the model?
3. What does `fit()` do?
4. What does `predict()` do?
5. Why inspect precision and recall as well as accuracy?

## Practice project

Change the test size and random state, then compare the results. Explain why a different split can produce a different score. Add a short report describing the dataset, model, evaluation metric, and limitations.

**Continue:** [Module 04 — Neural Networks](../04-neural-networks/README.md)
