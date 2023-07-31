# Exception Handling in Python

Exception handling is a critical aspect of programming. It allows the handling of errors that might occur during the execution of a program, thus preventing the program from crashing unexpectedly.

Here's what you will learn in this session:

1. Understand Exception Handling
2. Use of exception handling
3. Basics of exception handling

## Understanding Exception Handling

When a program encounters an unexpected input or condition, it generates an exception—an event that disrupts the normal flow of the program's instructions. Exception handling allows the program to catch these exceptions and handle them gracefully instead of crashing. 

## Demonstration of Exception Handling

In Python, exceptions can be handled using `try`, `except`, `else`, and `finally` blocks.

```python
try:
    # code block where an exception can occur
    open_file = open("file.txt", "w")
    open_file.write("Hello, World!")
except IOError:
    # code block that will be executed if an IOError is raised
    print("Unable to open or read the data in the file.")
else:
    # code block that will be executed if no exception is raised
    print("The file was written successfully.")
finally:
    # code block that will be executed no matter what
    open_file.close()
    print("File is now closed.")
```

Here's how it works:

1. **`try` block**: This block contains the code that might raise an exception. The Python interpreter tries to execute this code.

2. **`except` block**: If an exception occurs in the `try` block, the program execution immediately moves to the `except` block that matches the exception. If no specific exception type is mentioned, it will catch any exception.

3. **`else` block**: If no exception is raised in the `try` block, the `else` block is executed. This is generally used for code that must be executed if the `try` block does not raise an exception.

4. **`finally` block**: This block is executed no matter what, and is generally used for cleanup actions (like closing files).

## Importance of Defining Specific Exceptions

It's generally a good practice to mention specific exceptions in the `except` block. Catching all exceptions without specifying any type is not recommended as it can hide bugs and make debugging harder.

## Summary

Through exception handling, you can control your program's response to unexpected events and prevent abrupt termination of the program. It improves the robustness and stability of the code.