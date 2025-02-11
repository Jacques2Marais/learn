**Chapter 3: Advanced Data Retrieval – Filtering, Sorting, and Aliasing**

Welcome to Chapter 3! Building upon the foundational SQL skills you've acquired, we'll now explore advanced data retrieval techniques. This chapter focuses on enhancing your queries by applying complex filtering conditions, sorting results, and utilizing aliases for clarity and efficiency.

**3.1 Advanced Filtering Techniques**

In SQL, the `WHERE` clause is pivotal for filtering records based on specified conditions. To refine your data retrieval further, you can combine multiple conditions using the `AND` and `OR` operators.

- **Using `AND` Operator:**

  The `AND` operator allows you to filter records that meet all specified conditions.

  *Example:*

  ```sql
  SELECT *
  FROM Employees
  WHERE Department = 'Sales' AND HireDate > '2020-01-01';
  ```

  This query retrieves employees who work in the Sales department and were hired after January 1, 2020.

- **Using `OR` Operator:**

  The `OR` operator retrieves records that meet at least one of the specified conditions.

  *Example:*

  ```sql
  SELECT *
  FROM Products
  WHERE Category = 'Electronics' OR Category = 'Furniture';
  ```

  This query fetches products that belong to either the Electronics or Furniture categories.

- **Combining `AND` and `OR`:**

  When combining `AND` and `OR` operators, it's essential to use parentheses to define the order of evaluation clearly.

  *Example:*

  ```sql
  SELECT *
  FROM Orders
  WHERE (Status = 'Shipped' OR Status = 'Delivered') AND OrderDate > '2025-01-01';
  ```

  This query selects orders that have either been shipped or delivered and were placed after January 1, 2025.

**3.2 Sorting Data with `ORDER BY`**

The `ORDER BY` clause is used to sort the result set of a query by one or more columns, either in ascending (`ASC`) or descending (`DESC`) order. By default, sorting is in ascending order.

- **Sorting in Ascending Order:**

  *Example:*

  ```sql
  SELECT FirstName, LastName, HireDate
  FROM Employees
  ORDER BY HireDate ASC;
  ```

  This query lists employees ordered by their hire date from the earliest to the latest.

- **Sorting in Descending Order:**

  *Example:*

  ```sql
  SELECT ProductName, Price
  FROM Products
  ORDER BY Price DESC;
  ```

  This query displays products ordered by price from highest to lowest.

- **Sorting by Multiple Columns:**

  You can sort by multiple columns by specifying them in the `ORDER BY` clause, separated by commas.

  *Example:*

  ```sql
  SELECT FirstName, LastName, Department
  FROM Employees
  ORDER BY Department ASC, LastName ASC;
  ```

  This query sorts employees first by department in ascending order and then by last name within each department.

**3.3 Utilizing Aliases for Clarity**

Aliases provide temporary names for columns or tables, enhancing the readability and manageability of your queries. They are created using the `AS` keyword.

- **Column Aliases:**

  *Example:*

  ```sql
  SELECT FirstName AS 'First Name', LastName AS 'Last Name'
  FROM Employees;
  ```

  This query renames the `FirstName` and `LastName` columns to 'First Name' and 'Last Name' in the result set.

- **Table Aliases:**

  *Example:*

  ```sql
  SELECT e.FirstName, e.LastName, d.DepartmentName
  FROM Employees AS e
  JOIN Departments AS d ON e.DepartmentID = d.DepartmentID;
  ```

  Here, `e` and `d` are aliases for the `Employees` and `Departments` tables, respectively, simplifying the query notation.

**3.4 Leveraging SQL Functions**

SQL functions allow you to perform operations on your data, such as string manipulation, mathematical calculations, and date processing.

- **String Functions:**

  - `UPPER()`: Converts a string to uppercase.

    *Example:*

    ```sql
    SELECT UPPER(FirstName) AS 'First Name'
    FROM Employees;
    ```

  - `LOWER()`: Converts a string to lowercase.

    *Example:*

    ```sql
    SELECT LOWER(LastName) AS 'Last Name'
    FROM Employees;
    ```

  - `CONCAT()`: Concatenates two or more strings.

    *Example:*

    ```sql
    SELECT CONCAT(FirstName, ' ', LastName) AS 'Full Name'
    FROM Employees;
    ```

- **Date Functions:**

  - `YEAR()`: Extracts the year from a date.

    *Example:*

    ```sql
    SELECT FirstName, LastName, YEAR(HireDate) AS 'Hire Year'
    FROM Employees;
    ```

  - `DATEDIFF()`: Calculates the difference between two dates.

    *Example:*

    ```sql
    SELECT FirstName, LastName, DATEDIFF(CURDATE(), HireDate) AS 'Days Employed'
    FROM Employees;
    ```

**3.5 Practical Examples and Exercises**

Let's apply these concepts through practical examples:

1. **Filter Data with Multiple Conditions:**

   - **Task:** Retrieve all orders placed by customer 'John Doe' that have a total amount greater than $500.

     ```sql
     SELECT *
     FROM Orders
     WHERE CustomerName = 'John Doe' AND TotalAmount > 500;
     ```

2. **Sort Data:**

   - **Task:** List all products in the 'Electronics' category, sorted by price in descending order.

     ```sql
     SELECT ProductName, Price
     FROM Products
     WHERE Category = 'Electronics'
     ORDER BY Price DESC;
     ```

3. **Use Aliases:**

   - **Task:** Display a list of employees with their full names and departments, using aliases for clarity.

     ```sql
     SELECT CONCAT(e.FirstName, ' ', e.LastName) AS 'Full Name', d.DepartmentName AS 'Department'
     FROM Employees AS e
     JOIN Departments AS d ON e.DepartmentID = d.DepartmentID;
     ```

4. **Apply Functions:**

   - **Task:** Retrieve the first and last names of employees, converting them to uppercase.

     ```sql
     SELECT UPPER(FirstName) AS 'First Name', UPPER(LastName) AS 'Last Name'
     FROM Employees;
     ```

**3.6 Additional Considerations**

- **Interactive Query Debugging:**

  When encountering errors in your queries, carefully read the error messages provided by your SQL environment. They often indicate the exact issue, such as syntax errors or missing tables. Debugging involves checking for common mistakes like missing commas, incorrect table names, or misused operators.

- **Real-World Datasets:**

  To make your learning experience more relevant, practice with datasets that mimic real-world scenarios. For instance, use a fictional company's employee records or sales data to test your queries.

- **Encourage Experimentation:**

  Don't hesitate to modify and experiment with the provided queries. Change conditions, sorting orders, or apply different

  [Next chapter >>](https://github.com/Jacques2Marais/learn/blob/main/sql/chapter4.md)
