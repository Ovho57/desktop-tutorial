# 01 — Python Foundations

This module teaches the Python language used in the rest of the course. It starts with basic instructions and builds toward small programs that work with data.

**Prerequisite:** Complete [00 — Setup](../00-setup/README.md), or already know how to open a terminal, create a file, and run Python.

**Teaching promise:** every new term is explained before it appears in a question. Work through the lessons in order if you are new.

[Back to course home](../README.md)

## What you will build

A small command-line study tracker that asks for information, stores it, makes decisions, and saves data to a file.

---

# Lesson 1 — Values, variables, and data types

A Python program works with **values**. A value can be text, a number, or another kind of information.

Try this in `first.py`:

```python
print("Ada")
print(17)
print(3.14)
print(True)
```

Text inside quotes is a **string** (`str`). Whole numbers are **integers** (`int`). Numbers with a decimal point are **floating-point numbers** (`float`). `True` and `False` are **Boolean** values (`bool`): they represent yes/no or true/false conditions.

A **variable** is a name that refers to a value. It lets you use information again:

```python
student_name = "Ada"
age = 17
print(student_name)
print(age)
```

The equals sign here is called **assignment**. It stores the value on the right under the name on the left. It does not mean “is equal to” in the mathematical sense.

Python can tell you the type of a value with `type()`:

```python
print(type(student_name))
print(type(age))
```

### Checkpoint

1. What is a variable used for?
2. What is the difference between `17` and `"17"`?
3. Which Boolean values does Python use?

**Practice:** Create variables for your name, favourite subject, and age. Print each one.

---

# Lesson 2 — Calculations and comparisons

Python can calculate with numbers:

```python
a = 10
b = 3

print(a + b)   # addition
print(a - b)   # subtraction
print(a * b)   # multiplication
print(a / b)   # division
print(a // b)  # whole-number division
print(a % b)   # remainder
print(a ** b)  # power
```

The symbols such as `+` and `*` are called **operators**. An operator tells Python what operation to perform.

Python can also compare values:

```python
print(10 > 3)
print(10 == 3)
print(10 != 3)
```

A comparison produces a Boolean result: `True` or `False`.

Important comparison operators:

| Operator | Meaning |
|---|---|
| `==` | equal to |
| `!=` | not equal to |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal to |
| `<=` | less than or equal to |

Notice the difference between `=` (assignment) and `==` (comparison).

### Checkpoint

1. What does `%` return?
2. What is the difference between `=` and `==`?
3. What type of value does `8 > 5` produce?

**Practice:** Store two numbers in variables. Print their sum and whether the first is greater than the second.

---

# Lesson 3 — Getting information from a user

So far, the program's information was written directly into the file. The `input()` function lets a person type a response while the program runs.

```python
name = input("What is your name? ")
print("Hello, " + name)
```

A **function** is a named, reusable action. `input()` asks for text and returns the text that was typed. The returned text is stored in `name`.

Important: `input()` returns a string, even if the person types digits. Convert it when you need a number:

```python
age_text = input("How old are you? ")
age = int(age_text)
print(age + 1)
```

`int()` converts suitable text into an integer. `float()` converts suitable text into a decimal number. Conversion can fail if the text is not a valid number; we will learn how to handle errors later.

### Checkpoint

1. What does `input()` return?
2. Why do we use `int()` in the age example?
3. What could happen if someone types `hello` when the program expects an integer?

**Practice:** Ask the user for two whole numbers, convert them to integers, and print their sum.

---

# Lesson 4 — Decisions with if, elif, and else

Programs often need to choose what to do. An **if statement** runs a block of code only when a condition is true.

```python
score = 72

if score >= 50:
    print("You passed.")
else:
    print("Try again.")
```

The condition `score >= 50` is checked. If it is true, the first indented block runs. Otherwise, the `else` block runs.

Use `elif` (“else if”) when there are several possible cases:

```python
score = 82

if score >= 80:
    print("Excellent")
elif score >= 50:
    print("Passed")
else:
    print("Needs more practice")
```

Python checks conditions from top to bottom and runs the first matching block. **Indentation** means the spaces at the beginning of a line. In Python, indentation marks which instructions belong inside a block. Use four spaces consistently.

You can combine conditions:
- `and`: both conditions must be true.
- `or`: at least one condition must be true.
- `not`: reverses a Boolean value.

```python
age = 20
has_ticket = True

if age >= 18 and has_ticket:
    print("Entry allowed")
```

### Checkpoint

1. When does an `if` block run?
2. What is `else` for?
3. What does `and` require?
4. Why does indentation matter?

**Practice:** Ask for a test score. Print “Excellent” for 80 or above, “Passed” for 50–79, and “Needs practice” below 50.

---

# Lesson 5 — Repeating work with loops

A **loop** repeats instructions. Use a `for` loop when you want to go through a known sequence of items or repeat a known number of times.

```python
for number in range(5):
    print(number)
```

This prints 0, 1, 2, 3, 4. `range(5)` produces five numbers, starting at zero and stopping before five.

A **while loop** repeats as long as its condition remains true:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1
```

The final line changes `count`, so eventually the condition becomes false. If a while-loop condition never becomes false, the loop can run forever. This is called an **infinite loop**.

### Checkpoint

1. What does a loop do?
2. What numbers does `range(4)` produce?
3. Why must the counter change in the while-loop example?

**Practice:** Use a `for` loop to print the numbers 1 through 10. Then use a `while` loop to do the same.

---

# Lesson 6 — Collections: lists and dictionaries

A **list** stores multiple values in order:

```python
subjects = ["Math", "Science", "Computing"]
print(subjects[0])
subjects.append("English")
print(subjects)
```

List positions are called **indexes**. Python starts counting indexes at zero, so `subjects[0]` is the first item. `append()` adds an item to the end.

A **dictionary** stores information as key-value pairs. A key is the label; the value is the information attached to it.

```python
student = {
    "name": "Ada",
    "age": 17,
    "subject": "Computing"
}

print(student["name"])
student["age"] = 18
```

Use a list when you have an ordered collection of items. Use a dictionary when each item has a meaningful label.

You can loop through a collection:

```python
for subject in subjects:
    print(subject)
```

### Checkpoint

1. What is a list?
2. Why is the first list index zero?
3. What is a dictionary key?
4. When might a dictionary be more useful than a list?

**Practice:** Make a list of three favourite books or games. Make a dictionary containing a person's name, age, and city. Print the information.

---

# Lesson 7 — Functions

A **function** is a reusable block of code. You define it once and call it whenever you need it.

```python
def greet(name):
    print("Hello, " + name)

greet("Ada")
greet("Sam")
```

The word `def` starts a function definition. `greet` is its name. The name inside the parentheses, `name`, is a **parameter**: a named input that the function can receive. When we call `greet("Ada")`, the value `"Ada"` is the **argument** supplied to that parameter.

A function can send a result back using `return`:

```python
def add(a, b):
    result = a + b
    return result

total = add(4, 6)
print(total)
```

Here, `a` and `b` are parameters. The values 4 and 6 are arguments. `return` sends the result to the code that called the function.

Why use functions?
- Avoid repeating the same code.
- Give a task a clear name.
- Break a large problem into smaller parts.
- Make code easier to test.

### Checkpoint

1. What is a function?
2. What does `def` do?
3. In `add(4, 6)`, what are the arguments?
4. What does `return` do?
5. Explain the difference between a parameter and an argument.

**Practice:** Write a function called `rectangle_area` that receives a width and height and returns their product.

---

# Lesson 8 — Errors, files, and modules

An **error** is a problem that stops code from doing what you intended. Python displays an error message to help identify what went wrong.

A common error is trying to convert unsuitable text to a number. Use `try` and `except` to handle a problem without immediately crashing:

```python
try:
    age = int(input("Age: "))
    print("Next year you will be", age + 1)
except ValueError:
    print("Please enter a whole number.")
```

`ValueError` is the type of error raised when a value has the right general form for an operation but cannot be used as requested, such as converting `"hello"` to an integer.

Python can read and write files. The `with` statement helps open a file and close it correctly afterward:

```python
with open("notes.txt", "w", encoding="utf-8") as file:
    file.write("I am learning Python.\n")

with open("notes.txt", "r", encoding="utf-8") as file:
    contents = file.read()

print(contents)
```

The mode `"w"` writes and replaces existing file contents. The mode `"r"` reads. Be careful: writing with `"w"` can erase earlier contents.

A **module** is a Python file that can be imported by another Python file. Python also comes with a **standard library**, a collection of modules included with Python.

```python
import random

number = random.randint(1, 10)
print(number)
```

This imports Python's `random` module and uses it to choose an integer from 1 to 10.

### Checkpoint

1. Why do we use `try` and `except`?
2. What is the difference between file modes `"r"` and `"w"`?
3. What does `with open(...)` help manage?
4. What is a module?
5. What does `import random` do?

**Practice:** Ask the user for a short note, save it to `my_note.txt`, then read the file and print its contents.

---

# Lesson 9 — NumPy: working with numerical data

As we move toward AI, we will often work with many numbers at once. Python lists can store numbers, but mathematical operations on large collections can become awkward.

**NumPy** is a Python library designed for efficient numerical computing. A NumPy **array** is a collection of values arranged in one or more dimensions.

Install it while your project virtual environment is active:

```bash
python -m pip install numpy
```

On systems where your Python command is `python3`, use `python3 -m pip install numpy`.

Try:

```python
import numpy as np

values = np.array([2, 4, 6])
print(values)
print(values * 2)
print(values.mean())
```

`import numpy as np` imports NumPy and gives it the short name `np`. Multiplying the array by 2 multiplies each element. `mean()` calculates the average.

A two-dimensional array can represent rows and columns:

```python
grid = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(grid.shape)
```

The `shape` tells you the size along each dimension. This array has two rows and three columns.

### Checkpoint

1. Why might NumPy be useful when working with many numbers?
2. What does `np.array()` create?
3. What does `mean()` calculate?
4. What does the shape `(2, 3)` describe?

**Practice:** Create an array containing five test scores. Print the average and the array multiplied by 2.

---

# Module project — A command-line study tracker

Build a small program that:

1. Asks for a student's name.
2. Repeatedly asks for a subject to study.
3. Stores each subject in a list.
4. Stops when the user types `done`.
5. Prints the full subject list.
6. Saves the name and subjects in a text file.
7. Handles an empty subject list without crashing.

Suggested starting point:

```python
name = input("Your name: ")
subjects = []

while True:
    subject = input("Subject (or done): ")
    if subject.lower() == "done":
        break
    subjects.append(subject)

print("Study plan for", name)
for subject in subjects:
    print("-", subject)
```

This starter demonstrates input, a list, a loop, a decision, and printing. Extend it by saving the information to a file. The `break` statement exits the loop immediately.

## Final review

You should now be able to explain:
- Values, variables, and basic data types.
- Arithmetic and comparison operators.
- User input and type conversion.
- Decisions and loops.
- Lists and dictionaries.
- Functions, parameters, arguments, and return values.
- Errors and exception handling.
- Reading and writing files.
- Modules and NumPy arrays.

If a term is unclear, return to the lesson where it was introduced before continuing.

## Continue

[Go to 02 — Math for AI](../02-mathematics/README.md) or [return to the course home](../README.md)
