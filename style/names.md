# Names
## Overview
Programmers are constantly called upon to name variables, functions/methods, classes, and other things. Choosing names carefully can vastly improve the legibility (and therefore maintainability) of code.

The guidelines below have exceptions, but any deviations should be made deliberately.

- Choose names so that code using them reads like clear prose.
  
  **Bad:**
  ```python
  if player_turn.check_legality():
    the_array.updating(player_turn)
  ```
  **Good:**
  ```python
  if move.is_legal():
    board.play(move)
  ```
- Use appropriate parts of speech:
  - Variable and class names should be nouns, like `filename` or `Editor`.
  - Function and method names shoud be verbs, like `get_shipping_price` or `is_legal_move`.
- Give something a name if, and only if, it will be referred to more than once.
  - If you need a value more than once, storing it in a variable both removes redundant code and avoids redundant computation.
  - 

## Methods and Instance Variables
Python's programming convention suggests that you name your non-public methods and instance variables with *one* leading underscore.

## Magic Methods
The names of all "magic" methods comprise two leading and two trailing underscores. For instance, an initializer must be named `__init__`.

## Resource
- [Style Guide for Python Code](https://peps.python.org/pep-0008/)

## Questions
1. :star: Must the name of non-public instance variables have a leading underscore?
1. :star: Make the following class definition adhere to the naming convention for non-public instance variables.
    ```python
    class Complex:
        def __init__(self, real, imag):
            self.real = real
            self.imag = imag
    ```
1. :star: Must the initializer be named `__init__`?
1. :star::star: Must the first parameter of methods in a class be named `self`?

## Answers
1. No, it is only a convention. The Python compiler does not enforce this rule.
1.
    ```python
    class Complex:
        def __init__(self, real, imag):
            self._real = real
            self._imag = imag
    ```
1. Yes. Your program may not even compile if you don't name your initializer `__init__`.
1. No, it is merely a widely-adopted convention.
