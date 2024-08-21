# Magic Methods
The [Classes and Initializers](./classes.md) page describes how to define initializers to give your instance variables initial value. The name of an initializer method follows a strict convention: it must be `__init__`, including the double underscores on both ends.

Python specifies several other special names for methods that many classes will have. Because these methods cause certain things to happen automatically, they are sometimes called *magic methods*.

## The `__str__` method
Whenever you call the `str` function, Python will automatically invoke the magic method `__str__` on the object that is passed to as an argument to `str`. In other words, `str(obj)` is equivalent to `obj.__str__`.

Say you wanted to define your own data type to support complex numbers. (Python has built-in support for complex numbers, so this example is purely for illustrative purposes). Here is an initial sketch:
```python
class Complex:

    def __init__(self, r, i):
        self.real = r
        self.imag = i
```

With this definition, if we create an instance of a complex number and tried to print its value
```python
c = Complex(1.0, 1.0)
print(str(c))
```

we would see an output something like:
```
<__main__.Complex object at 0x1061d0b10>
```

This output has limited usefulness.

So let us add a pertinent definition for `__str__`:
```python
class Complex:

    def __init__(self, r, i):
        self.real = r
        self.imag = i

    def __str__(self):
        return str(self.real) + ' + ' + str(self.imag) + 'i'
```

Now if we create and print an instance of `Complex`
```python
c = Complex(1.0, 1.0)
print(str(c))
```

we obtain something more informative:
```
1.0 + 1.0i
```

Here's what happens behind the scenes when you evaluate `str(c)`:
1. Python calls the function `str` with the argument `c`.
1. It calls that method on the object to which `c` refers.
1. Finally, `str` returns the string returned by `__str__`.

If you don't define `__str__` for your class, your class inherits a default version like the one that produced `<__main__.Complex object at 0x1061d0b10>` above.

## Equality
Unless you define an appropriate method (`__eq__`), two distinct objects are considered different even if their contents match. For example,
```python
a = Complex(2.0, 3.0)
b = Complex(2.0, 3.0)
```

creates two instances of the `Complex` class. Even though their instance variables happen to have the same values, `a == b` evaluates to `False`, because `a` and `b` do not refer to *the same object*.

Here is the `Complex` class again, this time with a definition of what it means for two instances of that class to be equal.
```python
class Complex:

    def __init__(self, r, i):
        self.real = r
        self.imag = i

    def __str__(self):
        return str(self.real) + ' + ' + str(self.imag) + 'i'

    def __eq__(self, other):
        return self.real == other.real and self.imag == other.imag
```

Here's what happens behind the scenes when you evaluate `c1 == c2`:
1. Python calls the `__eq__` method on `c1` with `c2` as an argument (i.e., `c1.__eq__(c2)`).
1. It returns the boolean value returned by that method.

Again, if you don't define `__eq__`, you inherit a default version which simply checks whether `self` and `other` are the same object.

## Operator Overloading
By now you must have grown accustomed to using the `==` operator with the built-in types (`int`, `float`, `bool`, and `str`). In the previous section, you have also seen how to define what this operator means for a new type of your own creation (`Complex`).

An operator that behaves differently depending on the types of its operands is said to be *overloaded*.

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
1. :star: Supply a plausible `__str__` method for the class below.
    ```python
    class Position:
        def __init__(self, x, y):
            self.x = x
            self.y = y
   ```
1. :star: Supply a plausible `__eq__` method for the class below.
    ```python
    class Position:
        def __init__(self, x, y):
            self.x = x
            self.y = y
   ```
1. :star: Can one overload the addition operator (`+`) in Python?
1. :star: What is the name of the method one must define to overload the multiplication operator (`*`) in Python?
1. :star::star: Assuming two distinct objects, `o1` and `o2`, of the same type, will the expression `o1 == o2` always return `True` as long as their contents are equal?
1. :star::star: Assume class `MyType` does not define the magic method `__str__`. Is it an error to call `str` on an instance/object of that class?
1. :star::star: Can you overload the `is` operator?
1. :star::star: Can you overload a method or function in Python?
1. :star::star::star: If a class defines the magic method `__eq__`, must it also also define the magic method `__ne__`?

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
1. No. If a class does not define `__eq__`, it inherits a default version that returns `False` when used to compare distinct objects, even if their contents are the same.
1. No, it is not an error. If `__str__` is not provided, then a default implementation is invoked instead, typically producing a string like `<__main__.MyType object at 0x1036a4a90>`.
1. No, certain Python operators cannot be overloaded. They include `is`, `not`, `and`, and `or`.
1. No, Python does not support function or method overloading. If you define multiple functions or methods within a module or class, the last definition will overwrite all previous ones.
1. No. If you don't specify a method `__ne__`, Python will invoke `__eq__` and return its inverse.
