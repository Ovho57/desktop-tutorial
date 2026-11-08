# Chapter 3: Python Environments and Git

## What you are learning

As projects grow, they need libraries and a reliable way to track changes. This chapter introduces packages, virtual environments, and the basic Git workflow.

## 1. What is a package?

A **package** is reusable code that someone has made available for other programs to use. Python includes a standard library, which is code that comes with Python. Other packages can be installed separately.

For example, NumPy is a package used for numerical computing. Later, you will use packages for data handling and machine learning.

A package may depend on other packages. A **dependency** is another piece of software a project needs in order to work.

## 2. Why separate environments?

Imagine two projects:
- Project A needs version 1 of a library.
- Project B needs version 2 of the same library.

Installing both versions into one shared Python environment can cause conflicts. A **virtual environment** gives a project its own isolated place for Python packages.

From your project folder, create one:

```bash
python -m venv .venv
```

On Windows PowerShell, activate it with:

```powershell
.venv\Scripts\Activate.ps1
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

When it is active, your terminal prompt often displays `.venv`. Install packages while the correct environment is active:

```bash
python -m pip install numpy
```

Here, `pip` is Python's package installer. Using `python -m pip` helps ensure that pip belongs to the Python interpreter you are using.

To leave the environment, run:

```bash
deactivate
```

## 3. What should Git track?

Git records changes to project files. Start a repository inside your project folder:

```bash
git init
```

Tell Git which files to include in the next snapshot:

```bash
git add hello.py
```

Save a commit:

```bash
git commit -m "Create first Python program"
```

The three actions have different jobs:
1. `git init` starts tracking a project.
2. `git add` stages selected changes.
3. `git commit` saves the staged snapshot in the project's history.

To inspect the current state:

```bash
git status
```

## 4. The .gitignore file

Some files should not be committed. A virtual environment can be recreated, so it usually does not belong in the repository. Secret files such as API keys must not be uploaded.

Create a file named `.gitignore` and add:

```text
.venv/
__pycache__/
.env
```

This tells Git to ignore matching files and folders that are not already tracked. Never put passwords, private keys, or access tokens in source code or public repositories.

## 5. Git and GitHub

Git stores project history locally. GitHub hosts a copy online so you can back up work, share it, and collaborate.

A typical first connection uses a remote repository created on GitHub. Git calls the remote `origin` by convention:

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git branch -M main
git push -u origin main
```

Replace the URL with the one GitHub gives you. Do not copy this example URL literally.

## Check your understanding

1. What is a package?
2. Why might two projects need separate virtual environments?
3. What does `pip` do?
4. Explain the difference between `git add` and `git commit`.
5. Why should `.env` normally be ignored?
6. What does GitHub add to local Git?

## Practice project

Prepare your `ai-learning` folder as a small Git project:
1. Create and activate a virtual environment.
2. Install NumPy.
3. Create a `.gitignore` file.
4. Run `git init`.
5. Add your Python file and commit it.
6. Run `git status` and write down what it reports.

Do not upload secrets. If you connect the repository to GitHub, use your own repository URL and GitHub's authentication flow.

## Chapter summary

Virtual environments keep project dependencies separate. Git records your changes, and GitHub can host the repository online. These habits make later AI projects easier to reproduce and maintain.

**Continue:** [Module 01 — Python Foundations](../01-python/README.md)
