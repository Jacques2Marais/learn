# Chapter 6: Data Manipulation with Pandas

Welcome to the world of Pandas! Pandas is a powerful and essential Python library for data manipulation and analysis. It provides data structures like Series and DataFrames that are designed to make working with structured (tabular) data intuitive and efficient. If NumPy is the foundation for numerical computing, Pandas builds upon it to provide high-level data manipulation capabilities, making it a cornerstone of data science workflows.

## Pandas Series and DataFrames: Creating, Indexing, Selecting Data

Pandas introduces two primary data structures:

*   **Series:** A Series is a 1-dimensional labeled array-like object. It can hold data of any type (integers, floats, strings, Python objects, etc.). Think of it as a column in a spreadsheet or a labeled NumPy array.

*   **DataFrame:** A DataFrame is a 2-dimensional labeled data structure with columns of potentially different types. It's like a table or a spreadsheet, where each column is a Series and they share a common index. DataFrames are the workhorse of Pandas and are incredibly versatile for representing and manipulating tabular data.

### Pandas Series

**Creating Series:**

You can create a Series from various data sources, including lists, NumPy arrays, dictionaries, and scalars.

**1. From a list or NumPy array:**

```python
# Code cell
import pandas as pd
import numpy as np

# From a Python list
data_list = [10, 20, 30, 40, 50]
series_from_list = pd.Series(data_list)
print("Series from list:\n", series_from_list)
# Output:
# 0    10
# 1    20
# 2    30
# 3    40
# 4    50
# dtype: int64

# From a NumPy array
data_array = np.array([5, 10, 15, 20, 25])
series_from_array = pd.Series(data_array)
print("\nSeries from NumPy array:\n", series_from_array)
# Output: (similar to above, but potentially different dtype)

# Custom index
custom_index = ['a', 'b', 'c', 'd', 'e']
series_custom_index = pd.Series(data_list, index=custom_index)
print("\nSeries with custom index:\n", series_custom_index)
# Output:
# a    10
# b    20
# c    30
# d    40
# e    50
# dtype: int64
```

**2. From a dictionary:**

When creating a Series from a dictionary, the keys become the index, and the values become the Series values.

```python
# Code cell
import pandas as pd

data_dict = {'apple': 10, 'banana': 20, 'orange': 15, 'grape': 5}
series_from_dict = pd.Series(data_dict)
print("Series from dictionary:\n", series_from_dict)
# Output:
# apple     10
# banana    20
# orange    15
# grape      5
# dtype: int64
```

**3. From a scalar value:**

You can create a Series with a scalar value, which will be repeated for all index labels.

```python
# Code cell
import pandas as pd

scalar_value = 100
index_labels = ['x', 'y', 'z']
series_from_scalar = pd.Series(scalar_value, index=index_labels)
print("Series from scalar:\n", series_from_scalar)
# Output:
# x    100
# y    100
# z    100
# dtype: int64
```

**Indexing and Selecting Data in Series:**

You can access elements in a Series using label-based indexing (using index labels) or position-based indexing (using integer positions, like NumPy arrays or lists).

**1. Label-based indexing:**

```python
# Code cell
import pandas as pd

data_series = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

print(data_series['a'])   # Access by label 'a' - Output: 10
print(data_series[['c', 'e', 'a']]) # Access multiple labels - Output: (Series with labels 'c', 'e', 'a' and corresponding values)
print(data_series['b':'d']) # Slicing with labels (inclusive of end label 'd') - Output: (Series from label 'b' to 'd')
```

**2. Position-based indexing (integer-based):**

Use `.iloc[]` for purely integer-location based indexing.

```python
# Code cell
import pandas as pd

data_series = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])

print(data_series.iloc[0])    # Access by position 0 - Output: 10
print(data_series.iloc[[2, 4, 1]]) # Access multiple positions - Output: (Series with values at positions 2, 4, 1)
print(data_series.iloc[1:4])   # Slicing with positions (exclusive of end position 4) - Output: (Series from position 1 to 3)
```

**3. Boolean indexing (conditional selection):**

Similar to NumPy, you can use boolean conditions to select elements in a Series.

```python
# Code cell
import pandas as pd

data_series = pd.Series([10, 25, 15, 30, 5])

bool_series = data_series > 20 # Create boolean Series based on condition
print("Boolean Series:\n", bool_series)
# Output:
# 0    False
# 1     True
# 2    False
# 3     True
# 4    False
# dtype: bool

filtered_series = data_series[bool_series] # Select elements where bool_series is True
print("\nFiltered Series (values > 20):\n", filtered_series)
# Output:
# 1    25
# 3    30
# dtype: int64

# Combining conditions:
condition = (data_series > 10) & (data_series < 30)
filtered_series_combined = data_series[condition]
print("\nFiltered Series (10 < values < 30):\n", filtered_series_combined)
# Output:
# 1    25
# 2    15
# 3    30 # Oops, 30 is not < 30, condition should be <= 30 or < 31
condition_corrected = (data_series > 10) & (data_series <= 30)
filtered_series_combined_corrected = data_series[condition_corrected]
print("\nFiltered Series (10 < values <= 30) - corrected:\n", filtered_series_combined_corrected)
# Output:
# 1    25
# 2    15
# 3    30
# dtype: int64
```

### Pandas DataFrames

**Creating DataFrames:**

DataFrames can be created from various sources, including dictionaries of Series or lists, NumPy arrays, CSV files, Excel files, and more.

**1. From a dictionary of lists or NumPy arrays:**

Each key in the dictionary represents a column name, and the corresponding list or NumPy array represents the column values.

```python
# Code cell
import pandas as pd
import numpy as np

data = {
    'physics': [60, 70, 80, 90],
    'chemistry': [65, 75, 85, 95],
    'math': [70, 80, 90, 100]
}
student_df = pd.DataFrame(data)
print("DataFrame from dictionary:\n", student_df)
# Output:
#    physics  chemistry  math
# 0       60         65    70
# 1       70         75    80
# 2       80         85    90
# 3       90         95   100

# With custom index
student_names = ['Alice', 'Bob', 'Charlie', 'David']
student_df_custom_index = pd.DataFrame(data, index=student_names)
print("\nDataFrame with custom index:\n", student_df_custom_index)
# Output:
#          physics  chemistry  math
# Alice         60         65    70
# Bob           70         75    80
# Charlie       80         85    90
# David         90         95   100
```

**2. From a list of dictionaries:**

Each dictionary in the list represents a row in the DataFrame.

```python
# Code cell
import pandas as pd

data_list_of_dicts = [
    {'name': 'Alice', 'age': 20, 'major': 'Physics'},
    {'name': 'Bob', 'age': 22, 'major': 'Chemistry'},
    {'name': 'Charlie', 'age': 21, 'major': 'Math'}
]
student_df_from_list_of_dicts = pd.DataFrame(data_list_of_dicts)
print("DataFrame from list of dictionaries:\n", student_df_from_list_of_dicts)
# Output:
#        name  age    major
# 0     Alice   20  Physics
# 1       Bob   22  Chemistry
# 2   Charlie   21     Math
```

**3. From NumPy arrays:**

You can create a DataFrame from a NumPy array, optionally providing column names and index.

```python
# Code cell
import pandas as pd
import numpy as np

data_array_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
column_names = ['col1', 'col2', 'col3']
df_from_array = pd.DataFrame(data_array_2d, columns=column_names)
print("DataFrame from NumPy array:\n", df_from_array)
# Output:
#    col1  col2  col3
# 0     1     2     3
# 1     4     5     6
# 2     7     8     9
```

**Indexing and Selecting Data in DataFrames:**

DataFrames offer versatile ways to access and select data:

**1. Column selection:**

You can select one or more columns by name using square brackets `[]` or dot notation (for valid column names without spaces or special characters).

```python
# Code cell
import pandas as pd

data = {'col1': [1, 2, 3], 'col2': [4, 5, 6], 'col3': [7, 8, 9]}
df = pd.DataFrame(data)

print(df['col1'])     # Select single column 'col1' (returns a Series)
print(df[['col1', 'col3']]) # Select multiple columns (returns a DataFrame)
# print(df.col2)      # Dot notation for column selection (if column name is valid) - Output: (Series for 'col2')
```

**2. Row selection (slicing):**

You can slice rows using standard Python slicing notation.

```python
# Code cell
import pandas as pd

data = {'col1': [1, 2, 3, 4, 5], 'col2': [6, 7, 8, 9, 10]}
df = pd.DataFrame(data)

print(df[1:4]) # Slice rows from index 1 up to (but not including) 4
```

**3. Label-based indexing using `.loc[]`:**

Use `.loc[]` to select rows and columns by labels (index labels and column names).

```python
# Code cell
import pandas as pd

data = {'col1': [1, 2, 3], 'col2': [4, 5, 6], 'col3': [7, 8, 9]}
df = pd.DataFrame(data, index=['row1', 'row2', 'row3'])

print(df.loc['row1']) # Select row with label 'row1' (returns a Series)
print(df.loc[['row1', 'row3']]) # Select multiple rows by labels (returns a DataFrame)
print(df.loc['row2', 'col2']) # Select specific element at row 'row2', column 'col2' - Output: 5
print(df.loc['row1':'row3', 'col1':'col2']) # Slice rows 'row1' to 'row3' and columns 'col1' to 'col2' (inclusive)
```

**4. Position-based indexing using `.iloc[]`:**

Use `.iloc[]` for purely integer-location based indexing for both rows and columns.

```python
# Code cell
import pandas as pd

data = {'col1': [1, 2, 3], 'col2': [4, 5, 6], 'col3': [7, 8, 9]}
df = pd.DataFrame(data)

print(df.iloc[0]) # Select row at position 0 (returns a Series)
print(df.iloc[[0, 2]]) # Select rows at positions 0 and 2 (returns a DataFrame)
print(df.iloc[1, 1]) # Select element at row position 1, column position 1 - Output: 5
print(df.iloc[0:2, 0:2]) # Slice rows from position 0 to 1 and columns from position 0 to 1 (exclusive of position 2)
```

**5. Boolean indexing (conditional selection):**

You can use boolean conditions to filter rows based on column values.

```python
# Code cell
import pandas as pd

data = {'col1': [10, 20, 30, 40, 50], 'col2': [5, 15, 25, 35, 45]}
df = pd.DataFrame(data)

bool_series_col1 = df['col1'] > 25 # Boolean Series for 'col1' > 25
print("Boolean Series for col1 > 25:\n", bool_series_col1)
# Output:
# 0    False
# 1    False
# 2     True
# 3     True
# 4     True
# Name: col1, dtype: bool

filtered_df = df[bool_series_col1] # Filter DataFrame based on boolean Series
print("\nFiltered DataFrame (col1 > 25):\n", filtered_df)
# Output:
#    col1  col2
# 2    30    25
# 3    40    35
# 4    50    45

# Combining conditions:
condition = (df['col1'] > 15) & (df['col2'] < 40)
filtered_df_combined = df[condition]
print("\nFiltered DataFrame (col1 > 15 AND col2 < 40):\n", filtered_df_combined)
# Output:
#    col1  col2
# 1    20    15
# 2    30    25
# 3    40    35
```

## Data Loading and Saving

Pandas excels at reading data from and writing data to various file formats.

**1. Reading data:**

*   `pd.read_csv('filename.csv')`: Reads data from a CSV file into a DataFrame.
*   `pd.read_excel('filename.xlsx')`: Reads data from an Excel file into a DataFrame.
*   `pd.read_json('filename.json')`: Reads data from a JSON file.
*   `pd.read_sql_table('tablename', connection)`: Reads data from a SQL table.
*   `pd.read_html('url')`: Reads HTML tables from a webpage.
*   ... and many more formats (see Pandas documentation).

**Example: Reading a CSV file**

Assume you have a CSV file named `data.csv` in the same directory:

```csv
col1,col2,col3
1,4,7
2,5,8
3,6,9
```

```python
# Code cell
import pandas as pd

df_csv = pd.read_csv('data.csv') # Reads data.csv into a DataFrame
print("DataFrame from CSV:\n", df_csv)
# Output:
#    col1  col2  col3
# 0     1     4     7
# 1     2     5     8
# 2     3     6     9
```

**2. Saving data:**

*   `df.to_csv('filename.csv', index=False)`: Writes DataFrame to a CSV file. `index=False` prevents writing DataFrame index to the file.
*   `df.to_excel('filename.xlsx', index=False)`: Writes to an Excel file.
*   `df.to_json('filename.json')`: Writes to a JSON file.
*   `df.to_sql('tablename', connection, if_exists='replace')`: Writes to a SQL table (`if_exists` controls behavior if table exists).
*   `df.to_html('filename.html')`: Writes to an HTML file.
*   ... and many more formats.

**Example: Saving DataFrame to CSV**

```python
# Code cell
import pandas as pd

data = {'col1': [10, 20, 30], 'col2': [40, 50, 60]}
df_to_save = pd.DataFrame(data)

df_to_save.to_csv('output.csv', index=False) # Saves DataFrame to output.csv (without index)
print("DataFrame saved to output.csv")
```

## Data Cleaning and Preprocessing

Real-world datasets are often messy and require cleaning and preprocessing before analysis. Pandas provides tools to handle common data cleaning tasks:

**1. Handling Missing Values:**

*   `df.isnull()`: Detects missing values (returns a DataFrame of boolean values).
*   `df.notnull()`: Opposite of `isnull()`.
*   `df.dropna()`: Removes rows or columns with missing values.
*   `df.fillna(value)`: Fills missing values with a specified value.
*   `df.interpolate()`: Fills missing values using interpolation.

**Example: Handling missing data**

Assume you have a DataFrame `df_missing_data` with some NaN (Not a Number) values representing missing data.

```python
# Code cell
import pandas as pd
import numpy as np

data_missing = {'col1': [1, 2, np.nan, 4, 5], 'col2': [np.nan, 6, 7, np.nan, 9]}
df_missing_data = pd.DataFrame(data_missing)
print("DataFrame with missing data:\n", df_missing_data)
# Output:
#    col1  col2
# 0   1.0   NaN
# 1   2.0   6.0
# 2   NaN   7.0
# 3   4.0   NaN
# 4   5.0   9.0

print("\nDetecting missing values (isnull()):\n", df_missing_data.isnull())
# Output: (DataFrame of boolean values, True where value is NaN)

df_dropped_rows = df_missing_data.dropna() # Drop rows with any NaN
print("\nDataFrame after dropping rows with NaN:\n", df_dropped_rows)
# Output:
#    col1  col2
# 1   2.0   6.0
# 2   NaN   7.0 # Row 2 still has NaN in col1, so it's not dropped in row-wise dropna

df_dropped_cols = df_missing_data.dropna(axis=1) # Drop columns with any NaN
print("\nDataFrame after dropping columns with NaN:\n", df_dropped_cols)
# Output:
# Empty DataFrame
# Columns: []
# Index: [0, 1, 2, 3, 4] # Both columns had NaNs, so both are dropped

df_filled_0 = df_missing_data.fillna(0) # Fill NaN values with 0
print("\nDataFrame after filling NaN with 0:\n", df_filled_0)
# Output:
#    col1  col2
# 0   1.0   0.0
# 1   2.0   6.0
# 2   0.0   7.0
# 3   4.0   0.0
# 4   5.0   9.0

df_filled_mean = df_missing_data.fillna(df_missing_data.mean()) # Fill NaN with column means
print("\nDataFrame after filling NaN with column means:\n", df_filled_mean)
# Output:
#        col1  col2
# 0  1.000000   7.333333
# 1  2.000000   6.000000
# 2  3.000000   7.000000
# 3  4.000000   7.333333
# 4  5.000000   9.000000
```

**2. Data Transformation:**

*   **Column-wise operations:** You can apply functions to columns (Series) element-wise.
*   **`df.apply(function)`:** Applies a function along an axis of the DataFrame (row-wise or column-wise).
*   **`df.map(function)` (for Series):** Applies a function element-wise to a Series.
*   **`df.replace(to_replace, value)`:** Replaces values in a DataFrame.

**Example: Data transformation**

```python
# Code cell
import pandas as pd

data = {'temperature_celsius': [20, 25, 30, 22]}
df_temp = pd.DataFrame(data)

# Convert Celsius to Fahrenheit (element-wise operation on Series)
df_temp['temperature_fahrenheit'] = df_temp['temperature_celsius'] * 9/5 + 32
print("DataFrame with Fahrenheit conversion:\n", df_temp)
# Output:
#    temperature_celsius  temperature_fahrenheit
# 0                   20                    68.0
# 1                   25                    77.0
# 2                   30                    86.0
# 3                   22                    71.6

# Apply a function using apply() (row-wise - calculate difference between F and C)
def temp_diff(row):
    return row['temperature_fahrenheit'] - row['temperature_celsius']

df_temp['temp_difference'] = df_temp.apply(temp_diff, axis=1) # axis=1 for row-wise apply
print("\nDataFrame with temperature difference:\n", df_temp)
# Output:
#    temperature_celsius  temperature_fahrenheit  temp_difference
# 0                   20                    68.0             48.0
# 1                   25                    77.0             52.0
# 2                   30                    86.0             56.0
# 3                   22                    71.6             49.6
```

## Data Aggregation and Grouping: `groupby`, Aggregation Functions

Pandas `groupby()` is a powerful tool for grouping rows based on one or more columns and then performing aggregate calculations within each group.

**`groupby()` operation:**

1.  **Split:** The DataFrame is split into groups based on the values in the specified column(s).
2.  **Apply:** An aggregation function (e.g., `sum()`, `mean()`, `count()`, `min()`, `max()`, `std()`) is applied to each group independently.
3.  **Combine:** The results are combined back into a new DataFrame or Series.

**Example: Grouping and aggregation**

Assume you have a DataFrame `df_sales` with sales data for different categories and regions.

```python
# Code cell
import pandas as pd

data_sales = {
    'category': ['Electronics', 'Electronics', 'Books', 'Books', 'Electronics', 'Books'],
    'region': ['North', 'South', 'North', 'South', 'East', 'West'],
    'sales': [1000, 1200, 800, 900, 1500, 1100]
}
df_sales = pd.DataFrame(data_sales)
print("Sales DataFrame:\n", df_sales)
# Output:
#        category region  sales
# 0   Electronics  North   1000
# 1   Electronics  South   1200
# 2         Books  North    800
# 3         Books  South    900
# 4   Electronics   East   1500
# 5         Books   West   1100

# Group by 'category' and calculate total sales for each category
grouped_category = df_sales.groupby('category')
category_sales_sum = grouped_category['sales'].sum() # Aggregate sum of 'sales' column
print("\nTotal sales by category:\n", category_sales_sum)
# Output:
# category
# Books          2800
# Electronics    3700
# Name: sales, dtype: int64

# Group by 'category' and 'region', calculate mean sales
grouped_category_region = df_sales.groupby(['category', 'region'])
category_region_sales_mean = grouped_category_region['sales'].mean() # Mean sales
print("\nMean sales by category and region:\n", category_region_sales_mean)
# Output:
# category     region
# Books        North      800.0
#              South      900.0
#              West      1100.0
# Electronics  East      1500.0
#              North     1000.0
#              South     1200.0
# Name: sales, dtype: float64

# Multiple aggregation functions at once using .agg()
category_sales_agg = grouped_category.agg(['sum', 'mean', 'count', 'max'])
print("\nAggregated sales by category (sum, mean, count, max):\n", category_sales_agg)
# Output:
#              sales
#              sum   mean  count   max
# category
# Books         2800  933.333333      3  1100
# Electronics   3700 1233.333333      3  1500
```

Pandas `groupby()` and aggregation capabilities are incredibly powerful for summarizing and gaining insights from datasets.

Pandas is a vast library with many more features for data manipulation, analysis, and visualization. In this chapter, we've covered the fundamentals of Series and DataFrames, data loading/saving, basic cleaning, and aggregation. As you continue your data science journey, you'll discover more advanced Pandas functionalities and techniques to handle increasingly complex data tasks.

**In this chapter, we've covered:**

*   Introduction to Pandas and its importance for data manipulation.
*   Pandas Series: creation, indexing, selection.
*   Pandas DataFrames: creation, indexing, column/row selection, boolean indexing.
*   Data loading and saving using Pandas (CSV example).
*   Basic data cleaning: handling missing values.
*   Data transformation and column-wise/row-wise operations.
*   Data aggregation and grouping using `groupby()` and aggregation functions.

In the next chapter, we'll explore data visualization with Matplotlib and Seaborn to create insightful plots and charts from your data.
