# Magic Methods

The [Classes and Initializers](./classes.md) page describes how to define initializers to give your objects an initial value. The name of those initializer methods follows a strict convention: the word `init` enclosed between a pair of double underscores.

Python defines a series of similarly named methods to provide important and convenient functionality to our objects.

## The `__str__()` method

Whenever you invoke the function `str()` on an object, Python will automatically invoke the method `__str__()` on the object, if such a method is defined.

Say, we wanted to define our own data type to support complex numbers. Here is an initial sketch.

```python
class Complex:

    def __init__(self, r, i):
        self._r = r
        self._i = i
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

So let us add a pertinent definition for `__str__()`:

```python
class Complex:

    def __init__(self, r, i):
        self._r = r
        self._i = i

    def __str__(self):
        return str(self._r) + ' + ' + str(self._i) + 'i'
```

Now if we create and print an instance of such class:

```
c = Complex(1.0, 1.0)
print(str(c))
```

we obtain something more informative:

```
1.0 + 1.0i
```

Notice how the `__str__()` method takes only a single argument, named `self` by convention. That argument is a reference to the object for which we wish to have human-readable representation in the form of a string that the method returns.

Here's what happens behind the scenes when you evaluate `str(c)`:
1. Python calls the function `str()` with the argument `c`.
1. `str()` checks if a method called `__str__()` is defined for `c`.
1. If so, it calls that method with `c` as its parameter.
1. Finally, `str()` returns the string returned by `__str__()`.

## Equality

Unless you define the appropriate functions (`__eq__()` and `__ne__()`), two distinct objects will be considered different even if their contents match.

Here are our complex numbers again, this time with a definition of what it means for two instances of that class to be equal.

```python
class Complex:

    def __init__(self, r, i):
        self._r = r
        self._i = i

    def __str__(self):
        return str(self._r) + ' + ' + str(self._i) + 'i'

    def __eq__(self, other):
        return self._r == other._r and self._i == other._i

    def __ne__(self, other):
        return self._r != other._r or self._i != other._i
```

Here's what happens behind the scenes when you evaluate `c1 == c2`:
1. Python checks if a method called `__eq__()` is defined for `c1`.
1. If so, it calls that function on `c1` with `c2` as an argument (i.e., `c1.__eq__(c2)`).
1. It returns the boolean value returned by that function.

If you don't specify a method `__ne__()`, Python will invoke `__eq__()`, if available, and return its inverse. So, in principle, it is not necessary to specify both `__eq__()` and `__ne__()`.