# Introduction
This is a simple project for learning and practicing tests with python.

# Testing Your Code
There are many ways to test your code. In this demo, you’ll learn the techniques from the most basic steps and work towards advanced methods.

## Unit Tests vs. Integration Tests

You have just seen two types of tests:

- An integration test checks that components in your application operate with each other.
- A unit test checks a small component in your application.

You can write both integration tests and unit tests in Python.

To write a unit test for the built-in function sum(), you would check the output of sum() against a known output.

````python
def test_sum():
    assert sum([1, 2, 3]) == 6, "Should be 6"


if __name__ == "__main__":
    test_sum()
    print("Everything passed")
````

In Python, sum() accepts any iterable as its first argument.

We can test with a tuple as well:
````python
def test_sum():
    assert sum([1, 2, 3]) == 6, "Should be 6"

def test_sum_tuple():
    assert sum((1, 2, 2)) == 6, "Should be 6"

if __name__ == "__main__":
    test_sum()
    test_sum_tuple()
    print("Everything passed")
````

## Choosing a Test Runner

There are three most popular test runners are:

- unittest
- nose or nose2
- pytest

In this demo we will be using unittest.

unittest requires that:

- You put your tests into classes as methods
- You use a series of special assertion methods in the unittest.TestCase class instead of the built-in assert statement

To convert the earlier example to a unittest test case, you would have to:

- Import unittest from the standard library
- Create a class called TestSum that inherits from the TestCase class
- Convert the test functions into methods by adding self as the first argument
- Change the assertions to use the self.assertEqual() method on the TestCase class
- Change the command-line entry point to call unittest.main()

Follow those steps by creating a new file test_sum_unittest.py with the following code:

````python
import unittest


class TestSum(unittest.TestCase):

    def test_sum(self):
        self.assertEqual(sum([1, 2, 3]), 6, "Should be 6")

    def test_sum_tuple(self):
        self.assertEqual(sum((1, 2, 2)), 6, "Should be 6")


if __name__ == '__main__':
    unittest.main()
````

If you execute this at the command line, you’ll see one success (indicated with .) and one failure (indicated with F).

### nose

You may find that over time, as you write hundreds or even thousands of tests for your application,
it becomes increasingly hard to understand and use the output from unittest.

nose is compatible with any tests written using the unittest framework and can be used as a drop-in replacement for the
unittest test runner. The development of nose as an open-source application fell behind,
and a fork called nose2 was created. If you’re starting from scratch, it is recommended that you use nose2
instead of nose.

To get started with nose 2, run the following commands:

````shell
$ pip install nose2
$ python -m nose2
````

nose2 offers many command-line flags for filtering the tests that you execute.
For more information, you can explore [the Nose 2 documentation](https://docs.nose2.io/en/latest/).

## pytest

pytest supports execution of unittest test cases. The real advantage of pytest comes by writing pytest test cases. pytest test cases are a series of functions in a Python file starting with the name test_.

pytest has some other great features:

Support for the built-in assert statement instead of using special self.assert*() methods
Support for filtering for test cases
Ability to rerun from the last failing test
An ecosystem of hundreds of plugins to extend the functionality
Writing the TestSum test case example for pytest would look like this:

````python
def test_sum():
    assert sum([1, 2, 3]) == 6, "Should be 6"


def test_sum_tuple():
    assert sum((1, 2, 2)) == 6, "Should be 6"
````

You have dropped the TestCase, any use of classes, and the command-line entry point.

More information can be found at the [Pytest Documentation Website](https://docs.pytest.org/en/latest/).

# Writing Your First Test
