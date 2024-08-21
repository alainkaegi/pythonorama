# Jupyter Notebooks / Google Colab

## Overview
A Jupyter notebook combines text, pictures, and runnable code. Such notebooks can be created locally on your own machine or, without installing anything, using Google Colab.

Jupyter notebooks are useful for learning because instructions can be interlaced with code and because nothing needs to be installed. They are also good for presenting results because steps can be explained with text and pictures and because they allow the reader to play with the code and see how it changes the results.

For more complex software development projects, an integrated development environment like [PyCharm](development_tools/pycharm.md) or [Visual Studio Code](development_tools/vs_code.md) is often a better choice.

## Opening a Colab Notebook
To create a blank notebook in Google Drive, click on `New` (at the upper left) > `More` > `Google Colaboratory`.

You may also sometimes receive a link to a notebook that someone else (like an instructor) has created. You can edit such a notebook and run the code.

If you want to keep (or hand in) work that you do in a notebook someone else has created, you probably don't have permission to modify it. You therefore can't simply save, but you can **save a copy** in your own Google Drive. It's wise to do this first. Google Colab then saves automatically every few seconds.

## Cells
A notebook comprises a series of cells, each of which holds text (and possibly pictures) or code.

In a new notebook, there is already one code cell present. You can type a Python expression into it directly, e.g.:
```python
2 + 2
```

### Creating and Editing Cells
To create a new cell under the current one, click on `+ Code` or `+ Text` at the upper left.

In a text cell, you can simply type text. Buttons are provided for bold, italics, bulleted lists, and other fancy text. The raw text (in a language called markdown) is shown on the left side; the formatted text is on the right. If you are not currently editing a text cell, only the formatted text is shown.

In a code cell, you can type all the Python code you want. The notebook provide some support such as color syntax highlighting and automatic indentation.

### Running Cells
To run a code cell, either press `shift-return` or click on the little "play" triangle to the left of the cell. The output will appear under the cell.

The first time you run a cell in a notebook, it will take a moment for Google Colab to set things up. Subsequent runs will be much faster.

If a cell goes into an infinite loop, you can stop it by clicking on the square that has replaced the play button.

If you define something, like a variable or function, in one cell, you can refer to that definition in another cell *provided that the first cell has been run*.

You can run a bunch of cells using the `Runtime` menu.

## Left Sidebar
There are a series of icons on the left side of the notebook.

### Table of Contents
If you have used headers (like `# Title`, `## Section`, etc.) in your text cells, they will show up here. This can be helpful for navigating in a large notebook.

### Search
This lets you find (and optionally replace) some particular text in your notebook.

### Variables
This shows you the names and types of your currently defined variables. By hovering over the name of one, you can see its value.

The `Shape` column gives the size of compound structures like lists, strings, and `numpy` arrays.

### Secrets
This is a place to put things you don't want to share with other users of the same notebook. You probably won't need to use this.

### Files
You can upload files here, then access them from code cells in the notebook.

Beware that if the notebook becomes inactive (which happens when it hasn't been touched for a few minutes), any files here go away. Don't use this as a permanent place to store files!

## Resources
- [Jupyter Notebook documentation](https://jupyter-notebook.readthedocs.io/en/latest/notebook.html)
- [The Ultimate Markdown Guide (for Jupyter Notebook)](https://medium.com/analytics-vidhya/the-ultimate-markdown-guide-for-jupyter-notebook-d5e5abf728fd)

## Questions
1. :star: How do you run a cell?
1. :star::star: In one cell, you have defined `x = 2`. In the cell below, you have `x + 3`. When you run the second cell, Python complains that `'x' is not defined`. What's going on?
1. :star::star::star: Why is Jupyter spelled that way?
1. :star::star::star: Can text cells contain LaTeX math?

## Answers
1. By pressing `shift-return` or clicking on the little "play" triangle to the left of the cell.
1. You have to run the first cell before running the second cell.
1. It combines the names of the three languages the notebooks support: Julia, Python, and R.
1. Yes. Inline LaTeX should be surrounded by dollar signs: `$\int_{a}^{b} x^2 \,dx$`. For a block equation, use double dollar signs: `$$\sum_{n=1}^{\infty} 2^{-n} = 1$$`.
