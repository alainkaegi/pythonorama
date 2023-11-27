# Linked Lists
## Overview
One way to represent a sequence of items is an [array](arrays.md). Another is a *linked list*, which is a chain of Node objects, each of which contains one item and a [reference](references.md) to the next Node.

![list contains a reference to a node. That node contains 5 and a reference to the next node. The second node contains 2 and a reference to the third node. The third node contains 3 and a None reference.](linked_list.svg)

If you have defined the Node class as

```python
class Node:
    def __init__(self, item, next):
        self.item = item
        self.next = next
```

then the list in the diagram above could be created by the following code:

```python
c = Node(3, None)
b = Node(2, c)
a = Node(5, b)
list = a
```

(The temporary variables `a`, `b`, and `c` are not shown in the diagram.) Note that `c`'s `next` instance variable is set to `None`. The value `None` is also used to represent an empty linked list (one containing no items).

A linked list is a [recursive](../control_structures/recursion.md) data structure, in that a linked list is either:

- empty (represented as `None`), or
- an item and a reference to another linked list.

Methods operating on lists tend to either be recursive, taking advantage of this structure, or iterative, walking down the chain of `next` references. For example, here are two ways to find the sum of the numbers in a list:

```python
def recursive_sum(list):
    if list == None:
        return 0
    return list.item + recursive_sum(list.next)
```

```python
def iterative_sum(list):
    sum = 0
    n = list
    while n != None:
        sum += n.item
        n = n.next
    return sum
```

## Resource
Note: many sources, including other parts of Pythonorama, discuss linked lists in the context of more complex objects.

- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 4.3](https://introcs.cs.princeton.edu/python/43stack/)

## Questions
1. :star: Write a `Node` class for building linked lists.
1. :star: Name an advantage linked lists have over arrays.
1. :star: What is the value of the `next` instance variable in the *last* Node in a linked list?
1. :star::star: The method below is supposed to determine the length of a linked list, but it contains an off-by-one error. How should it be fixed?
    ```python
    def length(list):
        l = 0
        n = list.next
        while n != None:
            l += 1
            n = n.next
        return l
    ```

## Answers
1.  ```python
    class Node:
        def __init__(self, item, next):
            self.item = item
            self.next = next
    ```
1. A linked list can grow longer or shorter. An array, in many programming languages, must have its length specified when it is created.
1. `None`.
1. `n` should start at `list`, not `list.next`.
