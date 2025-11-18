# Higher-Order Functions

## Overview
In Python, functions are "first-class citizens", alongside integers, strings, and other objects. This means that variable names can refer to them, they can be passed to functions, and they can be returned by functions. Functions that receive or return other functions are called *higher-order functions*.

*Lambda expressions* are a handy way to create anonymous functions.

## Functions as Arguments
To have something to work with, suppose you define the following functions:

```python
def add_1(x):
    return x + 1

def double(x):
    return x * 2

def one_two_three(f):
    return [f(1), f(2), f(3)]
```

Now `one_two_three(add_1)` returns `[2, 3, 4]` but `one_two_three(double)` returns `[2, 4, 6]`. Whatever function was passed in as `f` is called inside `one_two_three`.

## Returning Functions
A function can be defined inside another function and even returned. Here's an example:

```python
def create_adder(n):
    def f(x):
        return x + n
    return f
```

Now if you define

```python
plus_four = create_adder(x)
```

then `plus_four(3)` returns `7`.

## Lambda Expressions
The following two definitions are equivalent:

```python
def add_1(x):
    return x + 1

add_1 = lambda x : x + 1
```

The second definition uses a lambda expression, which consists of:
* The keyword `lambda`,
* Zero or more arguments separated by commas,
* A colon, and
* An expression that the function returns

This is particularly useful when you're only going to use a function once, so you don't want to bother naming it.

As an example, the built-in function `sorted` takes an optional named argument `key`, which specified how values are to be compared. When sorting strings, if you provide `len` as the key, the strings will be sorted by length, so

```python
sorted(['eggs', 'bread', 'tea', 'cheese'], key=len)
```

returns `['tea', 'eggs', 'bread', 'cheese']`.

If, instead, you want to sort the strings by their *last* characters, you can use a lambda expression.

```python
sorted(['eggs', 'bread', 'tea', 'cheese'], key=lambda s: s[-1])
```

This returns `['tea', 'bread', 'cheese', 'eggs']`.

If you want to sort the strings in the usual lexicographic order, provide the "identity function" using a lambda expression.

```python
sorted(['eggs', 'bread', 'tea', 'cheese'], key=lambda s: s)
```

This returns `['bread', 'cheese', 'eggs', 'tea']`.

If you don't provide a key, `sorted` uses the identity function.

## Resource
* Lubanovic, *Introducing Python: Modern Computing in Simple Packages, Second Edition*, Chapter 9.

## Questions
1. :star: Can a function be passed as an argument to another function?
1. :star: Can a function return another function?
1. :star: If you evaluate an assignment statement that begins with `f =`, what might the right side of the assignment be to make the value of `f` a function?
1. :star::star: Knowing that the built-in function `max`, much like `sorted`, takes an optional argument `key`, you try to find the longest string in a list with:
   ```python
   max(['eggs', 'bread', 'tea', 'cheese'], key=len())
   ```
   Why does this not work?
1. :star::star::star: Suppose you define
   ```python
   def create_multipliers(n):
       result = []
       for i in range(1, n + 1):
           result.append(lambda x: x * i)
       return result

   times_1, times_2, times_3 = create_multipliers(3)
   ```
   Now `times_3(5)` returns 15, as you would expect, but `times_1(5)` does *not* return `5`. What went wrong?
1. :star::star::star: How could you fix the definition to avoid the problem in the previous question?
## Answers
1. Yes.
1. Yes.
1. Possibilities include a lambda expression or a call to a function that returns a function.
1. You have passed in `len()`, which is the a value of *a call to* `len`. Instead you should pass in `len`, the function itself.
1. The function created by the lambda expression remembers the *local variable* `i` instead of its value at the time the lambda expression was evaluated. The value is not looked up until the function created by the lambda expression is called. Since the for loop changes the value of `i` on each iteration, `i` is `3` by the time any of the created functions is called. Any function created inside another function (whether using `def` or `lambda`) acts this way and is called a *closure*.

1. 
   ```python
   def create_multipliers(n):
       def create_multiplier(i):
           return lambda x: x * i
       result = []
       for i in range(1, n + 1):
           result.append(create_multiplier(i))
       return result
   ```
   Now the lambda expression refers to a local variable `i` inside a call to the inner function `create_multiplier`, which is a different variable for each call to `create_multiplier`.
