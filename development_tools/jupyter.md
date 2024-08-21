# Jupyter Notebooks / Google Colab

## Overview
A Jupyter notebook combines text, pictures, and runnable code. Such notebooks can be created locally on your own machine or, without installing anything, using Google Colab.

Jupyter notebooks are useful for learning because instructions can be interlaced with code and because nothing needs to be installed. They are also good for presentating results because steps can be explained with text and pictures and because they allow the reader to play with the code and see how it changes the results.

For more complex software development projects, an integrated development environment like [PyCharm](development_tools/pycharm.md) or [Visual Studio Code](development_tools/vs_code.md) is often a better choice.

## Opening a Colab Notebook

To create a blank notebook in Google Drive, click on `New` (at the upper left) > `More` > `Google Colaboratory`.

You may also sometimes receive a link to a notebook that someone else (like an instructor) has created. You can edit such a notebook and run the code.

If you want to keep (or hand in) work that you do in a notebook someone else has created, you probably don't have permission to modify it. You therefore can't simply save, but you can **save a copy** in your own Google Drive. It's wise to do this first. Also, **save early and often**; Google Colab doesn't do this automatically.

## Cells

A notebook comprises a series of cells, each of which holds text (and possibly pictures) or code.

In a new notebook, there is already one code cell present. You can type a Python expression into it directly, e.g.:

```python
2 + 2
```

Run this cell by pressing `shift-return`. The first time you run a cell in a notebook, it will take a moment for Google Colab to set things up. Subsequent runs will be much faster.

### Creating Cells

