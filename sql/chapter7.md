### [Module 7: Data Modification and Transaction Control](https://github.com/Jacques2Marais/learn/blob/main/sql/chapter7.md) (coming soon)

**Description:**  
Learn how to modify data within a database safely and reliably. This module covers data manipulation (INSERT, UPDATE, DELETE) and introduces transaction control to maintain data integrity during operations.

**Key Learnings:**
- Write queries to insert, update, and delete records.
- Understand the importance of transactions and ACID properties.
- Practice using COMMIT and ROLLBACK to control data changes.
- Recognize best practices for managing data integrity.

**Practical Examples:**
- Exercises to add new records to a “Products” table.
- Simulated scenarios where students update and then rollback changes.
- Lab activities involving the creation of transactions and testing their behavior.

**Additional Considerations:**
- Emphasize safe data manipulation techniques and backups.
- Introduce tools or simulators that allow safe experimentation with live data.
- Discuss real-world scenarios where transaction management is critical (e.g., banking systems).

---

#### 7.1 Introduction to Data Modification

SQL is not just for retrieving data; it's also crucial for modifying data within databases. Data modification involves three primary operations:

- **INSERT:** Adding new records into a table.
- **UPDATE:** Modifying existing records in a table.
- **DELETE:** Removing records from a table.

These operations are part of Data Manipulation Language (DML) in SQL. It's essential to use these commands carefully, as they directly alter the data stored in your database.

---

#### 7.2 INSERT Statement: Adding New Records

The `INSERT` statement is used to add new rows to a table. There are two main forms of the `INSERT` statement:

1. **Inserting values into all columns:**

   ```sql
   INSERT INTO table_name
   VALUES (value1, value2, value3, ...);
   ```

   In this form, you must provide values for all columns in the table in the order they are defined.

2. **Inserting values into specific columns:**

   ```sql
   INSERT INTO table_name (column1, column2, column3, ...)
   VALUES (value1, value2, value3, ...);
   ```

   This form allows you to specify the columns you are inserting data into. Columns not listed will receive default values or `NULL` if no default is specified.

**Example 7.2.1: Inserting into Products table**

Let's assume we have a `Products` table with columns: `ProductID`, `ProductName`, `Category`, and `Price`.

```sql
-- Sample Products Table Structure:
-- ProductID INTEGER, ProductName VARCHAR, Category VARCHAR, Price DECIMAL

INSERT INTO Products (ProductID, ProductName, Category, Price)
VALUES (101, 'Laptop', 'Electronics', 1200.00);

INSERT INTO Products (ProductName, Price, ProductID, Category) -- Column order doesn't matter if specified
VALUES ('Mouse', 25.00, 102, 'Electronics');

INSERT INTO Products (ProductName, Price) -- Inserting into specific columns
VALUES ('Keyboard', 75.00); -- ProductID and Category will be NULL or default values if defined
```

**Explanation:**
- The first `INSERT` statement adds a new product, 'Laptop', specifying values for all four columns.
- The second `INSERT` demonstrates that the order of columns in the `INSERT INTO` clause can be different from the table definition, as long as the `VALUES` are in the corresponding order.
- The third `INSERT` shows inserting data into only `ProductName` and `Price` columns. `ProductID` and `Category` will be set to `NULL` (assuming no default values are defined for these columns).

---

#### 7.3 UPDATE Statement: Modifying Existing Records

The `UPDATE` statement is used to modify existing records in a table. It's crucial to use the `WHERE` clause with `UPDATE` to specify which rows should be updated; otherwise, all rows in the table will be affected.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Example 7.3.1: Updating Product Price**

Let's say we need to increase the price of 'Laptop' in the `Products` table by 10%.

```sql
-- Sample Products Table (before update):
-- ProductID | ProductName | Category    | Price
-- -----------|-------------|-------------|--------
-- 101        | Laptop      | Electronics | 1200.00

UPDATE Products
SET Price = Price * 1.10
WHERE ProductName = 'Laptop';

-- Sample Products Table (after update):
-- ProductID | ProductName | Category    | Price
-- -----------|-------------|-------------|--------
-- 101        | Laptop      | Electronics | 1320.00
```

**Explanation:**
- The `UPDATE Products` statement specifies the table to be updated.
- `SET Price = Price * 1.10` sets the new value for the `Price` column by increasing the current price by 10%.
- `WHERE ProductName = 'Laptop'` ensures that only the row where `ProductName` is 'Laptop' is updated.

**Caution:** Forgetting the `WHERE` clause in an `UPDATE` statement will result in updating the `Price` for all products in the table, which is likely not the intended outcome.

---

#### 7.4 DELETE Statement: Removing Records

The `DELETE` statement is used to remove rows from a table. Similar to `UPDATE`, it's vital to use a `WHERE` clause to specify which rows to delete. Omitting the `WHERE` clause will delete all rows from the table.

```sql
DELETE FROM table_name
WHERE condition;
```

**Example 7.4.1: Deleting a Product**

Suppose we want to remove the 'Mouse' product from the `Products` table.

```sql
-- Sample Products Table (before delete):
-- ProductID | ProductName | Category    | Price
-- -----------|-------------|-------------|--------
-- 101        | Laptop      | Electronics | 1320.00
-- 102        | Mouse       | Electronics | 25.00

DELETE FROM Products
WHERE ProductName = 'Mouse';

-- Sample Products Table (after delete):
-- ProductID | ProductName | Category    | Price
-- -----------|-------------|-------------|--------
-- 101        | Laptop      | Electronics | 1320.00
```

**Explanation:**
- `DELETE FROM Products` specifies the table from which rows will be deleted.
- `WHERE ProductName = 'Mouse'` condition ensures that only the row where `ProductName` is 'Mouse' is deleted.

**Caution:**  Executing `DELETE FROM Products;` without a `WHERE` clause will remove all records from the `Products` table, effectively emptying it. This operation is irreversible without a backup.

---

#### 7.5 Introduction to Transactions and ACID Properties

Transactions are a sequence of operations performed as a single logical unit of work. They are crucial for maintaining data integrity, especially when dealing with complex operations that involve multiple steps. Transactions adhere to ACID properties:

- **Atomicity:**  Ensures that all operations within a transaction are treated as a single "atomic" unit. Either all operations succeed, or none of them do. If any part of the transaction fails, the entire transaction is rolled back, and the database state is left unchanged as if the transaction never occurred.

- **Consistency:**  Ensures that a transaction brings the database from one valid state to another. It maintains database integrity by ensuring that data remains valid according to defined rules and constraints.

- **Isolation:**  Ensures that concurrent transactions are isolated from each other. The intermediate state of a transaction is invisible to other transactions, preventing conflicts and ensuring that the outcome is the same as if transactions were executed sequentially.

- **Durability:**  Ensures that once a transaction is committed, the changes are permanent and will survive even system failures (e.g., power outage, crashes). Committed data is typically written to persistent storage.

---

#### 7.6 Transaction Control: COMMIT and ROLLBACK

SQL provides commands to control transactions:

- **START TRANSACTION (or BEGIN):**  Initiates a new transaction. In some systems, transactions may start implicitly with the first DML statement.
- **COMMIT:**  Saves all changes made within the current transaction and makes them permanent in the database.
- **ROLLBACK:**  Discards all changes made within the current transaction and reverts the database to the state it was in before the transaction began.

**Example 7.6.1: Using Transactions for Data Transfer**

Consider a scenario where we are transferring funds from one bank account to another. This operation should be atomic – either both the debit from one account and the credit to another account happen, or neither should.

```sql
-- Sample Tables:
-- Accounts Table
-- AccountID | AccountBalance
-- ----------|---------------
-- 1         | 1000
-- 2         | 500

START TRANSACTION;

UPDATE Accounts
SET AccountBalance = AccountBalance - 200
WHERE AccountID = 1; -- Debit $200 from account 1

UPDATE Accounts
SET AccountBalance = AccountBalance + 200
WHERE AccountID = 2; -- Credit $200 to account 2

COMMIT; -- Make changes permanent
```

**Explanation:**
1. `START TRANSACTION;` begins a new transaction.
2. The first `UPDATE` statement debits $200 from `AccountID = 1`.
3. The second `UPDATE` statement credits $200 to `AccountID = 2`.
4. `COMMIT;` commits the transaction, making both updates permanent. If any step fails (e.g., insufficient funds in account 1), we would use `ROLLBACK;` instead of `COMMIT;` to cancel both operations and maintain the original account balances.

**Example 7.6.2: Rollback in Case of Error**

```sql
START TRANSACTION;

UPDATE Products
SET Price = Price * 1.10
WHERE Category = 'Electronics';

-- Simulate an error condition (e.g., constraint violation, system error)
-- If an error occurs, execute ROLLBACK

ROLLBACK; -- Discard changes due to error

-- If no error, execute COMMIT
-- COMMIT;
```

**Explanation:**
- If, after increasing prices of electronics, we find an issue (simulated error), we use `ROLLBACK;`. This command undoes the price updates, reverting the `Products` table to its state before the `START TRANSACTION;` command.

---

#### 7.7 Practical Exercises

1. **INSERT Exercise:**
   - Add three new products to the `Products` table with different categories and prices.

2. **UPDATE Exercise:**
   - Increase the price of all products in the 'Books' category by 5%.

3. **DELETE Exercise:**
   - Remove all products from the `Products` table that are in the 'Clothing' category.

4. **Transaction Exercise:**
   - Simulate a bank transaction by transferring $100 from 'AccountA' to 'AccountB' using `START TRANSACTION`, `UPDATE` for both accounts, and `COMMIT`.
   - Then, simulate a failed transaction where you attempt to transfer $500 from 'AccountA' to 'AccountB', but 'AccountA' only has $300. Use `ROLLBACK` to ensure no changes are made if the transaction cannot be fully completed. (You might need to simulate the error condition, as SQL might not automatically rollback in all cases of business logic failure).

---

#### 7.8 Additional Considerations for Module 7

- **Backup Before Modification:**  Always recommend backing up data before performing significant data modification operations, especially `UPDATE` and `DELETE` without careful `WHERE` clauses.
- **Testing in Development Environment:** Encourage students to test their DML statements in a development or staging environment before applying them to production databases.
- **Implicit vs. Explicit Transactions:** Explain the difference between implicit (auto-commit) and explicit transactions and when to use each. Most database systems operate in auto-commit mode by default, where each SQL statement is treated as a transaction and automatically committed unless explicitly started.
- **Transaction Isolation Levels:** Briefly introduce the concept of transaction isolation levels and how they affect concurrency and data consistency (more advanced topic for later study).
- **Data Integrity Constraints:** Reiterate the importance of database constraints (e.g., `NOT NULL`, `UNIQUE`, `FOREIGN KEY`, `CHECK`) in maintaining data integrity during data modification operations.

By the end of this module, students should be proficient in using `INSERT`, `UPDATE`, and `DELETE` statements to modify data in SQL databases. They should also understand the critical role of transactions in ensuring data integrity and be able to use `COMMIT` and `ROLLBACK` to manage transactions effectively. They will appreciate the importance of careful planning and testing when performing data modification operations.
