# Chapter 2: Files, Folders, and the Terminal

## What you are learning

Software projects are made of files arranged in folders. This chapter teaches you how to understand that arrangement and navigate it using the terminal.

## 1. Files and folders

A **file** is a named piece of information stored on a computer. A text document, image, spreadsheet, and Python program are all files.

A **folder** is a container for files and other folders. Folders help keep related work together.

For example:

```text
ai-learning/
    hello.py
    notes.txt
    experiments/
        first-test.py
```

Here, `ai-learning` is the main folder. It contains two files and another folder called `experiments`. That inner folder contains one Python file.

A folder can contain another folder. This creates a hierarchy, like chapters inside a book.

## 2. File extensions

A file extension is the ending after the final dot in a filename. Examples:
- `.py` usually means Python source code.
- `.txt` means plain text.
- `.md` means Markdown documentation.
- `.json` means data stored in JSON format.

An extension helps software recognise the kind of file, but renaming a file does not automatically convert its contents. Renaming `notes.txt` to `notes.py` does not turn ordinary sentences into valid Python.

## 3. Paths: addresses for files

A **path** tells the computer where a file or folder is located.

A Windows path may look like:

```text
C:\Users\Student\ai-learning\hello.py
```

A macOS or Linux path may look like:

```text
/home/student/ai-learning/hello.py
```

The exact path differs between computers. A path is an address, not the file itself.

A **relative path** describes a location starting from your current folder. An **absolute path** describes the full location from the filesystem's root or drive. Relative paths are useful in projects because they can keep working when the project folder is moved.

## 4. Your current directory

The **current working directory** is the folder the terminal is currently using as its starting point.

Run:

```bash
pwd
```

This prints the current directory in PowerShell, macOS, and Linux.

To list the contents:
- PowerShell: `dir` or `Get-ChildItem`
- macOS/Linux: `ls`

To move into a folder named `ai-learning`:

```bash
cd ai-learning
```

The command `cd` means change directory. To move up one folder:

```bash
cd ..
```

The two dots mean the parent directory.

## 5. Create a practice project

You can create a folder in your file manager, or use the terminal.

PowerShell:

```powershell
mkdir ai-learning
cd ai-learning
New-Item hello.py -ItemType File
```

macOS/Linux:

```bash
mkdir ai-learning
cd ai-learning
touch hello.py
```

If you already created the folder, do not run `mkdir` again in the same location. Move into the existing folder instead.

Open `hello.py` in your editor and add:

```python
print("My project is organised.")
```

## 6. Run the file

Make sure the terminal is inside the folder containing `hello.py`. Then run:

```bash
python hello.py
```

If your Windows installation uses the Python launcher, try:

```powershell
py hello.py
```

If the terminal says the file cannot be found, check your current directory and the spelling of the filename. If it says Python cannot be found, check the installation and PATH configuration.

## Check your understanding

1. What is the difference between a file and a folder?
2. What does a path tell the computer?
3. What is the current working directory?
4. What does `cd ..` do?
5. Why does renaming a text file to `.py` not convert it into Python code?

## Practice

Create this structure:

```text
ai-learning/
    notes.txt
    practice/
        first.py
```

Put a Python print statement in `first.py`. Navigate into the `practice` folder with the terminal and run the file.

## Chapter summary

Files hold information, folders organise files, and paths describe locations. The terminal lets you move through this structure and run programs from the correct folder.

**Next:** [Chapter 3 — Python environments and Git](03-python-environments-and-git.md)
