# Array-Based Structures

Python uses the list as its default linear structure. Lower-level languages like C instead use primitive arrays. Key differences include:
- An array's size must be allocated when it is created; it cannot change.
- Python list features, such as slicing and methods like the `count` method, are not directly available for primitive arrays.

This page describes how to build various linear structures out of [Python lists masquerading as] primitive arrays. While you would normally just use Python's lists, sets, and so on, this is worthy of study because:
- Understanding the underlying data structures and algorithms clarifies the performance of Python's fancier data structures. For example, it will help you understand why adding something to the *beginning* of a long list is much more expensive than adding something to the *end*.
- You may someday be working in a language that uses primitive arrays.
- You may need a data structure that is slightly different from what Python provides.

Many of these data structures can also be implemented using other techniques, such as linked lists and hash tables.

## Primitive Arrays

To use Python's convenient list syntax while limiting yourself to what a primitive array can do, use only the following features, all of which take constant time:

Operation|Syntax
-|-
Allocate an array of length $n$|`a = [None] * n`
Access element $i$|`a[i]`
Set element $i$ to $x$|`a[i] = x`
Get the length of an array|`len(a)`

To iterate through a primitive array, use the following syntax:

```python
for i in range(len(a)):
  # Do something with a[i]
```

If, for efficiency reasons, you want an actual primitive array, use Python's numpy library.

# Stacks

```python
class ArrayStack:
    def __init__(self):
        self._data = [None]
        self._count = 0

    def push(self, item):
        if self._count == len(self._data):
            self._expand()
        self._data[self._count] = item
        self._count += 1

    def pop(self):
        self._count -= 1
        return self._data[self._count]

    def is_empty(self):
        return self._count == 0

    def _expand(self):
        new_data = [None] * self._count * 2
        for i in range(self._count):
            new_data[i] = self._data[i]
        self._data = new_data
```

The class ArrayStack has two attributes, `_data` and `_count`. `_data` is a primitive array holding the items on the stack. In order to allow the stack to grow and shrink without resizing the array, the capacity of `_data` may be larger than the current height of the stack. `_count` indicates how much of the array is actually part of the stack. It also indicates the index of the next available slot in the array.

For example, an ArrayStack with capacity for 8 items, but currently only holding 5, would look like this:

DIAGRAM

This simple implementation's behavior is undefined if a user pops an empty stack (which they should have detected by calling `is_empty`). A more robust implementation would throw an EmptyStackException instead.

## Resizing the data array
What if a user pushes something onto a stack that is full? Stacks should behave as if they have unlimited capacity. In this situation, the `_expand` method copied the data into a larger array, which then replaces `_data`.

DIAGRAM

The new array is not merely one slot larger but *twice* as large, keeping the amortized running time of `pop` constant.

# Queues
# Lists
# Sets

# Resources

# Questions
1. shrinking stack when it gets far under capacity

# Answers
