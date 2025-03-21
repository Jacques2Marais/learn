# Chapter 18: Data Collection and Exploration

Chapter 18 marks the beginning of the implementation phase for your capstone project. This chapter focuses on the crucial steps of data collection and exploration. High-quality data is the foundation of any successful data science project, and thorough exploration is essential to understand your data and identify potential challenges and opportunities.

## Data Acquisition and Loading

The first step is to acquire the dataset you've chosen for your capstone project. This may involve:

*   **Downloading a public dataset:** If you're using a dataset from Kaggle, NASA Open Data, UCI Machine Learning Repository, or other public sources, download the data files to your project directory. Ensure you understand the data license and terms of use.
*   **Accessing data via API:** If your dataset is accessible through an API (e.g., for weather data, astronomical data), you'll need to write Python code to interact with the API and retrieve the data programmatically. Libraries like `requests` (for general APIs) or specialized API client libraries may be needed.
*   **Collecting your own data (optional and more advanced):** In some cases, you might consider collecting your own data, for example, from sensors, simulations, or experiments. This is more complex and time-consuming but can be very rewarding.

**Loading Data into Python:**

Once you have acquired your dataset, you need to load it into Python for analysis. Pandas is the primary library for data loading in data science, especially for tabular data.

*   **Pandas `read_csv()`:** For CSV files (most common for tabular data).
*   **Pandas `read_excel()`:** For Excel files.
*   **Pandas `read_json()`:** For JSON files.
*   **Pandas `read_table()`:** For general delimited text files.
*   **NumPy `np.loadtxt()` or `np.genfromtxt()`:** For loading data from simple text files into NumPy arrays (more suitable for numerical data without complex structure).
*   **SciPy `scipy.io.loadmat()`:** For loading data from MATLAB `.mat` files (common in some scientific fields).
*   **Specialized libraries:** For domain-specific data formats (e.g., FITS files in astronomy using `astropy.io.fits`, HDF5 files using `h5py`).

**Example: Loading a CSV Dataset with Pandas**

Assume you have downloaded a CSV file named `capstone_dataset.csv` and placed it in your project directory.

```python
# Code cell
import pandas as pd

dataset_filename = 'capstone_dataset.csv' # Replace with your actual filename
try:
    df_capstone = pd.read_csv(dataset_filename) # Load CSV into Pandas DataFrame
    print(f"Dataset '{dataset_filename}' loaded successfully.")
    print("\nFirst 5 rows of the dataset:\n", df_capstone.head()) # Display first few rows
    print("\nDataFrame information (data types, memory usage):\n")
    df_capstone.info() # Get DataFrame info
except FileNotFoundError:
    print(f"Error: File '{dataset_filename}' not found. Make sure the dataset file is in the correct directory.")
except Exception as e:
    print(f"An error occurred while loading the dataset: {e}")
```

Make sure to handle potential file loading errors using `try-except` blocks, as shown in the example.

## Data Cleaning and Preprocessing (Capstone Project Specific)

Once you have loaded your dataset, the next crucial step is data cleaning and preprocessing. The specific cleaning and preprocessing steps will depend heavily on the nature of your dataset and the chosen project. 

**Common Data Cleaning and Preprocessing Tasks (revisit Chapter 6 and adapt to your project):**

*   **Handling Missing Values:**
    *   Identify columns with missing values (`df.isnull().sum()`).
    *   Decide on a strategy:
        *   **Removal:** `df.dropna()` (remove rows or columns with NaNs - use cautiously, may lose data).
        *   **Imputation:** `df.fillna(value)`, `df.fillna(df.mean())`, `df.interpolate()` (fill missing values with a constant, mean, median, interpolated values). Choose imputation methods based on data context.
*   **Handling Inconsistent Formatting:**
    *   **Data type conversion:** `pd.to_numeric()`, `pd.to_datetime()`, `astype()` to ensure correct data types for columns.
    *   **String cleaning:** `.str.strip()`, `.str.lower()`, `.str.replace()` to standardize text data.
    *   **Unit conversion:** Convert units to a consistent system if necessary (e.g., convert all lengths to meters, temperatures to Celsius or Kelvin).
*   **Outlier Handling:**
    *   Identify potential outliers using visualizations (box plots, scatter plots) and statistical methods (e.g., Z-score, IQR).
    *   Decide how to handle outliers:
        *   **Removal:** Remove outlier data points (use cautiously, justify removal).
        *   **Transformation:** Apply transformations to reduce outlier influence (e.g., log transformation).
        *   **Robust methods:** Use models or statistical methods that are less sensitive to outliers.
*   **Handling Duplicates:**
    *   Identify duplicate rows: `df.duplicated()`, `df.drop_duplicates()`.
    *   Decide whether to remove duplicates based on your data context.
*   **Data Validation:**
    *   Check for data inconsistencies, errors, or impossible values.
    *   Validate data against domain knowledge or expected ranges.

**Adapt Cleaning to Your Capstone Dataset:**

For your capstone project, carefully examine your dataset and determine the necessary cleaning and preprocessing steps. Document your cleaning decisions and justify your choices in your project report.

**Example: Data Cleaning - Placeholder (Adapt to your dataset)**

```python
# Code cell
import pandas as pd

# Assume df_capstone is your loaded DataFrame

# --- Example Data Cleaning Steps (Adapt these to your dataset!) ---

# 1. Handle Missing Values (example: fill missing numerical values with mean, categorical with 'Unknown')
for col in df_capstone.columns:
    if df_capstone[col].isnull().any(): # Check if column has any missing values
        if pd.api.types.is_numeric_dtype(df_capstone[col]): # Check if column is numeric
            mean_value = df_capstone[col].mean()
            df_capstone[col].fillna(mean_value, inplace=True) # Impute with mean for numeric columns
            print(f"Imputed missing values in column '{col}' with mean: {mean_value:.2f}")
        elif pd.api.types.is_categorical_dtype(df_capstone[col] or pd.api.types.is_object_dtype(df_capstone[col])): # Check if categorical or object (string)
            df_capstone[col].fillna('Unknown', inplace=True) # Impute with 'Unknown' for categorical/string columns
            print(f"Imputed missing values in column '{col}' with 'Unknown'")

# 2. Data Type Conversion (example: convert date column to datetime)
try:
    df_capstone['date_column'] = pd.to_datetime(df_capstone['date_column']) # Replace 'date_column' with your actual date column name
    print("Converted 'date_column' to datetime type.")
except KeyError:
    print("Warning: 'date_column' not found, skipping datetime conversion (adapt to your dataset).")
except Exception as e:
    print(f"Error converting 'date_column' to datetime: {e}")

# 3. Outlier Handling (example: remove rows with outliers in 'value_column' - placeholder, define your outlier criteria)
# Example - remove values outside of a reasonable range (replace 'value_column' and range with your actual column and criteria)
value_column_name = 'value_column' # Replace with your column name
if value_column_name in df_capstone.columns and pd.api.types.is_numeric_dtype(df_capstone[value_column_name]):
    lower_bound = -1000 # Define your lower bound for valid values
    upper_bound = 10000 # Define your upper bound for valid values
    outlier_condition = (df_capstone[value_column_name] < lower_bound) | (df_capstone[value_column_name] > upper_bound)
    df_cleaned_outliers = df_capstone[~outlier_condition] # Keep rows that are NOT outliers
    print(f"Removed {len(df_capstone) - len(df_cleaned_outliers)} rows with outliers in '{value_column_name}' (example criteria).")
    df_capstone = df_cleaned_outliers # Update DataFrame to use cleaned version
else:
    print(f"Warning: Column '{value_column_name}' not found or not numeric, skipping outlier removal (adapt to your dataset).")


# ... Add more cleaning steps specific to your dataset and project ...

print("\nDataFrame info after cleaning:\n")
df_capstone.info() # Check DataFrame info after cleaning
print("\nFirst 5 rows of cleaned DataFrame:\n", df_capstone.head()) # Display first few rows of cleaned data
```

Remember to replace the placeholder cleaning steps and column names in the example code with steps relevant to your actual capstone dataset.

## Exploratory Data Analysis (EDA) for Capstone Project

Exploratory Data Analysis (EDA) is essential to gain insights into your dataset, understand its characteristics, and guide your subsequent analysis and modeling. Perform EDA techniques learned in Chapter 9, tailored to your capstone project dataset and research questions.

**Key EDA Techniques for Capstone Project:**

*   **Descriptive Statistics:** Use `df.describe()`, `df.info()`, `df.head()`, `df.tail()`, `df.sample()`, `df.value_counts()`, `df.unique()`, etc. to summarize data distributions, data types, and get a feel for your dataset.
*   **Univariate Analysis:** Examine individual variables (columns) using histograms (`sns.histplot()`, `plt.hist()`), box plots (`sns.boxplot()`, `plt.boxplot()`), distribution plots (`sns.displot()`), summary statistics (mean, median, std dev, skewness, kurtosis).
*   **Bivariate and Multivariate Analysis:** Explore relationships between variables using scatter plots (`sns.scatterplot()`, `plt.scatter()`), pair plots (`sns.pairplot()`), correlation matrices (`df.corr()`, `sns.heatmap()`), grouped box plots or violin plots (`sns.boxplot(x='category', y='value')`, `sns.violinplot()`), etc.
*   **Time Series Analysis (if applicable):** If your dataset has a time component, perform basic time series analysis (time series plots, decomposition, autocorrelation plots) as introduced in Chapter 12.
*   **Domain-Specific Visualizations:** Consider visualizations that are particularly relevant to your physics domain (e.g., spectra plots, phase space plots, geographical plots if data is spatial).

**Example: EDA - Placeholder (Adapt to your dataset and research questions)**

```python
# Code cell
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Assume df_capstone is your cleaned DataFrame

# --- Example EDA Visualizations (Adapt these to your dataset and research questions!) ---

# 1. Histograms for key numerical features
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
sns.histplot(df_capstone['numerical_feature_1'].dropna(), bins=30, kde=True, color='skyblue') # Replace 'numerical_feature_1'
plt.title("Distribution of Feature 1")
plt.xlabel("Feature 1 Value")

plt.subplot(1, 2, 2)
sns.histplot(df_capstone['numerical_feature_2'].dropna(), bins=30, kde=True, color='lightcoral') # Replace 'numerical_feature_2'
plt.title("Distribution of Feature 2")
plt.xlabel("Feature 2 Value")
plt.tight_layout()
plt.show()

# 2. Scatter plot for relationship between two numerical features
plt.figure(figsize=(7, 6))
sns.scatterplot(x='numerical_feature_1', y='numerical_feature_2', data=df_capstone, alpha=0.5, color='purple') # Replace feature names
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.title("Scatter Plot: Feature 1 vs. Feature 2")
plt.grid(True)
plt.show()

# 3. Box plots for categorical vs. numerical feature (if applicable)
plt.figure(figsize=(8, 6))
sns.boxplot(x='categorical_feature', y='numerical_feature_3', data=df_capstone, color='lightgreen') # Replace feature names
plt.xlabel("Categorical Feature")
plt.ylabel("Numerical Feature 3")
plt.title("Box Plot: Numerical Feature 3 by Category")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 4. Correlation Heatmap (for numerical features - if relevant)
numerical_cols = df_capstone.select_dtypes(include=np.number).columns # Select numerical columns
correlation_matrix = df_capstone[numerical_cols].corr()
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title("Correlation Matrix of Numerical Features")
plt.show()

# ... Add more EDA visualizations and analysis based on your project and research questions ...
```

Adapt these EDA examples to your specific dataset, research questions, and relevant features. Focus your EDA on exploring patterns, relationships, and potential insights that can help you address your capstone project goals.

**Document Your Data Collection and Exploration Process:**

Thoroughly document your data collection, cleaning, and EDA process in your project report (Chapter 20). Explain:

*   **Data sources and acquisition methods.**
*   **Data cleaning steps performed and justifications.**
*   **Key findings from EDA, visualizations, and summary statistics.**
*   **Any challenges or limitations encountered during data collection and exploration.**

This chapter provides a starting point for your capstone project's data phase. In the next chapter, you'll move on to data analysis and modeling, applying statistical methods or machine learning techniques to extract insights and address your research questions.
