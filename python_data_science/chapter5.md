# Chapter 5: Introduction to NumPy

Welcome to the world of numerical computing with NumPy! NumPy (Numerical Python) is a cornerstone library in Python for data science, scientific computing, and engineering. It provides powerful tools for working with arrays, performing mathematical operations, linear algebra, random number generation, and much more. If you're familiar with MATLAB or similar numerical computing environments, you'll find NumPy conceptually similar but with Python's ease of use and extensive ecosystem.

## NumPy Arrays: Creating, Indexing, Slicing

The fundamental data structure in NumPy is the **NumPy array** (ndarray). NumPy arrays are homogeneous, meaning they store elements of the same data type (e.g., all integers, all floats). This homogeneity allows for efficient storage and computation. NumPy arrays are also multi-dimensional, allowing you to represent vectors, matrices, and higher-dimensional tensors.

### Creating NumPy Arrays

There are several ways to create NumPy arrays:

**1. From Python lists or tuples:**

You can convert Python lists or tuples into NumPy arrays using `np.array()`.

```python
# Code cell
import numpy as np

# From a Python list
python_list = [1, 2, 3, 4, 5]
numpy_array_from_list = np.array(python_list)
print(numpy_array_from_list) # Output: [1 2 3 4 5]
print(type(numpy_array_from_list)) # Output: <class 'numpy.ndarray'>

# From a tuple
python_tuple = (10, 20, 30)
numpy_array_from_tuple = np.array(python_tuple)
print(numpy_array_from_tuple) # Output: [10 20 30]

# Creating a 2D array (matrix) from a list of lists
list_of_lists = [[1, 2, 3], [4, 5, 6]]
matrix = np.array(list_of_lists)
print(matrix)
# Output:
# [[1 2 3]
#  [4 5 6]]
```

**2. Using NumPy's array creation functions:**

NumPy provides functions to create arrays with specific initial values or patterns:

*   `np.zeros(shape)`: Creates an array filled with zeros.
*   `np.ones(shape)`: Creates an array filled with ones.
*   `np.full(shape, fill_value)`: Creates an array filled with a specified value.
*   `np.eye(N)`: Creates an N x N identity matrix (ones on the diagonal, zeros elsewhere).
*   `np.arange(start, stop, step)`: Creates a 1D array with a range of values (similar to Python's `range()`).
*   `np.linspace(start, stop, num_samples)`: Creates a 1D array with evenly spaced values over a specified range.
*   `np.random.rand(shape)`: Creates an array with random values between 0 and 1 (uniform distribution).
*   `np.random.randn(shape)`: Creates an array with random values from a standard normal distribution (mean 0, std dev 1).
*   `np.random.randint(low, high, size)`: Creates an array with random integers within a specified range.

**Examples of array creation functions:**

```python
# Code cell
import numpy as np

zeros_array = np.zeros((3, 4)) # Create a 3x4 array of zeros
print("Zeros array:\n", zeros_array)

ones_array = np.ones((2, 2)) # Create a 2x2 array of ones
print("\nOnes array:\n", ones_array)

full_array = np.full((5,), 7) # Create a 1D array of length 5 filled with 7s
print("\nFull array:\n", full_array)

identity_matrix = np.eye(3) # 3x3 identity matrix
print("\nIdentity matrix:\n", identity_matrix)

arange_array = np.arange(0, 20, 2) # Array from 0 to <20, step 2
print("\nArange array:\n", arange_array)

linspace_array = np.linspace(0, 1, 5) # 5 evenly spaced values from 0 to 1
print("\nLinspace array:\n", linspace_array)

random_uniform_array = np.random.rand(2, 3) # 2x3 array of uniform random numbers (0-1)
print("\nRandom uniform array:\n", random_uniform_array)

random_normal_array = np.random.randn(4) # 1D array of 4 random numbers from normal distribution
print("\nRandom normal array:\n", random_normal_array)

random_int_array = np.random.randint(1, 10, (2, 2)) # 2x2 array of random integers from 1 to <10
print("\nRandom integer array:\n", random_int_array)
```

### Array Attributes: `shape`, `dtype`, `ndim`, `size`

NumPy arrays have useful attributes that describe their properties:

*   `shape`: A tuple representing the dimensions of the array (e.g., `(rows, columns)` for a 2D array).
*   `dtype`: The data type of the elements in the array (e.g., `int64`, `float64`, `bool`).
*   `ndim`: The number of dimensions (axes) of the array (e.g., 1 for a vector, 2 for a matrix).
*   `size`: The total number of elements in the array.

```python
# Code cell
import numpy as np

matrix = np.array([[1, 2, 3], [4, 5, 6]])

print("Shape:", matrix.shape) # Output: (2, 3) - 2 rows, 3 columns
print("Data type:", matrix.dtype) # Output: int64 (or int32, depending on system)
print("Number of dimensions:", matrix.ndim) # Output: 2
print("Size:", matrix.size) # Output: 6 (2*3 = 6 elements)
```

### Indexing and Slicing NumPy Arrays

Indexing and slicing in NumPy arrays are similar to Python lists, but with more powerful and flexible options, especially for multi-dimensional arrays.

**1. Basic Indexing:** Accessing individual elements using their indices. For multi-dimensional arrays, you use a tuple of indices.

```python
# Code cell
import numpy as np

array_1d = np.array([10, 20, 30, 40, 50])
print(array_1d[0])    # Output: 10 (first element)
print(array_1d[-1])   # Output: 50 (last element)

matrix_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(matrix_2d[0, 1]) # Output: 2 (element at row 0, column 1)
print(matrix_2d[2, 2]) # Output: 9 (element at row 2, column 2)
```

**2. Slicing:** Extracting subarrays (views) using slices. Similar to list slicing, but can be done along multiple dimensions.

```python
# Code cell
import numpy as np

array_1d = np.arange(10) # [0 1 2 3 4 5 6 7 8 9]
print(array_1d[2:7])    # Output: [2 3 4 5 6] (elements from index 2 up to < 7)
print(array_1d[:5])     # Output: [0 1 2 3 4] (elements from start up to < 5)
print(array_1d[5:])     # Output: [5 6 7 8 9] (elements from index 5 to end)
print(array_1d[::2])    # Output: [0 2 4 6 8] (every other element)

matrix_2d = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
print("\nOriginal matrix:\n", matrix_2d)
# Output:
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]

print("\nSlice of rows 0 and 1, all columns:\n", matrix_2d[0:2, :])
# Output:
# [[1 2 3 4]
#  [5 6 7 8]]

print("\nSlice of all rows, columns 1 to 3:\n", matrix_2d[:, 1:4])
# Output:
# [[ 2  3  4]
#  [ 6  7  8]
#  [10 11 12]]

print("\nSpecific element matrix_2d[1, 2]:\n", matrix_2d[1, 2])
# Output: 7
```

**3. Boolean Indexing (Conditional Indexing):** Selecting elements based on a boolean condition.

```python
# Code cell
import numpy as np

array_1d = np.array([1, 2, 3, 4, 5, 6])
bool_index = array_1d > 3 # Create a boolean array based on condition
print("Boolean index array:\n", bool_index) # Output: [False False False  True  True  True]

filtered_array = array_1d[bool_index] # Select elements where bool_index is True
print("\nFiltered array (elements > 3):\n", filtered_array) # Output: [4 5 6]

# Combining conditions with logical operators (&, |):
condition = (array_1d > 2) & (array_1d < 6) # Elements > 2 AND < 6
print("\nCombined condition:\n", condition) # Output: [False False  True  True  True False]
filtered_array_combined = array_1d[condition]
print("\nFiltered array (2 < elements < 6):\n", filtered_array_combined) # Output: [3 4 5]
```

**4. Integer Array Indexing (Fancy Indexing):** Selecting elements using arrays of indices.

```python
# Code cell
import numpy as np

array_1d = np.array([10, 20, 30, 40, 50, 60])
indices = [0, 2, 4] # Indices to select
fancy_indexed_array = array_1d[indices] # Select elements at specified indices
print("Fancy indexed array:\n", fancy_indexed_array) # Output: [10 30 50]

matrix_2d = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
row_indices = [0, 2]
col_indices = [1, 3]
fancy_indexed_matrix = matrix_2d[row_indices, col_indices] # Select elements at (0, 1) and (2, 3)
print("\nFancy indexed matrix:\n", fancy_indexed_matrix) # Output: [ 2 12]
```

## Array Operations: Element-wise Operations, Broadcasting

NumPy enables efficient element-wise operations on arrays, meaning operations are performed on corresponding elements of arrays. It also supports broadcasting, which allows operations on arrays with different shapes under certain conditions.

### 1. Element-wise Arithmetic Operations

You can perform arithmetic operations (+, -, \*, /, \*\*, %, //) directly on NumPy arrays. These operations are applied element-wise.

```python
# Code cell
import numpy as np

array1 = np.array([1, 2, 3])
array2 = np.array([4, 5, 6])

print("Array 1:", array1) # Output: [1 2 3]
print("Array 2:", array2) # Output: [4 5 6]

print("\nElement-wise addition:", array1 + array2) # Output: [5 7 9]
print("Element-wise subtraction:", array2 - array1) # Output: [3 3 3]
print("Element-wise multiplication:", array1 * array2) # Output: [ 4 10 18]
print("Element-wise division:", array2 / array1) # Output: [4.  2.5 2. ]
print("Element-wise exponentiation:", array1 ** 2) # Output: [1 4 9]
```

### 2. Broadcasting

Broadcasting is a powerful feature in NumPy that allows you to perform operations on arrays with different shapes, making them compatible by automatically "broadcasting" the smaller array to match the shape of the larger array. Broadcasting is subject to certain rules, but in many common cases, it works intuitively.

**Broadcasting rules (simplified):**

*   NumPy compares array dimensions from right to left (trailing dimensions).
*   Two dimensions are compatible if:
    *   They are equal, or
    *   One of them is 1.
*   If these rules are not met, NumPy will raise a `ValueError` indicating incompatible shapes.

**Examples of Broadcasting:**

**Example 1: Scalar broadcasting**

```python
# Code cell
import numpy as np

array_1d = np.array([1, 2, 3])
scalar = 10

print("Array:", array_1d) # Output: [1 2 3]
print("Scalar:", scalar) # Output: 10

print("\nArray + scalar (broadcasting scalar to array shape):", array_1d + scalar) # Output: [11 12 13] (scalar 10 is broadcasted to [10, 10, 10])
print("Array * scalar:", array_1d * scalar) # Output: [10 20 30]
```

**Example 2: Broadcasting along one dimension**

```python
# Code cell
import numpy as np

matrix_2d = np.array([[1, 2, 3], [4, 5, 6]]) # 2x3 matrix
array_1d_row = np.array([10, 20, 30]) # 1x3 array (or simply 1D array of length 3)
array_1d_col = np.array([[100], [200]]) # 2x1 array (column vector)

print("Matrix:\n", matrix_2d)
# Output:
# [[1 2 3]
#  [4 5 6]]
print("\nRow array:", array_1d_row) # Output: [10 20 30]
print("Column array:\n", array_1d_col)
# Output:
# [[100]
#  [200]]

print("\nMatrix + row array (broadcasting row-wise):\n", matrix_2d + array_1d_row)
# Output:
# [[11 22 33]
#  [14 25 36]]
# array_1d_row is broadcasted to [[10, 20, 30], [10, 20, 30]] to match matrix_2d shape

print("\nMatrix + column array (broadcasting column-wise):\n", matrix_2d + array_1d_col)
# Output:
# [[101 102 103]
#  [204 205 206]]
# array_1d_col is broadcasted to [[100, 100, 100], [200, 200, 200]] to match matrix_2d shape
```

### 3. Universal Functions (UFuncs)

NumPy provides a large set of universal functions (ufuncs) that perform element-wise operations efficiently. UFuncs cover a wide range of operations, including:

*   **Math functions:** `np.sin()`, `np.cos()`, `np.exp()`, `np.log()`, `np.sqrt()`, etc.
*   **Comparison functions:** `np.greater()`, `np.less()`, `np.equal()`, etc.
*   **Logical functions:** `np.logical_and()`, `np.logical_or()`, `np.logical_not()`, etc.
*   **Bit-wise functions:** `np.bitwise_and()`, `np.bitwise_or()`, etc.

UFuncs are highly optimized and often implemented in compiled code, making them much faster than writing equivalent operations using loops in Python.

**Examples of UFuncs:**

```python
# Code cell
import numpy as np

angles = np.array([0, np.pi/6, np.pi/3, np.pi/2]) # Angles in radians

sin_values = np.sin(angles) # Element-wise sine
print("Sine values:", sin_values) # Output: [0.         0.5        0.8660254  1.        ]

exp_array = np.array([0, 1, 2, 3])
exp_values = np.exp(exp_array) # Element-wise exponential
print("\nExponential values:", exp_values) # Output: [ 1.          2.71828183  7.3890561  20.08553692]

array1 = np.array([1, 5, 3, 8])
array2 = np.array([2, 4, 3, 9])
greater_than = np.greater(array1, array2) # Element-wise comparison (array1 > array2)
print("\nGreater than:", greater_than) # Output: [False  True False False]
```

## Linear Algebra with NumPy

NumPy provides a `linalg` (linear algebra) module that offers functions for linear algebra operations, essential in many physics and data science applications.

**Common linear algebra operations:**

*   **Matrix multiplication:** `np.dot()` or `@` operator.
*   **Transpose:** `array.T` attribute or `np.transpose()` function.
*   **Determinant:** `np.linalg.det()`.
*   **Inverse:** `np.linalg.inv()`.
*   **Eigenvalues and eigenvectors:** `np.linalg.eig()`.
*   **Singular Value Decomposition (SVD):** `np.linalg.svd()`.
*   **Solving linear systems:** `np.linalg.solve()`.

**Examples of linear algebra operations:**

```python
# Code cell
import numpy as np

matrix_a = np.array([[1, 2], [3, 4]])
matrix_b = np.array([[5, 6], [7, 8]])
vector_v = np.array([2, 3])

print("Matrix A:\n", matrix_a)
# Output:
# [[1 2]
#  [3 4]]
print("\nMatrix B:\n", matrix_b)
# Output:
# [[5 6]
#  [7 8]]
print("\nVector v:", vector_v) # Output: [2 3]

# Matrix multiplication
matrix_product = np.dot(matrix_a, matrix_b) # or matrix_a @ matrix_b
print("\nMatrix product (A * B):\n", matrix_product)
# Output:
# [[19 22]
#  [43 50]]

# Matrix-vector multiplication
matrix_vector_product = np.dot(matrix_a, vector_v) # or matrix_a @ vector_v
print("\nMatrix-vector product (A * v):\n", matrix_vector_product) # Output: [ 8 18]

# Transpose
matrix_a_transpose = matrix_a.T # or np.transpose(matrix_a)
print("\nTranspose of A:\n", matrix_a_transpose)
# Output:
# [[1 3]
#  [2 4]]

# Determinant
determinant_a = np.linalg.det(matrix_a)
print("\nDeterminant of A:", determinant_a) # Output: -2.0

# Inverse
try:
    inverse_a = np.linalg.inv(matrix_a)
    print("\nInverse of A:\n", inverse_a)
    # Output:
    # [[-2.   1. ]
    #  [ 1.5 -0.5]]
except np.linalg.LinAlgError:
    print("\nMatrix A is singular (not invertible).")

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(matrix_a)
print("\nEigenvalues of A:", eigenvalues) # Output: [-0.37228132  5.37228132]
print("Eigenvectors of A:\n", eigenvectors)
# Output:
# [[-0.82456484 -0.41597356]
#  [ 0.56576746 -0.90937671]]

# Solving a linear system Ax = v
try:
    x = np.linalg.solve(matrix_a, vector_v) # Solve Ax = v for x
    print("\nSolution to Ax = v (x):\n", x) # Output: [-1.  2.]
    # Check solution:
    print("\nCheck: A * x =\n", np.dot(matrix_a, x)) # Output: [2. 3.] (approximately equals v)
except np.linalg.LinAlgError:
    print("\nLinear system has no unique solution.")
```

## Random Number Generation with NumPy

NumPy's `random` module provides functions for generating random numbers from various probability distributions. This is crucial for simulations, statistical sampling, and machine learning tasks.

**Common random number functions:**

*   `np.random.rand(shape)`: Uniform distribution between 0 and 1.
*   `np.random.randn(shape)`: Standard normal distribution (mean 0, std dev 1).
*   `np.random.randint(low, high, size)`: Discrete uniform distribution of integers.
*   `np.random.random_sample(size)`: Uniform distribution between 0 and 1 (similar to `rand` but with size as a tuple or integer).
*   `np.random.choice(a, size, replace, p)`: Randomly samples from a given array `a`.
*   `np.random.shuffle(array)`: Shuffles an array in place.
*   `np.random.permutation(array)`: Returns a random permutation of an array (or range).
*   `np.random.seed(seed_value)`: Sets the seed for the random number generator for reproducibility.

**Examples of random number generation:**

```python
# Code cell
import numpy as np

# Set random seed for reproducibility
np.random.seed(42) # Using seed 42 (any integer value will work)

uniform_rand_array = np.random.rand(3, 3) # 3x3 uniform random numbers (0-1)
print("Uniform random array:\n", uniform_rand_array)

normal_rand_array = np.random.randn(2, 4) # 2x4 random numbers from standard normal distribution
print("\nNormal random array:\n", normal_rand_array)

randint_array = np.random.randint(0, 100, 5) # 5 random integers between 0 and <100
print("\nRandom integers array:", randint_array)

choices = np.array(['a', 'b', 'c', 'd', 'e'])
random_choices = np.random.choice(choices, size=10) # 10 random choices from 'choices' array
print("\nRandom choices:", random_choices)

numbers = np.arange(10) # [0 1 2 3 4 5 6 7 8 9]
np.random.shuffle(numbers) # Shuffle in place
print("\nShuffled array (in-place):\n", numbers) # Output will vary each run, but array is shuffled

permutation_array = np.random.permutation(np.arange(5)) # Random permutation of [0 1 2 3 4]
print("\nPermutation array:\n", permutation_array) # Output will vary, but will be a permutation of [0 1 2 3 4]
```

Setting a random seed using `np.random.seed()` is important for reproducibility. If you use the same seed value, you'll get the same sequence of random numbers each time you run your code. This is useful for debugging and ensuring consistent results when sharing or repeating experiments.

NumPy is a vast and powerful library. In this chapter, we've only scratched the surface, covering fundamental concepts like array creation, indexing, slicing, element-wise operations, broadcasting, linear algebra, and random number generation. As you progress in data science and scientific computing, you'll find NumPy to be an indispensable tool in your Python toolkit.

**In this chapter, we've covered:**

*   Introduction to NumPy and its importance in data science.
*   NumPy arrays (ndarrays): creation from lists/tuples, array creation functions.
*   Array attributes: `shape`, `dtype`, `ndim`, `size`.
*   Indexing and slicing: basic indexing, slicing, boolean indexing, fancy indexing.
*   Array operations: element-wise operations, broadcasting, universal functions (ufuncs).
*   Basic linear algebra operations using `numpy.linalg`.
*   Random number generation with `numpy.random`.

In the next chapter, we'll move on to Pandas, another essential library for data manipulation and analysis, building upon the foundation we've established with NumPy.
