# Strings
## Overview
A String is a sequence of characters.

String literals are surrounded in single quotes:
```python
s = 'This is a String.'
```
Or in double quotes:
```python
s = "This is a string."
```
Or in triple quotes:
```python
s = """This is a single string."""
```
If the literal contains one type of quote, you can use the other type as delimiters:
```python
s = "mom's"
```
Or escape it:
```python
s = 'mom\'s'
```

Strings can be concatenated using the `+` operator, so the expression `'hot' + 'dog'` has the value `'hotdog'`.

You can establish if a string contains a substring with the `in` operator, so the expression `'e' in 'flower'` returns `True`.

Strings in Python are *immutable*: they cannot be changed. If `s` is the string `'hello'`, the expression `s.upper()` doesn't modify `s`, but instead returns a new value, the new string `'HELLO'`. If you wanted to change the value of `s`, you would need to say:
```python
s = s.upper()
```

Strings have many useful methods (things you can ask of them). In almost all cases, they return a new string. Several of the most useful are defined below.

Expression | Value | Notes
---|---|---
`'flower'.find('e')`|4|`'e'` first appears at this index
`'Flower'.lower()`|`'flower'`|Converts to lower case
`'flower'.upper()`|`'FLOWER'`|Converts to upper case
`'flower'.startswith('fl')`|`True`|Return `True` if the string starts with the given pattern
`'flower'.endswith('er')`|`True`|Return 'True' if the string ends with the given pattern

Because, in most cases, string methods return a new string, you can chain calls. For instance, you could write:
```python
'Flower'.lower().startswith('fl')
```
to find out if our string starts with either `'fl'` or `'Fl'`.

You can use slices to extract substrings from a string. For instance:
```python
'flower'[2:5]
```
returns `'owe'``.

## Resources
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.2](https://introcs.cs.princeton.edu/python/12types/)
- Python official documentation, The Python Standard Library, [String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)
- Python official documentation, The Python Standard Library, [slice](https://docs.python.org/3/library/functions.html#slice)

## Questions
1. :star: Can a String be zero characters long?
1. :star: What does `sub in s` do?
1. :star: How would you get the first character of a string `s`?
1. :star: How would you get the first three characters of a string `s`?
1. :star::star: How would you get the last character of a string `s`?
1. :star::star: How would you get the last three characters of a string `s`?
1. :star::star: Can the [for each loop](../control_structures/loops.md#for-each-loops) be used to iterate through the characters of a String `s`?
1. :star::star: Can a string literal include a backslash (`\`)?
1. :star::star::star: What is the value of `'three' + 3`?
1. :star::star::star: How would find out if a String `s` starts with optional spaces followed by either `"0x"` or `"0X"`?

## Answers
1. Yes: commonly `''` or `""`.
1. It returns `True` if `sub` is a substring of `s`.
1. `s[0]`. The arguments to slices are zero-based.
1. `s[0:3]`. The second argument is the index of first character to be omitted.
1. `s[-1]`. Negative arguments are relative to the end of the sequence.
1. `s[-3:]`.
1. Yes:
    ```python
    for c in s:
        ...
1. Yes, but you must escape it: `'this string literal contains a \\ (backslash)'`.
1. This expression does not return a value. Instead it throws a TypeError at run time because the string context established with the initial part of the expression ("`three` +") demands that the second argument be a string, but `3` is an integer.
1. `s.lstrip().replace('X', 'x').startswith('0x')` or `s.lstrip().lower().startswith('0x')`.
