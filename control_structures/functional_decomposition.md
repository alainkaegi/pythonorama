# Functional Decomposition
## Overview
A long program can be greatly improved by breaking it down into multiple *functions*. This has many advantages:
- Redundant code (repeating the same statements in several places) is avoided, making the code shorter.
- The structure of the code is made clearer, making the code easier to read and write.
- Individual functions can be [tested](../software_development/testing.md), making the code easier to debug.
- Functions can often be reused to solve other problems.

A well-designed function should *do only one thing*: either return a value or have some side effect (modify a data structure in memory, draw something on the screen, etc.).

### Calling Functions
To call a function defined in the same module, use the syntax:
<pre>
<em>function</em>(<em>expr</em>, ...)
</pre>
where *function* is the name of the function and the *expr*s are values given to the function (called *arguments*). If the function returns value, its call is also an expression, so you can, for instance, store the resulting value in a variable:
```python
int c = foo(a, b + 1)
```
To call a function defined in another module that you have imported, use the syntax:
<pre>
<em>module</em>.<em>function</em>(<em>expr</em>, ...)
</pre>
where *module* is the name of the module where *function* is defined.

For example:
```python
math.log(10.0, 2)
```

### Defining Functions
You may define any number of functions within a module, using the syntax
<pre>
def <em>name</em>(<em>parameter</em>, ...):
    <em>statement</em>
    ...
</pre>
where *name* is the name of the function and *parameter*s are the name of its arguments.

A *parameter* is a local variable that holds the value of an argument when the function is called.

Here is a more concrete example:
```python
def square(n):
    return n*n
```
If we call the function as
```python
square(3)
```
then the parameter `n` holds the value 3.

### Return Statements
To return a value from a function, use the syntax:
<pre>
return <em>expr</em>
</pre>
where *expr* is an expression whose value will be returned to the caller.

Once a return statement is executed, the function exits. No other code in the function is run after that. Code that cannot be reached because it is located after a return statement is useless; it will never execute. Such unreachable code is not illegal but considered poor style.

### The Call Stack
When your program calls a function, the program's execution pauses at the calling point, the function executes until it returns, and then execution resumes where it left off in the program. Behind the scenes, a structure called a *call frame* keeps track of where you are in each function as well as any local variables.

Of course, a function called by your program may in turn call another function. The *call stack* contains one call frame for the currently running function and one for each of the paused functions. Every time you call a function, a new call frame is pushed onto the top of the stack. Every time a function returns, a call frame is popped off the top of the stack and the next function down resumes. When the bottom call frame is popped off, the program ends.

## Resource
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 2.1](https://introcs.cs.princeton.edu/python/21function/)

## Questions
1. :star: How do you call a function that doesn't take any arguments?
1. :star::star: Simplify the following function by using a separate function to reduce redundant code:
    ```python
    def difference_of_sums(a, b):
        sum_a = 0
        for v in a:
            sum_a += v
        }
        sum_b = 0
        for v in b:
            sum_b += v
        }
        return sum_a - sum_b
    }
    ```
1. :star::star: Can my function have a return statement without specifying a value?
1. :star::star: Is it legal to have a function return a value in some cases and none in others?
1. :star::star: Is it legal to have two functions with the same name in two different modules?
1. :star::star::star: What would happen if you defined two functions with the same name in the same module?
1. :star::star::star: Take a function that returns a value. Is it legal to call this function as a statement (and effectively to ignore the return value)?
1. :star::star::star: Take a function that does not return any value (e.g., `print`). Is it an error to call this function within an expression?

## Answers
1. Don't put anything between the parentheses:
    ```python
    quux()
    ```
1.  ```python
    def difference_of_sums(a, b):
        return sum(a) - sum(b)

    def sum(a):
        result = 0
        for v in a:
            result += v
        return result
    ```
1. Yes. Technically, such a statement returns the `None` object, which is an object indicating no value and which is the sole member of the type `NoneType`.
1. Yes, but it is considered poor style as the caller would need to know when to expect a value and when not.
1. Yes. It occurs frequently.
1. The second definition would overwrite the first one.
1. Yes. For instance, in a timing experiment, you may be only interested in how long a function takes to execute.
1. No. In Python all functions return a value. A function that does not explicitly return a value is treated as a function that returns a value of type `NoneType`. If such a function is called within an expression context, it will be considered to have returned the value `None`.
