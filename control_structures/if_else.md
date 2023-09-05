# If Statements
## Overview
An `if` statement has one of the following three forms
<pre>
if <em>condition</em>:
    statement
    ...
</pre>
or
<pre>
if <em>condition</em>:
    <em>statement</em>
    ...
else:
    <em>statement</em>
    ...
</pre>
or
<pre>
if <em>condition1</em>:
    <em>statement</em>
    ...
elif <em>condition2</em>:
    <em>statement</em>
    ...
else:
    <em>statement</em>
    ...
</pre>
where *condition*, *condition1*, and *condition2* are a boolean expressions. The first version executes the statements in the body if the value of *condition* is `true`. The second executes the first batch of statements if *condition* is `true` and the second batch if it is `false`. The third executes the first batch of statements if *condition1* is `true`, the second batch if it is false and *condition2* is `true`, and the third batch if both *condition1* and *condition2* are `false`.

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
    elsif condition2:
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
1. :star::star: The first form at the top of this page is called a *one-armed* if statement. The second form is a *two-armed* if statement. How could you use if statements to make a three-way decision? 

## Answers
1. The second version only prints `B` if *both* `condition1` and `condition2` are true.
1. The second version only prints `B` if `condition1` is `false` *and* `condition2` is `true`.
1. `B`. The indentation is significant; only the first `print` statement is part of the `if` statement. Unlike C or Java, Python does not group statements using curly braces. Instead, Python uses indentation to group statements.
1.
    ```python
    if condition:
        print('A')
    else:
        print('B')
    ```
    If `condition` was `false`, then `not condition` *must* be `true`; there's no need to waste code or computation checking `condition` again.
1. The canonical implementation of a three-way decision in Python looks as follows:
    <pre>
    if <em>condition1</em>:
        <em>statement</em>
        ...
    elif <em>condition2</em>:
        <em>statement</em>
        ...
    else:
        <em>statement</em>
        ...</pre>
