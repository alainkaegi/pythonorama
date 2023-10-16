# Omitting Needless Code
## Overview
> Omit needless words.
>
> Vigorous writing is concise. A sentence should contain no unnecessary words, a paragraph no unnecessary sentences, for the same reason that a drawing should have no unnecessary lines and a machine no unnecessary parts. This requires not that the writer make all sentences short, or avoid all detail and treat subjects only in outline, but that every word tell.
>
> -Strunk and White, *The Elements of Style*

Programs should be clear. To that end, they should be concise. An overly long program is tedious to write and difficult to read and maintain. A program that solves a problem with a small amount of clear code is considered *elegant*.

Crafting elegant solutions is part of the art of programming. Several techniques will steer you in the right direction.

### Don't Check For Conditions That Must Be True
Consider this function to determine whether a number is even:
```python
def iseven(n):
    result = False
    if n % 2 == 0:
        result = True
    elif n % 2 == 1:
        result = False
    return result
```

This is correct, but it can be more concise.
`n % 2` must either be 0 or 1. You therefore don't need the second `if` check:
```python
def iseven(n)
    result = False
    if n % 2 == 0:
        result = True
    else:
        result = False
    return result
```

### Do Not Store Values That Will Never Be Read
Continuing the example, the initial value of `result` will never be read (it is *always* going to be set in the `if` statement) so there's no need to initialize it:
```python
def iseven(n):
    if n % 2 == 0:
        result = True
    else:
        result = False
    return result
```

This is correct and shorter than the original, but you can do even better.

### Stop As Soon As You Know The Answer
In this example, once the value of `result` has been set, it will never change. You can therefore return as soon as you know the answer:

```python
def iseven(n):
    if n % 2 == 0:
        return True
    else:
        return False
    return result
```

Now the local variable `result` can be eliminated completely:
```python
def iseven(int n):
    if n % 2 == 0:
        return True
    else:
        return False
```

### Use Shorter Expressions
In the example, the function returns `True` if `n % 2 == 0` is true and `False` if `n % 2 == 0` is false. In other words, the value of `n % 2 == 0` is the value you want to return:

```python
def iseven(n):
    return n % 2 == 0
```

### Avoid Redundant Code
If you find the identical code in several places in your program, strongly consider defining one function and calling it in each place. [Don't repeat yourself.](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

If you find several *similar* patches of code, see if you can figure out what's similar and what's different between them. Write a function whose parameters specify the different part.

If the identical or similar sections of code appear one right after another, a loop may be the easiest solution.

### Minimize Special Cases
Sometimes exactly the same code can handle more than one case.

### Separate Control From Data
This function finds the sum of the four elements adjacent to element `r`, `c` in a two-dimensional array:

```python
def neighbor_sum(grid, r, c):
    sum = 0
    if r > 0:
        sum += grid[r - 1][c]
    if r < len(grid) - 1:
        sum += grid[r + 1][c]
    if c > 0:
        sum += grid[r][c - 1]
    if c < len(grid[r]) - 1:
        sum += grid[r][c + 1]
    return sum
```

The four if statements differ only in their tests and in the array indices. By storing the four directions in a separate array `offsets`, you can accomplish all of these in one loop:

```python
def neighbor_sum(grid, r, c):
    offsets = [[-1, 0], [1, 0], [0, -1], [0, 1]]
    sum = 0
    for offset in offsets:
        rr = r + offset[0]
        cc = c + offset[1]
        if rr >= 0 and rr < len(grid) and cc >= 0 and cc < len(grid[r]):
            sum += grid[rr][cc]
    return sum
```

This improvement was made by separating the control (what to do with each neighbor) from the data (the list of offsets to find neighbors).

Modifying the function to also look at the diagonal neighbors now becomes trivial; only the data has to be modified.

```python
def neighbor_sum(grid, r, c):
    offsets = [[-1, 0], [1, 0], [0, -1], [0, 1], [-1, -1], [-1, 1], [1, -1], [1, 1]]
    sum = 0
    for offset in offsets:
        rr = r + offset[0]
        cc = c + offset[1]
        if rr >= 0 and rr < len(grid) and cc >= 0 and cc < len(grid[r]):
            sum += grid[rr][cc]
    return sum
```

## Resource
- Martin, *Clean Code*

## Questions
1. :star::star: Is a shorter program always preferable?
1. :star::star: Using an array, refactor the function below to avoid the long if/elif/else chain.
    ```python
    def __str__(n):
        if n == 0:
            return 'red'
        elif n == 1:
            return 'orange'
        elif n == 2:
            return 'yellow'
        elif n == 3:
            return 'green'
        elif n == 4:
            return 'blue'
        elif n == 5:
            return 'indigo'
        else:
            return 'violet'
    ```

## Answers
1. No. The goal is clarity, and to that end we omit only *needless* code. Programmers sometimes play ["code golf"](https://en.wikipedia.org/wiki/Code_golf), solving a problem in as few characters as possible, but a program so short that it becomes cryptic serves nothing but the ego of the programmer.
1.
    ```python
    def __str__(n):
        colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']
        return colors[n]
    ```
    It would be even better to use the Python convention of naming constants using only capital letters (e.g., `COLORS`).
    
    Strictly speaking, this code is not *precisely* equivalent to the original code, as it doesn't behave the same way if `n` is not a valid index into `colors`. This could be remedied by adding the following between the two lines in the function above:
    ```python
        if n < 0 or n >= len(colors):
            n = len(colors) - 1
    ```
