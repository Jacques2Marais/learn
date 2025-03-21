# Chapter 9: Working with Real-World Datasets

In the previous chapters, we've built a strong foundation in Python for data science, covering essential libraries like NumPy, Pandas, Matplotlib, Seaborn, and SciPy. Now, it's time to apply these skills to real-world datasets. Working with real-world data is often messier and more complex than textbook examples, but it's where data science truly shines. This chapter will guide you through the process of finding, accessing, cleaning, exploring, and analyzing real-world datasets, with a focus on datasets relevant to physics and related fields.

## Finding and Accessing Public Datasets

The first step is to find suitable datasets for your analysis. Many organizations and institutions make datasets publicly available for research and educational purposes. Here are some excellent sources for finding public datasets:

*   **Kaggle Datasets ([https://www.kaggle.com/datasets](https://www.kaggle.com/datasets)):** A vast collection of datasets from various domains, often used in data science competitions. You can find datasets on physics, astronomy, climate, and more.
*   **UCI Machine Learning Repository ([http://archive.ics.uci.edu/ml/datasets.php](http://archive.ics.uci.edu/ml/datasets.php)):** A classic repository of datasets used in machine learning research.
*   **Google Dataset Search ([https://datasetsearch.research.google.com/](https://datasetsearch.research.google.com/)):** A search engine specifically for datasets across the web.
*   **Data.gov ([https://www.data.gov/](https://www.data.gov/)):** US government's open data portal, with datasets from various federal agencies.
*   **European Open Data Portal ([https://data.europa.eu/euodp/en/data/](https://data.europa.eu/euodp/en/data/)):** Access to public data from European institutions and agencies.
*   **NASA Open Data ([https://data.nasa.gov/](https://data.nasa.gov/)):** NASA's open data portal, with datasets related to space science, earth science, and aeronautics.
*   **NOAA Data ([https://www.noaa.gov/data](https://www.noaa.gov/data)):** National Oceanic and Atmospheric Administration data, including climate, weather, and oceanographic data.
*   **Physics-related datasets on specialized repositories:** For specific physics domains (e.g., particle physics, astrophysics), look for datasets on relevant research institution websites or specialized data repositories.

**Accessing Datasets:**

Datasets can be available in various formats (CSV, Excel, JSON, SQL databases, etc.) and accessed through different methods:

*   **Direct download:** Many datasets can be downloaded directly as files (e.g., CSV, ZIP archives).
*   **APIs (Application Programming Interfaces):** Some datasets are accessed through APIs, which allow you to programmatically query and retrieve data.
*   **Web scraping:** In some cases, you might need to extract data from websites (use ethically and respect website terms of service).
*   **Database connections:** Datasets might be stored in databases that you can connect to using Python libraries like `sqlite3` or database connectors.

For this chapter, we'll focus on datasets that can be downloaded as files, particularly CSV files, as they are common and easy to work with in Pandas.

## Data Wrangling and Cleaning in Practice

Real-world datasets are rarely clean and ready for analysis right away. Data wrangling (or data munging) and cleaning are crucial steps to transform raw data into a usable format and handle imperfections. Common data cleaning tasks include:

*   **Handling missing values:** Identifying and dealing with missing data (NaN, None, empty strings, etc.) using techniques like imputation or removal.
*   **Dealing with inconsistent formatting:** Standardizing data formats (e.g., dates, times, units, string casing).
*   **Handling outliers:** Identifying and deciding how to treat or remove outlier data points.
*   **Data type conversion:** Ensuring columns have appropriate data types (e.g., numeric, categorical, datetime).
*   **Removing duplicates:** Identifying and removing duplicate records.
*   **Data validation:** Checking for data integrity and consistency, ensuring data makes sense in the context.

**Example: Data Wrangling and Cleaning with Pandas**

Let's consider a hypothetical dataset of exoplanet properties (you can find real exoplanet datasets on NASA Exoplanet Archive or Kaggle). Assume we have a CSV file `exoplanets.csv` with some imperfections.

```python
# Code cell
import pandas as pd
import numpy as np

# Load the dataset (replace 'exoplanets.csv' with your actual file path)
df_exoplanets = pd.read_csv('exoplanets.csv')

# Initial exploration
print("Initial DataFrame info:\n")
df_exoplanets.info() # Get DataFrame summary (data types, non-null counts, memory usage)
print("\nFirst 5 rows of DataFrame:\n", df_exoplanets.head()) # Display first few rows
print("\nSummary statistics:\n", df_exoplanets.describe()) # Summary statistics for numeric columns

# --- Data Cleaning Steps ---

# 1. Handle Missing Values
print("\nMissing values per column (initial):\n", df_exoplanets.isnull().sum()) # Count missing values per column

# Option 1: Drop rows with missing values in critical columns (e.g., 'planet_name', 'star_mass')
df_cleaned = df_exoplanets.dropna(subset=['planet_name', 'star_mass']) # Drop rows with NaN in specified columns
print("\nDataFrame shape after dropping rows with missing 'planet_name' or 'star_mass':", df_cleaned.shape)

# Option 2: Impute missing values (e.g., fill missing 'planet_radius' with mean radius)
mean_radius = df_cleaned['planet_radius'].mean()
df_cleaned['planet_radius'].fillna(mean_radius, inplace=True) # Fill NaN values in 'planet_radius' with mean
print("\nMissing values after imputation in 'planet_radius':", df_cleaned['planet_radius'].isnull().sum())

# 2. Data Type Conversion
print("\nData types before conversion:\n", df_cleaned.dtypes)
df_cleaned['discovery_year'] = pd.to_datetime(df_cleaned['discovery_year'], format='%Y') # Convert 'discovery_year' to datetime
df_cleaned['star_mass'] = pd.to_numeric(df_cleaned['star_mass'], errors='coerce') # Ensure 'star_mass' is numeric, coerce errors to NaN
print("\nData types after conversion:\n", df_cleaned.dtypes)

# 3. Handle Inconsistent Units (if applicable in your dataset)
# Example: Assume 'planet_radius' is in Earth radii, convert to km if needed
earth_radius_km = 6371 # km
df_cleaned['planet_radius_km'] = df_cleaned['planet_radius'] * earth_radius_km
print("\nDataFrame with 'planet_radius_km' column:\n", df_cleaned[['planet_name', 'planet_radius', 'planet_radius_km']].head())

# 4. Handle Outliers (example: remove planets with extremely large radii - hypothetical outlier removal)
radius_threshold = 20 # Earth radii (example threshold)
df_cleaned_no_outliers = df_cleaned[df_cleaned['planet_radius'] <= radius_threshold]
print("\nDataFrame shape after outlier removal (radius > 20 Earth radii):", df_cleaned_no_outliers.shape)

# 5. Remove Duplicates (if any, based on planet name or other identifiers)
df_cleaned_no_duplicates = df_cleaned_no_outliers.drop_duplicates(subset=['planet_name']) # Drop duplicates based on 'planet_name'
print("\nDataFrame shape after removing duplicate planet names:", df_cleaned_no_duplicates.shape)

# Final cleaned DataFrame
print("\nCleaned DataFrame info:\n")
df_cleaned_no_duplicates.info()
print("\nFirst 5 rows of cleaned DataFrame:\n", df_cleaned_no_duplicates.head())
```

**Note:** Data cleaning steps are highly dataset-dependent. You need to carefully examine your data, understand its context, and choose appropriate cleaning techniques.

## Exploratory Data Analysis (EDA) Techniques

Exploratory Data Analysis (EDA) is a crucial step to understand your dataset, discover patterns, and formulate hypotheses before formal analysis or modeling. Common EDA techniques include:

*   **Summary statistics:** Calculating descriptive statistics (mean, median, std dev, min, max, quartiles) using `df.describe()`, `df.mean()`, `df.median()`, `df.std()`, etc.
*   **Data visualization:** Creating plots and charts to visualize distributions, relationships, and patterns (histograms, scatter plots, box plots, heatmaps, etc.) using Matplotlib and Seaborn.
*   **Correlation analysis:** Calculating correlations between variables using `df.corr()` and visualizing correlation matrices with heatmaps.
*   **Grouped analysis:** Using `groupby()` to explore data within different categories or groups and calculate group-wise statistics or visualizations.
*   **Univariate and multivariate analysis:** Examining individual variables (univariate) and relationships between multiple variables (multivariate).

**Example: Exploratory Data Analysis on Exoplanet Dataset**

Continuing with the cleaned exoplanet dataset `df_cleaned_no_duplicates`.

```python
# Code cell
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Assume df_cleaned_no_duplicates is your cleaned DataFrame from previous steps

# 1. Summary Statistics
print("\nSummary statistics for cleaned DataFrame:\n", df_cleaned_no_duplicates.describe())

# 2. Histograms for numerical features
plt.figure(figsize=(12, 6))
plt.subplot(1, 2, 1)
sns.histplot(df_cleaned_no_duplicates['star_mass'].dropna(), bins=30, kde=True, color='skyblue')
plt.title("Distribution of Star Mass")
plt.xlabel("Star Mass (Solar Masses)")

plt.subplot(1, 2, 2)
sns.histplot(df_cleaned_no_duplicates['planet_radius_km'].dropna(), bins=30, kde=True, color='lightcoral')
plt.title("Distribution of Planet Radius (km)")
plt.xlabel("Planet Radius (km)")
plt.tight_layout()
plt.show()

# 3. Scatter plot: Star Mass vs. Planet Radius
plt.figure(figsize=(8, 6))
sns.scatterplot(x='star_mass', y='planet_radius_km', data=df_cleaned_no_duplicates, alpha=0.6, color='purple')
plt.xlabel("Star Mass (Solar Masses)")
plt.ylabel("Planet Radius (km)")
plt.title("Scatter Plot: Star Mass vs. Planet Radius")
plt.grid(True)
plt.show()

# 4. Box plot: Planet Radius by Discovery Year (example of categorical/time-based grouping)
plt.figure(figsize=(10, 6))
sns.boxplot(x=df_cleaned_no_duplicates['discovery_year'].dt.year, y='planet_radius_km', color='lightgreen') # Extract year from datetime
plt.xlabel("Discovery Year")
plt.ylabel("Planet Radius (km)")
plt.title("Box Plot: Planet Radius Distribution over Discovery Years")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 5. Correlation Matrix (for numerical features)
correlation_matrix = df_cleaned_no_duplicates[['star_mass', 'planet_radius_km']].corr()
plt.figure(figsize=(6, 5))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title("Correlation Matrix: Star Mass and Planet Radius")
plt.show()
```

EDA is an iterative and exploratory process. You'll generate various visualizations and statistics, ask questions about your data, and refine your analysis based on your findings.

## Case Studies: Analyzing Physics-Related Datasets

To solidify your understanding, let's consider potential case studies using physics-related datasets. Here are some ideas:

**1. Exoplanet Data Analysis:**

*   **Dataset:** NASA Exoplanet Archive, Kaggle Exoplanet datasets.
*   **Analysis goals:**
    *   Explore distributions of exoplanet properties (radius, mass, orbital period, etc.).
    *   Investigate correlations between star properties and planet properties.
    *   Search for potentially habitable exoplanets based on certain criteria (e.g., radius, temperature).
    *   Analyze trends in exoplanet discoveries over time.

**2. Particle Physics Dataset Analysis:**

*   **Dataset:** Open particle physics datasets from CERN Open Data Portal or other sources.
*   **Analysis goals:**
    *   Analyze particle collision events and identify different particle types.
    *   Study particle decay processes and branching ratios.
    *   Visualize particle momentum and energy distributions.
    *   Apply machine learning techniques for particle identification or event classification (in later chapters).

**3. Climate Change Data Analysis:**

*   **Dataset:** NOAA climate datasets, NASA GISS Surface Temperature Analysis (GISTEMP), etc.
*   **Analysis goals:**
    *   Analyze global temperature trends over time.
    *   Visualize temperature anomalies and climate patterns.
    *   Explore correlations between temperature and other climate variables (CO2 levels, sea ice extent, etc.).
    *   Study regional climate variations and trends.

**4. Astronomical Data Analysis:**

*   **Dataset:** Sloan Digital Sky Survey (SDSS), astronomical catalogs, etc.
*   **Analysis goals:**
    *   Analyze galaxy properties (size, luminosity, redshift).
    *   Classify galaxies based on morphology or spectral characteristics.
    *   Study the distribution of galaxies in the universe.
    *   Investigate relationships between galaxy properties and environment.

For each case study, you would follow these steps:

1.  **Dataset selection and access:** Choose a relevant dataset and download or access it.
2.  **Data loading:** Load the dataset into a Pandas DataFrame.
3.  **Data cleaning and wrangling:** Perform necessary cleaning steps to handle missing values, inconsistencies, etc.
4.  **Exploratory Data Analysis (EDA):** Use summary statistics and visualizations to explore the dataset and identify patterns.
5.  **Formulate questions and hypotheses:** Based on EDA, formulate specific questions or hypotheses you want to investigate further.
6.  **Statistical analysis or modeling:** Apply appropriate statistical techniques (hypothesis tests, regression, etc.) or machine learning models to answer your questions or test hypotheses (machine learning in later chapters).
7.  **Interpretation and communication:** Interpret your results and communicate your findings effectively using visualizations and clear explanations.

Working through case studies like these will provide you with valuable hands-on experience in applying Python data science tools to real-world problems in physics and related domains.

**In this chapter, we've covered:**

*   Finding and accessing public datasets from various sources.
*   Data wrangling and cleaning techniques in practice using Pandas.
*   Exploratory Data Analysis (EDA) techniques for understanding datasets.
*   Case study ideas for analyzing physics-related datasets (exoplanets, particle physics, climate, astronomy).

In the next chapter, we'll transition to Part 3 and begin exploring machine learning concepts and algorithms using scikit-learn.
