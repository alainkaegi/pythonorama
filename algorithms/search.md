# Search
This section deals with the question of whether some key (value) is present in an array.

## Linear Search
The obvious approach, *linear search*, is to simply look at each element of the array using a loop:
```python
def linear_search(key, a):
    """Returns the first index at which key appears in a, or -1 if it does not."""
    for i in range(len(a)):
        if a[i] == key:
            return i
    return -1
```

In the worst case, when `key` is either the last element or not present, this takes linear time. On average, assuming `key` is present and equally likely to be in any postion, about half of the elements have to be inspected, which still takes linear time.

## Binary Search
It is possible to do better than linear search if the array is *sorted* in increasing order. This is only meaningful for arrays of types that can be compared to see if one value is larger than another. Clearly numbers can be compared. Strings can also be compared in *lexicographical order* (which is similar to alphabetical order, but accounts for with upper and lower case letters, digits, and other characters).

For a sorted array, the *binary search* algorithm starts by examining the *middle* element of the array. If it is equal to they key, its position is returned. Otherwise, binary search recursively searches either the left half of the array (if the key is less than the element examined) or the right half (otherwise). This continues until either the key is found or the region being searched shrinks to nothing (indicating that the key is not present).

Sedgewick, Wayne, and Dondero provide [an implementation](https://introcs.cs.princeton.edu/python/42sort/binarysearch.py.html). Note that the function `search` calls `_search`, a private, more general, recursive helper function.

How long does binary search take in the worst case? An equivalent question is how many times the array length ![n](https://latex.codecogs.com/svg.latex?n) can be divided in half before getting down to 1. This is the definition of ![log base 2 of n](https://latex.codecogs.com/svg.latex?\log_2&space;n). The worst case running time of binary search is therefore in ![order log n](https://latex.codecogs.com/svg.latex?\Theta(\log&space;n)).

The average running time is also logarithmic because about half of the array elements won't be examined until just before giving up (that is, after ![order log n](https://latex.codecogs.com/svg.latex?\Theta(\log&space;n)) comparisons).

## Resource
- Sedgewic, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 4.2](https://introcs.cs.princeton.edu/python/42sort/)

## Questions
1. :star: What is the order of the worst-case running time of binary search?
1. :star: What must be true of an array for binary search to be used on it?
1. :star::star: What is the order of the best-case running time of linear search?
1. :star::star: Complete the function below.
    ```python
    def linear_search(key, a):
        """Returns the first index at which key appears in a, or -1 if it does not."""
    ```
1. :star::star::star: To find the midpoint, Sedgewick, Wayne, and Dondero use the expression `(lo + hi) // 2`. Wouldn't `lo + (hi - lo) // 2` work just as well and avoid an integer overflow?

## Answers
1. ![order log n](https://latex.codecogs.com/svg.latex?\Theta(\log&space;n))
1. It must be sorted.
1. Constant. This would happen if the first element of the array was the key being sought.
1.
    ```python
    def linear_search(key, a):
        """Returns the first index at which key appears in a, or -1 if it does not."""
        for i in range(len(a)):
            if a[i] == key:
                return i
        return -1
    ```
1. No. Python's integers have arbitrary range and therefore do not overflow.
