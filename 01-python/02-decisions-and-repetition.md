# Chapter 2: Decisions and Repetition

## The central idea

A useful program does not always do the same thing. It can choose between actions and repeat actions. Python uses conditions for decisions and loops for repetition.

## 1. Conditions are questions with true-or-false answers

A **condition** is an expression that evaluates to `True` or `False`.

```python
score = 72
print(score >= 50)
```

The comparison is true because 72 is greater than or equal to 50.

Common comparison operators:

| Operator | Meaning |
|---|---|
| `==` | equal to |
| `!=` | not equal to |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal to |
| `<=` | less than or equal to |

## 2. The if statement

An `if` statement runs a block of code only when its condition is true.

```python
score = 72

if score >= 50:
    print("You passed.")
else:
    print("Try again.")
```

The colon starts the block. The indented line belongs to the block. Python uses **indentation** (spaces at the beginning of a line) to show which instructions belong together. Use four spaces consistently.

The `else` block runs when the `if` condition is false.

Use `elif` when there are more possibilities:

```python
score = 82

if score >= 80:
    print("Excellent")
elif score >= 50:
    print("Passed")
else:
    print("Needs more practice")
```

Python checks the conditions from top to bottom and runs the first matching branch.

## 3. Combining conditions

Boolean operators combine true-or-false expressions:
- `and` is true only when both sides are true.
- `or` is true when at least one side is true.
- `not` reverses a Boolean value.

```python
age = 20
has_ticket = True

if age >= 18 and has_ticket:
    print("Entry allowed")
```

Both requirements must be satisfied for the message to appear.

## 4. Repeating with a for loop

A **loop** repeats a block of instructions. A `for` loop is useful when you want to process each item in a sequence or repeat a known number of times.

```python
for number in range(5):
    print(number)
```

This prints 0, 1, 2, 3, and 4. The `range(5)` function produces five integer values starting at zero and stopping before five.

You can choose a start and stop:

```python
for number in range(1, 6):
    print(number)
```

This prints 1 through 5.

## 5. Repeating with a while loop

A `while` loop repeats as long as its condition remains true.

```python
count = 1

while count <= 3:
    print("Attempt", count)
    count = count + 1
```

The variable changes on each repetition. When `count` becomes 4, the condition is false and the loop stops.

If the condition never becomes false, the program can get stuck in an **infinite loop**. Always think about what will eventually make a while-loop condition false.

## Worked example: a simple password attempt counter

```python
correct_code = "blue"
attempts = 0

while attempts < 3:
    answer = input("Enter the code: ")
    attempts += 1

    if answer == correct_code:
        print("Correct")
        break
    else:
        print("Not correct")

print("Finished")
```

The loop allows at most three attempts. The `break` statement exits the loop immediately when the answer is correct. This is only a learning example, not secure password storage.

## Check your understanding

1. What kind of value does a comparison produce?
2. When does an `else` block run?
3. What is the difference between `and` and `or`?
4. Why does `range(5)` stop at 4?
5. What causes an infinite while loop?
6. What does `break` do?

## Practice

Create a number guessing game. Store a secret number in a variable. Give the user up to five guesses. After each guess, tell them whether the guess is too high, too low, or correct. Use only concepts explained in this chapter and Chapter 1.

## Chapter summary

Conditions let a program make decisions. For loops repeat over a sequence or range, while loops repeat while a condition is true. These are the building blocks of program logic.

**Next:** [Chapter 3 — Functions and collections](03-functions-and-collections.md)
