# Documentation
## Overview
> Documentation is a love letter that you write to your future self.
>
> -Damian Conway, *Perl Best Practices*

Code is not just for the computer. It's also read by other people who need to understand how it works, debug it, or add new features. Unless it is thoroughly documented, even your own code will be completely mysterious to you if you haven't looked at it in a few months.

> Writing is thinking. To write well is to think clearly. That's why it's so hard.
>
> -David McCullough, interview with NEH chairman Bruce Cole, *Humanities* 23:4

A second advantage of commenting is that it forces you to think clearly about the code you are writing. What exactly is this function supposed to accomplish? What exactly does this array represent?

While additional documents and diagrams are in order for larger programs, the primary way to document code is to include *comments*, that is, sections of code what are visible to human readers but ignored by the compiler. Python offers three different comment styles, described below.

### Inline Comments
An inline comment is a comment that appears on the same line as a statement. It should be used sparingly. It starts with the `#` character and extends until the end of the line.
```python
HEIGHT = 175  # In centimeters
```

Avoid inline comments that add little information:
```python
HEIGHT = 175  # Set HEIGHT to 175
```

### Block Comments
A block comment is one or more lines of text that appears before a related block of code and indented at the same level as that code. Each line is preceded by the `#` character followed by a single space.
```python
# If we've sent more than RATE packets in the last second,
# drop the packet
if err_pkts_in_last_sec >= RATE:
    discard(skb)
    return
```

Block comments are also useful for commenting out a section of code, which can be useful while debugging. Most IDEs will provide a hotkey to toggle comments at the beginning of every line in the selected section of code.

### Docstrings
A docstring is a triple-quoted string literal that appears as the first statement in a module, function, class, or method definition.
```python
def max(a, b):
    """Return the larger of a and b."""
    if a > b:
        return a
    return b
```

The docstring becomes attached to its associated entity. Tools can then use this information in useful ways such as generating *application programming interface* (*API*) documents, which is extremely useful for anyone who wants to use the entity you've defined without reading the code.

Another advantage of docstrings is that many IDEs will read them to produce a pop-up tooltip wherever a function is called. This tooltip includes the function signature and the text from any associated docstring.

## Resources
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, Section 1.1 (print only)
- [Style Guide for Python Code](https://peps.python.org/pep-0008/)
- [Docstring Conventions](https://peps.python.org/pep-0257/)

## Questions
1. :star: How can you identify a docstring?
1. :star::star: How many comments do you need in your code?
1. :star::star: Which style is best for commenting out code?
1. :star::star: Why don't you include comments when writing code on the whiteboard?

## Answers
1. It is a triple-quoted string literal that appears as the first statement of the definition of a module, function, class, or method.
1. Include a docstring before each module, function, method, or class. If a function is particularly long or confusing, include block comments within the function (or, better yet, consider breaking the function up into multiple functions). You don't have to provide docstrings for methods that are private, are completely obvious (like standard getters and setters), or override special methods (like `__str__` or `__eq__`).
1. Use docstrings before all your module, function, method, and class definitions. Use blocks comments where necessary. Use inline comments sparingly.
1. The "documentation" for such code comes in the form of spoken words.
