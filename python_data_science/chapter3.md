# Chapter 3: Control Flow and Functions

In this chapter, we'll learn how to control the flow of execution in your Python programs using conditional statements and loops. We'll also introduce functions, which are fundamental for organizing code into reusable blocks and making your programs modular and efficient.

## Conditional Statements: `if`, `elif`, `else`

Conditional statements allow your program to make decisions based on conditions. The most common conditional statement is the `if` statement, often used with `elif` (else if) and `else` to handle multiple conditions.

**`if` statement syntax:**

```python
if condition:
    # Code to execute if condition is True
```

**`if-else` statement syntax:**

```python
if condition:
    # Code to execute if condition is True
else:
    # Code to execute if condition is False
```

**`if-elif-else` statement syntax:**

```python
if condition1:
    # Code to execute if condition1 is True
elif condition2:
    # Code to execute if condition2 is True (and condition1 is False)
elif condition3:
    # ... more elif conditions as needed
else:
    # Code to execute if none of the above conditions are True
```

**Example: Determining the sign of a number**

```python
# Code cell
number = float(input("Enter a number: ")) # Get input from the user and convert to float

if number > 0:
    print("The number is positive.")
elif number == 0:
    print("The number is zero.")
else:
    print("The number is negative.")
```

**Nested `if` statements:** You can nest `if` statements inside other `if` or `else` blocks to create more complex decision structures.

```python
# Code cell
temperature = 25
humidity = 60

if temperature > 20:
    print("Temperature is warm.")
    if humidity > 50:
        print("It's also humid.")
    else:
        print("But humidity is comfortable.")
else:
    print("Temperature is cool.")
```

## Loops: `for` and `while` loops

Loops are used to repeat a block of code multiple times. Python provides two main types of loops: `for` and `while`.

### `for` loop: Iterating over sequences

The `for` loop is used to iterate over a sequence (like a list, tuple, string, or range) or other iterable objects.

**`for` loop syntax:**

```python
for item in sequence:
    # Code to execute for each item in the sequence
```

**Example 1: Iterating through a list**

```python
# Code cell
planets = ['Earth', 'Mars', 'Jupiter']

for planet in planets:
    print(planet) # Output: Earth, Mars, Jupiter (each on a new line)
```

**Example 2: Iterating through a string**

```python
# Code cell
message = "Hello"

for char in message:
    print(char) # Output: H, e, l, l, o (each on a new line)
```

**`range()` function:** The `range()` function is commonly used with `for` loops to generate a sequence of numbers.

*   `range(stop)`: Generates numbers from 0 up to (but not including) `stop`.
*   `range(start, stop)`: Generates numbers from `start` up to (but not including) `stop`.
*   `range(start, stop, step)`: Generates numbers from `start` up to (but not including) `stop`, incrementing by `step`.

```python
# Code cell
for i in range(5): # Generates numbers 0, 1, 2, 3, 4
    print(i) # Output: 0, 1, 2, 3, 4 (each on a new line)

for j in range(2, 8): # Generates numbers 2, 3, 4, 5, 6, 7
    print(j) # Output: 2, 3, 4, 5, 6, 7 (each on a new line)

for k in range(0, 10, 2): # Generates even numbers 0, 2, 4, 6, 8
    print(k) # Output: 0, 2, 4, 6, 8 (each on a new line)
```

**`for` loop with `else`:**  A `for` loop can have an optional `else` block that executes if the loop completes normally (i.e., not interrupted by a `break` statement).

```python
# Code cell
numbers = [1, 2, 3, 4, 5]
search_value = 7

for num in numbers:
    if num == search_value:
        print(f"Value {search_value} found in the list.")
        break # Exit the loop if value is found
else: # Executes if the loop completes without a 'break'
    print(f"Value {search_value} not found in the list.")
```

### `while` loop: Repeating while a condition is True

The `while` loop repeatedly executes a block of code as long as a given condition remains `True`.

**`while` loop syntax:**

```python
while condition:
    # Code to execute as long as condition is True
    # Make sure to update something in the loop that will eventually make the condition False,
    # otherwise you'll create an infinite loop!
```

**Example: Countdown timer**

```python
# Code cell
countdown = 5

while countdown > 0:
    print(countdown)
    countdown -= 1 # Decrement countdown in each iteration
else: # Optional else block, executes when the condition becomes False
    print("Blast off!")
```

**Infinite loops:** Be careful with `while` loops to ensure that the condition eventually becomes `False`. If the condition always remains `True`, you'll create an infinite loop, which will run indefinitely (you might need to manually stop the program).

```python
# Example of an infinite loop (avoid this!):
# while True:
#     print("This will print forever!")
```

**`while` loop with `else`:** Similar to `for` loops, `while` loops can also have an `else` block that executes when the loop condition becomes `False` and the loop terminates normally (not by a `break`).

## Loop Control Statements: `break` and `continue`

*   **`break`:**  Immediately terminates the loop and execution continues with the statement following the loop.
*   **`continue`:** Skips the rest of the current iteration and proceeds to the next iteration of the loop.

**Example: Using `break` and `continue`**

```python
# Code cell
numbers = [10, 20, 30, 40, 5, 60]

for num in numbers:
    if num == 5:
        continue # Skip processing for number 5
    print(f"Processing number: {num}")
    if num >= 40:
        break # Exit the loop when number is 40 or greater
```

## Functions: Reusable Blocks of Code

Functions are essential for organizing your code, making it reusable, and improving readability. A function is a block of code that performs a specific task. You can define a function once and then call it multiple times from different parts of your program.

**Defining Functions:**

Functions are defined using the `def` keyword, followed by the function name, parentheses `()`, and a colon `:`. The function body is indented.

**`function` definition syntax:**

```python
def function_name(parameters):
    # Function body - code to perform the task
    return result # Optional return statement
```

*   **`def` keyword:**  Indicates the start of a function definition.
*   **`function_name`:**  The name you give to your function (follow naming conventions, e.g., use descriptive names).
*   **`parameters` (optional):** Input values that the function can receive (also called arguments). They are listed inside parentheses and separated by commas. A function may have no parameters.
*   **Function body:**  The indented block of code that executes when the function is called.
*   **`return` statement (optional):**  Used to send a value back to the caller of the function. If there's no `return` statement, the function implicitly returns `None`.

**Calling Functions:**

To execute a function, you need to "call" it by using its name followed by parentheses `()`, and providing any required arguments.

```python
function_name(arguments)
```

**Example 1: A simple function to square a number**

```python
# Code cell
def square(x):
    """This function returns the square of a number.""" # Docstring - describes what the function does
    return x ** 2

result = square(5) # Call the function with argument 5
print(result)      # Output: 25
print(square(10))    # Output: 100
```

**Example 2: Function with multiple parameters**

```python
# Code cell
def calculate_area_rectangle(length, width):
    """Calculates the area of a rectangle."""
    area = length * width
    return area

rectangle_area = calculate_area_rectangle(4, 5) # Call with length=4, width=5
print(rectangle_area) # Output: 20
```

**Example 3: Function with no parameters and no return value (prints a message)**

```python
# Code cell
def greet():
    """Prints a greeting message."""
    print("Hello! Welcome to Python functions.")

greet() # Call the function - Output: Hello! Welcome to Python functions.
```

**Function Scope and Lifetime of Variables:**

*   **Scope:** The region of a program where a variable is accessible.
    *   **Local scope:** Variables defined inside a function have local scope. They are only accessible within that function.
    *   **Global scope:** Variables defined outside of any function have global scope. They are accessible throughout the program, including inside functions (but need to be declared global inside the function to be modified).

*   **Lifetime:** The period during which a variable exists in memory.
    *   Local variables exist only while the function is executing. Once the function finishes, local variables are destroyed.
    *   Global variables exist throughout the program's execution.

```python
# Code cell
global_variable = 100 # Global variable

def my_function():
    local_variable = 10 # Local variable
    print("Inside function:")
    print("Local variable:", local_variable)
    print("Global variable:", global_variable)

my_function()

# print(local_variable) # This would cause an error (NameError: name 'local_variable' is not defined) - local_variable is not accessible outside the function
print("Outside function:")
print("Global variable:", global_variable)
```

**`return` statement:** Functions can return values using the `return` statement. The `return` statement does two things:

1.  **Specifies the value to be returned:** The expression after `return` is evaluated, and its value is sent back to the caller.
2.  **Terminates the function:** When a `return` statement is executed, the function immediately ends, even if there are more lines of code after it.

If a function doesn't have a `return` statement, or if it has `return` without any expression, it implicitly returns `None`.

**Docstrings (Documentation Strings):**

It's good practice to include docstrings in your function definitions. A docstring is a string literal that occurs as the first statement in a function body. It's used to document what the function does, its parameters, and return value. Docstrings are enclosed in triple quotes `"""Docstring goes here"""`.

**Example with docstring:**

```python
# Code cell
def power(base, exponent):
    """
    Calculates the power of a number.

    Args:
        base: The base number.
        exponent: The exponent.

    Returns:
        The result of base raised to the power of exponent.
    """
    return base ** exponent
```

You can access docstrings using the `help()` function or by accessing the `__doc__` attribute of the function.

```python
help(power) # Displays the docstring
print(power.__doc__) # Prints the docstring
```

Functions are a cornerstone of programming. They promote code organization, reusability, and abstraction, making your programs easier to write, understand, and maintain.

**In this chapter, we've covered:**

*   **Conditional statements (`if`, `elif`, `else`):** Making decisions in your programs.
*   **Loops (`for`, `while`):** Repeating blocks of code.
*   **Loop control statements (`break`, `continue`):** Modifying loop behavior.
*   **Functions:** Defining and calling functions, parameters, return values, scope, and docstrings.

In the next chapter, we'll explore modules and packages, which allow you to extend Python's capabilities by importing external code and libraries.
