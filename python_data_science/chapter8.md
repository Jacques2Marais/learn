# Chapter 8: Statistical Analysis with SciPy

SciPy (Scientific Python) is another core library in the Python scientific ecosystem. It builds upon NumPy and provides a wide range of modules for scientific and technical computing, including statistical analysis, optimization, integration, interpolation, signal processing, linear algebra, and more. In this chapter, we'll focus on SciPy's statistical capabilities, particularly relevant for data science and physics applications.

## Introduction to SciPy: Statistical Functions, Distributions

The `scipy.stats` module in SciPy is dedicated to statistical functions and probability distributions. It provides tools for:

*   **Probability distributions:** Working with various continuous and discrete probability distributions (e.g., normal, t-distribution, chi-squared, binomial, Poisson).
*   **Descriptive statistics:** Calculating summary statistics (e.g., mean, median, variance, standard deviation, skewness, kurtosis).
*   **Hypothesis testing:** Performing statistical tests to make inferences about populations based on sample data (e.g., t-tests, chi-squared tests, ANOVA).
*   **Regression and correlation:** Regression analysis, correlation calculations.

**Probability Distributions:**

SciPy `stats` module provides classes for numerous probability distributions. For each distribution, you can:

*   **Calculate probability density function (PDF) or probability mass function (PMF):** `dist.pdf(x)` for continuous, `dist.pmf(k)` for discrete.
*   **Calculate cumulative distribution function (CDF):** `dist.cdf(x)` or `dist.cdf(k)`.
*   **Generate random samples:** `dist.rvs(size=n)`.
*   **Calculate statistical moments (mean, variance, skewness, kurtosis):** `dist.mean()`, `dist.var()`, `dist.stats(moments='mvsk')`.

**Example: Working with the Normal (Gaussian) distribution**

```python
# Code cell
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

# Normal distribution (mean=0, std dev=1)
norm_dist = stats.norm

# Calculate PDF at x=0
pdf_value = norm_dist.pdf(0)
print("PDF at x=0:", pdf_value) # Output: 0.3989422804014327

# Calculate CDF at x=1
cdf_value = norm_dist.cdf(1)
print("CDF at x=1:", cdf_value) # Output: 0.8413447460685429

# Generate 1000 random samples from normal distribution
random_samples = norm_dist.rvs(size=1000)

# Calculate mean and standard deviation of the distribution
mean_val, std_val = norm_dist.stats(moments='mv') # 'mv' for mean and variance
print("Mean:", mean_val) # Output: 0.0 (theoretical mean of standard normal)
print("Standard deviation:", np.sqrt(std_val)) # Output: 1.0 (theoretical std dev of standard normal)

# Plot PDF
x = np.linspace(-4, 4, 100)
pdf_values = norm_dist.pdf(x)
plt.plot(x, pdf_values, label='Normal PDF')
plt.title("Normal Distribution PDF")
plt.xlabel("x")
plt.ylabel("PDF(x)")
plt.legend()
plt.show()

# Plot histogram of random samples
plt.hist(random_samples, bins=30, density=True, alpha=0.6, color='skyblue', label='Random Samples Histogram') # density=True for normalized histogram
plt.plot(x, pdf_values, 'r-', label='Normal PDF') # Overlay PDF
plt.title("Normal Distribution: Histogram of Random Samples vs. PDF")
plt.xlabel("Value")
plt.ylabel("Density")
plt.legend()
plt.show()
```

SciPy `stats` supports many other distributions, including:

*   **Continuous distributions:** `t`, `chi2`, `f`, `uniform`, `expon`, `gamma`, `beta`, ...
*   **Discrete distributions:** `binom`, `poisson`, `randint`, `geom`, ...

Refer to the SciPy documentation for a complete list and details on each distribution: [https://docs.scipy.org/doc/scipy/reference/stats.html](https://docs.scipy.org/doc/scipy/reference/stats.html)

## Hypothesis Testing: t-tests, chi-squared tests

Hypothesis testing is a fundamental part of statistical inference. It's used to make decisions or draw conclusions about a population based on sample data. SciPy `stats` provides functions to perform various hypothesis tests.

**1. t-tests:**

t-tests are used to compare means of one or two groups.

*   **One-sample t-test (`stats.ttest_1samp()`):** Tests if the mean of a single sample differs significantly from a known population mean.
*   **Independent samples t-test (`stats.ttest_ind()`):** Tests if the means of two independent groups are significantly different.
*   **Paired samples t-test (`stats.ttest_rel()`):** Tests if the means of two related (paired) samples are significantly different (e.g., before-and-after measurements).

**Example: Independent samples t-test**

Suppose you have two groups of physics students, and you want to test if there's a significant difference in their exam scores.

```python
# Code cell
from scipy import stats
import numpy as np

# Exam scores for two groups of students
group_a_scores = np.array([75, 80, 85, 90, 78, 82, 88, 92])
group_b_scores = np.array([68, 72, 78, 84, 70, 75, 80, 85])

# Perform independent samples t-test
t_statistic, p_value = stats.ttest_ind(group_a_scores, group_b_scores)

print("T-statistic:", t_statistic)
print("P-value:", p_value)

alpha = 0.05 # Significance level

if p_value < alpha:
    print("Reject null hypothesis: Means are significantly different.")
else:
    print("Fail to reject null hypothesis: No significant difference in means.")
```

**2. Chi-squared tests:**

Chi-squared tests are used for categorical data.

*   **Chi-squared goodness-of-fit test (`stats.chisquare()`):** Tests if observed frequencies of categories match expected frequencies.
*   **Chi-squared test of independence (`stats.chi2_contingency()`):** Tests if two categorical variables are independent in a contingency table.

**Example: Chi-squared goodness-of-fit test**

Suppose you want to test if a die is fair. You roll it 60 times and observe the frequencies of each face.

```python
# Code cell
from scipy import stats

observed_frequencies = [8, 11, 10, 9, 12, 10] # Observed counts for faces 1 to 6
expected_frequencies = [10, 10, 10, 10, 10, 10] # Expected counts

# Perform chi-squared goodness-of-fit test
chi2_statistic, p_value = stats.chisquare(f_obs=observed_frequencies, f_exp=expected_frequencies)

print("Chi-squared statistic:", chi2_statistic)
print("P-value:", p_value)

alpha = 0.05 # Significance level

if p_value < alpha:
    print("Reject null hypothesis: Die is not fair.")
else:
    print("Fail to reject null hypothesis: Die is fair (or we don't have enough evidence to reject fairness).")
```

**Example: Chi-squared test of independence**

Suppose you want to test if there's a relationship between gender and preference for physics vs. biology among students.

```python
# Code cell
from scipy.stats import chi2_contingency
import pandas as pd

# Contingency table (observed frequencies)
observed_data = pd.DataFrame({
    'Physics': [40, 60], # [Male, Female] preferring Physics
    'Biology': [60, 40]  # [Male, Female] preferring Biology
}, index=['Male', 'Female'])
print("Observed data (contingency table):\n", observed_data)
# Output:
#         Physics  Biology
# Male         40       60
# Female       60       40

# Perform chi-squared test of independence
chi2_statistic, p_value, dof, expected_frequencies = chi2_contingency(observed_data)

print("\nChi-squared statistic:", chi2_statistic)
print("P-value:", p_value)
print("Degrees of freedom:", dof)
print("Expected frequencies (under independence):\n", expected_frequencies)

alpha = 0.05 # Significance level

if p_value < alpha:
    print("Reject null hypothesis: Gender and subject preference are dependent.")
else:
    print("Fail to reject null hypothesis: Gender and subject preference are independent (or no enough evidence to reject independence).")
```

## Regression Analysis: Linear Regression, Polynomial Regression

Regression analysis is used to model the relationship between a dependent variable and one or more independent variables. SciPy `stats` and `numpy.polyfit` provide tools for regression.

**1. Linear Regression:**

Linear regression models the relationship as a linear equation:  `y = mx + c`.

*   `stats.linregress(x, y)`: Performs linear regression and returns slope, intercept, r-value, p-value, and standard error of the estimate.

**Example: Linear regression**

Suppose you have data on the height and weight of individuals, and you want to model the relationship between them using linear regression.

```python
# Code cell
from scipy import stats
import matplotlib.pyplot as plt
import numpy as np

height = np.array([160, 165, 170, 175, 180]) # Heights in cm
weight = np.array([60, 65, 70, 75, 80])     # Weights in kg

# Perform linear regression
slope, intercept, r_value, p_value, std_err = stats.linregress(height, weight)

print("Slope:", slope)
print("Intercept:", intercept)
print("R-value (correlation coefficient):", r_value)
print("P-value:", p_value)
print("Standard error of estimate:", std_err)

# Create regression line for plotting
regression_line = slope * height + intercept

# Plot scatter plot and regression line
plt.scatter(height, weight, color='blue', label='Data points')
plt.plot(height, regression_line, color='red', label='Linear regression line')
plt.xlabel("Height (cm)")
plt.ylabel("Weight (kg)")
plt.title("Linear Regression: Height vs. Weight")
plt.legend()
plt.show()
```

**2. Polynomial Regression:**

Polynomial regression models the relationship as a polynomial equation (e.g., quadratic, cubic).

*   `np.polyfit(x, y, degree)`: Fits a polynomial of a specified degree to the data and returns polynomial coefficients.
*   `np.poly1d(coefficients)`: Creates a polynomial function from the coefficients.

**Example: Polynomial regression (quadratic)**

Suppose you have data that shows a curved relationship, and you want to fit a quadratic polynomial.

```python
# Code cell
import numpy as np
import matplotlib.pyplot as plt

x_poly = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
y_poly = np.array([1.5, 3.2, 5.5, 8.3, 11.5, 15.2, 19.3, 23.8, 28.7, 34.0])

# Fit a 2nd-degree polynomial (quadratic)
poly_coefficients = np.polyfit(x_poly, y_poly, 2) # Degree=2 for quadratic
polynomial_function = np.poly1d(poly_coefficients) # Create polynomial function

# Generate points for plotting the polynomial curve
x_plot = np.linspace(x_poly.min(), x_poly.max(), 100)
y_plot = polynomial_function(x_plot)

# Plot scatter plot and polynomial curve
plt.scatter(x_poly, y_poly, color='blue', label='Data points')
plt.plot(x_plot, y_plot, color='red', label='Quadratic regression curve')
plt.xlabel("X-values")
plt.ylabel("Y-values")
plt.title("Polynomial Regression (Quadratic)")
plt.legend()
plt.show()
```

## Optimization and Curve Fitting

SciPy `optimize` module provides functions for optimization, root finding, and curve fitting.

*   **Curve fitting (`scipy.optimize.curve_fit()`):** Fits a user-defined function to data by finding optimal parameter values that minimize the difference between the function and the data.

**Example: Curve fitting with `curve_fit()`**

Suppose you have data that you believe follows an exponential decay model, and you want to fit an exponential function to the data to estimate the decay parameters.

```python
# Code cell
import numpy as np
from scipy.optimize import curve_fit
import matplotlib.pyplot as plt

# Sample data (simulated exponential decay)
x_data = np.linspace(0, 5, 50)
y_data = 10 * np.exp(-0.5 * x_data) + np.random.normal(0, 0.5, 50) # Exponential decay with noise

# Define the function to fit (exponential decay model)
def exponential_decay(x, amplitude, decay_rate):
    return amplitude * np.exp(-decay_rate * x)

# Initial guess for parameters (amplitude, decay_rate)
initial_guess = [8, 0.3]

# Perform curve fitting
optimal_parameters, covariance_matrix = curve_fit(exponential_decay, x_data, y_data, p0=initial_guess)

# Extract optimal parameters
amplitude_optimal, decay_rate_optimal = optimal_parameters
print("Optimal Amplitude:", amplitude_optimal)
print("Optimal Decay Rate:", decay_rate_optimal)

# Generate curve from fitted parameters
y_fit = exponential_decay(x_data, amplitude_optimal, decay_rate_optimal)

# Plot data and fitted curve
plt.scatter(x_data, y_data, label='Data', color='blue')
plt.plot(x_data, y_fit, label='Fitted Exponential Decay Curve', color='red')
plt.xlabel("X-values")
plt.ylabel("Y-values")
plt.title("Curve Fitting: Exponential Decay")
plt.legend()
plt.show()
```

SciPy `optimize` module offers many more optimization algorithms (e.g., minimization, root finding) and curve fitting capabilities.

SciPy is a vast and powerful library for scientific computing. In this chapter, we've introduced its statistical analysis capabilities, including probability distributions, hypothesis testing (t-tests, chi-squared tests), regression analysis (linear, polynomial), and curve fitting. These tools are essential for analyzing data, making statistical inferences, and building models in various scientific and data science domains.

**In this chapter, we've covered:**

*   Introduction to SciPy and its `stats` module for statistical analysis.
*   Working with probability distributions (Normal distribution example).
*   Hypothesis testing: t-tests (one-sample, independent samples), chi-squared tests (goodness-of-fit, independence).
*   Regression analysis: linear regression, polynomial regression.
*   Curve fitting using `scipy.optimize.curve_fit()`.

In the next part of the course, we'll move towards more advanced data science topics and applications, including working with real-world datasets and an introduction to machine learning.
