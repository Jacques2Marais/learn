# Chapter 8: Advanced Statistical Modeling

Welcome to Advanced Statistical Modeling in R! Building upon Chapter 4, this chapter delves into more sophisticated statistical techniques. We'll explore Generalized Linear Models (GLMs), Time Series Analysis, and Clustering & Dimensionality Reduction. These methods expand your ability to analyze complex data and extract deeper insights.

## Generalized Linear Models (GLMs)

Generalized Linear Models (GLMs) are a flexible extension of linear regression. They allow you to model response variables that don't follow a normal distribution, such as binary outcomes (logistic regression), count data (Poisson regression), and more. GLMs consist of three components:

1.  **Random Component:** Specifies the probability distribution of the response variable (e.g., binomial, Poisson, gamma).
2.  **Systematic Component:**  A linear predictor that combines the independent variables (features).
3.  **Link Function:**  Connects the random and systematic components. It transforms the expected value of the response variable to the linear predictor scale (e.g., logit link for logistic regression, log link for Poisson regression).

### Logistic Regression

Logistic regression is used for binary classification problems where the target variable is categorical with two levels (e.g., 0/1, TRUE/FALSE, success/failure). It models the probability of the outcome belonging to a specific category.

*   **`glm()` function:** Use `glm()` with `family = "binomial"` to fit logistic regression models.

    ```R
    # Example: Predicting 'Is_Setosa' (binary outcome created in Chapter 4) based on Sepal.Length and Sepal.Width
    iris$Is_Setosa <- ifelse(iris$Species == "setosa", 1, 0) # Ensure binary outcome

    logistic_model <- glm(Is_Setosa ~ Sepal.Length + Sepal.Width, data = iris, family = "binomial")
    summary(logistic_model) # Model summary
    ```

    **Interpreting Logistic Regression Output:**

    *   **Coefficients:**  Log-odds ratios. Exponentiating coefficients (`exp(coef(logistic_model))`) gives odds ratios. An odds ratio > 1 means the odds of the outcome increase with a one-unit increase in the predictor.
    *   **Deviance:**  Measures model fit (similar to residuals in linear regression).
    *   **Null deviance:** Deviance of a null model (intercept only).
    *   **Residual deviance:** Deviance of the fitted model. Lower residual deviance indicates better fit.
    *   **AIC (Akaike Information Criterion):**  Another measure of model fit, penalizing model complexity. Lower AIC is better.

    **Making Predictions with Logistic Regression:**

    ```R
    new_data <- data.frame(Sepal.Length = c(5.5, 6.5), Sepal.Width = c(3.0, 3.2))
    probabilities <- predict(logistic_model, newdata = new_data, type = "response") # type = "response" for probabilities
    probabilities # Predicted probabilities of Is_Setosa = 1

    # Classify based on a threshold (e.g., 0.5)
    predictions <- ifelse(probabilities > 0.5, 1, 0)
    predictions # Predicted classes (0 or 1)
    ```

### Poisson Regression

Poisson regression is used for count data, where the response variable represents counts of events (e.g., number of website visits, number of accidents, number of defects). It assumes the response variable follows a Poisson distribution.

*   **`glm()` function:** Use `glm()` with `family = "poisson"` to fit Poisson regression models.

    ```R
    # Hypothetical example: Modeling website visits (count data)
    website_data <- data.frame(
      day = 1:30,
      ads_spend = runif(30, 100, 500), # Daily ad spend
      visits = rpois(30, lambda = 50 + 0.2 * ads_spend) # Simulated visits (Poisson distributed)
    )

    poisson_model <- glm(visits ~ ads_spend, data = website_data, family = "poisson")
    summary(poisson_model)
    ```

    **Interpreting Poisson Regression Output:**

    *   **Coefficients:**  Log-rate ratios. Exponentiating coefficients (`exp(coef(poisson_model))`) gives rate ratios. A rate ratio > 1 means the rate of events increases with a one-unit increase in the predictor.
    *   Other output components are similar to logistic regression (deviance, AIC, etc.).

    **Making Predictions with Poisson Regression:**

    ```R
    new_data_visits <- data.frame(ads_spend = c(300, 600))
    predicted_visits <- predict(poisson_model, newdata = new_data_visits, type = "response") # type = "response" for expected counts
    predicted_visits # Predicted website visits
    ```

### Other GLM Families

R supports various GLM families beyond binomial and Poisson. Common families include:

*   `gaussian()`:  For normal distribution (standard linear regression).
*   `Gamma()`: For gamma distribution (for positive continuous data, often skewed).
*   `inverse.gaussian()`: For inverse Gaussian distribution.
*   `quasibinomial()`, `quasipoisson()`: For overdispersed binomial and Poisson data (variance greater than expected).

## Time Series Analysis

Time series data is data collected over time, often at regular intervals (e.g., daily, monthly, yearly). Time series analysis involves techniques for modeling, forecasting, and understanding patterns in time-dependent data.

### Basic Time Series Components

*   **Trend:**  Long-term direction or movement in the series (upward, downward, or horizontal).
*   **Seasonality:**  Regular, repeating patterns within a fixed period (e.g., yearly, quarterly, monthly, weekly).
*   **Cyclicality:**  Longer-term fluctuations that are not of a fixed period (cycles).
*   **Irregular/Random Component:**  Noise or random fluctuations that are not explained by trend, seasonality, or cycles.

### Time Series Objects in R

*   **`ts()` function:** Create time series objects in R.

    ```R
    # Example: Creating a simple time series
    time_series_data <- ts(rnorm(100), start = c(2020, 1), frequency = 12) # Monthly data starting Jan 2020
    time_series_data

    # Components:
    # Data: rnorm(100) - 100 random normal values
    # start = c(2020, 1) - Start date: Year 2020, Month 1 (January)
    # frequency = 12 - Frequency: 12 observations per year (monthly)

    plot(time_series_data, main = "Example Time Series Plot") # Basic time series plot
    ```

### Decomposing Time Series

Decomposition separates a time series into its components (trend, seasonal, random).

*   **`decompose()` function:**  For classical decomposition (additive or multiplicative).

    ```R
    # Example: Decomposing a time series (using 'AirPassengers' dataset - classic time series dataset in R)
    data("AirPassengers") # Load AirPassengers dataset
    air_passengers_ts <- ts(AirPassengers, frequency = 12) # Create time series object

    decomposed_series <- decompose(air_passengers_ts) # Additive decomposition by default
    plot(decomposed_series) # Plot decomposed components
    ```

### Forecasting with ARIMA Models

ARIMA (Autoregressive Integrated Moving Average) models are a widely used class of models for time series forecasting. They capture autocorrelation (correlation with past values) in the series.

*   **ARIMA components:**
    *   **AR (Autoregressive):**  Uses past values of the series to predict current values.
    *   **I (Integrated):**  Differencing to make the series stationary (constant mean and variance over time).
    *   **MA (Moving Average):**  Uses past forecast errors to predict current values.

*   **`arima()` function:**  Fit ARIMA models.

    ```R
    # Install forecast package if needed: install.packages("forecast")
    library(forecast)

    # Fit ARIMA model (example: ARIMA(2,1,2) - parameters p, d, q)
    arima_model <- arima(air_passengers_ts, order = c(2, 1, 2)) # ARIMA(p, d, q) order
    summary(arima_model) # Model summary

    # Forecast future values
    forecast_values <- forecast(arima_model, h = 24) # Forecast 24 periods ahead
    plot(forecast_values) # Plot forecast

    # Accuracy of the model (on training data - for model evaluation on hold-out data, you'd split the time series)
    accuracy(arima_model)
    ```

*   **`auto.arima()` function:**  Automatically selects the best ARIMA model order based on AIC/BIC criteria.

    ```R
    auto_arima_model <- auto.arima(air_passengers_ts) # Automatically find best ARIMA model
    summary(auto_arima_model)
    forecast_auto_arima <- forecast(auto_arima_model, h = 24)
    plot(forecast_auto_arima)
    ```

## Clustering and Dimensionality Reduction

Clustering and dimensionality reduction are unsupervised learning techniques.

### Clustering

Clustering groups similar data points together based on their features, without prior knowledge of group labels.

*   **K-Means Clustering:**  Partitions data into k clusters, where each data point belongs to the cluster with the nearest mean (centroid).

    *   **`kmeans()` function:** Perform k-means clustering.

        ```R
        # Example: Clustering iris data based on sepal and petal measurements (ignoring Species labels for unsupervised learning)
        iris_features <- iris[, 1:4] # Use only features, not Species

        set.seed(123) # For reproducibility
        kmeans_result <- kmeans(iris_features, centers = 3) # Cluster into 3 groups (k=3, as there are 3 iris species)
        kmeans_result

        # Cluster assignments for each data point
        cluster_assignments <- kmeans_result$cluster
        cluster_assignments

        # Cluster centers (centroids)
        cluster_centers <- kmeans_result$centers
        cluster_centers

        # Visualize clusters (for 2D, using first two features for simplicity)
        plot(iris_features[, 1:2], col = cluster_assignments,
             pch = 20, cex = 3, main = "K-Means Clustering (k=3)")
        points(cluster_centers[, 1:2], col = 1:3, pch = 4, cex = 4, lwd = 4) # Plot cluster centers
        ```

    *   **Choosing the number of clusters (k):**  Techniques like the elbow method or silhouette analysis can help determine an appropriate value for k.

*   **Hierarchical Clustering:**  Builds a hierarchy of clusters, represented as a dendrogram. Can be agglomerative (bottom-up) or divisive (top-down).

    *   **`hclust()` function:** Perform hierarchical clustering.

        ```R
        # Hierarchical clustering
        distance_matrix <- dist(iris_features) # Calculate distance matrix
        hierarchical_clusters <- hclust(distance_matrix, method = "ward.D2") # Ward's method for linkage

        plot(hierarchical_clusters, main = "Hierarchical Clustering Dendrogram") # Plot dendrogram

        # Cut dendrogram to get clusters (e.g., 3 clusters)
        cluster_assignments_hierarchical <- cutree(hierarchical_clusters, k = 3)
        cluster_assignments_hierarchical

        # Visualize hierarchical clusters (similar to k-means visualization)
        plot(iris_features[, 1:2], col = cluster_assignments_hierarchical,
             pch = 20, cex = 3, main = "Hierarchical Clustering (k=3)")
        ```

### Dimensionality Reduction: Principal Component Analysis (PCA)

PCA reduces the dimensionality of data by finding principal components, which are new uncorrelated variables that capture most of the variance in the original data.

*   **`prcomp()` function:** Perform PCA.

    ```R
    # PCA on iris features
    pca_result <- prcomp(iris_features, scale. = TRUE) # scale. = TRUE for standardization
    pca_result
    summary(pca_result) # Summary of PCA results (variance explained by components)

    # Scree plot (variance explained by each component)
    plot(pca_result, type = "l", main = "Scree Plot")

    # Biplot (visualize data in reduced dimensions and variable loadings)
    biplot(pca_result, scale = 0)

    # Access principal components (scores)
    principal_components <- pca_result$x
    head(principal_components) # First few principal components for each data point
    ```

    **Interpreting PCA Output:**

    *   **Principal Components (PCs):**  New variables, linear combinations of original features. PC1 explains the most variance, PC2 the second most, and so on.
    *   **Loadings:**  Coefficients that show how much each original feature contributes to each PC.
    *   **Variance Explained:**  Proportion of total variance explained by each PC. Scree plot helps visualize this.

## Let's Practice!

1.  **Generalized Linear Models (GLMs):**
    *   **Logistic Regression:**  Use a dataset with a binary outcome (e.g., create one from `iris` or find a suitable dataset). Fit a logistic regression model using `glm(family = "binomial")`. Interpret coefficients, make predictions, and evaluate model performance (e.g., using confusion matrix if you have true labels for evaluation).
    *   **Poisson Regression:**  Find or simulate count data (e.g., website visits, events). Fit a Poisson regression model using `glm(family = "poisson")`. Interpret coefficients and make predictions.
2.  **Time Series Analysis:**
    *   Load a time series dataset (e.g., `AirPassengers`, or find time series data online).
    *   Create a `ts` object.
    *   Decompose the time series using `decompose()`.
    *   Fit an ARIMA model using `arima()` or `auto.arima()`.
    *   Forecast future values and evaluate forecast accuracy.
3.  **Clustering and Dimensionality Reduction:**
    *   **K-Means Clustering:**  Apply k-means clustering to the `iris` dataset (features only, ignore `Species` labels). Experiment with different values of k and visualize the clusters.
    *   **Hierarchical Clustering:**  Apply hierarchical clustering to the same data. Plot the dendrogram and cut it to obtain clusters. Compare with k-means results.
    *   **PCA:**  Perform PCA on the `iris` features. Examine the scree plot, biplot, and variance explained. Reduce the dimensionality of the data using the first few principal components.

## Chapter Summary

In this chapter, you've expanded your statistical modeling skills in R to advanced techniques:

*   **Generalized Linear Models (GLMs):**  Learned about GLM framework, logistic regression for binary outcomes, and Poisson regression for count data.
*   **Time Series Analysis:**  Introduced time series concepts, decomposition, and ARIMA models for forecasting.
*   **Clustering and Dimensionality Reduction:**  Explored unsupervised learning techniques, including k-means and hierarchical clustering for grouping data, and PCA for reducing data dimensionality.

These advanced statistical modeling techniques are powerful tools for analyzing diverse types of data and extracting valuable insights. In the following chapters, we'll continue to explore more advanced topics in R for data science, including scaling R, performance optimization, and deploying R projects!
