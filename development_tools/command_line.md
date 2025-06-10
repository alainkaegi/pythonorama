# Command Line
## Overview
While some of us prefer to work with an integrated development environment (IDE) like [Visual Studio Code](vs_code.md) or [PyCharm](pycharm.md), it's certainly possible to develop Python programs from the command line.

You must first have [Python](https://www.python.org/downloads/) installed on your machine. We *highly* recommend that you use a Python 3 programming environment. All courses and tutorials at Lewis & Clark use that version. You can verify that your installation is working by typing `python --version` on your command line.

> [!IMPORTANT]
> Note: Some installations still have Python 2 available. On these systems, you may need to invoke the Python 3 interpreter with the command `python3` instead of `python`.

The simple program below should be saved in a file called `hello.py`. You can use any simple text editor, such as [nano](https://www.nano-editor.org) (which comes pre-installed on most \*nix-based systems, including macOS),
[Vim](https://www.vim.org/) (ditto), [Emacs](https://www.gnu.org/software/emacs/), or [Sublime Text](https://www.sublimetext.com/). Be careful not to use a word processor such as Microsoft Word, Notepad, or TextEdit, which will add extraneous formatting information to the file. Note that Python is case-sensitive.
```python
print('hello, world')
```

To run this program type:
```
python hello.py
```

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section
  1.1](https://introcs.cs.princeton.edu/python/11hello/)

## Questions
1. :star: What command is used to *run* a Python program from the command line?
1. :star: Is it better to use the Python 2 or the Python 3 programming environment?
1. :star::star: What happens if you run Python without specifying a filename on the command line?

## Answers
1. `python` (or `python3` on some machines)
1. Python 3, in almost all circumstances. Support for Python 2 has ceased in 2020.
1. Python runs in interactive mode. You may type individual Python expressions; the interpreter will evaluate each one and print the result. To exit interactive mode, enter `exit()`.
