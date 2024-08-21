# Testing
## Types of Testing
Testing is how we know whether our software is working correctly, that is, doing what it's supposed to do. There are several kinds of testing:
- *System testing* runs the entire program. This is probably what you did in your first programming class. For large programs, system testing is necessary but not sufficient. A system test is likely to leave some parts of the program insufficiently tested. Even if a bug is discovered, it will be very difficult to tell where in the code the defect lies.
- *Unit testing* tests individual parts of the program (e.g., methods). Unit testing has two big advantages over system testing. First, it can happen a lot earlier, before the entire system has been built. This is important because it gives you a chance to fix one bug before introducing the next one. Second, if a bug is found, unit testing gives a strong indication of where it is.
- *Regression testing* re-tests the system (or units thereof) after making a change to the program, to ensure that nothing broke.

## `pytest`
Manual testing is fine for very small, simple programs but it quickly becomes tedious and error-prone for larger ones. When you hear "tedious and error-prone", you should think, "Can I automate this?" `pytest` is a tool for automating unit tests in Python. (Other languages have similar frameworks.)

A `pytest` test suite is a module containing test functions. In its simplest form, `pytest` finds these test functions through a set of naming convention. The function names must begin with the prefix `test_` and be contained in files whose basename (i.e., the part of the filename that appears before the file's extension) must end with the suffix `_test`. A test generally sets up some data structures and then makes an assertion about the result of some function call. But it can be as simple as:
```python
def test_sum_of_first_4_numbers():
    assert sum_of_first_n_numbers(4) == 10
```

where `sum_of_first_n_numbers` is the function being tested. In this case, `10` is the expected value and `sum_of_first_n_numbers(4)` is the computation that is supposed to return that result.

Once [installed](../development_tools/pytest.md), `pytest` allows you to run all of the tests in a module (or even in a directory) at the click of a button or by running a simple command.

## Test-Driven Development
It seems natural to most students to first write code and then test it. The surprising technique of *test-driven development* turns this upside-down, writing the test *before* the code in question. This has several advantages:
- It forces us to actually write tests rather than put off doing so forever.
- It forces us to think precisely about what a method is supposed to do.
- When writing the code, repeatedly running the test will let us know when we've succeeded.
- After a test has passed, it provides a regression test that will let us know if we later break something.

The process for test-driven development is:
1. Write a test for some new feature to be added or bug to be corrected.
1. Fail the test. If the test passes before you've written the main code or fixed the bug, there's probably something wrong with the test.
1. Write the code to be tested.
1. Pass the test. (If the test doesn't pass, go back and edit the code.)

## Resources
- [pytest](https://pytest.org/)
- Christensen, *Flexible, Reliable Software Using Patterns and Agile Development*, chapters 2, 5, 8, 12, and 34
- Martin, *Clean Code*, chapter 9
- Masella, [Automated Testing of Gameplay Features in 'Sea of Thieves'](https://www.youtube.com/watch?v=X673tOi8pU8)

## Questions
1. :star: Describe at least one advantage of test-driven development.
1. :star: What is the naming convention of test functions in a `pytest` test module?
1. :star: If you pass all of your unit tests, does that mean your program is correct?
1. :star: What claim does the following assertion make?
    ```python
    assert amp.volume() == 11
    ```
1. :star::star: If a test doesn't pass, how do you know the problem isn't in the test itself?
1. :star::star: How do you test a user interface that involves detecting mouse clicks and graphics?

## Answers
1. It forces you to actually write tests rather than put off doing so forever. It forces you to think precisely about what a method is supposed to do. It allows you to detect bugs sooner. When writing the code, repeatedly running the test lets you know when you've succeeded. After a test has passed, it provides a regression test that will let you know if we later break something.
1. The name of each of the test function must begin with the prefix `test_`.
1. No. Passing all of the tests is *necessary* but not *sufficient*. Certainly a program that *doesn't* pass the tests has a problem.
1. If the `volume` method is called on the object `amp`, it will return 11.
1. You can't be absolutely sure. Since the test is usually much simpler than the code being tested, any test failure is *probably* due to the code being tested, but sometimes there are bugs in the test. Testing mostly just gives us more confidence when tests *do* pass. This is similar to the reasoning behind doing a math problem two different ways or [double-entry bookkeeping](https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system).
1. In general, you don't. This is why it's important to separate back-end logic from user-interface code: the former can be easily tested, the latter cannot.
