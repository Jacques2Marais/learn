# Chapter 8: Calculated Columns and Measures

Let's get practical and start creating **calculated columns** and **measures** using DAX in Power BI Desktop! In this chapter, we'll walk through step-by-step examples to solidify your understanding and get you writing your own DAX calculations.

## Creating Calculated Columns

Calculated columns are added to existing tables and are evaluated row by row. Here's how to create them:

1.  **Data View:**  Switch to the **Data View** in Power BI Desktop (using the Panes Switcher on the left).
2.  **Select Table:** In the Data pane, select the table where you want to add the calculated column.
3.  **New Column:**
    *   **Method 1 (Ribbon):** Go to the **"Table tools" ribbon** (which appears when you're in Data View and have a table selected). Click **"New column"** in the "Calculations" group.
    *   **Method 2 (Right-Click):** Right-click on any column header in the table's data grid. Select **"New column"** from the context menu.
    *   **Method 3 (Fields Pane):** In the "Fields" pane, right-click on the table name. Select **"New column"**.
4.  **Formula Bar:** A new column will be added to the table, and the cursor will be in the **formula bar**, ready for you to enter your DAX formula. The formula bar will initially show `Column = `.
5.  **Write DAX Formula:**  Replace `Column` with the desired **name for your new calculated column**, followed by the `=` sign, and then write your DAX formula.

**Example 1: Concatenating First and Last Name**

Let's say you have a `Customers` table with `FirstName` and `LastName` columns. You want to create a calculated column called `FullName` that combines these.

```dax
FullName = Customers[FirstName] & " " & Customers[LastName] 
```

*   **`FullName =`**:  Names the calculated column "FullName".
*   **`Customers[FirstName]`**:  Refers to the `FirstName` column in the `Customers` table.  Table and column names are enclosed in square brackets `[]`.
*   **`& " " &`**:  The `&` operator is used for text concatenation. `" "` is a text literal representing a space (to separate first and last names).
*   **`Customers[LastName]`**: Refers to the `LastName` column in the `Customers` table.

**Press Enter** or click the **checkmark icon** next to the formula bar to commit the formula. The `FullName` calculated column will be created in the `Customers` table, displaying the concatenated full names for each customer.

**Example 2: Calculating Age from Birthdate**

Assume you have a `Customers` table with a `BirthDate` column (Date data type). You want to calculate the age of each customer as of today.

```dax
Age = 
VAR Today = TODAY()
RETURN
YEAR( Today ) - YEAR( Customers[BirthDate] ) - 
IF( MONTH( Today ) * 100 + DAY( Today ) < MONTH( Customers[BirthDate] ) * 100 + DAY( Customers[BirthDate] ), 1, 0 )
```

*   **`Age =`**: Names the calculated column "Age".
*   **`VAR Today = TODAY()`**:  Uses the `VAR` keyword to declare a variable named `Today` and assigns it the current date using the `TODAY()` function. Variables are useful for breaking down complex formulas and improving readability.
*   **`RETURN`**:  Indicates the start of the expression that will be returned as the calculated column's value.
*   **`YEAR( Today ) - YEAR( Customers[BirthDate] )`**: Calculates the difference in years between today's year and the birth year.
*   **`- IF(...)`**: Subtracts 1 from the year difference if the current month and day are *before* the birth month and day in the year (meaning the birthday hasn't occurred yet this year).
    *   **`IF( condition, value_if_true, value_if_false )`**:  The `IF` function performs conditional logic.
    *   **`MONTH( Today ) * 100 + DAY( Today ) < MONTH( Customers[BirthDate] ) * 100 + DAY( Customers[BirthDate] )`**:  This condition cleverly compares the month and day of today's date with the birth date's month and day to check if the birthday has passed this year.
*   **`, 1, 0 )`**: If the condition is true (birthday hasn't passed), subtract 1 (age is one year less). Otherwise, subtract 0 (age is the year difference).

**Data Types in Calculated Columns:**

Power BI automatically determines the data type of your calculated column based on the formula. You can also explicitly set the data type in the "Formatting" pane when you have the calculated column selected in Data View or Report View. Common data types include:

*   **Text**
*   **Whole Number**
*   **Decimal Number**
*   **Date**
*   **DateTime**
*   **Boolean (True/False)**
*   **Currency**

## Creating Measures

Measures are dynamic calculations that aggregate data and respond to report context. Here's how to create them:

1.  **Report View or Model View:** You can create measures in either **Report View** or **Model View** in Power BI Desktop.
2.  **Select Table (Measure Table):** In the "Fields" pane, **select the table where you want to *store* your measure.**  Measures are associated with a table for organizational purposes, but they are not actually added as columns to that table.  You can even create a dedicated "Measures" table just to hold your measures for better organization.
3.  **New Measure:**
    *   **Method 1 (Ribbon):** Go to the **"Report" ribbon** (in Report View) or **"Modeling" ribbon** (in Model View). Click **"New measure"** in the "Calculations" group.
    *   **Method 2 (Right-Click):** Right-click on the table name in the "Fields" pane. Select **"New measure"** from the context menu.
4.  **Formula Bar:** A new measure will be created and appear in the "Fields" pane under the selected table (it will have a calculator icon next to it). The cursor will be in the **formula bar**, ready for you to enter your DAX formula. The formula bar will initially show `Measure = `.
5.  **Write DAX Formula:** Replace `Measure` with the desired **name for your new measure**, followed by the `=` sign, and then write your DAX formula.

**Example 3: Total Sales Measure**

Let's create a measure to calculate the total sales amount from a `SalesFact` table with a `SalesAmount` column.

```dax
Total Sales = SUM(SalesFact[SalesAmount])
```

*   **`Total Sales =`**: Names the measure "Total Sales".
*   **`SUM(SalesFact[SalesAmount])`**:  Uses the `SUM()` aggregation function to sum up all values in the `SalesAmount` column of the `SalesFact` table.

**Press Enter** or click the **checkmark icon** to commit the formula. The `Total Sales` measure will be created and will appear in the "Fields" pane under the `SalesFact` table (or whichever table you selected).

**Example 4: Average Order Value Measure**

Let's create a measure to calculate the average order value. Assume you have `SalesFact` table with `SalesAmount` and `OrderID` columns.

```dax
Average Order Value = 
AVERAGEX(
    SUMMARIZE(SalesFact, SalesFact[OrderID], "OrderTotal", SUM(SalesFact[SalesAmount])),
    [OrderTotal]
)
```

*   **`Average Order Value =`**: Names the measure "Average Order Value".
*   **`AVERAGEX(...)`**:  Uses the `AVERAGEX()` iterator function. `AVERAGEX()` iterates over a table and calculates the average of an expression evaluated for each row of the table.
*   **`SUMMARIZE(SalesFact, SalesFact[OrderID], "OrderTotal", SUM(SalesFact[SalesAmount]))`**:  This `SUMMARIZE()` function creates a **virtual summarized table** on the fly.
    *   **`SalesFact`**:  Specifies the table to summarize (`SalesFact`).
    *   **`SalesFact[OrderID]`**:  Specifies the grouping column (`OrderID`).  `SUMMARIZE()` will group rows by unique `OrderID` values.
    *   **`"OrderTotal"`**:  Defines the name of a new column in the summarized table, called "OrderTotal".
    *   **`SUM(SalesFact[SalesAmount])`**:  Defines the expression to calculate for each group (each `OrderID`). It calculates the sum of `SalesAmount` for each order.
    *   **Result of `SUMMARIZE()`**:  The `SUMMARIZE()` function returns a table with two columns: `OrderID` and `OrderTotal`, where each row represents a unique order and its total sales amount.
*   **`, [OrderTotal]`**:  The second argument of `AVERAGEX()` is the expression to average. Here, we specify `[OrderTotal]`, which refers to the "OrderTotal" column in the virtual table created by `SUMMARIZE()`.  `AVERAGEX()` then calculates the average of the `OrderTotal` values across all rows in the summarized table, effectively giving you the average order value.

**Measure Formatting:**

Measures, by default, might not have specific formatting (e.g., currency symbol, decimal places). You can format measures to improve their display in reports:

1.  **Select Measure:** In Report View or Model View, select the measure in the "Fields" pane (click on it).
2.  **Formatting Pane:** Go to the "Formatting" pane (it usually appears below the "Fields" pane or "Visualizations" pane).
3.  **Format Options:**  You'll see formatting options relevant to the measure's data type (e.g., for numeric measures: format, decimal places, currency symbol, display units).  Adjust these options as needed.

## Using Calculated Columns and Measures in Reports

Once you've created calculated columns and measures, you can use them in your Power BI reports and visualizations:

*   **Calculated Columns:**  Calculated columns behave just like regular columns in your tables. You can:
    *   Drag them onto the report canvas to create visuals.
    *   Use them as axes, legends, values, slicers, filters in visualizations.
    *   Group and summarize data by calculated columns.

*   **Measures:** Measures are primarily used to display aggregated values in visuals. You typically:
    *   Drag measures to the "Values" field well of visualizations (e.g., in a chart, table, matrix, card visual).
    *   Measures will then be evaluated in the context of the visual, responding to filters and groupings.
    *   You can also use measures in card visuals to display single, key metric values.

## Practice Creating DAX Calculations

Now it's your turn to practice!

1.  **Create Calculated Columns:**
    *   In a sample table (e.g., Customers, Products, Sales), create a few calculated columns using different DAX functions and operators. Examples:
        *   Combine address fields into a "FullAddress" column.
        *   Calculate profit margin (if you have cost and price columns).
        *   Categorize products based on price ranges.
        *   Extract year or month from a date column.
2.  **Create Measures:**
    *   Create several measures to perform aggregations and calculations on your data. Examples:
        *   Total Revenue, Total Quantity Sold, Average Price.
        *   Maximum Sales Amount, Minimum Sales Amount.
        *   Count of Customers, Count of Orders.
        *   Percentage of Total Sales for each product category (requires using `CALCULATE()` and filter functions - we'll cover these in detail later).
        *   Year-over-year sales growth (requires time intelligence functions - we'll cover these later).
3.  **Use in Reports:**
    *   Create a simple Power BI report with a few visuals (charts, tables, cards).
    *   Use your calculated columns and measures in these visuals to display and analyze your data.
    *   Experiment with slicers and filters to see how measures respond dynamically to context changes.
    *   Format your measures appropriately.

By practicing creating calculated columns and measures, you'll build a solid foundation in DAX and start to experience the power of this language for data analysis in Power BI! In the next chapter, we'll explore more advanced DAX concepts, including **filter context**, **row context**, and the powerful `CALCULATE()` function!
