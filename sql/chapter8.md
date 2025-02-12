### [Module 8: Database Schema Design and Data Definition Language (DDL)](https://github.com/Jacques2Marais/learn/blob/main/sql/chapter8.md) (coming soon)

**Description:**  
Focus on creating and modifying the structure of a database. This module teaches students how to design schemas, define tables, and set constraints to ensure data quality and integrity.

**Key Learnings:**
- Use DDL statements such as CREATE, ALTER, and DROP.
- Define table structures with appropriate data types and constraints.
- Understand the importance of normalization and its impact on design.
- Learn to design relationships between tables using keys and indexes.

**Practical Examples:**
- Create a sample database schema for a fictional business (e.g., an e-commerce platform).
- Exercises on adding constraints such as PRIMARY KEY, FOREIGN KEY, UNIQUE, and NOT NULL.
- Step-by-step walkthrough of normalizing a dataset to eliminate redundancy.

**Additional Considerations:**
- Include diagrams to illustrate schema design and table relationships.
- Discuss trade-offs between normalization and performance.
- Provide guidelines on how to approach schema design in real-world applications.

---

#### 8.1 Introduction to Database Schema Design and DDL

Database schema design is the process of creating a blueprint for how data will be organized and structured within a database. A well-designed schema is crucial for efficient data storage, retrieval, and maintenance. Data Definition Language (DDL) is the subset of SQL used to create and modify database objects such as tables, indexes, and schemas.

Key DDL statements include:

- **CREATE:** To create database objects (tables, databases, indexes, views, etc.).
- **ALTER:** To modify the structure of existing database objects.
- **DROP:** To delete database objects.

Understanding DDL is fundamental for anyone involved in database administration or development, as it allows you to define the structure of your data.

---

#### 8.2 CREATE Statement: Building Database Objects

The `CREATE` statement is used to create various database objects. The most common use is creating tables.

**8.2.1 CREATE TABLE Statement**

The `CREATE TABLE` statement defines a new table in the database, specifying column names, data types, and constraints.

```sql
CREATE TABLE table_name (
    column1 datatype1 [constraint],
    column2 datatype2 [constraint],
    column3 datatype3 [constraint],
    ...
    [table_constraints]
);
```

- **table_name:** The name of the table to be created.
- **column_name:** The name of a column in the table.
- **datatype:** The data type of the column (e.g., INTEGER, VARCHAR, DATE).
- **constraint:** Optional rules enforced on the column or table (e.g., NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY).
- **table_constraints:** Constraints that apply to the whole table, not just a single column.

**Example 8.2.1: Creating a Customers Table**

Let's create a `Customers` table with columns for customer ID, name, email, and registration date.

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    RegistrationDate DATE DEFAULT CURRENT_DATE
);
```

**Explanation:**
- `CREATE TABLE Customers` creates a table named `Customers`.
- `CustomerID INT PRIMARY KEY`: Defines a column named `CustomerID` of integer type and sets it as the primary key. `PRIMARY KEY` implies `NOT NULL` and `UNIQUE`.
- `FirstName VARCHAR(50) NOT NULL`: Defines a column `FirstName` to store variable-length strings up to 50 characters and ensures it cannot be `NULL`.
- `LastName VARCHAR(50) NOT NULL`: Similar to `FirstName`, ensures last name is provided.
- `Email VARCHAR(100) UNIQUE`: Defines `Email` column for unique email addresses.
- `RegistrationDate DATE DEFAULT CURRENT_DATE`: Defines `RegistrationDate` of type DATE and sets the default value to the current date if not specified during insertion.

**8.2.2 Data Types in SQL**

SQL supports various data types. Common ones include:

- **Numeric Types:** `INT`, `INTEGER`, `SMALLINT`, `BIGINT`, `DECIMAL(precision, scale)`, `NUMERIC(precision, scale)`, `FLOAT`, `REAL`, `DOUBLE PRECISION`.
- **String Types:** `VARCHAR(length)`, `CHAR(length)`, `TEXT`.
- **Date and Time Types:** `DATE`, `TIME`, `DATETIME`, `TIMESTAMP`.
- **Boolean Type:** `BOOLEAN` (or `BOOL` in some systems).
- **Binary Types:** `BINARY`, `VARBINARY`, `BLOB` (Binary Large Object).

The specific data types available and their names can vary slightly between different database systems (e.g., MySQL, PostgreSQL, SQL Server).

**8.2.3 Constraints in SQL**

Constraints are rules enforced on data columns to ensure data integrity and accuracy. Common constraints are:

- **PRIMARY KEY:** Uniquely identifies each record in a table; must contain unique and non-null values.
- **FOREIGN KEY:** Establishes a link between data in two tables. A `FOREIGN KEY` in one table points to a `PRIMARY KEY` in another table.
- **UNIQUE:** Ensures that all values in a column are unique.
- **NOT NULL:** Ensures that a column cannot have a `NULL` value.
- **CHECK:** Defines a condition that must be true for all values in a column.
- **DEFAULT:** Specifies a default value for a column when no value is provided during insertion.

---

#### 8.3 ALTER Statement: Modifying Database Objects

The `ALTER` statement is used to modify the structure of existing database objects. For tables, `ALTER TABLE` is used to add, modify, or delete columns, constraints, and more.

**8.3.1 Adding a Column**

```sql
ALTER TABLE table_name
ADD COLUMN column_name datatype [constraint];
```

**Example 8.3.1: Adding a Phone Number Column**

Let's add a `PhoneNumber` column to the `Customers` table.

```sql
ALTER TABLE Customers
ADD COLUMN PhoneNumber VARCHAR(20);
```

**8.3.2 Modifying a Column**

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype [constraint]; -- MySQL syntax

ALTER TABLE table_name
ALTER COLUMN column_name TYPE datatype; -- PostgreSQL syntax

ALTER TABLE table_name
ALTER COLUMN column_name datatype; -- SQL Server syntax
```

**Example 8.3.2: Modifying Email Column Length**

Let's increase the length of the `Email` column in the `Customers` table to 255 characters.

```sql
ALTER TABLE Customers
MODIFY COLUMN Email VARCHAR(255) UNIQUE; -- MySQL syntax (example)
```

**8.3.3 Dropping a Column**

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

**Example 8.3.3: Dropping the Registration Date Column**

Let's remove the `RegistrationDate` column from the `Customers` table.

```sql
ALTER TABLE Customers
DROP COLUMN RegistrationDate;
```

**8.3.4 Adding and Dropping Constraints**

Constraints can also be added or dropped using `ALTER TABLE`.

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name constraint_definition;

ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

**Example 8.3.4: Adding a NOT NULL Constraint to PhoneNumber**

```sql
ALTER TABLE Customers
MODIFY COLUMN PhoneNumber VARCHAR(20) NOT NULL; -- MySQL - modifies and adds constraint
```

**Example 8.3.5: Adding a Foreign Key Constraint**

Assume we have an `Orders` table with a `CustomerID` column that should reference `Customers` table.

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    -- ... other columns
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

Or, to add it after table creation:

```sql
ALTER TABLE Orders
ADD FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID);
```

---

#### 8.4 DROP Statement: Deleting Database Objects

The `DROP` statement is used to delete database objects. Be very careful when using `DROP`, as it permanently removes objects and data.

**8.4.1 DROP TABLE Statement**

```sql
DROP TABLE table_name;
```

**Example 8.4.1: Dropping the Customers Table**

```sql
DROP TABLE Customers; -- This will delete the Customers table and all its data.
```

**Caution:** `DROP TABLE` is irreversible and will delete the table and all data within it. Always ensure you have backups or are certain about deleting a table.

**8.4.2 DROP DATABASE Statement**

```sql
DROP DATABASE database_name;
```

**Example 8.4.2: Dropping a Database**

```sql
DROP DATABASE MyDatabase; -- Deletes the entire database named 'MyDatabase'.
```

**Caution:** `DROP DATABASE` is even more critical as it deletes the entire database and all objects within it. Use with extreme caution.

---

#### 8.5 Database Normalization

Database normalization is the process of organizing data in a database to minimize redundancy and improve data integrity. It involves dividing larger tables into smaller tables and defining relationships between them. Normalization is typically achieved through a series of normal forms (1NF, 2NF, 3NF, BCNF, etc.). The most commonly used are the first three normal forms.

**8.5.1 First Normal Form (1NF)**

- Each column should contain atomic values (not divisible).
- No repeating groups of columns.

**8.5.2 Second Normal Form (2NF)**

- Must be in 1NF.
- All non-key attributes must be fully functionally dependent on the entire primary key. (Applies to tables with composite primary keys).

**8.5.3 Third Normal Form (3NF)**

- Must be in 2NF.
- No transitive dependencies. Non-key attributes should depend only on the primary key, not on other non-key attributes.

**Example 8.5.3: Normalization Example**

Consider an `Orders` table that is not normalized:

```
Orders Table (Unnormalized)
OrderID | CustomerID | CustomerName | CustomerAddress         | ProductID | ProductName | ProductPrice | OrderDate
--------|------------|--------------|-------------------------|-----------|-------------|--------------|------------
1001    | 1          | John Doe     | 123 Main St, Anytown    | 101       | Laptop      | 1200.00      | 2023-01-15
1001    | 1          | John Doe     | 123 Main St, Anytown    | 102       | Mouse       | 25.00        | 2023-01-15
1002    | 2          | Jane Smith   | 456 Oak Ave, Otherville | 201       | Keyboard    | 75.00        | 2023-01-20
```

**Normalization Steps:**

1. **1NF:** Already in 1NF as columns are atomic and no repeating groups.

2. **2NF:** Create separate tables for Customers and Products to remove redundancy.

   - **Customers Table:** `CustomerID (PK), CustomerName, CustomerAddress`
   - **Products Table:** `ProductID (PK), ProductName, ProductPrice`
   - **Orders Table:** `OrderID (PK), CustomerID (FK), OrderDate`
   - **OrderItems Table:** `OrderItemID (PK), OrderID (FK), ProductID (FK), Quantity` (To handle multiple products per order)

3. **3NF:** Check for transitive dependencies. In this example, CustomerName and CustomerAddress depend on CustomerID, and ProductName and ProductPrice depend on ProductID. The schema is already in 3NF.

**Normalized Schema:**

- **Customers Table:**
  `CustomerID INT PRIMARY KEY, CustomerName VARCHAR(100), CustomerAddress VARCHAR(255)`
- **Products Table:**
  `ProductID INT PRIMARY KEY, ProductName VARCHAR(100), ProductPrice DECIMAL(10, 2)`
- **Orders Table:**
  `OrderID INT PRIMARY KEY, CustomerID INT, OrderDate DATE, FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)`
- **OrderItems Table:**
  `OrderItemID INT PRIMARY KEY, OrderID INT, ProductID INT, Quantity INT, FOREIGN KEY (OrderID) REFERENCES Orders(OrderID), FOREIGN KEY (ProductID) REFERENCES Products(ProductID)`

---

#### 8.6 Keys and Indexes

**Keys:** Used to establish relationships between tables and ensure data integrity.
- **Primary Key:** Uniquely identifies records within a table.
- **Foreign Key:** Links to the primary key of another table, establishing relationships.
- **Unique Key:** Ensures uniqueness of values in a column or set of columns.
- **Composite Key:** A primary or unique key made up of multiple columns.

**Indexes:** Improve the speed of data retrieval operations. Indexes are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table.

- **Creating Indexes:**

  ```sql
  CREATE INDEX index_name
  ON table_name (column1, column2, ...);

  CREATE UNIQUE INDEX unique_index_name
  ON table_name (column1, column2, ...);
  ```

**Example 8.6.1: Creating an Index on Customer Last Name**

```sql
CREATE INDEX idx_customer_lastname
ON Customers (LastName);
```

This creates an index on the `LastName` column of the `Customers` table, which can speed up queries that filter or sort by last name.

---

#### 8.7 Practical Exercises

1. **CREATE TABLE Exercise:**
   - Create a table named `Employees` with columns: `EmployeeID` (INT, PRIMARY KEY), `FirstName` (VARCHAR(50), NOT NULL), `LastName` (VARCHAR(50), NOT NULL), `Department` (VARCHAR(100)), `Salary` (DECIMAL(10, 2)).

2. **ALTER TABLE Exercise:**
   - Add a column `HireDate` of type DATE to the `Employees` table.
   - Modify the `Salary` column in the `Employees` table to be of type `DECIMAL(12, 2)`.
   - Add a `NOT NULL` constraint to the `Department` column in the `Employees` table.
   - Drop the `Department` column from the `Employees` table.

3. **DROP TABLE Exercise:**
   - Drop the `Employees` table created in exercise 1.

4. **Normalization Exercise:**
   - Take an unnormalized table (e.g., a table storing student course information with repeating course details) and describe the steps to normalize it to at least 3NF. Define the tables and relationships in the normalized schema.

5. **Indexes Exercise:**
   - Create an index on the `LastName` and `FirstName` columns of the `Customers` table to improve query performance for searching customers by name.

---

#### 8.8 Additional Considerations for Module 8

- **Schema Design Tools:** Introduce database design tools (e.g., ER diagram tools) that help visualize and design database schemas.
- **Trade-offs of Normalization:** Discuss the benefits of normalization (reduced redundancy, improved integrity) and potential drawbacks (increased complexity, potential performance overhead due to joins).
- **Denormalization:** Briefly introduce denormalization as a technique to improve read performance in certain scenarios by adding redundancy back into the schema (trade-off between read and write performance).
- **Database Design Best Practices:** Provide guidelines for designing effective database schemas, including choosing appropriate data types, using constraints effectively, and considering scalability and performance.
- **SQL Dialect Variations:** Remind students that DDL syntax can have slight variations across different SQL database systems. Always refer to the specific DBMS documentation for precise syntax and available options.

By the end of this module, students should be able to design and implement database schemas using DDL statements. They will understand how to create, alter, and drop tables, define data types and constraints, and apply normalization principles to design efficient and robust database structures. They will also appreciate the importance of keys and indexes for data relationships and performance optimization.
