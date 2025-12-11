# Methods
## Calling Methods
In addition to data, an object can have *methods*: things you can ask it to do. For example, the expression `'hello'.upper()` is asking the string `'hello'`, "give me an upper-case version of yourself". It returns
`'HELLO'`.

Similarly, the expression `'hello'.index('e')` asks the same string, "at what position does the substring `'e'` appear within you?". The returned answer is `1`.

Calling a method is almost exactly like calling a regular function, but you have to call it *on* some particular object. Whereas a regular function call might look like `max(3, 2)`, a method call might look like `s.index('e')` (where `s` is some string). You are therefore *calling the `index` method on `s`*.

One key advantage of this approach is that different classes can have methods with the same name. For example, suppose `c` is an instance of the `Circle` class and `s` is an instance of the `Square` class. (These classes will be defined below.) Evaluating `c.area()` uses `Circle`'s `area` method, while `s.area()` uses `Square`'s. This ability for the same word to mean different things in different contexts is called *polymorphism*.

## Defining Methods
Methods are defined exactly like regular functions, but with two differences:
- methods are defined inside a class, and
- methods have an extra first argument `self`.

Here is a definition of `Circle`:
```python
import math

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * (self.radius ** 2)
```

Now if you define `c = Circle(1)`, then when the expression `c.area()` is evaluated, `self` refers to `c`. The method returns `3.141592653589793`.

Here is `Square`:
```python
class Square:
    def __init__(self, width):
        self.width = width

    def area(self):
        return self.width ** 2
```

## Resource
- Lubanovic, *Introducing Python, 3rd Edition*, Chapter 10

## Questions
1. :star: Assuming `Square` has been defined with an `area` method, why does the code below not run?
    ```python
    s = Square(2)
    print(area())
    ```
1. :star::star: Add a method `perimeter` to the `Square` class. It should take no arguments (other than `self`) and return the `Square`'s perimeter.
1. :star::star: Define a class `Student` with an initializer and instance variables for first name, last name, and id number. Add two methods, one to access a student's last name, and another to change that student's last name.
1. :star::star: Is `self` a reserved word?
1. :star::star::star: You could just define `area` directly as a regular function (below). What are the pros and cons of each approach?
   ```python
   def area(shape):
       if isinstance(shape, Circle):
           return math.pi * (shape.radius ** 2)
       elif isinstance(shape, Square):
           return shape.width ** 2
   ```

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
1.
    ```python
    class Student:
        def __init__(self, first_name, last_name, id):
            self.first_name = first_name
            self.last_name = last_name
            self.id = id

        def get_last_name(self):
            return self.last_name

        def set_last_name(self, new_name):
            self.last_name = new_name
    ```
   The collection of methods that access and alter a particular attribute are often referred to as *getters* and *setters*, respectively.
1. No, but it is the conventional name for this argument. Using is consistenly will make your code more legible to other Python users.
1. The difference is largely one of organization, which is no small concern for large software projects. The functional approach keeps all of the information about *areas* together, while the object-oriented approach keeps all of the information about *circles* together. The object-oriented approach can also be more efficient, because each object knows where to find its own methods; you don't have to go through a potentially long if/elif/else chain.
