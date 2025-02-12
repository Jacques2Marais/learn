### [Module 9: Advanced SQL Features and Performance Optimization](https://github.com/Jacques2Marais/learn/blob/main/sql/chapter9.md) (coming soon)

**Description:**  
Delve into more advanced SQL topics such as window functions, common table expressions (CTEs), and performance tuning techniques. This module is designed to take students’ skills to the next level with modern SQL practices.

**Key Learnings:**
- Understand and use window functions (e.g., RANK, ROW_NUMBER, OVER).
- Write queries using common table expressions (CTEs) for improved readability.
- Explore strategies for query optimization and performance tuning.
- Learn how to use indexes and analyze query execution plans.

**Practical Examples:**
- Develop queries that calculate running totals, moving averages, and rankings.
- Exercises using CTEs to break down complex queries.
- Case studies analyzing and improving the performance of sample queries.

**Additional Considerations:**
- Provide tools and resources for monitoring query performance.
- Include interactive sessions where students optimize provided queries.
- Emphasize the importance of writing readable, maintainable code even in advanced scenarios.

---

#### 9.1 Introduction to Advanced SQL Features and Performance Optimization

As you become more proficient in SQL, you'll encounter scenarios that require more advanced querying techniques and a focus on performance. This module introduces window functions and Common Table Expressions (CTEs) to enhance your querying capabilities, and explores methods for optimizing SQL query performance.

---

#### 9.2 Window Functions: Performing Calculations Across Sets of Rows

Window functions perform calculations across a set of rows that are related to the current row. Unlike aggregate functions that group rows into a single summary row, window functions operate on a "window" of rows and return a value for each row in the original query.

**Key Window Functions:**

- **Ranking Functions:** `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` - Assign ranks to rows within a partition.
- **Value Functions:** `LEAD()`, `LAG()`, `FIRST_VALUE()`, `LAST_VALUE()` - Access values from other rows in the same result set.
- **Aggregate Functions as Window Functions:** `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()` - Calculate aggregates over a window of rows.

**Syntax for Window Functions:**

```sql
window_function(expression) OVER (
    [PARTITION BY column1, column2, ...]
    [ORDER BY column3, column4, ...]
    [frame_clause]
)
```

- **window_function:** The name of the window function (e.g., `RANK()`, `SUM()`).
- **expression:** The column or expression on which the function operates (optional for some functions like `RANK()`).
- **OVER clause:** Defines the window of rows on which the function operates.
    - **PARTITION BY:** Divides the rows into partitions based on specified columns. The window function is applied to each partition independently.
    - **ORDER BY:** Defines the order of rows within each partition. Many window functions are order-sensitive.
    - **frame_clause:** (Optional) Defines a subset of rows within a partition, forming a "frame" (e.g., `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`).

**Example 9.2.1: Using RANK() to Rank Employees by Salary within Departments**

Let's rank employees by salary within each department using the `Employees` table.

```sql
-- Sample Employees Table (extended)
-- EmployeeID | EmployeeName | DepartmentID | Salary
-- -----------|--------------|-------------|--------
-- 1          | John Doe     | 1            | 50000
-- 2          | Jane Smith   | 2            | 60000
-- 3          | Peter Jones  | 1            | 55000
-- 4          | Alice Brown  | 2            | 70000
-- 5          | Bob White    | 1            | 55000

SELECT 
    EmployeeName,
    DepartmentID,
    Salary,
    RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS SalaryRank
FROM Employees;

-- Result:
-- EmployeeName | DepartmentID | Salary | SalaryRank
-- -------------|--------------|--------|------------
-- Peter Jones  | 1            | 55000  | 1
-- Bob White    | 1            | 55000  | 1
-- John Doe     | 1            | 50000  | 3
-- Alice Brown  | 2            | 70000  | 1
-- Jane Smith   | 2            | 60000  | 2
```

**Explanation:**
- `RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC)` calculates the rank of each employee's salary within their department.
    - `PARTITION BY DepartmentID` divides employees into partitions by `DepartmentID`.
    - `ORDER BY Salary DESC` orders employees within each department partition by `Salary` in descending order.
    - `RANK()` assigns a rank based on the order. Employees with the same salary in the same department get the same rank, and the next rank is skipped.

**Example 9.2.2: Using SUM() as a Window Function to Calculate Running Total of Sales**

Let's calculate the running total of sales over order dates using an `Orders` table.

```sql
-- Sample Orders Table
-- OrderID | OrderDate  | SalesAmount
-- --------|------------|------------
-- 1       | 2023-01-01 | 100
-- 2       | 2023-01-01 | 150
-- 3       | 2023-01-02 | 200
-- 4       | 2023-01-03 | 120

SELECT 
    OrderDate,
    SalesAmount,
    SUM(SalesAmount) OVER (ORDER BY OrderDate) AS RunningTotalSales
FROM Orders;

-- Result:
-- OrderDate  | SalesAmount | RunningTotalSales
-- -----------|-------------|-----------------
-- 2023-01-01 | 100         | 100
-- 2023-01-01 | 150         | 250
-- 2023-01-02 | 200         | 450
-- 2023-01-03 | 120         | 570
```

**Explanation:**
- `SUM(SalesAmount) OVER (ORDER BY OrderDate)` calculates the cumulative sum of `SalesAmount` as we move through the ordered dates.
    - `ORDER BY OrderDate` specifies that the window should be ordered by `OrderDate`.
    - `SUM(SalesAmount)` calculates the sum of `SalesAmount` for all rows up to the current row in the ordered window.

---

#### 9.3 Common Table Expressions (CTEs): Simplifying Complex Queries

Common Table Expressions (CTEs) are temporary, named result sets that you can reference within a single SQL statement (e.g., `SELECT`, `INSERT`, `UPDATE`, `DELETE`). CTEs help break down complex queries into more manageable and readable parts. They are defined using the `WITH` clause.

**Syntax for CTEs:**

```sql
WITH CTE_name AS (
    -- CTE query definition
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition
)
-- Main query that uses the CTE
SELECT column1, column2, ...
FROM CTE_name
WHERE condition;
```

- **WITH CTE_name AS (...):** Defines a CTE named `CTE_name`. The query inside the parentheses is the CTE query definition.
- **CTE query definition:** A `SELECT` statement that defines the result set for the CTE.
- **Main query:** The primary query that can reference the CTE as if it were a regular table.

**Example 9.3.1: Using CTE to Find Departments with Above Average Salary**

Let's find departments where the average salary is greater than the overall average salary using a CTE.

```sql
-- Using Employees and Departments tables

WITH DepartmentAvgSalaries AS (
    SELECT DepartmentID, AVG(Salary) AS AvgSalary
    FROM Employees
    GROUP BY DepartmentID
),
OverallAvgSalary AS (
    SELECT AVG(Salary) AS OverallAvg FROM Employees
)
SELECT 
    d.DepartmentName,
    das.AvgSalary
FROM DepartmentAvgSalaries das
JOIN Departments d ON das.DepartmentID = d.DepartmentID
JOIN OverallAvgSalary oas ON 1=1 -- Cross join to access OverallAvgSalary
WHERE das.AvgSalary > oas.OverallAvg;
```

**Explanation:**
1. **`DepartmentAvgSalaries` CTE:** Calculates the average salary for each department.
2. **`OverallAvgSalary` CTE:** Calculates the overall average salary across all employees.
3. **Main Query:**
   - Joins `DepartmentAvgSalaries` with `Departments` to get department names.
   - Cross joins with `OverallAvgSalary` to access the overall average salary.
   - Filters departments where `AvgSalary` is greater than `OverallAvg`.

**Benefits of CTEs:**

- **Readability:** Break down complex logic into smaller, named parts, making queries easier to understand and maintain.
- **Reusability:** CTEs can be referenced multiple times within the main query or even in subsequent CTEs.
- **Recursion:** CTEs can be recursive, allowing you to query hierarchical data (more advanced use case).
- **Organization:** Improve the structure of complex queries, making them more modular.

---

#### 9.4 Query Performance Optimization Techniques

Optimizing SQL query performance is crucial for ensuring applications are fast and responsive, especially with large datasets. Here are several techniques for query optimization:

1. **Use Indexes Effectively:**
   - Indexes speed up data retrieval by providing quick lookup paths.
   - Create indexes on columns frequently used in `WHERE` clauses, `JOIN` conditions, and `ORDER BY` clauses.
   - Avoid indexing columns that are frequently updated, as index maintenance can add overhead to write operations.
   - Use composite indexes for queries that filter or sort on multiple columns.

2. **Optimize `WHERE` Clause:**
   - Filter data as early as possible in the query to reduce the amount of data processed.
   - Avoid using functions in `WHERE` clauses on indexed columns (e.g., `WHERE UPPER(column) = 'VALUE'`), as it can prevent index usage.
   - Use specific conditions instead of `OR` conditions where possible, as `OR` can sometimes hinder index usage. Consider using `UNION ALL` as an alternative to `OR` in some cases.

3. **Optimize `JOIN` Operations:**
   - Ensure join columns are indexed.
   - Use appropriate join types. `INNER JOIN` is generally faster than `LEFT JOIN` or `RIGHT JOIN` if you don't need to preserve all rows from one table.
   - Be mindful of join order, especially in complex queries. The database optimizer usually handles this, but in some cases, specifying join order can help.

4. **Avoid `SELECT *`:**
   - Explicitly list the columns you need in your `SELECT` clause instead of using `SELECT *`. This reduces the amount of data transferred from the database to the application and can improve performance, especially for wide tables.

5. **Limit Results with `LIMIT`:**
   - Use `LIMIT` (or `TOP` in SQL Server) to retrieve only a subset of rows when you don't need all of them (e.g., for pagination or previewing data).

6. **Use `EXPLAIN PLAN` to Analyze Queries:**
   - Most database systems provide a tool (e.g., `EXPLAIN PLAN` in Oracle, `EXPLAIN` in MySQL and PostgreSQL) to analyze the execution plan of a query.
   - `EXPLAIN PLAN` shows how the database optimizer intends to execute the query, including index usage, join methods, and order of operations.
   - Use `EXPLAIN PLAN` to identify performance bottlenecks and areas for optimization.

7. **Optimize Data Types:**
   - Use the most appropriate and efficient data types for your columns. Smaller data types (e.g., `SMALLINT` instead of `BIGINT` if the range allows) can save storage space and improve performance.

8. **Regularly Update Statistics:**
   - Database optimizers rely on statistics about data distribution to make efficient query execution plans.
   - Regularly update table and index statistics, especially after significant data changes (inserts, updates, deletes).

9. **Consider Denormalization (with Caution):**
    - In read-heavy applications, denormalization (adding some redundancy to reduce the need for joins) can sometimes improve read performance. However, it can complicate data maintenance and increase storage costs, so it should be done judiciously.

10. **Query Caching:**
    - Many database systems and application frameworks support query caching. If the same query is executed repeatedly, caching can significantly reduce database load and response time by serving results from the cache.

---

#### 9.5 Analyzing Query Execution Plans with `EXPLAIN PLAN`

The `EXPLAIN PLAN` (or similar commands like `EXPLAIN` in MySQL and PostgreSQL) is a powerful tool for understanding how the database executes your SQL queries. It provides insights into:

- **Index Usage:** Whether indexes are being used and which ones.
- **Join Methods:** The types of joins being used (e.g., nested loop join, hash join, merge join).
- **Order of Operations:** The sequence in which tables are accessed and operations are performed.
- **Estimated Costs:** The optimizer's estimate of the resources (e.g., time, I/O) required to execute different parts of the query.

**Example 9.5.1: Using `EXPLAIN` in PostgreSQL**

```sql
EXPLAIN SELECT * FROM Orders WHERE CustomerID = 123 ORDER BY OrderDate DESC LIMIT 10;
```

The output of `EXPLAIN` will be a plan describing the steps PostgreSQL will take to execute this query. The plan typically shows operations like:

- **Seq Scan:** Sequential scan of a table (usually less efficient for large tables).
- **Index Scan:** Using an index to retrieve rows (more efficient if indexes are properly used).
- **Sort:** Sorting operation.
- **Limit:** Limiting the number of returned rows.
- **Join Type (e.g., Hash Join, Merge Join, Nested Loop):** The algorithm used for joining tables.

By analyzing the `EXPLAIN PLAN` output, you can identify potential performance bottlenecks. For example, if you see a "Seq Scan" on a large table where you expect an index to be used, it indicates a need to review your indexes or query conditions. If you see inefficient join types or sort operations on large datasets, you can consider rewriting the query or adjusting indexes to improve performance.

---

#### 9.6 Practical Exercises

1. **Window Function Exercise:**
   - Using the `Sales` table (with columns `SaleID`, `ProductID`, `SaleDate`, `SaleAmount`), calculate the moving average of `SaleAmount` over the last 3 sales for each product, ordered by `SaleDate`.

2. **CTE Exercise:**
   - Using the `Employees` and `Departments` tables, find all employees who belong to departments located in 'New York'. Assume `Departments` table has a `Location` column. Use a CTE to first filter departments in 'New York', and then join with `Employees`.

3. **Query Optimization Exercise:**
   - Analyze a given slow-performing SQL query using `EXPLAIN PLAN` (or `EXPLAIN`). Identify potential bottlenecks and suggest optimization techniques (e.g., adding indexes, rewriting `WHERE` clause, optimizing joins). Implement your suggested optimizations and compare the execution plan and performance before and after optimization. (Note: You'll need access to a database system to run `EXPLAIN PLAN` and measure performance).

---

#### 9.7 Additional Considerations for Module 9

- **Database System Specifics:** Performance optimization techniques can be database system-specific. What works well in one system (e.g., MySQL) might not be as effective in another (e.g., PostgreSQL or SQL Server). Encourage students to learn about the specific optimization features and tools of their chosen database system.
- **Real-World Performance Testing:** Emphasize the importance of testing query performance in real-world scenarios with realistic data volumes and concurrency. Performance in development or test environments might not always reflect production performance.
- **Continuous Monitoring and Tuning:** Performance optimization is an ongoing process. Encourage students to monitor query performance regularly and tune queries and database configurations as needed, especially as data volumes grow and application requirements change.
- **Balance Readability and Performance:** While performance is crucial, also emphasize the importance of writing readable and maintainable SQL code. Sometimes, a slightly less performant but more readable query might be preferable to a highly optimized but cryptic one, especially in team environments.
- **Further Learning Resources:** Provide links to documentation, articles, and tools for advanced SQL performance tuning for different database systems.

By the end of this module, students should be able to use window functions and CTEs to write more sophisticated and efficient SQL queries. They will also have a foundational understanding of SQL query performance optimization techniques and be able to use tools like `EXPLAIN PLAN` to analyze and improve query performance. They will appreciate the importance of writing not only correct but also performant SQL queries for real-world applications.
