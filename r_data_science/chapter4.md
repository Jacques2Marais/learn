# Chapter 4: Statistical Analysis in R

Welcome to the world of statistical analysis with R! In this chapter, we'll explore how R can be used to perform various statistical analyses, from basic descriptive statistics to hypothesis testing and linear regression. R's statistical capabilities are a major reason for its popularity in data science.

## Descriptive Statistics and Hypothesis Testing

Descriptive statistics help summarize and describe the main features of a dataset. Hypothesis testing allows us to make inferences about populations based on sample data.

### Descriptive Statistics

R provides functions to calculate common descriptive statistics:

*   **`mean()`:** Calculate the mean (average).
*   **`median()`:** Calculate the median (middle value).
*   **`sd()`:** Calculate the standard deviation (measure of spread).
*   **`var()`:** Calculate the variance (squared standard deviation).
*   **`min()`:** Find the minimum value.
*   **`max()`:** Find the maximum value.
*   **`range()`:** Get the range (minimum and maximum values).
*   **`quantile()`:** Calculate quantiles (including percentiles).
*   **`summary()`:** Provides a summary of common statistics for each column in a data frame.

Let's use the `iris` dataset again.

```R
# Calculate mean and standard deviation of Sepal.Length
mean(iris$Sepal.Length)
sd(iris$Sepal.Length)

# Calculate median of Sepal.Width
median(iris$Sepal.Width)

# Get the range of Petal.Length
range(iris$Petal.Length)

# Calculate quantiles of Sepal.Width (e.g., quartiles)
quantile(iris$Sepal.Width) # Default quantiles: 0%, 25%, 50%, 75%, 100%
quantile(iris$Sepal.Width, probs = c(0.1, 0.9)) # 10th and 90th percentiles

# Summary statistics for the entire iris data frame
summary(iris)
```

For grouped data, you can use `dplyr`'s `group_by()` and `summarise()` to calculate group-wise descriptive statistics.

```R
library(dplyr)

iris %>%
  group_by(Species) %>%
  summarise(
    mean_sepal_length = mean(Sepal.Length),
    sd_sepal_length = sd(Sepal.Length),
    median_petal_width = median(Petal.Width)
  )
```

### Hypothesis Testing

Hypothesis testing is used to assess evidence for a claim about a population. Common hypothesis tests in R include:

*   **t-tests:**  Compare means of one or two groups (`t.test()`).
*   **ANOVA (Analysis of Variance):** Compare means of more than two groups (`aov()`).
*   **Chi-squared tests:**  Test for association between categorical variables (`chisq.test()`).
*   **Correlation tests:** Test for correlation between numeric variables (`cor.test()`).

**Example: One-sample t-test**

Suppose we want to test if the mean sepal length of iris flowers is significantly different from 5.5 cm.

*   **Null hypothesis (H0):**  Mean sepal length = 5.5 cm
*   **Alternative hypothesis (H1):** Mean sepal length ≠ 5.5 cm

```R
t.test(iris$Sepal.Length, mu = 5.5) # mu is the hypothesized mean
```

The output will give you:

*   **t-statistic:**  The calculated test statistic.
*   **df:** Degrees of freedom.
*   **p-value:**  The probability of observing the data if the null hypothesis is true.
*   **Confidence interval:**  A range of plausible values for the true mean.
*   **Sample mean:** The mean of your sample data.

If the p-value is less than a chosen significance level (e.g., 0.05), you reject the null hypothesis.

**Example: Independent samples t-test**

Let's test if there's a significant difference in mean sepal length between *setosa* and *versicolor* iris species.

*   **H0:** Mean sepal length of setosa = Mean sepal length of versicolor
*   **H1:** Mean sepal length of setosa ≠ Mean sepal length of versicolor

```R
setosa_sepal_length <- iris$Sepal.Length[iris$Species == "setosa"]
versicolor_sepal_length <- iris$Sepal.Length[iris$Species == "versicolor"]

t.test(setosa_sepal_length, versicolor_sepal_length) # Two-sample t-test
```

**Example: Chi-squared test**

Let's consider a hypothetical example. Suppose we have a data frame `survey_data` with categorical variables `gender` and `preference` (e.g., "coffee" vs. "tea"). We want to test if there's an association between gender and preference.

```R
# Hypothetical survey data (replace with your actual data)
survey_data <- data.frame(
  gender = factor(rep(c("Male", "Female"), each = 100)),
  preference = factor(sample(c("Coffee", "Tea"), 200, replace = TRUE, prob = c(0.6, 0.4))) # Example preferences
)

# Create a contingency table
contingency_table <- table(survey_data$gender, survey_data$preference)
contingency_table

# Perform chi-squared test
chisq.test(contingency_table)
```

## Linear Regression and Correlation

Linear regression models the linear relationship between a dependent variable and one or more independent variables. Correlation measures the strength and direction of a linear relationship between two variables.

### Linear Regression

In R, you can fit linear models using the `lm()` function (linear model).

**Example: Simple linear regression**

Let's model `Sepal.Width` as a function of `Sepal.Length` in the `iris` dataset.

```R
linear_model <- lm(Sepal.Width ~ Sepal.Length, data = iris) # Formula: y ~ x, data source
summary(linear_model) # Get model summary
```

`summary(linear_model)` provides important information:

*   **Coefficients:**  Estimates for the intercept and slope.  In `Sepal.Width ~ Sepal.Length`, `Sepal.Length`'s coefficient represents the change in `Sepal.Width` for a one-unit increase in `Sepal.Length`.
*   **Standard Errors:**  Measures of the variability of coefficient estimates.
*   **t-values and p-values:**  For hypothesis tests that coefficients are zero (no effect).
*   **R-squared:**  Coefficient of determination, representing the proportion of variance in the dependent variable explained by the model.
*   **Adjusted R-squared:**  Adjusted R-squared, which penalizes adding unnecessary variables to the model.
*   **F-statistic and p-value:**  For overall model significance test.

**Making predictions with a linear model:**

```R
new_data <- data.frame(Sepal.Length = c(5, 6, 7)) # New Sepal.Length values
predictions <- predict(linear_model, newdata = new_data) # Predict Sepal.Width
predictions
```

**Multiple linear regression:**  Include more than one independent variable in the model.

```R
multiple_model <- lm(Sepal.Width ~ Sepal.Length + Petal.Length + Petal.Width + Species, data = iris)
summary(multiple_model)
```

### Correlation

Calculate correlation coefficients using `cor()`. Common types are Pearson, Spearman, and Kendall. Pearson measures linear correlation, Spearman and Kendall are rank-based (non-parametric).

```R
# Pearson correlation between Sepal.Length and Sepal.Width
cor(iris$Sepal.Length, iris$Sepal.Width, method = "pearson") # Default method is Pearson

# Spearman correlation
cor(iris$Sepal.Length, iris$Sepal.Width, method = "spearman")

# Correlation matrix for multiple variables
cor_matrix <- cor(iris[, 1:4], method = "pearson") # Correlation matrix for first 4 columns (numeric)
cor_matrix

# Test for correlation and get confidence interval and p-value using cor.test()
cor.test(iris$Sepal.Length, iris$Sepal.Width, method = "pearson")
```

## Basic Statistical Models in R

Beyond linear regression, R offers a vast array of statistical modeling capabilities. Here are a few examples:

*   **Generalized Linear Models (GLMs):**  Extend linear regression to handle non-normal response variables (e.g., binary, count data). Use `glm()`.

    ```R
    # Example: Logistic regression (for binary outcomes) - using a hypothetical binary outcome for Species
    iris$Is_Setosa <- ifelse(iris$Species == "setosa", 1, 0) # Create binary outcome: Is it setosa?
    logistic_model <- glm(Is_Setosa ~ Sepal.Length + Sepal.Width, data = iris, family = "binomial") # family = "binomial" for logistic regression
    summary(logistic_model)
    ```

*   **Analysis of Variance (ANOVA):**  Compare means across multiple groups. Use `aov()` or `lm()`.

    ```R
    # ANOVA to compare mean Sepal.Length across Species
    anova_model <- aov(Sepal.Length ~ Species, data = iris)
    summary(anova_model) # ANOVA table

    # Equivalent using lm()
    lm_anova_model <- lm(Sepal.Length ~ Species, data = iris)
    anova(lm_anova_model) # ANOVA table
    ```

*   **Non-parametric tests:**  For situations where assumptions of parametric tests (like normality) are violated. Examples: Wilcoxon rank-sum test (`wilcox.test()`), Kruskal-Wallis test (`kruskal.test()`).

    ```R
    # Wilcoxon rank-sum test (non-parametric alternative to t-test)
    wilcox.test(setosa_sepal_length, versicolor_sepal_length) # Using sepal length data from earlier t-test example

    # Kruskal-Wallis test (non-parametric alternative to ANOVA)
    kruskal.test(Sepal.Length ~ Species, data = iris)
    ```

*   **Time Series Analysis:**  For analyzing data collected over time. Packages like `forecast`, `tseries`, `xts` provide tools for time series modeling, forecasting, decomposition, etc.

*   **Clustering and Dimensionality Reduction:**  Techniques for unsupervised learning. R packages offer implementations of k-means clustering (`kmeans()`), hierarchical clustering (`hclust()`), principal component analysis (PCA, `prcomp()`), and more. We'll touch on these in later chapters.

## Let's Practice!

1.  **Descriptive Statistics:**
    *   Choose a dataset (e.g., `iris` or one you imported in Chapter 2).
    *   Calculate descriptive statistics (mean, median, sd, quantiles, etc.) for numeric variables.
    *   Use `group_by()` and `summarise()` to calculate group-wise statistics for categorical variables.
2.  **Hypothesis Testing:**
    *   Perform one-sample t-tests to test hypotheses about population means.
    *   Conduct independent samples t-tests to compare means of two groups.
    *   If you have categorical data, try chi-squared tests for association.
3.  **Linear Regression:**
    *   Build simple linear regression models to predict a numeric variable from another.
    *   Interpret the model summary (coefficients, R-squared, p-values).
    *   Make predictions using your linear model.
    *   Explore multiple linear regression with several predictors.
4.  **Correlation:**
    *   Calculate Pearson and Spearman correlation coefficients between numeric variables.
    *   Examine correlation matrices.
    *   Perform correlation tests using `cor.test()`.
5.  **Explore other statistical models:**  (Optional, if you're ready for more)
    *   Try fitting a logistic regression model using `glm()` (you might need to create a binary outcome variable from your data).
    *   Perform ANOVA using `aov()` to compare means across groups.
    *   Experiment with non-parametric tests like `wilcox.test()` or `kruskal.test()`.

## Chapter Summary

In this chapter, you've taken a significant step into statistical analysis with R. You've learned about:

*   Calculating **descriptive statistics** to summarize data.
*   Performing **hypothesis tests** like t-tests and chi-squared tests to make inferences.
*   Building and interpreting **linear regression models** to understand relationships between variables.
*   Measuring **correlation** between variables.
*   An overview of **basic statistical models** available in R, including GLMs and ANOVA.

R's statistical capabilities are vast, and this chapter is just the beginning. As you continue your data science journey, you'll delve into more advanced statistical techniques and models. In the next chapter, we'll focus on advanced data wrangling and transformation techniques to prepare your data for even more sophisticated analyses!
