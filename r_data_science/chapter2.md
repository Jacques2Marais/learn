# Chapter 2: Working with Data in R

Welcome back! In the previous chapter, you got your feet wet with R and its basic data structures. Now, we'll dive into the heart of data science: working with data. This chapter will guide you through importing data into R, exploring it, and performing initial manipulations using the powerful `dplyr` package.

## Importing Data into R

Real-world data comes in various formats. R can handle many, but we'll focus on the most common ones: CSV, Excel, and text files.

### Importing CSV Files

CSV (Comma Separated Values) files are plain text files where values are separated by commas. They are a ubiquitous format for data exchange.

*   **`read.csv()`:** The base R function for reading CSV files.

    ```R
    # Assuming you have a file named "data.csv" in your working directory
    data <- read.csv("data.csv")

    # If the file is in a different directory, specify the full path
    data <- read.csv("/path/to/your/file/data.csv")

    # Explore the imported data
    head(data) # View the first few rows
    str(data)  # Check the structure of the data frame
    ```

    **Common `read.csv()` arguments:**

    *   `header = TRUE/FALSE`:  Does the first row contain column names? (Default: `TRUE`)
    *   `sep = ","`:  Separator character (comma is default for CSV). For tab-separated files, use `sep = "\t"`.
    *   `stringsAsFactors = FALSE`:  Should character vectors be converted to factors? (Default: `TRUE` in older R versions, `FALSE` is often preferred now). Setting to `FALSE` prevents automatic conversion to factors, which can be useful for data manipulation.

*   **`read_csv()` from `readr` package:**  Part of the `tidyverse` (which includes `dplyr` and `ggplot2`).  Generally faster and more consistent than `read.csv()`.  You'll need to install and load the `readr` package first.

    ```R
    # Install readr package (if you haven't already)
    # install.packages("readr")

    library(readr) # Load the readr package

    data <- read_csv("data.csv") # Simpler syntax

    # Explore the data
    head(data)
    str(data)
    ```

    `read_csv()` automatically handles many common CSV variations and guesses column types effectively.

### Importing Excel Files

Excel files (`.xls`, `.xlsx`) are also widely used.  R requires packages to read Excel files.  A popular choice is `readxl`.

*   **`read_excel()` from `readxl` package:**

    ```R
    # Install readxl package (if needed)
    # install.packages("readxl")

    library(readxl)

    excel_data <- read_excel("excel_file.xlsx") # Or "excel_file.xls"

    # Explore
    head(excel_data)
    str(excel_data)
    ```

    **Common `read_excel()` arguments:**

    *   `sheet = 1` or `sheet = "Sheet1"`:  Specify sheet number or name to read (default is the first sheet).
    *   `col_names = TRUE/FALSE`:  Does the first row contain column names? (Default: `TRUE`)
    *   `skip = n`:  Skip the first `n` rows.

### Importing Text Files

For simple text files where data is separated by spaces, tabs, or other delimiters, you can use `read.table()` or `scan()`.

*   **`read.table()`:**  More general function for reading tabular data from text files.

    ```R
    text_data <- read.table("text_file.txt") # Assumes space-separated

    # For tab-separated, use sep = "\t"
    text_data_tab <- read.table("tab_separated_file.txt", sep = "\t")

    # Explore
    head(text_data)
    str(text_data)
    ```

*   **`scan()`:**  More flexible for reading various types of text data, but output is often a vector or list, not directly a data frame. Useful for reading in data that isn't neatly tabular.

    ```R
    # Read space-separated numbers into a numeric vector
    numbers <- scan("numbers.txt")
    numbers

    # Read lines of text into a character vector
    lines <- scan("text_lines.txt", what = character(), sep = "\n")
    lines
    ```

## Data Exploration and Manipulation with `dplyr`

`dplyr` is a game-changing package for data manipulation in R. It provides a set of intuitive "verbs" that make data wrangling efficient and readable. `dplyr` is part of the `tidyverse`, so if you loaded `readr` earlier, you likely already have `dplyr` installed. If not, install it: `install.packages("dplyr")` and load it with `library(dplyr)`.

Let's assume you have a data frame called `data` (you can import one using the methods above).

### Core `dplyr` Verbs

*   **`filter()`:** Select rows based on conditions.

    ```R
    # Filter rows where 'age' is greater than 25
    older_data <- filter(data, age > 25)

    # Filter rows where 'city' is "New York" AND 'category' is "A"
    filtered_data <- filter(data, city == "New York" & category == "A")

    # Filter rows where 'city' is "London" OR 'city' is "Paris"
    filtered_cities <- filter(data, city == "London" | city == "Paris")
    ```

*   **`select()`:** Choose specific columns.

    ```R
    # Select only the 'name' and 'age' columns
    name_age_data <- select(data, name, age)

    # Select all columns EXCEPT 'city'
    no_city_data <- select(data, -city)

    # Select columns starting with "sales_"
    sales_columns_data <- select(data, starts_with("sales_"))
    ```

*   **`arrange()`:** Reorder rows based on column values.

    ```R
    # Arrange data by 'age' in ascending order
    sorted_by_age <- arrange(data, age)

    # Arrange by 'sales' in descending order
    sorted_by_sales_desc <- arrange(data, desc(sales))

    # Arrange by 'category' then by 'sales' within each category
    sorted_by_category_sales <- arrange(data, category, sales)
    ```

*   **`mutate()`:** Create new columns or modify existing ones.

    ```R
    # Create a new column 'age_in_months'
    data_with_months <- mutate(data, age_in_months = age * 12)

    # Create a 'category_flag' column based on a condition
    data_with_flag <- mutate(data, category_flag = ifelse(category == "A", "High", "Low"))

    # Modify the 'sales' column (e.g., apply a discount)
    data_discounted <- mutate(data, sales = sales * 0.9) # 10% discount
    ```

*   **`summarise()` (or `summarize`):**  Compute summary statistics. Often used with `group_by()`.

    ```R
    # Calculate the mean age
    mean_age <- summarise(data, mean_age = mean(age, na.rm = TRUE)) # na.rm = TRUE to handle missing values

    # Calculate the total sales
    total_sales <- summarise(data, total_sales = sum(sales, na.rm = TRUE))

    # Calculate multiple summaries
    data_summary <- summarise(data,
                               mean_age = mean(age, na.rm = TRUE),
                               median_sales = median(sales, na.rm = TRUE),
                               n = n()) # n() counts the number of rows
    ```

*   **`group_by()`:**  Group data by one or more columns for group-wise operations.  Often used before `summarise()`.

    ```R
    # Group data by 'category' and calculate mean sales for each category
    category_sales_summary <- data %>%
      group_by(category) %>%
      summarise(mean_sales = mean(sales, na.rm = TRUE))

    # Group by 'city' and 'category' and count the number of records in each group
    city_category_counts <- data %>%
      group_by(city, category) %>%
      summarise(count = n())
    ```

### The Pipe Operator `%>%`

The pipe operator `%>%` (from the `magrittr` package, which comes with `dplyr`) is a powerful tool for chaining `dplyr` operations. It takes the output of one operation and "pipes" it as the first argument to the next function. This makes code much more readable and easier to follow.

**Example without pipe:**

```R
# Nested function calls (harder to read)
result <- summarise(
  group_by(
    filter(data, age > 20),
    city
  ),
  mean_sales = mean(sales)
)
```

**Example with pipe:**

```R
# Using pipe operator (much more readable)
result_piped <- data %>%
  filter(age > 20) %>%
  group_by(city) %>%
  summarise(mean_sales = mean(sales))
```

The piped version reads like a sequence of actions: "Take the `data`, THEN filter for `age > 20`, THEN group by `city`, THEN summarise by calculating `mean_sales`."

## Data Cleaning and Preprocessing

Real-world data is often messy. Data cleaning and preprocessing are crucial steps before analysis. Common tasks include:

*   **Handling Missing Values:**
    *   **Identifying missing values:**  Use `is.na()` to detect `NA` (Not Available) values.
    *   **Removing rows with missing values:** `na.omit(data)` (removes rows with *any* missing values). Be cautious, as you might lose valuable data.
    *   **Imputation:**  Replacing missing values with estimates (e.g., mean, median, mode). More advanced techniques exist, but simple imputation can be a starting point.

        ```R
        # Check for missing values in each column
        colSums(is.na(data))

        # Remove rows with any missing values
        data_cleaned <- na.omit(data)

        # Impute missing 'age' values with the mean age (simple example)
        mean_age_val <- mean(data$age, na.rm = TRUE) # Calculate mean, ignoring NAs
        data_imputed <- data %>%
          mutate(age = ifelse(is.na(age), mean_age_val, age)) # Replace NAs with mean
        ```

*   **Dealing with Duplicates:**
    *   **Identifying duplicates:** `duplicated(data)` returns logical vector indicating duplicate rows.
    *   **Removing duplicates:** `distinct(data)` (from `dplyr`) removes duplicate rows.

        ```R
        # Check for duplicate rows
        duplicated_rows <- duplicated(data)
        data[duplicated_rows, ] # View duplicate rows

        # Remove duplicate rows
        data_unique <- distinct(data)
        ```

*   **Data Type Conversion:**
    *   Use functions like `as.numeric()`, `as.character()`, `as.factor()`, `as.Date()`, etc., to convert column data types.

        ```R
        # Convert 'sales' column to numeric
        data$sales <- as.numeric(data$sales)

        # Convert 'category' to factor (for categorical analysis)
        data$category <- as.factor(data$category)

        # Convert 'date_column' to Date format
        data$date_column <- as.Date(data$date_column)
        ```

*   **Text Cleaning:**
    *   For character columns, you might need to trim whitespace, convert to lowercase/uppercase, remove punctuation, etc.  Packages like `stringr` (part of `tidyverse`) are helpful for string manipulation.

        ```R
        # Install stringr if needed: install.packages("stringr")
        library(stringr)

        # Trim whitespace from 'city' column
        data <- mutate(data, city = str_trim(city))

        # Convert 'product_name' to lowercase
        data <- mutate(data, product_name = str_to_lower(product_name))
        ```

## Let's Practice!

1.  **Download a sample CSV dataset:** You can find many free datasets online (e.g., from Kaggle, UCI Machine Learning Repository, government open data portals). Download a CSV file and save it in your working directory (or note the path).
2.  **Import the CSV data into RStudio** using `read_csv()` or `read.csv()`.
3.  **Explore the data:**
    *   Use `head()`, `tail()`, `str()`, `summary()`, `View()` to get a feel for the data.
    *   Calculate descriptive statistics using `summarise()` (e.g., mean, median, standard deviation for numeric columns).
    *   Use `filter()` to select subsets of data based on conditions.
    *   Use `select()` to choose specific columns.
    *   Use `arrange()` to sort the data.
    *   Create new columns using `mutate()`.
    *   Try grouping the data using `group_by()` and then summarise within groups.
4.  **Practice data cleaning:**
    *   Check for missing values using `is.na()` and `colSums(is.na(data))`.
    *   If there are missing values, experiment with `na.omit()` or simple imputation.
    *   Check for and remove duplicate rows using `duplicated()` and `distinct()`.
    *   If needed, convert column data types using `as.numeric()`, `as.factor()`, etc.

## Chapter Summary

In this chapter, you've gained essential skills for working with data in R:

*   **Importing data** from CSV, Excel, and text files using various R functions.
*   **Exploring data** using functions like `head()`, `str()`, `summary()`, and `View()`.
*   **Manipulating data** with the core `dplyr` verbs: `filter()`, `select()`, `arrange()`, `mutate()`, `summarise()`, and `group_by()`.
*   Understanding and using the **pipe operator `%>%`** for efficient data workflows.
*   Basic **data cleaning and preprocessing** techniques for handling missing values, duplicates, and data type conversions.

With these skills, you're well-equipped to bring data into R and start shaping it for analysis and visualization. In the next chapter, we'll unleash the power of `ggplot2` to create compelling data visualizations!
