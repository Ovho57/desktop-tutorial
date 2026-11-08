# Chapter 3: Functions and Collections

## The central idea

As programs grow, repeating the same code becomes difficult to maintain. Functions let you give a reusable task a name. Collections let you keep multiple related values together.

## 1. Functions

A **function** is a named block of reusable code. Define one with `def`:

```python
def greet():
    print("Welcome to the AI course.")

greet()
greet()
```

The definition describes what the function does. Calling `greet()` runs it. The parentheses are part of the function-call syntax.

## 2. Parameters and arguments

A **parameter** is a name listed in a function definition. An **argument** is the actual value supplied when the function is called.

```python
def greet(name):
    print("Hello,", name)

greet("Ada")
greet("Sam")
```

Here, `name` is the parameter. `"Ada"` and `"Sam"` are arguments.

A function can return a result:

```python
def add(a, b):
    return a + b

total = add(4, 6)
print(total)
```

`return` sends a value back to the code that called the function. This is different from `print()`, which displays a value on the screen.

## 3. Lists

A **list** stores multiple values in a specific order. Lists use square brackets:

```python
scores = [72, 88, 91, 65]
print(scores[0])
```

Python indexing starts at zero, so `scores[0]` is the first item. `scores[1]` is the second.

Add an item with `append()`:

```python
scores.append(95)
```

Loop through a list:

```python
for score in scores:
    print(score)
```

A list can contain different data types, but in data and AI work you will often use collections with a consistent structure.

## 4. Dictionaries

A **dictionary** stores values under keys. It is useful when each value has a descriptive name.

```python
student = {
    "name": "Ada",
    "age": 17,
    "score": 91
}

print(student["name"])
```

The strings `"name"`, `"age"`, and `"score"` are keys. Their associated values can be retrieved using the key.

## 5. Choosing a collection

Use a list when order matters and you want a sequence of items. Use a dictionary when you want to look up information by a meaningful key. These are not the only collection types in Python, but they are two of the most important.

## Worked example: calculate an average

```python
def average(values):
    if len(values) == 0:
        return 0

    return sum(values) / len(values)

scores = [70, 80, 90]
print(average(scores))
```

The built-in `len()` function counts items. `sum()` adds numeric items. The function checks for an empty list so it does not divide by zero.

## Check your understanding

1. What is the difference between defining and calling a function?
2. Explain parameter versus argument.
3. What does `return` do?
4. Why does `scores[0]` refer to the first item?
5. When would a dictionary be more useful than a list?
6. Why does the average function check for an empty list?

## Practice

Build a small study tracker:
- Store three subject names in a list.
- Store a score for each subject in a dictionary.
- Write a function that receives a list of scores and returns the average.
- Print each subject and its score.
- Print the average score.

## Chapter summary

Functions organise reusable behaviour. Lists store ordered collections, and dictionaries store key-value information. These tools will help you prepare and inspect datasets later.

**Next:** [Chapter 4 — Files, errors, and modules](04-files-errors-and-modules.md)
