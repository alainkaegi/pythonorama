# PyCharm

## Overview
PyCharm is an Integrated Development Environment (IDE) for programming in Python. It is "integrated" in that it brings together the editor, interpreter, debugger, and other features.

PyCharm is made by [JetBrains](https://www.jetbrains.com/). They also make [IDEs for a number of other languages](https://www.jetbrains.com/ides/), including C, C++, C#, Java, and JavaScript. A popular alternative is [Microsoft Visual Studio Code](development_tools/vs_code.md).

## Setup
### Downloading
PyCharm is already installed on the machine in the CS computer labs, so you won't need to do this if you're working there.

You can download the [PyCharm](https://www.jetbrains.com/pycharm/) Community Edition for free.

You should also make sure you have [Python](https://www.python.org/) installed on your machine.

### Creating a Project
Everything you do in PyCharm takes place within a project. You'll typically have one project for each of your courses.

When you open PyCharm, it will either open your most recent project or (if there is none) take you to the `Welcome to Python` window. If you close any project(s) you have open, it should take you back to `Welcome to Python`.

From there, click on `New Project` to create a project. Choose the name of your project (something like `algo`) and decide in which directory you'd like to store the project (typically `PycharmProjects` within your home directory). Make sure the Python version is set. If you check the `Create a welcome script` box, you'll get a simple program right away.

### Running a Program
You can run the `main.py` program in any of several ways, including:
- Right-clicking on the name of the program in the `Project` pane on the left and choosing `Run 'main'`.
- Right-clicking within the text of the program and choosing `Run 'main'`.
- Pressing `ctrl-r`.
- Pressing the green "play" triangle at the upper right or in the `Run` pane at the lower left.

### Creating a Program
To create a program, right-click on the name of the project and choose `New` > `Python File`. Give the file a name; PyCharm will add the `.py` suffix for you.

Here's a very simple program to type in:

```python
print('Hello, world!')
```

### Importing Packages

To import an additional package like `numpy`:
1. Open `PyCharm` > `Settings`.
2. Click on the `>` next to the name of your project (e.g., `Project: algo`) to expand it.
3. Click on `Project Interpreter`.
4. Click on the `+` at the left side above the list of packages.
5. Type the name of the package you want.
6. Click on `Install Package` at the lower right.

### Using the Interactive Interpreter

If you just want to evaluate some Python expressions, `Tools` > `Python or Debug Console` will give you an interactive read-eval-print loop.

If you want to have access to this after loading all of the definitions in a file:
1. Right-click in the file.
2. Choose `Modify Run Configuration...`.
3. Click `Modify options` at the upper right.
4. Click `Run with Python Console`.
5. Click `OK`.

Now, whenever you run this program, you'll get a console pane where you can evaluate additional expressions.

### Gotchas and Gimmes

Here are some things to be aware of:

PyCharm saves your edits automatically every few seconds.

When creating a file, it should be within your project but *not* within the `.venv` directory.

Using the green "play" triangle or `ctrl-r` to run a program runs the *most recent* program you've run, which might not be the one you're currently looking at.

To stop a running program, click on the red square in the `Run` or `Python Console` pane. If you have many programs running (either because they are in infinite loops or have Python consoles waiting for commands), they can take up memory and slow down your computer until they are close. All running programms are closed automatically when you close the project.

### Documentation
See the `Help` menu or hover with your cursor over some word in your code.

## Resources
- [PyCharm documentation](https://www.jetbrains.com/help/pycharm/)


## Questions
1. :star: In what directory do program files generally live?
1. :star: How do you stop a running program (e.g., one that has gone into an infinite loop)?
1. :star::star: You have a data file that your program is going to read. Where should you put that file?

## Answers
1. Inside the project, which is in a directory you specified when you created the project. You are free to create subdirectories for organization.
1. By clicking on the red square on the left side of the `Run` or `Python Console` pane.
1. In your project alongside your other files.
