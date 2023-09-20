# Classes and Initializers
## Objects and Classes
Every value in Python is an *object*. For example, the int `5`, the list `[1, 2, 3]`, and the string `'hello'` are all objects.

Every object is an *instance* of some *class* (also known as a *type*). The `type` function lets you see the type of an object. For example, `type(3)` returns `<class 'int'>`.

You can also define your own classes. Here is a first draft of the Pet class:

```python
class Pet:
    pass
```

By convention, class names start with upper-case letters. If a class name involves multiple words, use PascalCase. The keyword `pass` just indicates that, for the moment, the body of the class definition is empty.

You can now create an instance of `Pet`:

```python
p = Pet()
```

Your object doesn't do anything yet, but you can at least ask what type it is. `type(p)` returns `<class '__main__.Pet'>`. (You can ignore the `__main__.` part for now.)

## Attributes
You can add values called *attributes* to an object. Attributes associated with an object are also called *instance variables*. Continuing the previous example:

```python
p.name = 'Violet'
p.species = 'dog'
```

Now you can use `p.name` or `p.species` anywhere you want to know about these values, but you can use `p` to refer to the entire Pet. This ability to refer to a whole collection of named values (and, for example, pass it into or return it from a function) is a key feature of objects.

Each instance of the pet class can have its own values for these instance variables. If you define

```python
q = Pet()
q.name = 'Vinnie'
q.species = 'snake'
```

then `p.species` is `'dog'` but `q.species` is `'snake'`.

## Initializers
Rather than attaching the instance variables after the fact, it would be nicer to be able to specify them when you create the object:

```python
p = Pet('Violet', 'dog')
```

You can do this by defining an *initializer* inside the class. Here's the improved version:

```python
class Pet:
    def __init__(self, name, species):
        self.name = name
        self.species = species
```

There are several things to note here:

`__init__` (which must have exactly that name, with the double underscores before and after) is a sort of function defined inside the `Pet` class.

`__init__` takes three parameters: `self` (which refers to the object being initialized), `name`, and `species`

Inside the initializer, `name` refers to the value that was passed into the initializer, but `self.name` refers to an instance variable of the current object. The line `self.name = name` therefore takes the value that was passed in and stores it in the instance variable. This is important because, as with any functions, as soon as `__init__` ends, the parameter `name` goes away, but `self.name` remains associated with the object.

Here's what happens behind the scenes when you evaluate `p = Pet('Violet', 'dog')`:

1. Python creates a new instance of Pet. Let's call it `temp`.
2. Python calls `__init__(temp, 'Violet', 'dog')`.
3. Inside the initializer, `self` is `temp`, `name` is `'Violet'`, and `species` is `'dog'`. The body of the initializer is run, setting the instance variables.
4. The initializer returns the object `temp`.
5. Now that the function call is complete, the name `p` is made to refer to the returned object.

## Resources
* Lubanovic, *Introducing Python, 3rd Edition*, Chapter 10

## Questions
1. :star: Define a class `Student` with an initializer and instance variables for first name, last name, and id number.
1. :star: If you define a class `Tree`, can you make a list of Trees?
1. :star::star: Explain why the program below does not print `5`.
    ```python
    class Box:
        def __init__(self):
            x = 5
    
    print(Box().x)
    ```
1. :star::star: If you define the class
    ```python
    class Point:
        def __init__(self, x, y):
            self.x = x
            self.y = y
    ```
    what is printed by the code below?
    ```python
    p = Point(3, 4)
    print(p.x)
    ```
1. :star::star: This seems like a lot of work. Couldn't you just use a list (or a tuple) like `p = [3, 4]` instead of defining the class and then doing `p = Point(3, 4)`?
1. :star::star: Couldn't you just use a dictionary like `p = {'x':3, 'y':4}` instead?
1. :star::star::star: Given the definition of the `Point` class above, what happens if you ask for `Point.x`?
1. :star::star::star: What keyword used in Java, C++, and C# is analogous to Python's `self`?
1. :star::star::star: If `int` is a class, why doesn't its name start with an upper-case letter?
## Answers
1.
    ```python
    class Student:
        def __init__(self, first_name, last_name, id):
            self.first_name = first_name
            self.last_name = last_name
            self.id = id
    ```
1. Yes. You might say something like `forest = [Tree('oak'), Tree('spruce'), Tree('pine')]`.
1. The initializer does not set an instance variable. It merely creates a local variable `x` which goes away when the initalizer ends. The line should be `self.x = 5`.
1. 3, which is the value of `p`'s instance variable `x`.
1. You could, and in some cases it would be reasonable. One major difference is that the elements of a list can only be accessed by their numeric indices, so you'd have to ask for `p[0]` and `p[1]` instead of `p.x` and `p.y`. Another is the ability of classes to define methods.
1. You could, although `p = Point(3, 4)` is slightly shorter and clearer. Defining a class is also more efficient at runtime, allows you to see the type of an object, and allows you define methods.
1. You get `AttributeError: type object 'Point' has no attribute 'x'`. This is because `Point.x` is asking for the `x` attribute of the *class* rather than a specific *instance*. Otherwise, since there may be many Points, Python doesn't know which one to look in for an `x` value.
1. `this`. Note that `self` is not actually a reserved keyword in Python, just the conventional name for this parameter.
1. For historical reasons, a few core built-in types like int, list, and dict have lower-case names. Class names in libraries and your own code should be PascalCase.
