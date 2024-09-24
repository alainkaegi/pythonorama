# Queues
## Abstract Data Type
A *queue* (pronounced like the letter Q) is similar to a [stack](stacks.md), but items are added at one end (the back) and removed from the other (the front). The metaphor is a line of people waiting to buy tickets: new people arrive at the back and (after buying their tickets) leave from the front. Britons call such a line a queue and will talk about "queuing up".

A queue supports the following operations:
- `dequeue` (pronounced DQ) removes and returns the front item from the queue
- `enqueue` (pronounced NQ) adds an item to the back of the queue
- `is_empty` returns `True` if the queue is empty

Because items leave in the same order they arrive, queues are *first in, first out* (FIFO).

If `q` is an empty queue, you might evaluate the following sequence of expressions:
| **Expression** | **Queue contents** | **Result** |
|-|-|-|
|`s.is_empty()`| |`True`|
|`s.enqueue(1)`|`1`| |
|`s.is_empty()`|`1`|`False`|
|`s.enqueue(2)`|`1` `2`| |
|`s.enqueue(3)`|`1` `2` `3`| |
|`s.dequeue()`|`2` `3`|`1`|
|`s.dequeue()`|`3`|`2`|
|`s.dequeue()`| |`3`|
|`s.is_empty()`| |`True`|

As described below, Python lists can function as inefficient queues. The [`deque`](https://docs.python.org/3/library/collections.html#collections.deque) (pronounced deck) class in the [`collections`](https://docs.python.org/3/library/collections.html) module provides a more efficient queue. A queue can also be implemented using an array-based or linked data structure.

## Analysis
All of the queue operations take constant time with an efficient implementation. This analysis is worst-case for a linked implementation (like `deque`) but (except for `is_empty`) only amortized for an array-based implementation.

A queue holding $n$ items uses space in $\Theta(n)$.

## Python Implementation
A Python list *can* be used as a queue, but the `dequeue` operation (implemented as `pop(0)`) takes linear time. This should therefore be avoided unless the queue is guaranteed to remain small.

The `deque` class, in the `collections` module, provides a more efficient, doubly-linked implementation. The name `deque` is short for "double-ended queue", as this implementation support inserting and removing items at both ends. A new instance can be created as `deque()`.
|**Abstract data type implementation**|**List operation**|**Deque operation**|
|-|-|-|
|`q.is_empty()`|`q == []`|`len(q) == 0`|
|`q.enqueue(x)`|`q.append(x)`|`q.append(x)`|
|`q.dequeue()`|`q.pop(0)`|`q.popleft()`|

Both empty lists and empty deques are falsy, so you can simply say `if q: ...` to check if a queue is (not) empty.

## Resources
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 4.3](https://introcs.cs.princeton.edu/python/43stack/)
- Python official documentation, The Python Standard Library, [`collections` —
 Container datatypes](https://docs.python.org/3/library/collections.html)
- Python official documentation, The Python Standard Library, [`deque` objects](https://docs.python.org/3/library/collections.html#collections.deque)

## Questions
1. :star: What is the difference between a stack and a queue?
1. :star::star: Here is queue `q`:

    `5` `2` `7`

    Draw the final state of the queue after executing the following sequence of operations:
    ```python
    q.enqueue(4)
    q.dequeue()
    q.dequeue()
    q.enqueue(8)
    ```
1. :star::star: Assuming `LinkedQueue` implements the queue abstract data type, what does the code below do?
    ```python
    from linked_queue import LinkedQueue

    with open('file.txt') as f:
        q = LinkedQueue()
        for line in f:
            q.enqueue(line)
        while not q.is_empty():
            print(q.dequeue(), end='')
    ```

## Answers
1. A stack is last in, first out while a queue is first in, first out.
1. `7` `4` `8`
1. It prints the lines of `file.txt` in their original order.
