# Chapter 1: Values, Variables, and Input

## The central idea

A program becomes useful when it can work with information. Python represents information using values. A value might be a name, a number, or a true/false answer.

## 1. Values and data types

Run:

```python
print("Ada")
print(17)
print(3.14)
print(True)
```

The four values have different **data types**:
- A string (`str`) is text, usually written inside quotes.
- An integer (`int`) is a whole number.
- A float (`float`) is a number that can contain a decimal part.
- A Boolean (`bool`) is either `True` or `False`.

Why do types matter? Python needs to know what operations make sense. Adding two numbers calculates a sum. Joining two strings combines text.

```python
print(4 + 3)          # 7
print("AI" + " lab")  # AI lab
```

But adding a number directly to a string is not normally valid:

```python
# This raises a TypeError:
# print("Age: " + 17)
```

You can convert a number to text with `str(17)`.

## 2. Variables: names for values

A **variable** is a name that refers to a value. It lets you store information and use it later.

```python
student_name = "Ada"
age = 17
print(student_name)
print(age)
```

The equals sign here performs **assignment**: Python evaluates the expression on the right and assigns its result to the name on the left.

Assignment is different from mathematical equality. In Python:
- `=` assigns a value.
- `==` compares two values.

Names should describe their purpose. `student_age` is clearer than `x` when the value represents someone's age.

## 3. Reading user input

The `input()` function pauses the program and waits for a person to type text.

```python
name = input("What is your name? ")
print("Hello, " + name)
```

A **function** is a reusable operation with a name. `input()` returns the text the user entered. The returned value is assigned to `name`.

Important: `input()` returns a string, even if the person types digits.

```python
age_text = input("How old are you? ")
age = int(age_text)
print(age + 1)
```

The `int()` function converts suitable text to an integer. Use `float()` when decimal values are expected. If the user types something that cannot be converted, Python raises an error. You will learn to handle errors in a later chapter.

## 4. Expressions and operators

An **expression** is a piece of code Python can evaluate to produce a value. Operators tell Python how to combine or compare values.

```python
a = 10
b = 3

print(a + b)   # 13
print(a - b)   # 7
print(a * b)   # 30
print(a / b)   # 3.333...
print(a // b)  # 3
print(a % b)   # 1
print(a ** b)  # 1000
```

The percent operator `%` returns the remainder. It is useful for checking whether a number is even: `number % 2 == 0`.

## Worked example: a simple age calculator

```python
name = input("Name: ")
age_text = input("Age: ")

age = int(age_text)
next_year_age = age + 1

print(name, "will be", next_year_age, "next year.")
```

Read the program from top to bottom. It asks for two pieces of text, converts the age text into an integer, adds one, and prints a sentence.

## Check your understanding

1. What is the difference between a string and an integer?
2. What does a variable allow you to do?
3. What is the difference between `=` and `==`?
4. Why does the age example use `int()`?
5. What does `17 % 5` evaluate to?

## Practice

Write a program that asks for a person's name and birth year. Convert the year to an integer and calculate an approximate age using the current year you choose. Print a sentence containing the result. State that it is approximate because you have not checked whether their birthday has happened this year.

## Chapter summary

Python programs store values in variables, use types to distinguish kinds of information, and use input to receive information from people. Expressions and operators let programs calculate with those values.

**Next:** [Chapter 2 — Decisions and repetition](02-decisions-and-repetition.md)
