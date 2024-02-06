# Names
## Overview
Programmers are constantly called upon to name variables, functions/methods, classes, and other things. Choosing names carefully can vastly improve the legibility (and therefore maintainability) of code.

The guidelines below have exceptions, but any deviations should be deliberate.
- Be consistent, both within your own program and with the conventions of your language and team.
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
  - Variable and class names should be nouns, like `maximum_health` or `Garden`.
  - Function and method names shoud be verbs, like `get_shipping_price` or `is_legal_move`.
- A name should specify what something *represents* or *does*, not how it is implemented. `words` is preferable to `word_array`. `find_shortest_path` is preferable to `Dijkstras_algorithm`.
- Give something a name if, and only if, it will be referred to more than once.
  - If you need a value more than once, storing it in a variable both removes redundant code and avoids redundant computation.

    **Bad:**
    ```python
    def hypotenuse(x1, y1, x2, y2):
        return math.sqrt(((x2 - x1) * (x2 - x1)) + ((y2 - y1) * (y2 - y1)))
    ```
    **Good:**
    ```python
    def hypotenuse(x1, y1, x2, y2):
        x = x2 - x1
        y = y2 - y1
        return math.sqrt((x * x) + (y * y))
    ```
  - If you only refer to something once, it may be clearer to not give it a name at all.

    **Bad:**
    ```python
    def mean(numbers):
        n = len(numbers)
        return sum(numbers) / n
    ```
    **Good:**
    ```python
    def mean(numbers):
        return sum(numbers) / len(numbers)
    ```
    If you only refer to something once but naming it would make an expression too complicated, or if the value is set in a separate configuration file, go ahead and give it a name.
  - The larger the scope of a name, the more descriptive its name should be. One-letter names are only appropriate when they have small scope (e.g., the inside of a small function) or are used for very standard purposes (like `i` for a loop index).
  - Avoid abbreviations and clever in-jokes. Something that makes sense to you right now will not make sense to someone (possibly you) who has to read the code a month later.
  - Avoid the variable names `l` (which looks too much like the upper-case letter `I` and the numeral `1`) and `O` (which looks too much like the numeral `0`).

## Python-Specific Rules
Every language has its own rules and conventions for names. Those below are specific to Python.

### Capitalization
- Variable and method names should use `lower_case_with_underscores`, also known as "snake case".
- Class names should use `CapitalizedWords`, also known as "Pascal case".
- Constants should use `UPPER_CASE_WITH_UNDERSCORES`, also known as "screaming snake case".

### Underscores
- A single leading underscore, as in `_width`, indicates that the name is meant to be used only inside the current class. Some other programming languages allow you to declare an instance variable or method *private*, so that it cannot be accessed outside the class.
- A double leading underscore, as in `__hashcode`, is the "I mean it!" version of the above. It's still possible for another class to get at the value, but it requires jumping through some hoops.
- Double leading and trailing underscores, as in `__init__`, are used for various "magic" methods.

## Resources
- [Style Guide for Python Code](https://peps.python.org/pep-0008/)
- [Single and Double Underscores in Python Names](https://realpython.com/python-double-underscore/)
- Benner, *Naming Things: The Hardest Problem in Software Engineering*

## Questions
1. :star: Must the name of a non-public instance variable have a leading underscore?
1. :star: Make the following class definition adhere to the naming convention for non-public instance variables.
    ```python
    class Complex:
        def __init__(self, real, imag):
            self.real = real
            self.imag = imag
    ```
1. :star: Must the initializer be named `__init__`?
1. :star::star: Must the first parameter of methods in a class be named `self`?
1. :star::star: Is Pascal case the same as camel case?

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
1. Not quite. Pascal case capitalizes the *first* word, while camel case does not. Camel case is so called because in a two-word name like `camelCase`, the upper case letter sticks up in the middle, like the hump of a (dromedary) camel.
