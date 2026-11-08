# Chapter 1: What Machine Learning Is

## 1. Programming rules versus learning from examples

In traditional programming, a developer writes rules that transform inputs into outputs. In **machine learning (ML)**, a program uses examples to learn patterns that help it make predictions on new inputs.

For example, instead of writing every rule for identifying spam messages, we can give a learning algorithm examples labelled as spam or not spam. It adjusts a model to recognise patterns associated with those labels.

Machine learning does not mean a computer thinks like a human. It means a mathematical procedure uses data to fit a model.

## 2. The important vocabulary

- **Example:** one item or observation in a dataset.
- **Feature:** an input measurement or property.
- **Label:** the answer we want a model to predict in supervised learning.
- **Dataset:** a collection of examples.
- **Model:** a mathematical system that maps inputs to predictions.
- **Training:** the process of adjusting a model using data.
- **Inference:** using a trained model to make a prediction.

A house-price dataset might contain house size, number of bedrooms, and sale price. Size and bedroom count are features. Sale price is the label.

## 3. Supervised learning

In **supervised learning**, training examples include the correct target or label.

Two common supervised tasks are:

**Regression** predicts a numerical quantity, such as a house price or tomorrow's temperature.

**Classification** predicts a category, such as spam/not spam or one animal class among several.

The type of output determines which task you are solving. Predicting a price is regression; predicting whether a message is spam is classification.

## 4. Unsupervised learning

In **unsupervised learning**, examples do not come with the target labels the model is supposed to predict. The algorithm looks for structure in the data.

For example, clustering can group customers based on similarities in their behaviour. The resulting groups are patterns found by the algorithm; they are not automatically meaningful human categories.

## 5. A simple prediction function

A linear model can make a numerical prediction:

```python
def predict_price(size, weight, bias):
    return weight * size + bias

print(predict_price(100, 2.5, 10000))
```

Here, `size` is the feature, and `weight` and `bias` are parameters. This code uses fixed values; it does not learn them. Training is the process that would adjust parameters based on examples.

## Check your understanding

1. How is machine learning different from writing every rule by hand?
2. What is a feature?
3. What is a label?
4. Give one regression example and one classification example.
5. What is the difference between training and inference?
6. Does unsupervised learning require target labels?

## Practice

Describe a machine-learning problem you could solve. Identify the examples, features, label (if there is one), and whether the task is regression, classification, or unsupervised learning.

**Next:** [Chapter 2 — Training and evaluating a model](02-training-and-evaluation.md)
