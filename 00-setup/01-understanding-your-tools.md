# Chapter 1: Understanding Your Tools

## What you are learning

Before building software, understand the tools you will use. A tool is simply a program that helps you perform a particular job. You do not need to know AI or advanced programming to understand this chapter.

## 1. What is programming?

A computer is very good at following precise instructions, but it does not automatically know what you want. Programming is the process of writing instructions that a computer can execute.

A **program** is a set of instructions. A calculator app, a web browser, and a video game are all programs. A program can be tiny:

```python
print("Hello, world!")
```

The instruction asks Python to display the words between the quotation marks. The displayed result is:

```text
Hello, world!
```

A **programming language** is a structured language used to write instructions for a computer. We will use Python because it is readable and has a large ecosystem of AI libraries.

## 2. What is Python?

Python is both the name of the language and commonly the name used for its interpreter. The **Python interpreter** is the program that reads Python instructions and runs them.

Think of a recipe: the recipe is the instructions, and the cook follows them. In this analogy, your Python file contains the recipe and the interpreter follows it.

Python files usually end in `.py`, for example `hello.py`.

## 3. What is a code editor?

A **code editor** is an application for writing and editing source code. Source code is the human-readable text that makes up a program.

A normal text editor can write code, but a code editor often adds helpful features:
- Syntax highlighting colours different parts of the code.
- Indentation guides help you line up code.
- Error hints can point out likely mistakes.
- File navigation helps you move around a project.

These features help you work; they do not replace understanding.

## 4. What is a terminal?

A **terminal** is an application where you type commands instead of choosing every action with a mouse. A command is a text instruction to the operating system.

For example, `pwd` prints the folder you are currently working in on macOS and Linux, and in PowerShell. A folder is also called a **directory**.

The terminal is useful because developers can repeat commands, run programs, install packages, and automate tasks.

## 5. What is Git?

Git is a **version control system**. Version control records changes to files over time. It lets you inspect earlier versions and understand what changed.

A Git repository (often shortened to **repo**) is a project whose history Git tracks. Git is not the same thing as GitHub:
- Git is the version-control tool.
- GitHub is a website and service that hosts Git repositories and supports collaboration.

A **commit** is a saved snapshot in the project's history. A commit message should briefly explain the change.

## 6. Your first tool check

Open your terminal and run:

```bash
python --version
git --version
```

On some Windows computers, use `py --version` if `python --version` is not recognised. These commands ask the tools to print their installed versions. A version number is evidence that the command can find the program; it does not mean you have mastered the tool.

## Check your understanding

1. What is the difference between a program and a programming language?
2. What does the Python interpreter do?
3. Why is a code editor useful?
4. What is a terminal?
5. Explain the difference between Git and GitHub.
6. What is a commit?

## Practice

Create a folder called `ai-learning`. Open it in your code editor. Create a file named `hello.py` containing the example from this chapter. Run it from the terminal.

Write down:
- Which editor you used.
- Which terminal you used.
- The exact command you used to run the file.
- The output you received.

## Chapter summary

You now know the purpose of the main tools used throughout this course: Python runs your programs, an editor helps you write them, the terminal lets you issue commands, and Git records the history of your work.

**Next:** [Chapter 2 — Files, folders, and the terminal](02-files-folders-and-terminal.md)
