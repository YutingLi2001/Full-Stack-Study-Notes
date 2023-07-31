# Python Style Guide and Coding Practices

## Learning Outcomes

- Understand the importance of writing readable code
- Learn Python coding conventions
- Comprehend static code analysis

## Importance of Readable Code

- Code readability ensures team members can easily understand and navigate through the codebase.
- Python.org provides PEP8, a document with conventions and guidelines to improve Python code readability and format.

## Key PEP8 Guidelines

- **Indentation**: Use four spaces instead of tabs for indentation to avoid non-uniformity in code.
    ```python
    if condition:    # <-- 4 spaces before statement
        statement_1  # <-- 4 spaces before statement
    ```

- **Blank Lines**: Use blank lines to separate functions and classes, which helps define the beginning and end of code blocks.
    ```python
    def function_1():
        pass

    class UserClass:
        pass
    ```

- **Spaces**: Use spaces around operators and after commas to improve command readability.
    ```python
    a = b + c  # Better than: a=b+c
    ```

## Python Coding Conventions

- **Functions**: Encapsulate large code blocks within functions for better manageability and reusability.
    ```python
    def function_1(a, b):
        pass

    c = function_1(a, b)  # Function can be easily reused
    ```

- **Naming Conventions**:
    - Functions and files: Use lowercase with underscores.
        ```python
        def comp_surface_radiation():
            pass
        ```
    - Packages: Avoid underscores.
        ```python
        import mypackage
        ```
    - Classes: Use CamelCase.
        ```python
        class LamSquirrelCage:
            pass
        ```
    - Constants: Use all capital letters with underscores separating words.
        ```python
        MAX_FILE_UPLOAD_SIZE = 5000
        ```

## Static Code Analysis

- A method to evaluate code against a predefined style and standard without executing the code.
- Helps find programming errors, coding standard violations, undefined values, syntax violations, and security vulnerabilities.
- PyLint library can check the compliance of Python code with PEP8 guidelines.

## Summary

- Consistent code helps team members read and understand the code easily.
- Key PEP8 guidelines include four spaces for indentation, use of blank lines to separate functions and classes, and spaces around operators and after commas.
- Coding conventions include adding large blocks of code inside functions, naming conventions for functions, files, packages, classes, and constants.
- Use static code analysis to evaluate code against predefined styles and standards.

# Unit Testing

## Learning Outcomes

- Define unit testing
- Explain the unit test process
- Build and execute unit tests
- Review the output of a unit test

## Unit Testing

- Unit testing is a method to validate if units of code are operating as designed.
- A unit is a smaller testable part of an application.
    ```python
    def square(number):
        return number ** 2

    def doubler(number):
        return number * 2
    ```
- The Python `unittest` library provides a framework containing test functionality.

## Unit Test Process

- During code development, you will test each unit.
- The test is performed in two phases: local system and server environment (CI/CD test server).
- Once the unit passes the server test, the unit is integrated into the final code base.

## Building Unit Tests

- A good naming convention: unittest file should have the word 'test' appended or prepended.
- Import the `unittest` library and the functions to test.
    ```python
    import unittest
    from mymodule import square, doubler
    ```
- Build the unit testing class to call the unit test from a single class object.
    ```python
    class TestMyModule(unittest.TestCase):
        pass
    ```
- Make the class inherit the test case class of the unit test library.
- Create functions in the unit testing class corresponding to each function that needs to be tested.
    ```python
    def test_square(self):
        pass

    def test_doubler(self):
        pass
    ```
- Only functions that start with 'test' are run.

## Test Cases

- Add one or more assertion methods to ensure that the unit test condition is met.
- The `assertEqual` function compares two values and determines if they are equal.
    ```python
    def test_square(self):
        self.assertEqual(square(2), 4)
    ```

## Unit Test Output

- After running the test file, an output is generated displaying the test results.
- If the output displays "OK", the test passed.
- If a function fails, the output clearly displays that the unit test failed and which function caused the error.
- Detailed output helps in correcting a mistake before the actual deployment of the solution.

## Summary

- Unit testing validates if units of code are operating as designed.
- During code development, each unit is tested first on the local system and then on a server environment.
- Test files should be differentiated from the module file by preappending or appending the word 'test'.
- Unit tests are built using various test functions like the `assertEqual` function.
- The output of a unit test helps to determine if the test passed or failed.


# Packaging

## Learning Outcomes

- Differentiate between Python module, package, and library
- Create a Python package
- Verify a Python package
- Use a Python package

## Python Module, Package, and Library

- A Python module is a .py file containing Python definitions, statements, functions, and classes. It can be imported to other scripts and notebooks.
    ```python
    def square(number):
        return number ** 2

    def doubler(number):
        return number * 2
    ```

- A package is a collection of Python modules bundled into a directory with an `__init__.py` file. The presence of the `__init__.py` file distinguishes it from a regular directory of Python scripts.
    - The example shows the package `myproject` in `parent_directory` with two modules, `module1.py` and `module2.py`. It also contains the `__init__.py` file.

- A library is a collection of packages or it can be a single package. Examples include numpy, pytorch, and Pandas.

## Creating a Python Package

- To create a Python package, follow these steps:

    1. Create a folder with the package name.

    2. Create an empty `__init__.py` file.

    3. Create the required modules.

    4. In the `__init__.py` file, add code to reference the modules needed in the package.
        ```python
        from . import module1
        from . import module2
        ```

## Verifying a Python Package

- To verify the package:

    1. Open a bash terminal.
    2. Make sure the directory is the same as the folder where your package is located.
    3. Open the python interpreter by running the command `python` in the shell.
    4. Using the Python prompt, type `import` followed by the project name, e.g., `import myproject`.
    5. If the command runs without errors, it is an indication that the package is successfully loaded.

## Using a Python Package

- After creating the package, you can use it in other scripts if the package folder is in the same directory.
    ```python
    from myproject.module1 import square, doubler
    from myproject.module2 import mean

    print("4^2 = ", square(4))
    print("2*4 = ", doubler(4))
    print("(2+1+3)/3 = ", mean([2, 1, 3]))
    ```

## Summary

- A Python module is a .py file containing Python definitions, statements, functions, and classes.
- A package is a collection of Python modules into a directory with a `__init__.py` file.
- A library is a collection of packages or it can be a single package.
- To create a package: create a folder with the package name, create an empty `__init__.py` file, create the required modules, and in the `__init__.py` file, add code to reference the modules needed in the package.
- You can verify the package via the bash terminal.
- After creating the package, you can use it in other scripts if the package folder is in the same directory.