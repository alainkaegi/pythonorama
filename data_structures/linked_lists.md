# Linked Lists
## Overview
Linear structures like stacks, queues, and lists can be implemented using either [arrays](array_based.md) or linked data structures. A linked list is a chain of node objects, each of which holds one item and knows about the next node (if there is one).

![list contains a reference to a node. That node contains 5 and a reference to the next node. The second node contains 2 and a reference to the third node. The third node contains 3 and a None reference.](linked_list.svg)

## The Node Class

If you define the `Node` class as

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

(The temporary variables `a`, `b`, and `c` are not shown in the diagram.) Note that `c`'s `next` instance variable is set to `None`, indicating that there is no next node.

A linked list is a [recursive](../control_structures/recursion.md) data structure, in that a linked list is either:
- empty (represented as `None`), or
- an item and a reference to another linked list.

## Stacks

Assuming `Node` has already been defined as above, `LinkedStack` can be defined like this:

```python
class LinkedStack:
    def __init__(self):
        self._top = None

    def push(self, item):
        self._top = Node(item, self._top)

    def pop(self):
        result = self._top.item
        self._top = self._top.next
        return result

    def is_empty(self):
        return self._top is None
```

The `LinkedStack`'s sole attribute, `_top`, refers to either the top node in the stack or (if the stack is empty) `None`.

For example, the stack

`5`<br>`2`<br>`7`

would be represented like this:

TODO DIAGRAM

## Queues

TODO CODE

`LinkedQueue` is similar to `LinkedStack`, but it keeps track of both the front and the back of the queue.

The queue

`5` `2` `7`

would be represented like this:

TODO DIAGRAM

`dequeue` works just like `pop`, but `enqueue` modifies the *last* node. Some special handling is needed in case the queue is empty or contains exactly one item.

## Lists

Replicating all of the features of a Python list would require a great deal of code, but the `LinkedList` class below provides basic functionality. It is similar to `LinkedStack`.

TODO CODE

TODO CHECK THE TEXT BELOW -- WHICH METHODS TAKE LINEAR TIME?

The `__getitem__` and `__setitem__` magic methods allow elements of a `LinkedList` to be accessed using the usual square brackets. For example, you can say things like `a[2] = 100`. `__len__` and `__str__` make `len` and `str` work.

The `add_at` and `remove_at` methods insert and remove an item from the list, respectively. Since these potentially require walking down the list to , they take linear time in the worst case.

Sets and dictionaries can be implemented using similar techniques. If better runtime behavior is required, data structures such as hash tables might be preferred.

## Array-Based vs Linked Structures

TODO Advantages, disadvantages, including cache proximity

## Resources

- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 4.3](https://introcs.cs.princeton.edu/python/43stack/)

## Questions

TODO REVISE

1. :star: Write a `Node` class for building linked lists.
1. :star: Name an advantage linked lists have over arrays.
1. :star: What is the value of the `next` instance variable in the *last* `Node` in a linked list?
1. :star::star: The method below is supposed to determine the length of a linked list, but it contains an off-by-one error. How should it be fixed?
    ```python
    def length(list):
        count = 0
        n = list.next
        while n != None:
            count += 1
            n = n.next
        return count
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
