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

Create a new project folder and, inside that, create a new folder called my_sum. Inside my_sum,
create an empty file called __init__.py. Creating the __init__.py file means that the my_sum folder can be imported
as a module from the parent directory.

Open up my_sum/__init__.py and create a new function called my_sum(), which takes an iterable (a list, tuple, or set)
and adds the values together:

````python
def my_sum(arg):
    total = 0
    for val in arg:
        total += val
    return total
````

## Where to Write the Test
To get started writing tests, you can simply create a file called test.py, which will contain your first test case.
Because the file will need to be able to import your application to be able to test it, you want to place test.py above
the package folder, so your directory tree will look something like this:

````yaml
project/
│
├── my_sum/
│   └── __init__.py
|
└── test.py
````

You’ll find that, as you add more and more tests, your single file will become cluttered and hard to maintain,
so you can create a folder called tests/ and split the tests into multiple files. It is convention to ensure each file
starts with test_ so all test runners will assume that Python file contains tests to be executed.

## How to Structure a Simple Test

Before you dive into writing tests, you’ll want to first make a couple of decisions:

- What do you want to test?
- Are you writing a unit test or an integration test?

Then the structure of a test should loosely follow this workflow:

- Create your inputs
- Execute the code being tested, capturing the output
- Compare the output with an expected result

For this application, you’re testing sum(). There are many behaviors in sum() you could check, such as:

- Can it sum a list of whole numbers (integers)?
- Can it sum a tuple or set?
- Can it sum a list of floats?
- What happens when you provide it with a bad value, such as a single integer or a string?
- What happens when one of the values is negative?

The most simple test would be a list of integers. Create a file, test.py with the following Python code:

````python
import unittest

from my_sum import my_sum


class TestSum(unittest.TestCase):
    def test_list_int(self):
        """
        Test that it can sum a list of integers
        """
        data = [1, 2, 3]
        result = my_sum(data)
        self.assertEqual(result, 6)


if __name__ == '__main__':
    unittest.main()
````

## How to Write Assertions

unittest comes with lots of methods to assert on the values, types, and existence of variables.
Here are some of the most commonly used methods:

| Method                  | Equivalent to     |
|-------------------------|-------------------|
| .assertEqual(a, b)      | 	a == b           |
| .assertTrue(x)          | 	bool(x) is True  |
| .assertFalse(x)	        | bool(x) is False  |
| .assertIs(a, b)         | 	a is b           |
| .assertIsNone(x)        | x is None         |
| .assertIn(a, b)         | 	a in b           |
| .assertIsInstance(a, b) | 	isinstance(a, b) |

.assertIs(), .assertIsNone(), .assertIn(), and .assertIsInstance() all have opposite methods, named .assertIsNot(),
and so forth.

# Executing Your First Test
## Executing Test Runners

To execute the test:

- You can run in the terminal:
````shell
$ python test.py
````
- You can use the unittest command line:
````shell
$ python -m unittest test
````

You can provide additional options to change the output.
One of those is -v for verbose:
````shell
$ python -m unittest -v test
````

Instead of providing the name of a module containing tests, you can request an auto-discovery which looks
for all the tests using unittest:
````shell
$ python -m unittest discover
````

Once you have multiple test files, as long as you follow the test*.py naming pattern, you can provide the name of
the directory instead by using the -s flag and the name of the directory:
````shell
$ python -m unittest discover -s tests
````
 if your source code is not in the directory root and contained in a subdirectory, for example in a folder called src/,
 you can tell unittest where to execute the tests so that it can import the modules correctly with the -t flag:
 ````shell
$ python -m unittest discover -s tests -t src
````
unittest will change to the src/ directory, scan for all test*.py files inside the the tests directory,
and execute them.

## Understanding Test Output

Now we are going to try a falling test.
Add test_list_fraction function to your test.py file:

````python
import unittest

from my_sum import my_sum
from fractions import Fraction


class TestSum(unittest.TestCase):
    def test_list_int(self):
        """
        Test that it can sum a list of integers
        """
        data = [1, 2, 3]
        result = my_sum(data)
        self.assertEqual(result, 6)

    def test_list_fraction(self):
        """
        Test that it can sum a list of fractions
        """
        data = [Fraction(1, 4), Fraction(1, 4), Fraction(2, 5)]
        result = my_sum(data)
        self.assertEqual(result, 1)

if __name__ == '__main__':
    unittest.main()
````

In the output, you’ll see the following information:

- The first line shows the execution results of all the tests, one failed (F) and one passed (.).

- The FAIL entry shows some details about the failed test:

  - The test method name (test_list_fraction)
  - The test module (test) and the test case (TestSum)
  - A traceback to the failing line
  - The details of the assertion with the expected result (1) and the actual result (Fraction(9, 10))
  - Remember, you can add extra information to the test output by adding the -v flag to the python -m unittest command.

# Testing Flask App

Flask requires that the app be imported and then set in test mode.
You can instantiate a test client and use the test client to make requests to any routes in your application.

All the test client instantiation is done in the setUp method of your test case. In the following example,
my_app is the name of the application.

````python
import my_app
import unittest


class MyTestCase(unittest.TestCase):

    def setUp(self):
        my_app.app.testing = True
        self.app = my_app.app.test_client()

    def test_home(self):
        result = self.app.get('/')
        # Make your assertions
````
More information is available at the [Flask Documentation Website](https://flask.palletsprojects.com/en/0.12.x/testing/).

# Advanced Testing Scenarios

## Handling Expected Failures

What happens when you provide the my_sum function we tested earlier with a bad value,
such as a single integer or a string?

In this case, you would expect sum() to throw an error. When it does throw an error, that would cause the test to fail.

There’s a special way to handle expected errors. You can use .assertRaises() as a context-manager, then inside
the with block execute the test steps:

````python
import unittest

from my_sum import my_sum
from fractions import Fraction


class TestSum(unittest.TestCase):
    def test_list_int(self):
        """
        Test that it can sum a list of integers
        """
        data = [1, 2, 3]
        result = my_sum(data)
        self.assertEqual(result, 6)

    def test_list_fraction(self):
        """
        Test that it can sum a list of fractions
        """
        data = [Fraction(1, 4), Fraction(1, 4), Fraction(2, 5)]
        result = my_sum(data)
        self.assertEqual(result, 1)

    def test_bad_type(self):
        data = "banana"
        with self.assertRaises(TypeError):
            result = my_sum(data)


if __name__ == '__main__':
    unittest.main()
````
This test case will now only pass if sum(data) raises a TypeError. You can replace TypeError with any exception type
you choose.