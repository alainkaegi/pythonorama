# Defensive Programming
## Getters and Setters
Suppose we have a `Person` class with an instance variable `_height`. A convention described [elsewhere](names.md) suggests that `_height` should be private.

Indeed, but what if you need to get the height of person `p` in another class? Convention suggests that you shouldn't refer to `p._height` directly because it is private.

The correct solution is to provide a *getter* (*accessor*) and a *setter* (*mutator*):
```python
def get_height(self):
    return self._height

def set_height(self, height):
    self._height = height
```

Now other classses can refer to, for example, `p.get_height()`.

If other classes can now modify `_height` using `set_height`, what was the point of all this? Why not just make `_height` public? Using getters and setters provides several advantages:
- If you want to suggest that others can see an instance variable but not modify it, you can provide a getter but no setter.
- You can change your internal representation without modifying the getter and setter behavior. For example, a class representing a two-dimensional vector might use rectangular or polar coordinates; someone using such a class doesn't have to know which it is and their code won't break if the representation is changed.
- A setter can enforce constraints, such as disallowing negative heights or making sure that multiple instance variables have consistent values.
- While debugging, you know that any change to the instance variable *should* either be in this class or go through the setter, so you only have to look at code in this class.

While the Python compiler does not enforce the use of setters and getters to access private instance variables, other tools can verify adherence to the convention.

## Immutability
An object is immutable if the content of the object cannot be changed without creating a new object. In other words, immutability creates an unbreakable bond between the id of an object and its content. If your program has maintained a reference to a particular object, it can be sure that the value of that object hasn't changed.

Immutability is an important concept. It can help reason about the correctness of a program. For instance, it is often a programmer's expectation that a numeric type be immutable. Consider the following code snippet:
```python
a = 2
b = 3
c = a + b
```

It would come as a big surprise to many, if after executing this sequence the content of the variable `a` were containing any value other than `2`.

Immutable types are typically easier to use and harder to misuse. Unfortunately, the use of immutable types can lead to the creation of many object instances.

Some of Python's built-in types are immutable, including `int`, `float`, `boolean`, `str`, and tuples. Lists are, however, mutable.

### Defensive Copies
Designing your own immutable type with a class whose initializer takes a reference to a mutable type as an argument can be delicate. If this is the case, you cannot simply keep a copy of the provided reference (the caller might also keep a copy of that reference). Instead your initializer must take a *defensive* copy of the corresponding object.
```python
class Vector:
    def __init__(self, arr):
        self._arr = arr[:]  # make copy of arr
```

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, Sections [3.2](https://introcs.cs.princeton.edu/python/32class/) and [3.3](https://introcs.cs.princeton.edu/python/33design/)

## Questions
1. :star: In another class, you have created `p`, an instance of class `Person`. You'd like to print `p._height`. What is the proper object-oriented way to get the value of this variable?
1. :star: Give an example of an immutable Python built-in type.
1. :star: Give an example of a mutable Python built-in type.
1. :star::star: If you want to set an instance variable of another object of the same class, do you have to use a setter?
1. :star::star: Suppose you have an object `airplane` that has an instance variable `_speed`. How can you increase `_speed` by 3.2 from another class? Because `_speed` is private, you shouldn't probably just say `airplane._speed += 3.2`.
1. :star::star: If you have a boolean instance variable `_onfire`, what is the associated getter called?
1. :star::star: Fix the following class definition to make `Complex` an immutable type:
    ```python
    class Complex:
        def __init__(self, real, imag):
            self.real = real
            self.imag = imag
        def __add__(self, other):
            self.real += other.real
            self.imag += other.imag
            return self
    ```
1. :star::star: Fix the following class definition to make `Vector` an immutable type:
    ```python
    class Vector:
        def __init__(self, arr):
            self._arr = arr
    ```

## Answers
1. `p.get_height()`.
1. `int`, `float`, `boolean`, `str`, or tuples.
1. Arrays.
1. No; it is acceptable for code in the same class to access non-public parts of any instance of the class directly. You might choose to use a setter if it does extra work, like enforcing constraints.
1. `airplane.set_speed(airplane.get_speed() + 3.2)`
1. `isonfire`. This convention is used for booleans so that expressions like `hair.isonfire()` will make grammatical sense in English.
1.
    ```python
    class Complex:
        def __init__(self, real, imag):
            self.real = real
            self.imag = imag
        def __add__(self, other):
            # don't reuse an existing object; create a new object instead
            return Complex(self.real + other.real, self.imag + other.imag)
    ```
1.
    ```python
    class Vector:
        def __init__(self, arr):
            self._arr = arr[:]  # make a defensive copy
    ```
