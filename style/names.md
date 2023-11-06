# Names
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
