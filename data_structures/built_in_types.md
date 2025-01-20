# Built-in Types
## Overview
A data type defines a particular set of values and operations allowed on these values.

The table below shows Python's five built-in types. You will most often use those types shown in bold.

Whole numbers | Approximation of real numbers | True-false values | Sequences of characters
-|-|-|-
**int** | **float**, complex | **bool** | **str**

These types are called *built-in* because you do not need to import any libraries to make use of them.

### Literals
A *literal* is a value that is used exactly as it appears in the program.

Type | Examples of Literals
-|-
int | `23` `-100`
float | `3.14159` `1.3e-10`
bool | `True` `False`
str | `'Hello'` `'42.0'`

### Type Conversion
When a certain type is expected, that type must be used. There are two exceptions:
- Implicit conversion. Python will automatically convert an int when used in a context where a float is expected. For instance, if any of the literals or variables in an arithmetic expression are floats, it establishes a "float" context, and then all values in that expression are first converted to floats. Another example is a function expecting a float argument. In `math.sqrt(42)`, the value 42 is first converted to a float.
- Explicit conversion. You can explicitly *convert* one type to another using specific function calls. See the following table for a list of such functions.

Function | Description
-|-
`str(x)` | convert a value to a string
`int(x)` | convert a string to an int
`float(x)` | convert a string to a float
`round(x)` | convert a number to the nearest int

## Resources
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.2](https://introcs.cs.princeton.edu/python/12types/)
- Wired, [No, 'Gangnam Style' Didn't Break YouTube. We Did the Math](https://www.wired.com/2014/12/gangnam-style-youtube-math/)

## Questions
1. :star: What's the difference between a literal and and a constant?
1. :star: How many different boolean values are there?
1. :star: What's the difference between `'x'` and `"x"`?
1. :star: What's `int('-3')`?
1. :star: What's `float('-3')`?
1. :star: What's `round(-3.5)`?
1. :star::star: What's `int(-3.5)`?
1. :star::star: What is the maximum value of an `int`?
1. :star::star: What does the literal `float('nan')` mean?
1. :star::star: What's `int('  +12_345')`?

## Answers
1. Both are fixed values. A literal is a fixed value directly used in the code (e.g., `3.1415`). A constant is a fixed value assigned a name (e.g., `math.pi`).
1. Two: `True` and `False`.
1. There is no difference in this particular example. The use of either type of quotes is appropriate to specify a string literal. The use of one type of quotes is useful to embed the other type in a string without having to escape it. For example, `"mom's"` might be more readable than the equivalent `'mom\'s'`.
1. The int `-3`.
1. The float `-3.0`.
1. The int `-4`.
1. The int `-3`. The function `int` can also take a float, in which case it truncates the input towards zero.
1. An `int` value can be arbitrarily large, only constrained by the amount of available memory in your computer.
1. `float('nan')` is the float value *not a number*. It is the result of calculations such as `Infinity - Infinity`.
1. The int `12345`. The input string can be surrounded by whitespaces and digits interspersed with underscores (but there cannot be whitespaces after the optional sign).
