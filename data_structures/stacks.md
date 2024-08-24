# Stacks
## Abstract Data Type
An *abstract data type* defines a data type and associated operations. It does not say anything about how these operations are implemented; it merely conveys the idea of the data type.

The *stack* abstract data type defines a stack as a vertical sequence of items. The standard metaphor for a stack is one of those spring-loaded stacks of plates you might find in a cafeteria. You can push a new plate onto the stack or pop one off the top, but there's no way to access the plates underneath. The sequence of previously-viewed pages that your web browser maintains to allow you to go back is also represented as a stack.

A stack supports the following operations:
- `is_empty` returns `True` if the stack is empty
- `pop` removes and returns the top item from the stack
- `push` adds an item to the top of the stack

Because the last item pushed onto a stack will be the first one popped, stacks are said to be *last in, first out* (LIFO).

If `s` is an empty stack, you might evaluate the following sequence of expressions:
| **Expression** | **Stack contents** | **Result** |
|-|-|-|
|`s.is_empty()`| |`True`|
|`s.push(1)`|`1`| |
|`s.is_empty()`|`1`|`False`|
|`s.push(2)`|`2`<br>`1`| |
|`s.push(3)`|`3`<br>`2`<br>`1`| |
|`s.pop()`|`2`<br>`1`|`3`|
|`s.pop()`|`1`|`2`|
|`s.pop()`||`1`|
|`s.is_empty()`| |`True`|

As described below, Python lists can function as stacks. A stack can also be implemented using an array-based or linked data structure.

## Analysis
All of the stack operations take constant time. This analysis is worst-case for an linked implementation but (except for `is_empty`) only amortized for an array-based implementation. The default Python implementation discussed below is array-based.

A stack holding $n$ items uses space in $\Theta(n)$.

## Python Lists as Stacks
Python lists provide all of the stack operations, although `push` is called `append`.

| **Abstract data type operation** | **List operation** |
|-|-|
|`s.is_empty()`|`s == []`|
|`s.push(x)`|`s.append(x)`|
|`s.pop()`|`s.pop()`|

Since the empty list is considered falsy, you can simply say `if s: ...` instead of `if s == []: ...`.

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 4.3](https://introcs.cs.princeton.edu/python/43stack/)

## Questions
1. :star: What is the amortized running time of all three stack operations in both array-based and linked implementations?
1. :star::star: Here is a stack `s`:

    `5`<br>`2`<br>`7`

    Draw the final state of the stack after executing the following sequence of operations:
    ```python
    s.push(4)
    s.pop()
    s.pop()
    s.push(8)
    ```
1. :star::star: Assuming `ArrayStack` implements the stack abstract data type, what does the code below do?
    ```python
    from array_stack import ArrayStack

    with open('file.txt') as f:
        s = ArrayStack()
        for line in f:
            s.push(line)
        while not s.is_empty():
            print(s.pop(), end='')
    ```

## Answers
1. Constant.
1. `8`<br>`2`<br>`7`
1. It prints the lines of `file.txt` in reverse order.
