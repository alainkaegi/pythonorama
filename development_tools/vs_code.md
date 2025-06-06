# Visual Studio Code
## Overview
Visual Studio Code is an Integrated Development Environment (IDE). It is "integrated" in that it brings together the editor, interpreter, debugger, and other features.

Visual Studio Code is made by Microsoft. Visual Studio Code supports other programming languages through extensions. A popular alternative is [PyCharm](pycharm.md).

## Setup
### Downloading
You can download [Visual Studio Code](https://code.visualstudio.com/) for free.

### Enabling Microsoft Python's Extension
1. `View` > `Extensions`. (In other words, select the `View` menu and chose `Extensions` from the dropdown list.)
1. Enter `Python` in the search box.
1. Select the Python extension by Microsoft.
1. Click on `Install`.

### Creating a Program
1. Start Visual Studio Code and click `New File`.
1. Type code like this:
    ```python
    print('hello, world')
    ```
1. Click `Save` to save this file in a directory of your choice. Make sure to include the file extension `.py`, e.g., `hello.py`.

### Running a Program
There are several ways to do this:
- With the program file open, click on the white "play" triangle at the top corner of the window displaying your program. Clicking on that button, causes Visual Studio Code to open a `TERMINAL` window at the bottom in which it will run your program.
- `Run` > `Run Without Debuggging`.
- Hit `ctrl-F5`.
- Open a `TERMINAL` window (`Terminal` > `New Terminal`) and invoke the Python interpreter manually.

## Using Visual Studio Code
The information on this page is enough to let you write and run programs. Everything else is just gravy, but there is a *lot* of delicious gravy to be had:
- Code completion
- Debugging
- Power editing (e.g., multi-cursor editing)
- Refactoring
- Source control

Some of these features must be enabled through extensions.

#### Documentation
Use the `Help` menu.

## Resource
- [Visual Studio Code Docs](https://code.visualstudio.com/docs)

## Questions
1. :star: In what directory do program files generally live?
1. :star::star: How do you stop a running program (e.g., one that has gone into an infinite loop)?
1. :star::star::star: You have a data file that your program is going to read. Where should you put that file?
1. :star::star::star: Is Visual Studio Code the same as Visual Studio or Visual Studio for Mac?

## Answers
1. In the directory of your choice.
1. Hit `ctrl-C` in the `TERMINAL` window.
1. In your project alongside your other files.
1. No, each of these IDEs are distinct and not to be confused with each other. Also Visual Studio for Mac is now discontinued.
