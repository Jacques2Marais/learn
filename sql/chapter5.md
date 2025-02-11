# Module 5: Joins and Relationships Between Tables

Welcome to Module 5! In this chapter, we'll dive into one of the most powerful features of SQL: combining data from multiple tables using **joins**. Understanding how to link tables together is essential for working with relational databases, where data is logically split into separate tables to reduce redundancy and improve organization.

## 5.1 Understanding Table Relationships

Before we delve into joins, it's important to grasp how tables can relate to one another.

### 5.1.1 Primary Keys and Foreign Keys

- **Primary Key**: A column (or set of columns) whose values uniquely identify each row in a table.
- **Foreign Key**: A column (or set of columns) that establishes a link between data in two tables. It references the primary key in another table.

**Example**:

Consider two tables:

- **Customers**
  - `customer_id` (Primary Key)
  - `name`
  - `email`
- **Orders**
  - `order_id` (Primary Key)
  - `customer_id` (Foreign Key)
  - `order_date`
  - `amount`

Here, `customer_id` in the Orders table is a foreign key linking back to the Customers table.

### 5.1.2 Types of Relationships

- **One-to-One**: Each row in Table A relates to one row in Table B.
- **One-to-Many**: Each row in Table A relates to multiple rows in Table B.
- **Many-to-Many**: Multiple rows in Table A relate to multiple rows in Table B (usually implemented with a junction table).

## 5.2 Introduction to Joins

A **join** combines columns from one or more tables based on related columns between them.

### 5.2.1 The JOIN Clause

Basic syntax:

```sql
SELECT columns
FROM table1
JOIN table2 ON table1.column_name = table2.column_name;
```

## 5.3 Types of Joins

### 5.3.1 INNER JOIN

Returns records that have matching values in both tables.

**Syntax**:

```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;
```

**Venn Diagram Illustration**:

```
[Table1] ∩ [Table2]
```

**Example**:

Retrieve a list of all customer orders:

```sql
SELECT Customers.name, Orders.order_date, Orders.amount
FROM Customers
INNER JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

### 5.3.2 LEFT JOIN (or LEFT OUTER JOIN)

Returns all records from the left table, and the matched records from the right table. If there's no match, the result is NULL on the right side.

**Syntax**:

```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;
```

**Venn Diagram Illustration**:

```
[Table1] ⊃ [Table2]
```

**Example**:

Get all customers and their orders (including customers with no orders):

```sql
SELECT Customers.name, Orders.order_date, Orders.amount
FROM Customers
LEFT JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

### 5.3.3 RIGHT JOIN (or RIGHT OUTER JOIN)

Returns all records from the right table, and the matched records from the left table. If there's no match, the result is NULL on the left side.

**Syntax**:

```sql
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.column_name = table2.column_name;
```

**Venn Diagram Illustration**:

```
[Table1] ⊂ [Table2]
```

**Example**:

Get all orders and their customers (including orders without customer information):

```sql
SELECT Customers.name, Orders.order_date, Orders.amount
FROM Customers
RIGHT JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

### 5.3.4 FULL OUTER JOIN

Returns all records when there is a match in either left or right table. If there are no matches, missing values are filled with NULLs.

**Syntax**:

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
```

**Venn Diagram Illustration**:

```
[Table1] ∪ [Table2]
```

**Example**:

Get a comprehensive list of customers and orders, whether or not they have matching records:

```sql
SELECT Customers.name, Orders.order_date, Orders.amount
FROM Customers
FULL OUTER JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

**Note**: Not all database systems support FULL OUTER JOIN. An alternative is to use a UNION of LEFT and RIGHT JOINs.

## 5.4 Practical Examples

### 5.4.1 Joining Customers and Orders

Let's explore how joins work with practical examples.

#### Example Tables

**Customers**:

| customer_id | name         | email            |
|-------------|--------------|------------------|
| 1           | Alice Smith  | alice@example.com|
| 2           | Bob Johnson  | bob@example.com  |
| 3           | Carol Davis  | carol@example.com|

**Orders**:

| order_id | customer_id | order_date | amount |
|----------|-------------|------------|--------|
| 101      | 1           | 2023-01-15 | 250    |
| 102      | 1           | 2023-02-20 | 150    |
| 103      | 2           | 2023-03-05 | 300    |
| 104      | 4           | 2023-04-12 | 200    |

#### INNER JOIN Example

```sql
SELECT Customers.name, Orders.order_date, Orders.amount
FROM Customers
INNER JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

**Result**:

| name        | order_date | amount |
|-------------|------------|--------|
| Alice Smith | 2023-01-15 | 250    |
| Alice Smith | 2023-02-20 | 150    |
| Bob Johnson | 2023-03-05 | 300    |

*Note*: Only customers with matching orders are included.

#### LEFT JOIN Example

```sql
SELECT Customers.name, Orders.order_date, Orders.amount
FROM Customers
LEFT JOIN Orders ON Customers.customer_id = Orders.customer_id;
```

**Result**:

| name        | order_date | amount |
|-------------|------------|--------|
| Alice Smith | 2023-01-15 | 250    |
| Alice Smith | 2023-02-20 | 150    |
| Bob Johnson | 2023-03-05 | 300    |
| Carol Davis | NULL       | NULL   |

*Note*: Includes all customers, even those without orders.

### 5.4.2 Visualizing Joins with Venn Diagrams

Understanding joins can be made easier with Venn diagrams.

#### INNER JOIN Venn Diagram

```
   _________
  /         \
 /   A ∩ B   \
/_____________\
```

#### LEFT JOIN Venn Diagram

```
   _________
  /         \
 /   A       \
/_____________\
```

#### RIGHT JOIN Venn Diagram

```
   _________
  /         \
 /       B   \
/_____________\
```

#### FULL OUTER JOIN Venn Diagram

```
   _________
  /         \
 /   A ∪ B   \
/_____________\
```

### 5.4.3 Real-World Scenario: Linking User Profiles to Activity Logs

Suppose you have:

- **Users** table with all registered users.
- **ActivityLogs** table recording user activities.

To retrieve a list of all users and their recent activities:

```sql
SELECT Users.username, ActivityLogs.action, ActivityLogs.timestamp
FROM Users
LEFT JOIN ActivityLogs ON Users.user_id = ActivityLogs.user_id;
```

## 5.5 Performance Considerations

### 5.5.1 Impact on Query Performance

- **Indexes**: Ensure that columns used in joins are indexed to speed up queries.
- **Data Volume**: Joining large tables can be resource-intensive.
- **Join Order and Strategies**: The way tables are joined can affect performance.

### 5.5.2 Best Practices

- **Limit Data Retrieval**: Select only necessary columns.
- **Filter Early**: Use WHERE clauses to filter data before joining when possible.
- **Understand Execution Plans**: Analyze how the database executes your query.

## 5.6 Additional Tips

### 5.6.1 Comparing Join Types Side by Side

| Join Type   | Includes Rows from | Includes Unmatched Rows |
|-------------|--------------------|-------------------------|
| INNER JOIN  | Both Tables        | No                      |
| LEFT JOIN   | Left Table         | Yes (Right = NULL)      |
| RIGHT JOIN  | Right Table        | Yes (Left = NULL)       |
| FULL JOIN   | Both Tables        | Yes (Both Sides = NULL) |

### 5.6.2 Experiment with Joins

Use an interactive SQL environment like [SQLite Online](https://sqliteonline.com/) to practice:

- Modify join conditions.
- Observe how result sets change.
- Try combining multiple joins in one query.

### 5.6.3 Common Mistakes to Avoid

- **Ambiguous Column Names**: When columns have the same name in both tables, prefix them with the table name or alias.
- **Forgetting Join Conditions**: Omitting the ON clause can result in a Cartesian product (every combination of rows).
- **Assuming Data Matches Exactly**: Be cautious of NULLs and data inconsistencies.

## 5.7 Summary

In this module, we've explored how to:

- Understand the importance of primary and foreign keys in defining table relationships.
- Differentiate between various types of joins and their use cases.
- Write SQL queries that combine data from multiple tables effectively.
- Consider the performance implications of joining tables.

By mastering joins, you're now equipped to handle complex queries involving multiple tables, unlocking the full potential of relational databases.

---

## What's Next?

Looking ahead, we'll explore **subqueries and nested queries** in Module 6, allowing you to perform even more sophisticated data retrieval and analysis.

## Challenge Yourself!

- **Practical Exercise**: Given the following tables, write queries using different joins to answer specific questions.
  - Tables: `Employees`, `Departments`, `Salaries`
- **Real-World Application**: Think of a dataset you're interested in (e.g., books and authors, movies and directors) and sketch out how you'd model it with tables and joins.

---

**Remember**: Practice is key to becoming proficient in SQL. Don't hesitate to experiment with queries and explore how joins can help you answer complex data questions.
