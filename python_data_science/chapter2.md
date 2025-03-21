# Chapter 2: Data Structures in Python

In the previous chapter, we introduced basic Python syntax and data types. Now, we'll explore fundamental data structures that are essential for organizing and manipulating data in Python, especially in the context of data science. These structures will become your workhorses for handling datasets, performing calculations, and implementing algorithms.

## Lists: Ordered Collections

Think of lists as ordered containers that can hold a sequence of items. These items can be of any data type – numbers, strings, even other lists! Lists are mutable, meaning you can modify them after creation (add, remove, or change elements).

**Creating Lists:**

Lists are created using square brackets `[]` with items separated by commas.

```python
# Code cell
numbers = [1, 2, 3, 4, 5]
planets = ['Earth', 'Mars', 'Jupiter', 'Saturn']
mixed_data = [10, 'hello', 3.14, True]
empty_list = [] # An empty list
```

**Accessing List Elements (Indexing and Slicing):**

Lists are ordered, so each element has an index, starting from 0 for the first element.

```python
# Code cell
planets = ['Earth', 'Mars', 'Jupiter', 'Saturn']

print(planets[0])   # Access the first element (index 0) - Output: Earth
print(planets[2])   # Access the third element (index 2) - Output: Jupiter
print(planets[-1])  # Access the last element using negative indexing - Output: Saturn
```

**Slicing:** You can extract a portion of a list using slicing. It creates a new list containing a subset of the original list.

```python
# Code cell
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numbers[2:5])    # Slice from index 2 up to (but not including) 5 - Output: [2, 3, 4]
print(numbers[:4])     # Slice from the beginning up to (but not including) 4 - Output: [0, 1, 2, 3]
print(numbers[6:])     # Slice from index 6 to the end - Output: [6, 7, 8, 9]
print(numbers[::2])    # Slice with a step of 2 (every other element) - Output: [0, 2, 4, 6, 8]
print(numbers[::-1])   # Reverse the list using slicing - Output: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

**List Manipulation:**

Lists are mutable, offering various methods to modify them.

*   **Adding elements:**
    *   `append(item)`: Adds an item to the end of the list.
    *   `insert(index, item)`: Inserts an item at a specific index.
    *   `extend(iterable)`: Appends elements from an iterable (like another list) to the end.

```python
# Code cell
fruits = ['apple', 'banana']
fruits.append('orange')       # Add 'orange' to the end - fruits is now ['apple', 'banana', 'orange']
fruits.insert(1, 'grape')    # Insert 'grape' at index 1 - fruits is now ['apple', 'grape', 'banana', 'orange']
more_fruits = ['kiwi', 'mango']
fruits.extend(more_fruits)   # Extend fruits with more_fruits - fruits is now ['apple', 'grape', 'banana', 'orange', 'kiwi', 'mango']
print(fruits)
```

*   **Removing elements:**
    *   `remove(item)`: Removes the first occurrence of a specific item.
    *   `pop(index)`: Removes and returns the item at a given index (default is the last item).
    *   `clear()`: Removes all items from the list.

```python
# Code cell
colors = ['red', 'blue', 'green', 'blue']
colors.remove('blue')    # Removes the first 'blue' - colors is now ['red', 'green', 'blue']
removed_color = colors.pop(1) # Removes and returns item at index 1 ('green') - colors is now ['red', 'blue'], removed_color is 'green'
colors.clear()           # Removes all items - colors is now []
print(colors)
```

*   **Modifying elements:** You can directly change an element by assigning a new value to its index.

```python
# Code cell
temperatures = [25, 28, 30]
temperatures[1] = 29  # Change the element at index 1 - temperatures is now [25, 29, 30]
print(temperatures)
```

*   **Other useful list methods:**
    *   `index(item)`: Returns the index of the first occurrence of an item.
    *   `count(item)`: Returns the number of times an item appears in the list.
    *   `sort()`: Sorts the list in place (modifies the original list).
    *   `reverse()`: Reverses the list in place.
    *   `copy()`: Returns a shallow copy of the list.

## Tuples: Immutable Sequences

Tuples are similar to lists, but with a key difference: they are immutable. Once a tuple is created, you cannot change its elements (add, remove, or modify). Tuples are defined using parentheses `()`.

**Creating Tuples:**

```python
# Code cell
coordinates = (10, 20)
rgb_color = (255, 0, 0) # Red color in RGB
data_points = (1.5, 2.7, 3.9, 4.2)
empty_tuple = ()
single_element_tuple = (5,) # Note the trailing comma for single-element tuples
```

**Accessing Tuple Elements:**

You access tuple elements using indexing and slicing, just like lists.

```python
# Code cell
rgb_color = (255, 0, 0)
print(rgb_color[0])   # Output: 255
print(rgb_color[1:])  # Output: (0, 0)
```

**Immutability:**

Because tuples are immutable, you cannot use methods like `append()`, `insert()`, `remove()`, or modify elements directly.

```python
# This will raise an error:
# coordinates = (10, 20)
# coordinates[0] = 15  # TypeError: 'tuple' object does not support item assignment
```

**Use Cases for Tuples:**

*   **Representing fixed collections:** Use tuples when you want to ensure that the data structure remains constant, like coordinates, RGB colors, or database records.
*   **Returning multiple values from a function:** Functions can return tuples to efficiently return multiple values.
*   **Keys in dictionaries:** Tuples can be used as keys in dictionaries (since they are immutable), while lists cannot.

## Dictionaries: Key-Value Pairs

Dictionaries are unordered collections of key-value pairs. Each key in a dictionary must be unique and immutable (like strings, numbers, or tuples), while values can be of any data type. Dictionaries are defined using curly braces `{}`.

**Creating Dictionaries:**

```python
# Code cell
student = {
    'name': 'Alice',
    'student_id': 'S12345',
    'major': 'Physics',
    'grades': [85, 90, 78]
}

empty_dict = {}
```

**Accessing Values:**

You access values in a dictionary using their keys within square brackets `[]`.

```python
# Code cell
student = {
    'name': 'Alice',
    'student_id': 'S12345',
    'major': 'Physics'
}

print(student['name'])      # Output: Alice
print(student['major'])     # Output: Physics
# print(student['age'])       # This would raise a KeyError if 'age' key doesn't exist
print(student.get('age'))   # Using get() method returns None if key is not found, avoiding KeyError - Output: None
print(student.get('age', 20))# get() with a default value - Output: 20 (if 'age' is not found, return 20)
```

**Dictionary Manipulation:**

Dictionaries are mutable, allowing you to add, modify, and remove key-value pairs.

*   **Adding or modifying key-value pairs:**

```python
# Code cell
student = {'name': 'Alice', 'major': 'Physics'}
student['age'] = 20       # Add a new key-value pair
student['major'] = 'Astrophysics' # Modify the value for an existing key
print(student)
```

*   **Removing key-value pairs:**
    *   `pop(key)`: Removes and returns the value associated with a key (raises KeyError if key not found).
    *   `del dictionary[key]`: Deletes the key-value pair (raises KeyError if key not found).
    *   `clear()`: Removes all key-value pairs from the dictionary.

```python
# Code cell
planet_data = {'Earth': 1.0, 'Mars': 0.11, 'Jupiter': 317.8}
earth_mass = planet_data.pop('Earth') # Removes 'Earth' and returns its value - planet_data is now {'Mars': 0.11, 'Jupiter': 317.8}, earth_mass is 1.0
del planet_data['Mars']       # Deletes 'Mars' key-value pair - planet_data is now {'Jupiter': 317.8}
planet_data.clear()          # Clears the dictionary - planet_data is now {}
print(planet_data)
```

*   **Other useful dictionary methods:**
    *   `keys()`: Returns a view object that displays a list of all keys.
    *   `values()`: Returns a view object that displays a list of all values.
    *   `items()`: Returns a view object that displays a list of dictionary's key-value tuple pairs.
    *   `update(other_dict)`: Updates the dictionary with key-value pairs from another dictionary.

## Sets: Unordered Collections of Unique Elements

Sets are unordered collections of unique elements. This means that a set cannot contain duplicate values. Sets are useful for tasks like removing duplicates from a list, checking for membership, and performing mathematical set operations (union, intersection, difference). Sets are defined using curly braces `{}` or the `set()` constructor.

**Creating Sets:**

```python
# Code cell
unique_numbers = {1, 2, 3, 4, 5}
vowels = {'a', 'e', 'i', 'o', 'u'}
mixed_set = {10, 'hello', 3.14, True, 10} # Note: duplicate 10 will be automatically removed

print(mixed_set) # Output: {True, 3.14, 10, 'hello'} (order may vary, and only one 10 is present)

# Creating a set from a list (removes duplicates)
numbers_list = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique_numbers_set = set(numbers_list) # Output: {1, 2, 3, 4}
print(unique_numbers_set)

empty_set = set() # To create an empty set, use set() constructor (not {}) - {} creates an empty dictionary
```

**Set Operations:**

Sets support common mathematical set operations:

*   **Union (`|` or `union()`):** Returns a new set containing all elements from both sets.
*   **Intersection (`&` or `intersection()`):** Returns a new set containing common elements.
*   **Difference (`-` or `difference()`):** Returns a new set containing elements in the first set but not in the second set.
*   **Symmetric Difference (`^` or `symmetric_difference()`):** Returns a new set containing elements that are in either set, but not in both.

```python
# Code cell
set1 = {1, 2, 3, 4, 5}
set2 = {3, 4, 5, 6, 7}

print(set1 | set2)              # Union - Output: {1, 2, 3, 4, 5, 6, 7}
print(set1.union(set2))         # Union (method form) - Output: {1, 2, 3, 4, 5, 6, 7}
print(set1 & set2)              # Intersection - Output: {3, 4, 5}
print(set1.intersection(set2))    # Intersection (method form) - Output: {3, 4, 5}
print(set1 - set2)              # Difference (set1 - set2) - Output: {1, 2}
print(set1.difference(set2))     # Difference (method form) - Output: {1, 2}
print(set2 - set1)              # Difference (set2 - set1) - Output: {6, 7}
print(set1 ^ set2)              # Symmetric Difference - Output: {1, 2, 6, 7}
print(set1.symmetric_difference(set2)) # Symmetric Difference (method form) - Output: {1, 2, 6, 7}
```

**Set Manipulation:**

Sets are mutable, allowing you to add and remove elements.

*   **Adding elements:**
    *   `add(item)`: Adds an item to the set.
    *   `update(iterable)`: Adds elements from an iterable to the set.

```python
# Code cell
planets_set = {'Earth', 'Mars'}
planets_set.add('Jupiter')      # Add 'Jupiter' - planets_set is now {'Earth', 'Mars', 'Jupiter'}
planets_set.update(['Saturn', 'Uranus']) # Add multiple planets - planets_set is now {'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus'}
print(planets_set)
```

*   **Removing elements:**
    *   `remove(item)`: Removes an item (raises KeyError if item not found).
    *   `discard(item)`: Removes an item if it's present (does nothing if item not found, no error).
    *   `pop()`: Removes and returns an arbitrary element from the set (raises KeyError if set is empty).
    *   `clear()`: Removes all elements from the set.

```python
# Code cell
elements = {'H', 'He', 'Li', 'Be'}
elements.remove('Li')    # Remove 'Li' - elements is now {'H', 'He', 'Be'}
elements.discard('B')   # Discard 'B' (it's not in the set, no error)
removed_element = elements.pop() # Remove and return an arbitrary element - elements will have one less element
elements.clear()         # Clear the set - elements is now set()
print(elements)
```

**Membership Testing:**

You can efficiently check if an element is present in a set using the `in` operator.

```python
# Code cell
vowels = {'a', 'e', 'i', 'o', 'u'}
print('e' in vowels)    # Output: True
print('b' in vowels)    # Output: False
```

## Choosing the Right Data Structure

| Data Structure | Ordered | Mutable | Duplicates Allowed | Key-Value Pairs | Use Cases                                                                    |
| :--------------- | :------ | :------ | :----------------- | :-------------- | :--------------------------------------------------------------------------- |
| **List**         | Yes     | Yes     | Yes                | No              | Ordered collections, sequences, when order matters, elements may change.     |
| **Tuple**        | Yes     | No      | Yes                | No              | Fixed collections, representing records, data integrity, function returns. |
| **Dictionary**   | No (from Python 3.7+, insertion order preserved but still conceptually unordered before that) | Yes     | No (keys)          | Yes             | Lookups, mappings, representing structured data with labels (keys).         |
| **Set**          | No      | Yes     | No                 | No              | Unique elements, membership testing, removing duplicates, set operations.   |

Understanding these data structures is crucial for efficient data manipulation and algorithm design in Python. As we progress, you'll see how these structures are used extensively in data science libraries like NumPy and Pandas.

**In this chapter, we've covered:**

*   **Lists:** Ordered, mutable sequences, indexing, slicing, manipulation methods.
*   **Tuples:** Ordered, immutable sequences, use cases for fixed data.
*   **Dictionaries:** Unordered key-value pairs, accessing, modifying, and use cases for mappings.
*   **Sets:** Unordered collections of unique elements, set operations, membership testing.
*   Guidance on choosing the appropriate data structure for different scenarios.

In the next chapter, we'll explore control flow statements and functions to add logic and structure to your Python programs.
