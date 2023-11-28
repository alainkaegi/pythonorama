# Sets
## Overview
Python can represent a set like those you might have encountered in a math class:
```python
s = {1, 2, 3}
```
Like a list, a set is a collection of elements, but it differs in a few ways:
* The order of the elements in a set doesn't matter, so `{1, 2, 3}` and `{1, 3, 2}` are equal. An element is either contained in a set or not.
* A set cannot contain multiple copies of the same elements.
* The elements of a set must be "hashable". In general, this means immutable types like `int`, `float`, `bool`, `str`, and `tuple` are okay, but mutable types like `list` are not.
* Syntactically, a set uses curly braces (`{}`) rather than square brackets (`[]`).
## Set Operations
### Creating Sets
As seen above, you can create a set directly using curly braces.

The `set` function converts any other collection into a set, so `set('hello')` return the set `{'l', 'e', 'h', 'o'}`. Notice that it has removed duplicates and not preserved the order of the elements.

If you want an empty set, you might reason that since `[]` is the empty list and `()` is the empty tuple, then `{}` must be the empty set. The problem with this theory is that dictionaries *also* use curly braces. `{}` is an empty dictionary. The empty set is produced by (and displayed as) `set()`.
### `in`
You can determine if an element is in a set using the `in` operator. `2 in {1, 2, 3}` returns `True`.
### `add` and `remove`
You can add an element to a set with the `add` method and remove an element with `remove`. After
```python
a = {1, 2, 3}
a.add(5)
a.remove(2)
```
`a` is `{1, 3, 5}`.
### Set Operations
Standard mathematical set operations are supported. In the table below, assume we have defined:
```python
a = {1, 2, 3}
b = {2, 3, 4}
c = {2, 3}
```
|Operation|Description|Example|Result|
|---|---|---|---|
|Union|Elements in either set|`a \| b`|`{1, 2, 3, 4}`|
|Intersection|Elements in both sets|`a & b`|`{2, 3}`|
|Difference|Elements in first set but not in second set|`a - b`|`{1}`|
|Symmetric difference|Elements in one set but not the other|`a ^ b`|`{1, 4}`|
|Subset|First set contains only elements from second|`c <= b`|`True`|
| | |`b <= b`|`True`|
|Proper subset|First set contains only elements from second, but not all of them|`c < b`|`True`|
| | |`b < b`|`False`|
|Superset|Second set contains all elements from first|`b >= c`|`True`|
| | |`b >= b`|`True`|
|Proper superset|Second set contains all elements from second, plus at least one more|`b > c`|`True`|
| | |`b > b`|`False`|

## Resources
- Lubanovic, *Introducing Python: Modern Computing in Simple Packages (2nd Edition)*, pp. 129-136.
## Questions
1. :star: How do you create an empty set?
2. :star: Is `{1, 2, 3} == {3, 2, 1}`?
3. :star::star: What happens if you add an element to a set that already contains that element?
4. :star::star: What happens if you remove an element from a set that doesn't contain that element?
5. :star::star: Can you use a `for` loop to iterate through the elements of a set?
6. :star::star: How might you create the set of absolute values of the integers from -5 through 5?
7. :star::star: Can you make a set of sets?
8. :star::star::star: Can you use `set` to convert a zip into a set?
set of sets (frozenset)
can convert from any Iterable, not just a Collection
## Answers
1. `set()`
2. Yes, because the order of elements doesn't matter.
3. Nothing, because duplicates are discarded.
4. You get a KeyError, because the element (key) is not present. Use `in` to verify that an element is present before removing it.
5. Yes. For example, this is fine:
   ```python
   for a in {1, 2, 3}:
     print(a)
   ```
6. One way is using a set comprehension, which is analogous to a list comprehension: `{abs(n) for n in range(-5, 6)}`
7. No, because sets are mutable and therefore not hashable. If you really need to do this (or otherwise need an immutable set), research the `frozenset` type.
8. Yes. `set` works on any Iterable type. This includes `zip` and `generator`, as well as Collection types (such as `tuple`, `range`, `str`, `list`, `set`, and `dict`).
