# Chapter 6: Machine Learning Basics

Welcome to the exciting realm of Machine Learning in R! This chapter will introduce you to fundamental machine learning concepts and get you started with building simple machine learning models using the `caret` package. Machine learning is a vast field, and this chapter will lay the groundwork for your journey into predictive modeling and data-driven insights.

## Introduction to Machine Learning Concepts

Machine learning is about enabling computers to learn from data without being explicitly programmed. Instead of writing specific rules, you train algorithms on data to identify patterns, make predictions, and improve their performance over time.

**Key Concepts:**

*   **Algorithms:**  The set of rules or instructions that a machine learning model follows to learn from data. Examples include linear regression, decision trees, support vector machines, neural networks, etc.
*   **Models:** The trained output of a machine learning algorithm. It's the representation of the patterns learned from the data, which can be used to make predictions on new, unseen data.
*   **Training Data:** The data used to train a machine learning algorithm. It contains input features and, in supervised learning, the corresponding target variable (what you want to predict).
*   **Features:** The input variables used by the machine learning model to make predictions. Also known as predictors, independent variables, or attributes.
*   **Target Variable:** The variable you want to predict in supervised learning. Also known as the response variable, dependent variable, or outcome.
*   **Prediction:** The output of a trained machine learning model when given new input features.
*   **Evaluation:** Assessing the performance of a machine learning model using metrics relevant to the task (e.g., accuracy, precision, recall, R-squared, RMSE).
*   **Overfitting:** When a model learns the training data too well, including noise, and performs poorly on new, unseen data. It generalizes poorly.
*   **Underfitting:** When a model is too simple to capture the underlying patterns in the data and performs poorly on both training and new data.
*   **Bias-Variance Tradeoff:** A fundamental concept in machine learning. More complex models tend to have lower bias (fit training data well) but higher variance (sensitive to training data fluctuations, prone to overfitting). Simpler models have higher bias but lower variance.

## Supervised vs. Unsupervised Learning

Machine learning tasks are broadly categorized into supervised and unsupervised learning.

### Supervised Learning

In supervised learning, you train a model on labeled data, meaning data where you have both input features and the correct target variable. The goal is to learn a mapping from inputs to outputs so that the model can predict the target variable for new, unseen inputs.

**Types of Supervised Learning Tasks:**

*   **Classification:**  Predicting a categorical target variable (class label). Examples:
    *   Spam detection (spam or not spam).
    *   Image classification (cat, dog, bird).
    *   Disease diagnosis (positive, negative).
*   **Regression:** Predicting a continuous target variable (numeric value). Examples:
    *   Predicting house prices.
    *   Forecasting sales.
    *   Estimating temperature.

**Common Supervised Learning Algorithms:**

*   Linear Regression
*   Logistic Regression
*   Decision Trees
*   Random Forests
*   Support Vector Machines (SVMs)
*   K-Nearest Neighbors (KNN)
*   Neural Networks

### Unsupervised Learning

In unsupervised learning, you train a model on unlabeled data, where you only have input features and no target variable. The goal is to discover hidden patterns, structures, or relationships in the data.

**Types of Unsupervised Learning Tasks:**

*   **Clustering:** Grouping similar data points together. Examples:
    *   Customer segmentation.
    *   Document clustering.
    *   Image segmentation.
*   **Dimensionality Reduction:** Reducing the number of features while preserving important information. Examples:
    *   Principal Component Analysis (PCA).
    *   t-distributed Stochastic Neighbor Embedding (t-SNE).
*   **Anomaly Detection:** Identifying unusual or outlier data points. Examples:
    *   Fraud detection.
    *   Network intrusion detection.
    *   Equipment failure detection.
*   **Association Rule Mining:** Discovering relationships between items in a dataset. Example:
    *   Market basket analysis (what items are frequently bought together).

**Common Unsupervised Learning Algorithms:**

*   K-Means Clustering
*   Hierarchical Clustering
*   Principal Component Analysis (PCA)
*   t-SNE
*   Association Rule Mining (Apriori, Eclat)

## Building Simple Machine Learning Models with `caret`

`caret` (Classification and Regression Training) is a powerful R package that simplifies the process of building, training, and evaluating machine learning models. It provides a unified interface to hundreds of machine learning algorithms and streamlines common tasks like data splitting, preprocessing, feature selection, model tuning, and evaluation.

### Setting up `caret`

First, install and load the `caret` package:

```R
# Install caret package if needed
# install.packages("caret")

library(caret)
```

### Example: Classification with `caret` (using `iris` dataset)

Let's build a classification model to predict the `Species` of iris flowers based on sepal and petal measurements using the `iris` dataset. We'll use a simple algorithm: k-Nearest Neighbors (KNN).

**1. Data Preparation:**

*   The `iris` dataset is already loaded in R. It's reasonably clean, so we'll use it directly for this example.
*   Separate features (predictors) and the target variable (`Species`).

```R
features <- iris[, 1:4] # Sepal.Length, Sepal.Width, Petal.Length, Petal.Width
target <- iris$Species    # Species (setosa, versicolor, virginica)
```

**2. Data Splitting (Training and Testing Sets):**

*   Divide the data into training and testing sets. Train the model on the training set and evaluate its performance on the unseen testing set to estimate generalization ability.
*   `createDataPartition()` from `caret` is useful for creating balanced partitions.

```R
set.seed(123) # For reproducibility

trainIndex <- createDataPartition(target, p = 0.7, list = FALSE) # 70% for training
train_features <- features[trainIndex, ]
test_features <- features[-trainIndex, ]
train_target <- target[trainIndex]
test_target <- target[-trainIndex]
```

**3. Model Training:**

*   Use `train()` function from `caret` to train a model.
    *   `train_target ~ .`: Formula specifying the model. `.` means "all features".
    *   `data = train_features`: Training features data.
    *   `method = "knn"`:  Specify the machine learning algorithm (k-Nearest Neighbors).

```R
knn_model <- train(train_target ~ ., data = train_features, method = "knn")
knn_model # Display model information
```

**4. Model Prediction:**

*   Use `predict()` to make predictions on the test set using the trained model.

```R
predictions <- predict(knn_model, newdata = test_features)
predictions # Predicted species for test set
```

**5. Model Evaluation:**

*   Evaluate the model's performance using metrics like accuracy, confusion matrix, etc.
*   `confusionMatrix()` from `caret` is helpful for classification evaluation.

```R
confusionMatrix(predictions, test_target) # Compare predictions to actual test targets
```

`confusionMatrix()` output provides:

*   **Confusion Matrix:**  Table showing counts of true positives, true negatives, false positives, and false negatives for each class.
*   **Accuracy:** Overall accuracy of the model.
*   **Sensitivity (Recall):**  True positive rate for each class.
*   **Specificity:** True negative rate for each class.
*   **Precision:** Positive predictive value for each class.
*   **F1-Score:** Harmonic mean of precision and recall.
*   ** অন্যান্য metrics.**

In this example, you'll see the accuracy of the KNN model on the test set.

### Exploring Different Algorithms with `caret`

`caret` supports a vast number of machine learning algorithms. You can easily try different algorithms by changing the `method` argument in `train()`.

**Example: Trying a Decision Tree Model (method = "rpart")**

```R
dt_model <- train(train_target ~ ., data = train_features, method = "rpart") # method = "rpart" for decision tree
dt_model # Model information

dt_predictions <- predict(dt_model, newdata = test_features)
confusionMatrix(dt_predictions, test_target) # Evaluate decision tree model
```

Try other methods like `"rf"` (Random Forest), `"svmLinear"` (Support Vector Machine with linear kernel), `"glm"` (Generalized Linear Model - Logistic Regression for classification if target is factor), etc.  Refer to `caret` documentation for the extensive list of available methods (`?train`).

### Model Tuning (Hyperparameter Tuning)

Many machine learning algorithms have hyperparameters that control their behavior. Tuning these hyperparameters can significantly improve model performance. `caret` provides tools for automated hyperparameter tuning using techniques like cross-validation. We'll explore model tuning in more detail in later chapters.

## Let's Practice!

1.  **Classification Task:**
    *   Use the `iris` dataset or another classification dataset.
    *   Split the data into training and testing sets.
    *   Train a KNN classifier using `caret` (`method = "knn"`).
    *   Evaluate the model's performance using `confusionMatrix()`.
    *   Try training other classification algorithms supported by `caret` (e.g., decision trees `"rpart"`, logistic regression `"glm"`, random forests `"rf"`). Compare their performance.
2.  **Regression Task (Optional):**
    *   Choose a regression dataset (e.g., `mtcars` dataset in R, or find one online).
    *   Split the data into training and testing sets.
    *   Train a linear regression model using `caret` (`method = "lm"`).
    *   Evaluate the regression model using appropriate metrics (e.g., RMSE, R-squared - you can find these in the `train()` output or use custom evaluation functions).
    *   Try other regression algorithms in `caret` (e.g., `"rpart"` for regression trees, `"rf"` for random forests for regression).

## Chapter Summary

In this chapter, you've taken your first steps into the world of machine learning with R. You've learned:

*   Basic **machine learning concepts**: algorithms, models, training data, features, target variable, prediction, evaluation, overfitting, underfitting, bias-variance tradeoff.
*   The distinction between **supervised and unsupervised learning**, and common tasks and algorithms within each category.
*   How to use the **`caret` package** to build simple machine learning models in R.
*   A basic **machine learning workflow**: data preparation, data splitting, model training (`train()`), prediction (`predict()`), and evaluation (`confusionMatrix()`).
*   How to **try different machine learning algorithms** easily with `caret`.

This chapter provides a foundation for your machine learning journey in R. In the next parts of this course, we'll delve deeper into specific machine learning algorithms, model evaluation, feature engineering, model tuning, and more advanced topics. Get ready to build more sophisticated and powerful predictive models!
