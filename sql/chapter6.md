### [Module 6: Subqueries, Set Operations, and Nested Queries](https://github.com/Jacques2Marais/learn/blob/main/sql/chapter6.md) (coming soon)

**Description:**  
Explore advanced querying techniques that involve subqueries and set operations. This module covers how to embed queries within queries to solve complex problems and how to combine results from multiple queries using set operators.

**Key Learnings:**
- Write and understand subqueries in SELECT, FROM, and WHERE clauses.
- Use set operations such as UNION, INTERSECT, and EXCEPT.
- Identify scenarios where subqueries offer a cleaner solution compared to joins.
- Understand performance implications of nested queries.

**Practical Examples:**
- Create a subquery to filter records based on an aggregate calculation.
- Combine two datasets using UNION and analyze the differences.
- Exercises to transform nested queries into more readable formats.

**Additional Considerations:**
- Offer debugging tips for troubleshooting subqueries.
- Encourage side-by-side comparison of multiple query strategies.
- Use interactive labs to help students practice refactoring complex queries.

---

#### 6.1 Introduction to Subqueries

Subqueries, also known as inner queries or nested queries, are queries embedded within another SQL query. They are a powerful tool for performing operations in multiple steps or for queries that depend on the result of another query. Subqueries can be used in various parts of a SQL statement, including:

- **SELECT clause:** To return a single value.
- **FROM clause:** To use the result set of a subquery as a table.
- **WHERE clause:** To filter rows based on conditions derived from the subquery.

**Example 6.1.1: Subquery in WHERE clause**

Let's say we have two tables, `Employees` and `Departments`. We want to find all employees who work in the 'Sales' department.

```sql
-- Sample Tables:
-- Employees Table
-- EmployeeID | EmployeeName | DepartmentID
-- -----------|--------------|-------------
-- 1          | John Doe     | 1
-- 2          | Jane Smith   | 2
-- 3          | Peter Jones  | 1

-- Departments Table
-- DepartmentID | DepartmentName
-- -------------|---------------
-- 1            | Sales
-- 2            | Marketing

SELECT EmployeeName
FROM Employees
WHERE DepartmentID IN (SELECT DepartmentID FROM Departments WHERE DepartmentName = 'Sales');
```

**Explanation:**
1. The subquery `(SELECT DepartmentID FROM Departments WHERE DepartmentName = 'Sales')` selects the `DepartmentID` from the `Departments` table where `DepartmentName` is 'Sales'. This subquery returns the `DepartmentID` for the 'Sales' department, which is 1.
2. The outer query then selects `EmployeeName` from the `Employees` table where `DepartmentID` is in the result set of the subquery (which is 1).

**Key Takeaway:** Subqueries in the `WHERE` clause are often used to filter rows based on a condition that itself is the result of another query.

---

#### 6.2 Types of Subqueries

Subqueries can be categorized based on their return type and usage:

- **Scalar Subqueries:** Return a single value (one row and one column). They can be used wherever a single value is expected, such as in `SELECT` lists or `WHERE` clauses with comparison operators.

- **Row Subqueries:** Return a single row but can have multiple columns. They are often used with operators like `IN`, `EXISTS`, or when comparing tuples.

- **Table Subqueries:** Return multiple rows and multiple columns. They are typically used in the `FROM` clause as derived tables or with operators like `IN` or `EXISTS` in the `WHERE` clause.

**Example 6.2.1: Scalar Subquery in SELECT clause**

Let's find the name of each employee and the average salary of all employees.

```sql
-- Sample Table:
-- Employees Table (extended)
-- EmployeeID | EmployeeName | DepartmentID | Salary
-- -----------|--------------|-------------|--------
-- 1          | John Doe     | 1            | 50000
-- 2          | Jane Smith   | 2            | 60000
-- 3          | Peter Jones  | 1            | 55000

SELECT 
    EmployeeName,
    (SELECT AVG(Salary) FROM Employees) AS AverageSalary
FROM Employees;
```

**Explanation:**
1. The subquery `(SELECT AVG(Salary) FROM Employees)` calculates the average salary of all employees. This is a scalar subquery because it returns a single value.
2. The outer query selects `EmployeeName` and includes the result of the subquery (aliased as `AverageSalary`) for each employee.

**Example 6.2.2: Table Subquery in FROM clause (Derived Table)**

Suppose we want to find departments where the average salary is greater than $55,000.

```sql
-- Using the same Employees and Departments tables

SELECT d.DepartmentName, AvgSalary
FROM (SELECT DepartmentID, AVG(Salary) AS AvgSalary FROM Employees GROUP BY DepartmentID) AS DepartmentAvgSalaries
JOIN Departments d ON DepartmentAvgSalaries.DepartmentID = d.DepartmentID
WHERE AvgSalary > 55000;
```

**Explanation:**
1. The subquery `(SELECT DepartmentID, AVG(Salary) AS AvgSalary FROM Employees GROUP BY DepartmentID)` is a table subquery that calculates the average salary for each department. This is used as a derived table aliased as `DepartmentAvgSalaries`.
2. The outer query joins `DepartmentAvgSalaries` with the `Departments` table to get the `DepartmentName` and filters the result to include only departments where `AvgSalary` is greater than 55000.

---

#### 6.3 Set Operations: UNION, INTERSECT, EXCEPT

Set operations are used to combine the results of two or more SELECT queries into a single result set. SQL provides three main set operators:

- **UNION:** Combines the result sets of two or more queries and removes duplicate rows. `UNION ALL` includes duplicates.
- **INTERSECT:** Returns rows that are common to the result sets of two or more queries.
- **EXCEPT (or MINUS in some SQL dialects):** Returns rows from the first query's result set that are not present in the second query's result set.

**Rules for Set Operations:**
- All queries in a set operation must have the same number of columns.
- The corresponding columns in each query must have compatible data types.

**Example 6.3.1: UNION**

Let's say we have `EmployeesUS` and `EmployeesEU` tables and we want to get a list of all unique employee names from both regions.

```sql
-- Sample Tables:
-- EmployeesUS
-- EmployeeName
-- ------------
-- John Doe
-- Jane Smith

-- EmployeesEU
-- EmployeeName
-- ------------
-- Jane Smith
-- Peter Jones

SELECT EmployeeName FROM EmployeesUS
UNION
SELECT EmployeeName FROM EmployeesEU;

-- Result:
-- EmployeeName
-- ------------
-- John Doe
-- Jane Smith
-- Peter Jones
```

**Example 6.3.2: INTERSECT**

To find employee names that are in both `EmployeesUS` and `EmployeesEU` tables:

```sql
SELECT EmployeeName FROM EmployeesUS
INTERSECT
SELECT EmployeeName FROM EmployeesEU;

-- Result:
-- EmployeeName
-- ------------
-- Jane Smith
```

**Example 6.3.3: EXCEPT**

To find employee names that are in `EmployeesUS` but not in `EmployeesEU`:

```sql
SELECT EmployeeName FROM EmployeesUS
EXCEPT
SELECT EmployeeName FROM EmployeesEU;

-- Result:
-- EmployeeName
-- ------------
-- John Doe
```

---

#### 6.4 Nested Queries vs. Joins

Both nested queries and joins are used to combine data from multiple tables, but they approach it differently and are suited for different scenarios.

- **Joins:** Combine rows from two or more tables based on a related column between them. Joins are generally more efficient for retrieving related data across tables in a flat, denormalized way.

- **Nested Queries (Subqueries):** Used when you need to perform operations in steps, where the result of one query is used in another. Subqueries can sometimes be less efficient than joins, especially for simple relationships, but they can offer clearer logic for complex, multi-step data retrieval or filtering.

**When to use Subqueries:**
- When you need to filter rows based on an unknown value that is the result of an aggregate function (e.g., find employees who earn more than the average salary).
- When you need to check for existence or non-existence of rows (using `EXISTS` or `NOT EXISTS`).
- For set operations like `UNION`, `INTERSECT`, `EXCEPT`.

**When to use Joins:**
- When you need to combine columns from related tables in a single result set.
- For simple relationships between tables where performance is critical.
- When you are retrieving data that is naturally related and needs to be presented together.

In many cases, a query written with a subquery can also be written using a join, and vice versa. However, readability, maintainability, and performance considerations often dictate which approach is better suited for a particular situation.

---

#### 6.5 Practical Exercises

1. **Subquery in WHERE clause:**
   - Using the `Orders` and `Customers` tables, find all orders placed by customers from 'USA'. (Assume `Customers` table has `CustomerID`, `Country` and `Orders` table has `OrderID`, `CustomerID`).

2. **Scalar Subquery in SELECT clause:**
   - For each product in the `Products` table, display the product name and the average price of all products. (Assume `Products` table has `ProductName`, `Price`).

3. **Table Subquery in FROM clause:**
   - Find the departments that have more than 2 employees. (Use the `Employees` and `Departments` tables from previous examples).

4. **Set Operations:**
   - You have two tables, `ActiveCustomers` and `InactiveCustomers`. Using `UNION`, create a single list of all customers.
   - Using `INTERSECT`, find customers who appear in both `CustomersOnline` and `CustomersStore` tables.
   - Using `EXCEPT`, find customers who are in `CustomersMasterList` but not in `CustomersBlacklist`.

---

#### 6.6 Additional Considerations for Module 6

- **Performance of Subqueries:** Discuss the performance implications of subqueries, especially correlated subqueries (which execute once for each row of the outer query). Encourage students to be mindful of performance and consider if joins might be more efficient in some cases.
- **Readability and Maintainability:** Emphasize that while subqueries are powerful, they can make queries harder to read if overused or deeply nested. Encourage writing clear, well-formatted queries and using CTEs (Common Table Expressions - to be introduced in later modules) to improve readability for complex queries.
- **SQL Dialect Differences:** Note that some set operations and subquery syntax might have slight variations across different SQL databases (e.g., MySQL, PostgreSQL, SQL Server). Encourage students to consult the documentation for their specific DBMS.

By the end of this module, students should be comfortable writing and understanding subqueries and set operations, and be able to choose the appropriate technique for combining data from multiple queries effectively. They should also start to appreciate the trade-offs between different SQL constructs in terms of readability and performance.
