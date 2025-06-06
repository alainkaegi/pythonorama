# If Statements
## Overview
An `if` statement allows a program to behave differently depending on the value of some expression. For example,

```python
if x > 0:
    print('x is positive')
```
will only print `x is positive` if the variable `x` has a value greater than zero.

In general, an `if` statement has one of the following three forms
<pre>
if <em>condition</em>:
    <em>statement</em>
    ...
</pre>
or
<pre>
if <em>condition</em>:
    <em>statement1</em>
    ...
else:
    <em>statement2</em>
    ...
</pre>
or
<pre>
if <em>condition1</em>:
    <em>statement1</em>
    ...
elif <em>condition2</em>:
    <em>statement2</em>
    ...
else:
    <em>statement3</em>
    ...
</pre>
where *condition*, *condition1*, and *condition2* are a boolean expressions. The first version executes the statements in the body if the value of *condition* is `True`. The second executes the first batch of statements if *condition* is `True` and the second batch if it is `False`. The third executes the first batch of statements if *condition1* is `True`, the second batch if it is false and *condition2* is `True`, and the third batch if both *condition1* and *condition2* are `False`.

Like other control structures, `if` statements can be nested inside each other.

Some sources call an `if` statement a *conditional statement* or *branch*.

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.3](https://introcs.cs.princeton.edu/python/13flow/)

## Questions
1. :star::star: Explain the difference between
    ```python
    if condition1:
        print('A')
    if condition2:
        print('B')
    ```
    and
    ```python
    if condition1:
        print('A')
        if condition2:
            print('B')
    ```
1. :star::star: Explain the difference between
    ```python
    if condition1:
        print('A')
    if condition2:
        print('B')
    ```
    and
    ```python
    if condition1:
        print('A')
    elif condition2:
        print('B')
    ```
1. :star::star: What is printed by the code below?
    ```python
    if False:
        println('A')
    println('B')
    ```
1. :star::star: How can the following statement be shortened?
    ```python
    if condition:
        print('A')
    elif not condition:
        print('B')
    ```
1. :star::star: Could you have an `if` statement with more than three parts?
1. :star::star: How could you have an `if` statement do something only if some condition is *not* true?

## Answers
1. The first version prints `B` if `condition2` is true. The second version only prints `B` only if *both* `condition1` and `condition2` are true.
1. The first version prints `B` if `condition2` is true. The second version only prints `B` only if `condition1` is `False` *and* `condition2` is `True`.
1. `B`. The indentation is significant; only the first `print` statement is part of the `if` statement. Unlike C or Java, Python does not group statements using curly braces. Instead, Python uses indentation to group statements.
1.
    ```python
    if condition:
        print('A')
    else:
        print('B')
    ```
    If `condition` was false, then `not condition` *must* be true; there's no need to waste code or computation checking `condition` again.
1. Sure:
    <pre>
    if <em>condition1</em>:
        <em>statement1</em>
        ...
    elif <em>condition2</em>:
        <em>statement2</em>
        ...
    elif <em>condition3</em>
        <em>statement3</em>
        ...
    else:
        <em>statement4</em>
        ...</pre>
1. There are a couple of ways to do this. One is to use a `pass` statement, which does nothing:
    <pre>
    if <em>condition</em>:
        pass
    else:
        <em>statement</em>
        ...
    </pre>
    A clearer was is to use the `not` operator:
    <pre>
    if not <em>condition</em>:
        <em>statement</em>
        ...
    </pre>
