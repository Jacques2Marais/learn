# Chapter 5: Data Wrangling and Transformation

Welcome back to our R for Data Science journey! In Chapter 2, you learned the basics of data manipulation with `dplyr`. Now, we'll take your data wrangling skills to the next level. This chapter focuses on advanced data manipulation using `dplyr` and `tidyr`, along with techniques for reshaping, pivoting, and working with dates and times in R.

## Advanced Data Manipulation with `dplyr` and `tidyr`

We'll expand on your `dplyr` knowledge and introduce `tidyr`, another essential package in the `tidyverse` for data tidying and reshaping.

### Advanced `dplyr` Techniques

*   **`case_when()`:**  For creating new columns based on multiple conditional logic.  More flexible than `ifelse()` for complex conditions.

    ```R
    library(dplyr)

    data <- data.frame(
      score = c(85, 70, 92, 60, 78)
    )

    data_with_grades <- data %>%
      mutate(
        grade = case_when(
          score >= 90 ~ "A+",
          score >= 80 ~ "A",
          score >= 70 ~ "B",
          score >= 60 ~ "C",
          TRUE ~ "Fail" # Default case (else)
        )
      )
    data_with_grades
    ```

*   **Window Functions:**  Perform calculations across rows within groups, while keeping the original row structure. Examples: `row_number()`, `rank()`, `dense_rank()`, `lead()`, `lag()`, `cumsum()`, `cummean()`, etc.

    ```R
    sales_data <- data.frame(
      category = rep(c("Electronics", "Clothing"), each = 5),
      month = rep(1:5, 2),
      sales = sample(100:500, 10)
    )

    sales_ranked <- sales_data %>%
      group_by(category) %>%
      mutate(
        rank_within_category = rank(desc(sales)), # Rank sales within each category (descending)
        cumulative_sales = cumsum(sales) # Cumulative sum of sales within category
      )
    sales_ranked
    ```

*   **Joins:** Combine data from multiple tables based on common columns. `dplyr` provides various join types: `inner_join()`, `left_join()`, `right_join()`, `full_join()`, `semi_join()`, `anti_join()`.

    ```R
    # Example: Joining two data frames - customers and orders
    customers <- data.frame(
      customer_id = 1:4,
      customer_name = c("Alice", "Bob", "Charlie", "David")
    )

    orders <- data.frame(
      order_id = 101:105,
      customer_id = c(1, 2, 1, 3, 5), # Note customer_id 5 is not in 'customers'
      order_amount = sample(50:200, 5)
    )

    # Left join (keep all rows from 'customers', match with 'orders')
    left_joined_data <- left_join(customers, orders, by = "customer_id") # Join based on 'customer_id' column
    left_joined_data

    # Inner join (keep only matching rows from both)
    inner_joined_data <- inner_join(customers, orders, by = "customer_id")
    inner_joined_data

    # Full join (keep all rows from both, fill in NAs where no match)
    full_joined_data <- full_join(customers, orders, by = "customer_id")
    full_joined_data
    ```

### Data Tidying with `tidyr`

`tidyr` is designed to help you create tidy data. Tidy data has a specific structure:

1.  Each variable forms a column.
2.  Each observation forms a row.
3.  Each value has its own cell.

`tidyr` provides functions to reshape data into this tidy format.

*   **`pivot_longer()`:**  Converts wide data to long data by "pivoting" columns into rows.

    ```R
    library(tidyr)

    wide_data <- data.frame(
      student_id = 1:3,
      math_score = c(80, 90, 75),
      science_score = c(85, 88, 92),
      english_score = c(78, 85, 80)
    )
    wide_data

    # Pivot from wide to long format
    long_data <- wide_data %>%
      pivot_longer(
        cols = c(math_score, science_score, english_score), # Columns to pivot
        names_to = "subject",         # Name for the new column containing column names
        values_to = "score"          # Name for the new column containing values
      )
    long_data
    ```

*   **`pivot_wider()`:**  Converts long data to wide data by "pivoting" rows into columns.  The reverse of `pivot_longer()`.

    ```R
    # Pivot back from long to wide (using long_data from above)
    wide_again_data <- long_data %>%
      pivot_wider(
        names_from = subject,        # Column to get new column names from
        values_from = score         # Column to get values from
      )
    wide_again_data # Should be similar to original 'wide_data'
    ```

*   **`separate()`:**  Splits a single column into multiple columns based on a delimiter.

    ```R
    data_separated <- data.frame(
      product_code = c("P-123-A", "P-456-B", "P-789-C")
    )

    separated_data <- data_separated %>%
      separate(
        col = product_code,      # Column to separate
        into = c("product_type", "item_number", "variant"), # New column names
        sep = "-"               # Separator character
      )
    separated_data
    ```

*   **`unite()`:**  Combines multiple columns into a single column, pasting values together with a separator.  The reverse of `separate()`.

    ```R
    # Unite columns back (using separated_data from above)
    united_data <- separated_data %>%
      unite(
        col = "full_product_code", # New column name
        product_type, item_number, variant, # Columns to unite
        sep = "_"                 # Separator
      )
    united_data
    ```

## Reshaping and Pivoting Data

Reshaping data often involves converting between wide and long formats, as demonstrated by `pivot_longer()` and `pivot_wider()`. These operations are crucial for preparing data for different types of analysis and visualization.

**When to use wide vs. long format:**

*   **Wide format:**  Each row typically represents a single experimental unit or observation, with different variables as columns.  Good for:
    *   Data entry and human readability.
    *   Some types of statistical modeling.
*   **Long format:**  Each row represents a single variable measurement for an observation.  Good for:
    *   `ggplot2` visualizations (often requires long format).
    *   Repeated measures analysis.
    *   Tidy data principles.

**Example: Converting data to long format for `ggplot2`**

Suppose you want to create a line plot of math, science, and English scores for each student using `wide_data` from earlier. `ggplot2` often works best with long format data.

```R
# Convert wide_data to long format (if not already done)
long_data_for_plot <- wide_data %>%
  pivot_longer(
    cols = c(math_score, science_score, english_score),
    names_to = "subject",
    values_to = "score"
  )

# Create a line plot
ggplot(long_data_for_plot, aes(x = subject, y = score, group = student_id, color = factor(student_id))) +
  geom_line() +
  geom_point() +
  labs(title = "Student Scores Across Subjects", x = "Subject", y = "Score", color = "Student ID")
```

## Working with Dates and Times

Dates and times are common data types in data science. R has powerful tools for working with them.

*   **Date classes:**  `Date` (for dates only), `POSIXct` and `POSIXlt` (for date and time). `POSIXct` stores time as seconds since the epoch (January 1, 1970 UTC), `POSIXlt` stores date-time components as a list (year, month, day, hour, etc.). `POSIXct` is often preferred for computational use, `POSIXlt` for human-readable components.

*   **Converting to Date/Datetime:**  Use functions like `as.Date()`, `as.POSIXct()`, `as.POSIXlt()`. Specify the format of your date/time strings using format codes.

    ```R
    date_string <- "2025-02-23"
    date_obj <- as.Date(date_string) # Default format is YYYY-MM-DD
    date_obj

    datetime_string <- "2025-02-23 10:30:00"
    datetime_ct <- as.POSIXct(datetime_string) # Default format is YYYY-MM-DD HH:MM:SS
    datetime_ct

    datetime_lt <- as.POSIXlt(datetime_string)
    datetime_lt # List-like structure

    # If your date/time string has a different format, specify it:
    date_string_custom_format <- "23/02/2025" # DD/MM/YYYY
    date_obj_custom <- as.Date(date_string_custom_format, format = "%d/%m/%Y") # %d=day, %m=month, %Y=4-digit year
    date_obj_custom

    datetime_string_custom_format <- "Feb 23, 2025 10:30 AM" # Month name, day, year, time with AM/PM
    datetime_ct_custom <- as.POSIXct(datetime_string_custom_format, format = "%b %d, %Y %I:%M %p") # %b=abbreviated month name, %I=12-hour time, %p=AM/PM
    datetime_ct_custom
    ```

    **Common format codes:**

    *   `%Y`: 4-digit year
    *   `%y`: 2-digit year
    *   `%m`: Month (01-12)
    *   `%b`: Abbreviated month name (e.g., "Jan")
    *   `%B`: Full month name (e.g., "January")
    *   `%d`: Day of the month (01-31)
    *   `%H`: Hour (00-23)
    *   `%I`: Hour (01-12)
    *   `%M`: Minute (00-59)
    *   `%S`: Second (00-59)
    *   `%p`: AM/PM indicator

*   **Extracting Date/Time Components:**  For `Date` objects: `year()`, `month()`, `day()`, `wday()` (day of week), `yday()` (day of year) from `lubridate` package (install if needed: `install.packages("lubridate")`). For `POSIXlt` objects, you can access components directly like `datetime_lt$year`, `datetime_lt$mon`, etc.

    ```R
    library(lubridate)

    date_obj <- as.Date("2025-02-23")

    year(date_obj)   # 2025
    month(date_obj)  # 2
    day(date_obj)    # 23
    wday(date_obj)   # Day of week (1=Sunday, 7=Saturday)
    wday(date_obj, label = TRUE) # Day of week label (e.g., "Sun", "Mon")
    yday(date_obj)   # Day of year (1-365 or 366)

    datetime_lt <- as.POSIXlt("2025-02-23 10:30:00")
    datetime_lt$year # Year (starts from 0, so 125 for 2025)
    datetime_lt$mon  # Month (starts from 0, so 1 for February)
    datetime_lt$mday # Day of month
    datetime_lt$hour # Hour
    ```

*   **Date/Time Arithmetic:**  You can perform calculations with dates and times.

    ```R
    start_date <- as.Date("2025-02-23")
    end_date <- as.Date("2025-03-15")

    time_difference <- end_date - start_date # Difference in days
    time_difference # Time difference in days

    future_date <- start_date + 30 # Add 30 days
    future_date

    datetime_ct <- as.POSIXct("2025-02-23 10:30:00")
    future_datetime <- datetime_ct + hours(5) # Add 5 hours (using lubridate's hours() function)
    future_datetime
    ```

*   **Time Zones:**  R handles time zones. By default, `POSIXct` and `POSIXlt` use your system's time zone. You can specify time zones.

    ```R
    datetime_utc <- as.POSIXct("2025-02-23 10:30:00", tz = "UTC") # Specify UTC time zone
    datetime_utc

    datetime_london <- as.POSIXct("2025-02-23 10:30:00", tz = "Europe/London") # London time zone
    datetime_london

    # Convert between time zones
    datetime_london_utc <- with_tz(datetime_london, tzone = "UTC") # Convert London time to UTC
    datetime_london_utc
    ```

## Let's Practice!

1.  **Advanced `dplyr`:**
    *   Use `case_when()` to create new categorical columns based on numeric ranges or multiple conditions in a dataset.
    *   Experiment with window functions like `rank()`, `lead()`, `lag()`, `cumsum()` to calculate rankings, lags, leads, and cumulative sums within groups.
    *   Practice different types of joins (`left_join()`, `inner_join()`, `full_join()`) to combine data from related data frames.
2.  **Data Tidying with `tidyr`:**
    *   Take a wide dataset and use `pivot_longer()` to convert it to long format. Then, pivot it back to wide format using `pivot_wider()`.
    *   Use `separate()` to split columns (e.g., address column into street, city, zip code).
    *   Use `unite()` to combine columns (e.g., first name and last name into full name).
3.  **Reshaping and Pivoting:**
    *   Think about scenarios where long vs. wide format is more appropriate. Practice converting between formats for different analytical tasks.
4.  **Working with Dates and Times:**
    *   Import a dataset that includes date or datetime columns.
    *   Convert character date/datetime columns to `Date` or `POSIXct` objects using appropriate formats.
    *   Extract date components (year, month, day, etc.) using functions from `lubridate` or `POSIXlt` components.
    *   Perform date arithmetic (calculate time differences, add/subtract time intervals).
    *   If applicable, explore working with time zones.

## Chapter Summary

In this chapter, you've significantly expanded your data wrangling toolkit in R. You've mastered:

*   **Advanced `dplyr` techniques:** `case_when()`, window functions, and various types of joins.
*   **Data tidying with `tidyr`:** `pivot_longer()`, `pivot_wider()`, `separate()`, `unite()`.
*   **Reshaping and pivoting data** between wide and long formats for different analytical needs.
*   **Working with dates and times** in R, including date/datetime classes, conversion, extraction, arithmetic, and time zones.

These advanced data wrangling skills are essential for real-world data science projects. You can now handle complex data transformations and prepare your data effectively for analysis and visualization. In the next chapter, we'll dive into the exciting field of machine learning basics in R!
