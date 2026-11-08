# Chapter 4: Files, Errors, and Modules

## The central idea

A program often needs to save information after it closes, use code written in another file, and respond sensibly when something goes wrong. This chapter introduces those abilities.

## 1. Reading and writing files

A **file operation** reads information from storage or writes new information to storage.

Use `open()` with a context manager:

```python
with open("notes.txt", "w", encoding="utf-8") as file:
    file.write("I am learning Python.\n")
```

The mode `"w"` means write. It creates the file if it does not exist and replaces its previous contents if it does. Be careful with it.

Read the file:

```python
with open("notes.txt", "r", encoding="utf-8") as file:
    contents = file.read()

print(contents)
```

The mode `"r"` means read. The `with` statement ensures the file is closed properly when the block ends. UTF-8 is a common text encoding that supports many writing systems.

To add to an existing file rather than replace it, use append mode `"a"`.

## 2. Errors and exceptions

An **error** is a problem that prevents code from doing what was intended. Python reports many runtime problems using **exceptions**.

For example:

```python
number = int("hello")
```

This raises a `ValueError` because the text cannot be converted to an integer.

Use `try` and `except` to handle expected problems:

```python
age_text = input("Age: ")

try:
    age = int(age_text)
except ValueError:
    print("Please enter a whole number.")
else:
    print("Next year you will be", age + 1)
```

The `try` block contains code that may fail. The `except` block handles a particular exception. The optional `else` block runs when no exception occurred.

Do not hide every error with a broad empty exception handler. Handle the problems you understand and let unexpected failures remain visible during development.

## 3. Modules and imports

A **module** is a Python file that can be imported by another Python file. Modules help divide a large program into smaller, reusable parts.

Python includes modules such as `math`:

```python
import math

print(math.sqrt(25))
```

The `import` statement makes the module's functionality available. The dot in `math.sqrt` accesses the `sqrt` function inside the `math` module.

You can also import installed packages:

```python
import numpy as np

values = np.array([2, 4, 6])
print(values.mean())
```

The phrase `as np` gives NumPy a short conventional alias.

## 4. A first look at NumPy arrays

NumPy is a package for numerical computing. Its main structure is the **array**, a collection of values designed for efficient numerical operations.

```python
import numpy as np

values = np.array([1, 2, 3])
print(values * 2)
```

The result is `[2 4 6]`. NumPy applies the multiplication to each element. This is called element-wise operation.

Do not worry about advanced mathematics yet. The next module explains vectors and matrices and shows why arrays are useful.

## Check your understanding

1. What is the difference between write mode and append mode?
2. Why is `with open(...)` useful?
3. What is an exception?
4. Which block handles a `ValueError`?
5. What is a Python module?
6. What is a NumPy array useful for?

## Practice project: study tracker saved to disk

Extend the study tracker from Chapter 3:
1. Ask for a subject and a score.
2. Convert the score to a number inside a `try` block.
3. If conversion fails, show a helpful message.
4. If it succeeds, append the subject and score to a text file.
5. Run the program twice and inspect the file to confirm that both entries remain.

## Chapter summary

Files preserve information, exceptions help you handle expected failures, and modules let you reuse code. NumPy introduces efficient numerical arrays, which become essential in AI mathematics.

**Continue:** [Module 02 — Mathematics for AI](../02-mathematics/README.md)
