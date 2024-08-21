# Tuples
A tuple is an ordered, finite sequence of values.

A tuple literal is set as a comma-separated list of values. For clarity, and facilitating nesting, we recommend enclosing the list with a pair parentheses. In the following example, the tuple consists of four elements: two strings, an integer, and a float.
```python
t = ('Jane', 'Doe', 27, 3.76)
```

Tuples share some of the same attributes as [arrays](arrays.md). Using the familiar square bracket notation, you can access a specific value in a tuple:
```python
t[1]
```

Also, the `len` function, applied to a tuple, returns its arity (i.e., the number of values it holds):
```python
len(t)
```

There are two notable exceptions to the similarity between tuples and [arrays](arrays.md):
- Each of the values in a tuple can be of different types.
- Tuples are immutable. You cannot change a particular tuple's value without creating an entire new tuple.

You can unpack the values contained in a tuple as follows:
```python
(first, last, age, gpa) = tuple
```
Again, the parentheses are optional, but we are recommending their use.

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 3.3](https://introcs.cs.princeton.edu/python/33design/)

## Questions
1. :star: Assuming variable `t` holds a reference to a tuple of sufficient arity, how can you access its third value?
1. :star: Assuming variable `t` holds a reference to a tuple, how can you establish its arity?
1. :star: Assuming variable `t` holds a reference to a 3-tuple, how can you unpack all its values with a single expression?
1. :star: How you can you pack values `45.52`, `-122.68`, `'Portland'` to form a tuple?
1. :star::star: What do you call a 1-tuple?
1. :star::star: What do you call a 2-tuple?
1. :star::star: Can you have a 0-tuple?
1. :star::star: Can tuples nest?
1. :star::star: Can a value in a tuple be an array?
1. :star::star: You can change a particular value in a tuple?

## Answers
1. `t[2]`
1. `len(t)`
1. `(a, b, c) = t`
1. `(45.52, -122.68, 'Portland')`
1. A singleton.
1. An ordered pair.
1. Yes. There is only one 0-tuple and its called the empty tuple.
1. Yes. For instance, `((1, 2, 3), 'a', 'b', 'c')`
1. Yes. For instance, `([1, 2, 3], 'a', 'b', 'c')`
1. No. Tuples are immutable.
