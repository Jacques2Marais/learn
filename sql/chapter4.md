**Module 4: Data Aggregation and Grouping**

In this module, we will explore how to summarize and extract meaningful insights from large datasets using SQL's aggregation capabilities. By the end of this chapter, you'll be adept at using aggregate functions, grouping data, and filtering grouped data to answer complex analytical questions.

**Key Learnings:**

- Master aggregate functions and understand when to use them.
- Learn to group data with `GROUP BY`.
- Use the `HAVING` clause to filter groups.
- Recognize common pitfalls when aggregating data (such as forgetting to group by non-aggregated columns).

**Aggregate Functions:**

Aggregate functions perform calculations on multiple rows of a table's column and return a single value. The most commonly used aggregate functions in SQL are:

- **`COUNT()`**: Returns the number of rows that match a specified criterion.
- **`SUM()`**: Calculates the total sum of a numeric column.
- **`AVG()`**: Computes the average value of a numeric column.
- **`MIN()`**: Finds the minimum value in a set.
- **`MAX()`**: Finds the maximum value in a set.

**Grouping Data with `GROUP BY`:**

The `GROUP BY` statement groups rows that have the same values into summary rows. It's often used with aggregate functions to group the result set by one or more columns.

**Syntax:**

```sql
SELECT column_name(s), aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name(s);
```

**Example:**

Suppose we have a `Sales` table:

| OrderID | ProductID | Quantity | Price | Region  |
|---------|-----------|----------|-------|---------|
| 1       | 101       | 2        | 10.00 | East    |
| 2       | 102       | 1        | 20.00 | West    |
| 3       | 101       | 1        | 10.00 | East    |
| 4       | 103       | 5        | 5.00  | North   |
| 5       | 102       | 3        | 20.00 | West    |

To find the total quantity sold per product:

```sql
SELECT ProductID, SUM(Quantity) AS TotalQuantity
FROM Sales
GROUP BY ProductID;
```

Result:

| ProductID | TotalQuantity |
|-----------|---------------|
| 101       | 3             |
| 102       | 4             |
| 103       | 5             |

**Filtering Groups with `HAVING`:**

While the `WHERE` clause filters rows before grouping, the `HAVING` clause filters groups after aggregation. This is essential when you want to apply conditions to aggregated data.

**Syntax:**

```sql
SELECT column_name(s), aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING aggregate_function(column_name) condition;
```

**Example:**

To find products with a total quantity sold greater than 3:

```sql
SELECT ProductID, SUM(Quantity) AS TotalQuantity
FROM Sales
GROUP BY ProductID
HAVING SUM(Quantity) > 3;
```

Result:

| ProductID | TotalQuantity |
|-----------|---------------|
| 102       | 4             |
| 103       | 5             |

**Common Pitfalls:**

- **Not Grouping Non-Aggregated Columns:** Every column in the `SELECT` statement that isn't an aggregate function must be included in the `GROUP BY` clause.

  Incorrect:

  ```sql
  SELECT ProductID, Quantity, SUM(Price)
  FROM Sales
  GROUP BY ProductID;
  ```

  Correct:

  ```sql
  SELECT ProductID, SUM(Quantity), SUM(Price)
  FROM Sales
  GROUP BY ProductID;
  ```

- **Using `HAVING` Without `GROUP BY`:** The `HAVING` clause is designed to work with grouped data. Using it without `GROUP BY` can lead to unexpected results.

**Practical Examples:**

1. **Total Sales by Region:**

   ```sql
   SELECT Region, SUM(Quantity * Price) AS TotalSales
   FROM Sales
   GROUP BY Region;
   ```

2. **Average Order Quantity per Product:**

   ```sql
   SELECT ProductID, AVG(Quantity) AS AvgQuantity
   FROM Sales
   GROUP BY ProductID;
   ```

3. **Regions with Total Sales Above $50:**

   ```sql
   SELECT Region, SUM(Quantity * Price) AS TotalSales
   FROM Sales
   GROUP BY Region
   HAVING SUM(Quantity * Price) > 50;
   ```

**Visualizing Grouped Data:**

Visual aids can enhance understanding. For instance, bar charts can represent total sales by region, making it easier to compare performance across regions.

**Exercises:**

1. **Calculate Total Revenue per Product:**

   Using the `Sales` table, write a query to display each `ProductID` with its total revenue (`Quantity * Price`).

2. **Identify Products with Average Quantity Sold Greater Than 2:**

   List `ProductID`s where the average quantity sold is more than 2.

3. **Find Regions with More Than 3 Orders:**

   Display regions that have more than three orders.

**Conclusion:**

Mastering data aggregation and grouping is crucial for effective data analysis in SQL. These techniques 

[Next chapter >>](https://github.com/Jacques2Marais/learn/blob/main/sql/chapter5.md)
