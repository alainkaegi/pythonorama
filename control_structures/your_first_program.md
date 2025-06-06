# Your First Program
## Overview
Here is a simple Python program:
```python
print('Hello, world!')
```

When run, it prints the text `Hello, world!` to the screen.

In general, a program consists of a series of *statements*. Here is a slightly more complicated program:

```python
a = int(input('Enter a number: '))
b = int(input('Enter another number: '))
if a > b:
    print('The first number is larger')
print('The sum of the two numbers is', a + b)
```

### Expressions and Statements
An *expression* has a value: `2 + 2`. Expressions can be made up of other expressions. For example, the expression `5 + (8 - 4)` is made by using the `+` operator to combine the expressions `5` and `(8 - 4)`. 

A *statement* does something: `print('Hello, world!')`. Statements often contain expressions, such as `"Hello, world!"` within the previous statement. Complex statements, such as [loops](loops.md), can contain other statements.

Some things, such as assignment statements and some [function calls](functional_decomposition.md#calling-functions), are *both* expressions and statements, because they have values *and* do things.

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.1](https://introcs.cs.princeton.edu/python/11hello/)

## Question
1. :star: Is `x > 0` a statement or an expression?

## Answer
1. It is an expression. Its value is either `True` or `False`.
