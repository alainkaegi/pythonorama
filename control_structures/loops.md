# Loops
## Overview
Loops tell the computer to execute statements repeatedly, stopping at the appropriate point.

### While and Loops
A `while` loop has the form
<pre>
while <em>condition</em>:
    <em>statement</em>
    ...
</pre>
where *condition* is a boolean expression.

Its flow is:
1. If *condition* is `false`, stop.
1. Execute the statements in the body of the loop.
1. Go back to step 1.

Strictly speaking, this is the only loop you need, but the other variation can make your code clearer, more concise, and more idiomatic.

### Break and Continue
A `break` statement (just the word `break`) exits the current loop. If inside multiple nested loops, `break` only exits the innermost loop. This can be interpreted as "exit the loop".

A `continue` statement skips the rest of current loop iteration. This can be interpreted as "go on to the next pass through the loop".

### For Each Loops
A for each loop has the form:
<pre>
for <em>variable</em> in <em>sequence</em>:
    <em>statement</em>
    ...
</pre>
where *variable* is a new variable name and *sequence* is an expression evaluating into a sequence of values.

Its flow is:
1. If there are no values in *sequence* that haven't been visited yet, stop.
1. Assign *variable* to the next value in *sequence*.
3. Execute the statements in the body of the loop.
4. Go back to step 1.

Here is a more concrete example:
```python
for i in range(10, 0, -1):
    print(i)
```
This loop prints each of the integers from 10 down through 1.

The for each loop is extremely handy for iterating through a list of values:
```python
for n in numbers:
    print(n)
```
where `n` is a variable and `numbers` is a list of values.

The first line of code above can be read, "for each `n` in `numbers`...".

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 1.3](https://introcs.cs.princeton.edu/python/13flow/)

## Questions
1. :star: What is printed by the following code?
    ```python
    for i in range(0, 5):
        print(i, end='')
    ```    
1. :star: Explain how an `if` loop works.
1. :star: How would you write the `for` loop below as a `while` loop?
    ```python
    for i in range(0, 5):
        print(i)
    ```
1. :star: How would you write the `while` loop below as a for each loop? Assume `a` is a list of values.
    ```python
    i = 0
    while (i < len(a)):
        print(a[i])
        i += 1
    ```
1. :star::star: What's the best loop to use to iterate through the elements of a list *backward*?
1. :star::star: What's the best loop to use to modify a list of numbers to make each element 10 times as large?
1. :star::star: Can a loop body be empty?
1. :star::star: What does the code below accomplish? Assume `a` is a list of values.
    ```python
    for i in range(len(a)//2):
        j = len(a) - 1 - i
        t = a[i]
        a[i] = a[j]
        a[j] = t
    ```

## Answers
1. `01234`
1. There is no such thing as an `if` loop. Loops potentially execute their bodies multiple times, but `if` statements do so at most once.
1.
    ```python
    i = 0
    while (i < 5):
        print(i)
        i += 1
    ```
    This isn't *exactly* equivalent, because the local variable `i` holds a different value after the completion of the loop. After the `for` loop, `i` contains `4` (the last element of the range), but after the `while` loop `i` contains 5 (the first value of `i` that causes the condition to fail).
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
    This could also be done with a `while` loop, but it would be more code. A for each loop wouldn't work because it doesn't give you access to the *indices* into the list, just the elements themselves.
1. Sure. This is sometimes useful when all of the necessary work is done in the first line of the loop.
1. It reverses the order of the elements of `a`.
