# 00 — Setup & Your First Steps

This module prepares your computer for the course. It assumes you are new to programming. You do not need to know AI, machine learning, software architecture, or advanced programming words before starting.

**The rule for this course:** we explain a word before asking you to use it. Every exercise in this module uses only ideas introduced earlier in the module.

[Back to the course home](../README.md)

---

## What you will be able to do

By the end of this module, you should be able to:

- Explain what a programming language is.
- Open a terminal and understand what it is for.
- Move between folders using simple commands.
- Check whether Python is installed.
- Create and run a Python file.
- Understand what a code editor does.
- Use Git to save versions of your work.
- Create a separate Python environment for a project.

You do **not** need to understand model architecture, neural-network parameters, APIs, or AI training to finish this module. Those subjects belong later in the course and will be taught before they are used.

## Before you begin

You need:

- A computer running Windows, macOS, or Linux.
- An internet connection for installing tools.
- Permission to install software, if your computer requires it.

The instructions below use Windows examples first. Commands for macOS and Linux are included where they differ.

---

# Lesson 1 — What are we setting up?

### 1.1 What is a computer program?

A computer follows instructions. A **program** is a set of instructions written so that a computer can perform a task.

For example, a program could:
- Display a message.
- Add two numbers.
- Open and read a file.
- Sort a list of names.

A computer does not automatically understand ordinary English instructions. Programmers write instructions in a **programming language**. In this course, our main language will be Python.

### 1.2 What is Python?

Python is a programming language. We write instructions in Python, and the Python program on our computer runs those instructions.

Here is a tiny Python instruction:

```python
print("Hello, world!")
```

The word `print` tells Python to display something. The text inside the quotation marks is what we want displayed.

When this program runs, the output is:

```text
Hello, world!
```

Do not worry about memorising every symbol yet. We will explain Python properly in Module 01.

### Checkpoint 1

Answer using only what you have read:

1. What is a computer program?
2. What is Python?
3. What does `print("Hello, world!")` display?

**Try it:** In your own words, explain the difference between a computer and a program.

---

# Lesson 2 — Files, folders, and paths

Before writing code, understand where your work is stored.

### 2.1 What is a file?

A **file** is a named piece of information stored on your computer. A photo, a song, a document, and a Python program are all files.

A Python file usually ends in `.py`. For example:

```text
hello.py
```

The ending `.py` tells us that the file contains Python code.

### 2.2 What is a folder?

A **folder** is a container used to organise files and other folders. You might create a folder called `my-ai-learning` and keep your course work inside it.

A simple layout could look like this:

```text
my-ai-learning/
    hello.py
    notes.txt
```

Here, `hello.py` and `notes.txt` are files inside the `my-ai-learning` folder.

### 2.3 What is a path?

A **path** tells the computer where a file or folder is located.

For example, on Windows:

```text
C:\Users\Student\my-ai-learning\hello.py
```

On macOS or Linux, a path might look like:

```text
/home/student/my-ai-learning/hello.py
```

The exact path on your computer will be different. The important idea is that a path describes the location of something.

### Checkpoint 2

1. What is a file?
2. What is a folder?
3. What information does a path give us?
4. In the example layout above, which two files are inside `my-ai-learning`?

**Try it:** Create a folder named `my-ai-learning` somewhere easy to find. Inside it, create a text file named `notes.txt`.

---

# Lesson 3 — The terminal

### 3.1 What is a terminal?

The **terminal** is an application where you type text commands to ask your computer to do things.

You can use a mouse to open a folder. You can also use a terminal command to move into that folder. Both methods interact with your computer; the terminal gives you a text-based way to do it.

On Windows, open **Windows Terminal** or **PowerShell**. On macOS, open **Terminal**. On Linux, open your terminal application.

### 3.2 Commands

A **command** is an instruction you type into the terminal.

Try these commands:

Windows PowerShell:

```powershell
pwd
```

macOS or Linux:

```bash
pwd
```

This displays the folder you are currently working in. That folder is called the **current directory**. A directory is simply another name for a folder.

To see the files and folders in the current directory:

Windows PowerShell:

```powershell
dir
```

macOS or Linux:

```bash
ls
```

To move into a folder named `my-ai-learning`:

```bash
cd my-ai-learning
```

The `cd` command means “change directory.” It moves the terminal into the folder you name. The folder must exist in your current location for this example to work.

To move one folder up:

```bash
cd ..
```

### 3.3 Create a folder from the terminal

If you are in the location where you want your project folder, run:

Windows PowerShell, macOS, or Linux:

```bash
mkdir my-ai-learning
```

The `mkdir` command creates a new directory (folder).

If you already created that folder in Lesson 2, do not create it again. Move into it with `cd my-ai-learning`.

### Checkpoint 3

1. What is the terminal?
2. What does `pwd` show?
3. What does `cd` do?
4. What does `mkdir` create?
5. If you are inside a folder, what does `cd ..` do?

**Try it:** Open your terminal. Run `pwd`, then list the items in that location using `dir` on Windows or `ls` on macOS/Linux. Move into your `my-ai-learning` folder.

If a command fails, read the error message. Check the spelling of the folder and make sure you are in the correct location.

---

# Lesson 4 — Install and check Python

### 4.1 Install Python

Download Python from the official website:

[Python downloads](https://www.python.org/downloads/)

On Windows, run the installer. If the installer shows the option **Add Python to PATH**, select it before choosing Install. This helps the terminal find Python when you type its command.

On macOS or Linux, follow the installation instructions for your operating system. Some systems already have a Python version, but this course uses Python 3.

### 4.2 Check that Python works

Close and reopen your terminal after installation. Then run:

Windows:

```powershell
py --version
```

macOS or Linux:

```bash
python3 --version
```

You should see a version number beginning with `3`, for example:

```text
Python 3.x.x
```

The exact number may be different. The important thing is that the command prints a Python 3 version instead of an error.

If `py` does not work on Windows, try:

```powershell
python --version
```

If the command is not recognised, Python may not have been installed correctly or may not be available on your PATH. Reopen the installer and check the installation options.

### Checkpoint 4

1. Where should you download Python?
2. What does checking the version tell you?
3. What should the version begin with for this course?

**Try it:** Run the version command for your operating system. Write down the exact version displayed.

---

# Lesson 5 — Your code editor

### 5.1 What is a code editor?

A **code editor** is an application used to write and edit program files. It makes code easier to read and organise. It is different from the terminal: the editor is where you write the code; Python runs the code.

A popular editor is Visual Studio Code (VS Code).

[Download Visual Studio Code](https://code.visualstudio.com/)

Install it, open it, and choose **File → Open Folder**. Select your `my-ai-learning` folder.

You can use another editor if you already have one. The important thing is that you can create and save a plain-text file.

### 5.2 Create your first Python file

Inside VS Code:

1. Open the `my-ai-learning` folder.
2. Create a new file.
3. Name it `hello.py`.
4. Type this code:

```python
print("I am learning Python.")
print("This is my first program.")
```

5. Save the file.

Make sure the file is named `hello.py`, not `hello.py.txt`.

### 5.3 Run the file

Open a terminal in your project folder. Run:

Windows:

```powershell
py hello.py
```

macOS or Linux:

```bash
python3 hello.py
```

Expected output:

```text
I am learning Python.
This is my first program.
```

You have now written and run a Python program.

### Checkpoint 5

1. What is a code editor used for?
2. Is the editor the same thing as Python?
3. What file extension does our Python file use?
4. What command did you use to run your file?

**Try it:** Change the two messages in `hello.py`, save the file, and run it again. Confirm that the new messages appear.

---

# Lesson 6 — Git: saving the history of your work

### 6.1 Why do we use Git?

When you work on a project, you will change files. Sometimes a change works; sometimes it breaks something. **Git** is a tool that records snapshots of changes to your project so you can review its history and return to an earlier saved version.

A saved snapshot in Git is called a **commit**. Think of a commit as a labelled save point.

Git is not the same as GitHub:
- **Git** is the tool on your computer that tracks changes.
- **GitHub** is a website where you can store and share Git repositories online.

A **repository** (often called a repo) is a project whose files and change history are tracked by Git.

### 6.2 Install Git

Download Git from the official website:

[Git downloads](https://git-scm.com/downloads)

Install it using the recommended options for your operating system.

Check the installation:

```bash
git --version
```

You should see a Git version number.

### 6.3 Start tracking your project

In your terminal, move into your `my-ai-learning` folder. Then run:

```bash
git init
```

This starts a new Git repository in that folder.

Check the status:

```bash
git status
```

Git will show you which files are new or changed.

### 6.4 Save your first commit

Tell Git which file to include in the next save point:

```bash
git add hello.py
```

Then create the save point:

```bash
git commit -m "Create first Python program"
```

If Git asks you to set your name and email, follow Git's instructions to configure them. This name and email label your commits; use the details you want associated with your work.

### Checkpoint 6

1. What problem does Git help solve?
2. What is a commit?
3. What is the difference between Git and GitHub?
4. What does `git status` show?
5. What do `git add` and `git commit` do in the steps above?

**Try it:** Add a third `print()` line to `hello.py`. Run `git status`, then use `git add hello.py` and make a second commit with a message describing your change.

---

# Lesson 7 — Python virtual environments

### 7.1 Why separate environments?

As you build projects, you will install Python libraries. A **library** is reusable code that someone else has written so you do not have to build every common feature yourself.

Different projects may need different library versions. Installing every library into one shared Python location can cause conflicts.

A **virtual environment** is an isolated Python workspace for one project. It keeps that project's installed packages separate from other projects.

You do not need to know how virtual environments work internally yet. For now, learn how to create, activate, and leave one.

### 7.2 Create the environment

Make sure your terminal is inside `my-ai-learning`.

Windows:

```powershell
py -m venv .venv
```

macOS or Linux:

```bash
python3 -m venv .venv
```

This creates a folder named `.venv`. It contains the separate environment for this project.

### 7.3 Activate it

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks the activation script, you can use Command Prompt instead:

```cmd
.venv\Scripts\activate.bat
```

macOS or Linux:

```bash
source .venv/bin/activate
```

When it is active, your terminal prompt usually displays `.venv`.

### 7.4 Leave the environment

When you are finished working, run:

```bash
deactivate
```

This leaves the virtual environment. It does not delete your project or your code.

### Checkpoint 7

1. What is a Python library?
2. Why might two projects need separate environments?
3. What folder is created by the commands in this lesson?
4. What command leaves an active environment?

**Try it:** Create the environment, activate it, confirm that `.venv` appears in your terminal prompt, and then deactivate it.

---

# Lesson 8 — Put the pieces together

You have learned the basic tools. Now use them in one small task.

### Your first setup project

Your goal is to create a project folder, write a Python program, run it, and save its history with Git.

Follow these steps in order:

1. Open your terminal.
2. Move to a location where you keep your projects.
3. Create a folder called `setup-practice`.
4. Move into that folder.
5. Create a file called `about_me.py` in your code editor.
6. Write three `print()` instructions. They should display a project title, what you want to learn, and one question you have about AI.
7. Save the file.
8. Run the file using Python.
9. Start Git tracking with `git init`.
10. Check the files with `git status`.
11. Add the Python file and create a commit.

### Example program

Use your own words in place of the example text:

```python
print("My first AI learning project")
print("I want to understand how computers learn.")
print("My question: How does a computer learn from examples?")
```

### Final checkpoint

Try to answer these without looking back:

1. What is Python?
2. What is the terminal used for?
3. What is the difference between a file and a folder?
4. What is a path?
5. What does `cd` do?
6. What does `mkdir` do?
7. What is a code editor?
8. What is Git?
9. What is a commit?
10. Why do we use a virtual environment?

If you cannot answer one, return to that lesson. That is normal. Learning means understanding the ideas, not rushing through the page.

## Glossary — words introduced in this module

| Word | Meaning |
|---|---|
| Program | Instructions that a computer can run |
| Programming language | A language used to write computer instructions |
| Python | The programming language used in this course |
| File | A named item of stored information |
| Folder / directory | A container for files and other folders |
| Path | The location of a file or folder |
| Terminal | An application for entering text commands |
| Command | An instruction entered into the terminal |
| Current directory | The folder the terminal is currently working in |
| Code editor | An application for writing and editing code |
| Library | Reusable code that provides features |
| Git | A tool for tracking changes to files |
| Repository | A project tracked by Git |
| Commit | A saved point in a repository's history |
| Virtual environment | An isolated Python workspace for a project |

## You are ready for Module 01

You are ready to continue when you can create a Python file, run it from the terminal, and explain what Git and a virtual environment are for.

[Continue to 01 — Python Foundations](../01-python/README.md)

[Back to the course home](../README.md)
