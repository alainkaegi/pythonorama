# Methods
## Calling Methods
In addition to data, an object can have *methods*: things you can ask it to do. For example, `'hello'.upper()` is asking the string `'hello'`, "give me an upper-case version of yourself". It returns 
`'HELLO'`.

Similarly, `'hello'.index('e')` asks the same string, "at what position does the substring `'e'` appear within you?". The returned answer is `1`.

Calling a method is almost exactly like calling a regular function, but you have to call it *on* some particular object. Whereas a regular function call might look like `max(3, 2)`, a method call might look like `s.index('e')` (where `s` is some string). You are therefore *calling the `index` method on `s`*.

One key advantage of this approach is that different classes can have methods with the same name. For example, suppose `c` is an instance of the `Circle` class and `s` is an instance of the `Square` class. (These classes will be defined below.) Asking for `c.area()` uses `Circle`'s `area` method, while `s.area()` uses `Square`'s. This ability for the same word to mean different things in different contexts is called *polymorphism*.
## Defining Methods
Methods are defined exactly like regular functions, but with two differences:
- Methods are defined inside a class, and
- Methods have an extra first argument `self`.

Here is a definition of `Circle`:

```python
import math


class Circle:
    def __init__(self, radius):
        self.radius = radius
        
    def area(self):
        return math.pi * (self.radius ** 2)
```

Now if you define `c = Circle(1)`, then when `c.area()` is called, `self` refers to `c`. The method returns `3.141592653589793`.

Here is `Square`:

```python
class Square:
    def __init__(self, width):
        self.width = width

    def area(self):
        return self.width ** 2
```

## Resources
- Lubanovic, *Introducing Python, 3rd Edition*, Chapter 10

## Questions
1. :star: Assuming `Square` has been defined, why does the code below not run?
    ```python
    s = Square(2)
    print(area())
    ```
1. :star::star: Add a method `perimeter` to the `Square` class. It should take no arguments (other than `self`) and return the `Square`'s perimeter.
1. :star::star: Is `self` a reserved word?
## Answers
1. Since `area` is a method, it has to be called *on* some particular object. The last line should be `print(s.area())`.
1. Here is the complete class:
    ```python
    class Square:
        def __init__(self, width):
            self.width = width
    
        def area(self):
            return self.width ** 2
        
        def perimeter(self):
            return self.width * 4
    ```
1. No, but it is the conventional name for this argument. Using is consistenly will make your code more legible to other Python users.
