# Magic Methods

The [Classes and Initializers](./classes.md) page describes how to define initializers to give your objects an initial value. The name of those initializer methods follows a strict convention: it must be the word `init` enclosed between a pair of double underscores (`__init__`).

Python defines a series of similarly named methods to provide important and convenient functionality to our objects. We, and others, will refer to these methods as "magic" or "special" given their particular roles.

## The `__str__()` method

Whenever you invoke the function `str()` on an object, Python will automatically invoke the "magic" method `__str__()` on the object, if such a method is defined.

Say, we wanted to define our own data type to support complex numbers. (Note that Python does have built-in support for complex numbers, so this example is mostly for illustrative purposes). Here is an initial sketch:

```python
class Complex:

    def __init__(self, r, i):
        self.r = r
        self.i = i
```

With this definition, if we create an instance of a complex number and tried to print its value:

```python
c = Complex(1.0, 1.0)
print(str(c))
```

We would see an output close to:
```
<__main__.Complex object at 0x1061d0b10>
```

This output has limited usefulness.

So let us add a pertinent definition for `__str__()`:

```python
class Complex:

    def __init__(self, r, i):
        self.r = r
        self.i = i

    def __str__(self):
        return str(self.r) + ' + ' + str(self.i) + 'i'
```

Now if we create and print an instance of such class

```
c = Complex(1.0, 1.0)
print(str(c))
```

we obtain something more informative:

```
1.0 + 1.0i
```

Notice how the `__str__()` method takes only a single argument, named `self` by convention. That argument is a reference to the object for which we wish to have human-readable, informal representation in the form of a string that the method returns.

Here's what happens behind the scenes when you evaluate `str(c)`:
1. Python calls the function `str()` with the argument `c`.
1. `str()` checks if a method called `__str__()` is defined for the object referenced by `c`.
1. If so, it calls that method with `c` as its parameter.
1. Finally, `str()` returns the string returned by `__str__()`.

## Equality

Unless you define an appropriate method (`__eq__()`), two distinct objects will be considered different even if their contents match.

Here are our complex numbers again, this time with a definition of what it means for two instances of that class to be equal.

```python
class Complex:

    def __init__(self, r, i):
        self.r = r
        self.i = i

    def __str__(self):
        return str(self.r) + ' + ' + str(self.i) + 'i'

    def __eq__(self, other):
        return self.r == other.r and self.i == other.i
```

Here's what happens behind the scenes when you evaluate `c1 == c2`:
1. Python checks if a method called `__eq__()` is defined for the object referenced by `c1`.
1. If so, it calls that function on `c1` with `c2` as an argument (i.e., `c1.__eq__(c2)`).
1. It returns the boolean value returned by that function.

## Operator Overloading

We have grown accustomed to using the `==` operator with our built-in types (`int`, `float`, `bool`, and `str`). In the previous section, we have also been able to define what this operator means for a new type of our own creation (`Complex`).

The ability for a programming language to allow the programmer to define a meaning for an existing operator in conjunction with a new type is called *operator overloading*.

## Overloading Other Operators

Python provides the programmer the means to overload most of its operators. Here is a subset of these overloadable operators along with the corresponding magic methods that would need to be defined.

### Comparisons

Operator | Magic method
-|-
`<` | `__lt__(self, other)`
`<=` | `__let__(self, other)`
`>` | `__gt__(self, other)`
`>=` | `__ge__(self, other)`

### Mathematical Operations

Operator | Magic method
-|-
`+` | `__add__(self, other)`
`-` | `__sub__(self, other)`
`*` | `__mul__(self, other)`
`/` | `__truediv__(self, other)`
`//` | `__floordiv__(self, other)`
`%` | `__mod__(self, other)`
`**` | `__pow__(self, other)`

## Resources

* Lubanovic, *Introducing Python, 3rd Edition*, Chapter 10

## Questions

1. :star: Supply a plausible `__str__()` method for the class below
    ```python
    class Position:
        def __init__(self, x, y):
            self.x = x
            self.y = y
   ```
1. :star: Supply a plausible `__eq__()` method for the class below
    ```python
    class Position:
        def __init__(self, x, y):
            self.x = x
            self.y = y
   ```
1. :star: Can one overload the addition operator (`+`) in Python?
1. :star: What is the name of the method one must define to overload the multiplication operator (`*`) in Python?
1. :star::star: Assuming two distinct objects, `o1` and `o2`, of the same type, the expression `o1 == o2` will always return `True` as long as their contents are equal.
1. :star::star: Assume class `MyType` does not define the magic method `__str__()`. Then, is it an error to call `str()` on an instance/object of that class?
1. :star::star: Can you overload the `is` operator?
1. :star::star: Can you overload a method or function in Python?
1. :star::star::star: If a class defines the magic method `__eq__()`, must it also also define the magic method `__ne__()`?

## Answers

1. ```python
        def __str__(self):
            return '<' + str(self.x) + ', ' + str(self.y) + '>'
   ```
1. ```python
        def __eq__(self, other):
            return self.x == other.x and self.y == other.y
   ```
1. Yes. To do so, one must supply a definition for the magic method call `__add__`.
1. `__mul__`
1. No. If the associated class declaration does not provide a definition for equality, the comparison of two objects may yield `False` even if their contents are the same.
1. No, it is not an error. If `__str__()` is not provided, then a default implementation is invoked instead, typically producing a string like `<__main__.MyType object at 0x1036a4a90>`.
1. No, certain Python operators cannot be overloaded. They include `is`, `not`, `and`, and `or`.
1. No, Python does not support function or method overloading. If you define multiple functions or methods within a module or class, the last definition will overwrite all previous ones.
1. No. If you don't specify a method `__ne__()`, Python will invoke `__eq__()`, if available, and return its inverse.
