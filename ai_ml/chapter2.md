# Chapter 2: Data Fundamentals

## Data collection and preparation

Data collection is the foundation of any successful AI/ML project. It involves gathering data from various sources, ensuring its quality, and preparing it for analysis. Common data sources include:

*   **Databases:** Structured data stored in relational databases (e.g., MySQL, PostgreSQL) or NoSQL databases (e.g., MongoDB, Cassandra).
*   **APIs:** Data retrieved from web services using APIs (e.g., Twitter API, OpenWeather API).
*   **Web Scraping:** Extracting data from websites using web scraping tools (e.g., Beautiful Soup, Scrapy).
*   **Files:** Data stored in various file formats (e.g., CSV, JSON, Excel).

Data quality is crucial for building accurate and reliable ML models. It's important to ensure that the data is:

*   **Accurate:** Free from errors and inconsistencies.
*   **Complete:** Contains all the necessary information.
*   **Consistent:** Follows the same format and conventions.
*   **Timely:** Up-to-date and relevant.

Data preparation involves transforming the data into a suitable format for ML models. This may include:

*   **Data Cleaning:** Handling missing values, outliers, and inconsistencies.
*   **Data Transformation:** Scaling, normalization, and encoding categorical variables.
*   **Data Integration:** Combining data from multiple sources.

Common data storage formats include:

*   **CSV (Comma-Separated Values):** A simple text-based format for storing tabular data.
*   **JSON (JavaScript Object Notation):** A human-readable format for storing structured data.
*   **SQL (Structured Query Language):** A language for managing and querying data in relational databases.

## Data cleaning and preprocessing

Data cleaning and preprocessing are essential steps in preparing data for ML models. These steps involve handling missing values, outliers, inconsistencies, and transforming the data into a suitable format for analysis.

**Handling Missing Values:**

*   **Imputation:** Replacing missing values with estimated values. Common imputation methods include:
    *   Mean/Median Imputation: Replacing missing values with the mean or median of the available values.
    *   Mode Imputation: Replacing missing values with the most frequent value.
    *   K-Nearest Neighbors (KNN) Imputation: Replacing missing values with the average of the K nearest neighbors.
*   **Deletion:** Removing rows or columns with missing values. This should be done carefully, as it can lead to loss of information.

**Outlier Detection and Removal:**

*   **Z-Score:** A measure of how many standard deviations a data point is from the mean. Data points with a Z-score above a certain threshold (e.g., 3) are considered outliers.
*   **IQR (Interquartile Range):** The difference between the 75th percentile (Q3) and the 25th percentile (Q1). Data points below Q1 - 1.5 * IQR or above Q3 + 1.5 * IQR are considered outliers.

**Scaling and Normalization:**

*   **Min-Max Scaling:** Scaling the data to a range between 0 and 1.
*   **Standardization:** Scaling the data to have a mean of 0 and a standard deviation of 1.

**Encoding Categorical Variables:**

*   **One-Hot Encoding:** Creating a binary column for each category.
*   **Label Encoding:** Assigning a unique integer to each category.

## Data visualization

Data visualization is a powerful tool for gaining insights from data and communicating findings to others. Different types of visualizations are suitable for different types of data and purposes. Some common types of data visualizations include:

*   **Histograms:** Used to visualize the distribution of a single numerical variable.
*   **Scatter Plots:** Used to visualize the relationship between two numerical variables.
*   **Bar Charts:** Used to compare the values of different categories.
*   **Line Charts:** Used to visualize trends over time.
*   **Box Plots:** Used to visualize the distribution of a numerical variable and identify outliers.

Choosing the appropriate visualization depends on the type of data and the insights you want to convey. For example, if you want to visualize the distribution of customer ages, a histogram would be a good choice. If you want to visualize the relationship between advertising spend and sales, a scatter plot would be more appropriate.

Popular tools for data visualization include:

*   **Matplotlib:** A Python library for creating static, interactive, and animated visualizations.
*   **Seaborn:** A Python library built on top of Matplotlib that provides a high-level interface for creating informative and aesthetically pleasing visualizations.
*   **Tableau:** A commercial data visualization tool that allows users to create interactive dashboards and reports.

## Feature engineering

Feature engineering is the art and science of selecting, transforming, and creating new features from existing data to improve the performance of ML models. It often involves using domain knowledge to identify relevant features and create new ones that capture important relationships in the data. Some common feature engineering techniques include:

*   **Polynomial Features:** Creating new features by raising existing features to a power (e.g., squaring a feature).
*   **Interaction Features:** Creating new features by combining two or more existing features (e.g., multiplying two features).
*   **Domain-Specific Features:** Creating features based on domain knowledge. For example, in a marketing context, you might create a feature that represents the customer's lifetime value.

Feature selection is the process of selecting the most relevant features for a model. This can help to improve model performance, reduce overfitting, and simplify the model. Dimensionality reduction techniques, such as Principal Component Analysis (PCA), can also be used to reduce the number of features in a data set while preserving important information.
