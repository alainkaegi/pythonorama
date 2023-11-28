# Sets
## Overview
Python can represent a set as you might have encountered in a math class:
```python
s = {1, 2, 3}
```
Like a list, a set is a collection of elements, but it differs in a few ways:
* The order of the elements in a set doesn't matter, so `{1, 2, 3}` and `{1, 3, 2}` are equal. An element is either contained in a set or not.
* A set cannot contain multiple copies of the same elements.
* The elements of a set must be "hashable". In general, this means immutable types like int, float, bool, str, and tuple are okay, but mutable types like list are not.
* Syntatically, a set uses curly braces (`{}`) rather than square brackets (`[]`).
## Set Operations
### Creating Sets
As seen above, you can create a set directly using curly braces.

The `set` function converts any other collection into a set, so `set('hello')` return the set `{'l', 'e', 'h', 'o'}`. Notice that it has removed any duplicates and not preserved the order of the elements.

If you want an empty set, you might reason that since `[]` is the empty list and `()` is the empty tuple, then `{}` must be the empty set. The problem with this theory is that dictionaries *also* use curly braces, so `{}` is an empty dictionary. The empty set is produced by (and displayed as) `set()`.
### `in`
You can determine if an item is in a set using the `in` operator. `2 in {1, 2, 3}` returns `True`.
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
## Questions
empty set
== for different orders
add already present item
remove absent item
set in for loop
set comprehension
set of sets (frozenset)
can convert from any Iterable, not just a Collection
