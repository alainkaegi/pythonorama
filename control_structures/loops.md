# Loops
## Overview
Loops tell the computer to execute statements repeatedly, stopping at the appropriate point. This allows you to tell the computer to do a great deal of work with very little code.

The most general loop is the `while` loop -- if you were stranded on a desert island with only one loop, this is the one you would want. For common tasks, though, the `for` loop is often more convenient.

## While Loops
Here is a program using a `while` loop:

```python
i = 1
while i <= 5:
    print(i)
    i = i + 1
```

When run, it prints:

```
1
2
3
4
5
```

The general form of a `while` loop is
<pre>
while <em>condition</em>:
    <em>statement</em>
    ...
</pre>
where *condition* is a boolean expression.

Its flow is:
1. If *condition* is false, stop.
1. Execute the statements in the body of the loop.
1. Go back to step 1.

## `break` and `continue`
A `break` statement (just the word `break`) exits the current loop. If inside multiple nested loops, `break` only exits the innermost loop. This can be interpreted as "exit the loop".

A `continue` statement skips the rest of current loop iteration. This can be interpreted as "go on to the next pass through the loop".

## For Loops
In the common case where you want to iterate through a sequence of values, a `for` loop is more convenient. The example from the previous section could be written as:
```python
for i in [1, 2, 3, 4, 5]:
    print(i)
```

The general form of a `for` loop is
<pre>
for <em>variable</em> in <em>iterable</em>:
    <em>statement</em>
    ...
</pre>
where *`variable`* is a new variable name and *`iterable`* is an expression that evaluates to a sequence of values. Specifically, *`iterable`* might be a list or, as explained below, the result of calling the `range` function.

Its flow is:
1. If there are no values in *`iterable`* that haven't been visited yet, stop.
1. Assign *`variable`* to the next value in *`iterable`*.
3. Execute the statements in the body of the loop.
4. Go back to step 1.

### `range`
The expression `range(n)` returns an iterable of integers from 0 up to (but not inculding) `n`. The `for` loop
```python
for i in range(5):
    print(i)
```
therefore prints:
```
0
1
2
3
4
```

`range(start, stop)` returns an iterable of integers from `start` up to (but not including) `stop`. For example, `range(2, 5)` produces the numbers 2, 3, and 4.

`range(start, stop, step)` returns an iterable of integers from `start` up to (but not including) `stop`, advancing `step` at a time. For example, `range(2, 10, 3)` produces the numbers 2, 5, and 8.

## Other Looping Structures
There are other ways to get the computer to repeat some code, including [recursion](recursion.md) and list comprehensions. The NumPy library provides ways to efficiently do the same thing to every element of an array. These are more convenient than `while` or `for` loops in certain situations.

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.3](https://introcs.cs.princeton.edu/python/13flow/)

## Questions
1. :star: How would you write the `for` loop below as a `while` loop?
    ```python
    for i in range(5):
        print(i)
    ```
1. :star: Explain how an `if` loop works.
1. :star::star: Do `break` and `continue` statements work in `for` loops?
1. :star::star: How would you write the `while` loop below as a `for` loop? Assume `a` is a list of values.
    ```python
    i = 0
    while (i < len(a)):
        print(a[i])
        i += 1
    ```
1. :star::star: What's the best loop to use to iterate through the elements of a list *backward*?
1. :star::star: What's the best loop to use to modify a list of numbers to make each element 10 times as large?
1. :star::star: What does the code below accomplish? Assume `a` is a list of values.
    ```python
    for i in range(len(a) // 2):
        j = len(a) - 1 - i
        t = a[i]
        a[i] = a[j]
        a[j] = t
    ```
1. :star::star::star: Does a Python `while` loop work like a C `while` loop?
1. :star::star::star: Does a Python `for` loop work like a C `for` loop?
1. :star::star::star: Does the `range` function return a list?

## Answers
1.
    ```python
    i = 0
    while (i < 5):
        print(i)
        i = i + 1
    ```
    This isn't *exactly* equivalent, because the local variable `i` holds a different value after the completion of the loop. After the `for` loop, `i` contains `4` (the last element of the range), but after the `while` loop `i` contains 5 (the first value of `i` that causes the condition to fail).
1. There is no such thing as an `if` loop. Loops potentially execute their bodies multiple times, but `if` statements do so at most once.
1. Yes.
1.
    ```python
    for v in a:
        print(v)
    ```
1. Probably a `for` loop, for instance:
    ```python
    for i in range(len(a) - 1, -1, -1):
        print(a[i])
    ```
    This could also be done with a `while` loop, but it would be more code. There are even more compact notations using slices.
1. A `for` loop:
    ```python
    for i in range(len(a)):
        a[i] *= 10
    ```
    This could also be done with a `while` loop, but it would be more code. Note that `for i in a ...` wouldn't work because it would assign `i` to each *element* of `a`, but the last line requires the *indices*.
1. It reverses the order of the elements of `a`.
1. Yes, although C requires some extra punctuation.
1. Not exactly. C's `for` loop, which is essentially identical to the one found in Java or C#, has a more complicated first line. It is more convenient for some situations, but less so for iterating through the elements of an array or list. Python's `for` loop is more similar to the "for each" loop found in Java or C#.
1. Not exactly. It returns a range object, which (for efficiency reasons) only generates each number right when it is needed. A range object can be converted into a list: `list(range(5))` returns the list `[0, 1, 2, 3, 4]`.
