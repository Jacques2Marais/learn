# Chapter 10: Introduction to Machine Learning with scikit-learn

Machine learning (ML) is a field of artificial intelligence that focuses on developing algorithms that allow computers to learn from data without being explicitly programmed. It's a powerful set of techniques for pattern recognition, prediction, and decision-making, and it's transforming many areas of science and technology, including physics and data science. In this chapter, we'll provide a gentle introduction to machine learning concepts and get started with scikit-learn (sklearn), a popular and user-friendly Python library for machine learning.

## Machine Learning Concepts: Supervised vs. Unsupervised Learning

Machine learning problems are broadly categorized into two main types: supervised learning and unsupervised learning.

**1. Supervised Learning:**

In supervised learning, the algorithm learns from labeled data, where each data point is paired with a known output or target variable. The goal is to learn a mapping from input features to the target variable, so that the algorithm can predict the target for new, unseen inputs.

*   **Analogy:** Think of learning with a teacher who provides correct answers (labels) for examples.
*   **Types of supervised learning tasks:**
    *   **Classification:** Predicting a categorical target variable (e.g., spam or not spam, type of particle, galaxy classification).
    *   **Regression:** Predicting a continuous target variable (e.g., house price, temperature, energy consumption).

**Common Supervised Learning Algorithms (covered in this chapter):**

*   **Logistic Regression:** For binary and multi-class classification.
*   **Support Vector Machines (SVM):** For classification and regression.
*   **Linear Regression:** For regression tasks with a linear relationship.
*   **Decision Trees:** For both classification and regression, building tree-like models for decision-making.

**2. Unsupervised Learning:**

In unsupervised learning, the algorithm learns from unlabeled data, where there are no predefined output labels. The goal is to discover hidden patterns, structures, or groupings in the data.

*   **Analogy:** Think of learning without a teacher, exploring data to find inherent structures.
*   **Types of unsupervised learning tasks:**
    *   **Clustering:** Grouping similar data points together (e.g., customer segmentation, grouping stars by properties).
    *   **Dimensionality Reduction:** Reducing the number of variables while preserving essential information (e.g., Principal Component Analysis - PCA, t-SNE for visualization).
    *   **Anomaly Detection:** Identifying unusual or outlier data points (e.g., fraud detection, detecting unusual sensor readings).

**Common Unsupervised Learning Algorithms (briefly mentioned later):**

*   **K-Means Clustering:** For partitioning data into k clusters.
*   **Principal Component Analysis (PCA):** For dimensionality reduction.
*   **Hierarchical Clustering:** For building a hierarchy of clusters.

**Choosing between Supervised and Unsupervised Learning:**

*   **Supervised learning:** Use when you have labeled data and want to predict a specific target variable.
*   **Unsupervised learning:** Use when you have unlabeled data and want to explore data structure, find patterns, or reduce dimensionality.

## Introduction to scikit-learn (sklearn)

scikit-learn (sklearn) is a widely used Python library for machine learning. It provides a comprehensive set of tools for various ML tasks, including:

*   **Classification, Regression, Clustering, Dimensionality Reduction, Model Selection, Preprocessing.**

**Key Concepts in scikit-learn:**

*   **Estimators:** Objects that can learn from data and make predictions. Algorithms like classifiers and regressors are implemented as estimators in scikit-learn. Estimators have a `.fit(X, y)` method to learn from data (training) and a `.predict(X)` method to make predictions on new data.
*   **Transformers:** Objects that transform data. Preprocessing steps like scaling, feature selection, and dimensionality reduction are implemented as transformers. Transformers have a `.fit(X)` method to learn transformation parameters from data and a `.transform(X)` method to apply the transformation. They can also have a `.fit_transform(X)` method for convenience.
*   **Pipelines:** Tools to chain together multiple estimators and transformers into a single workflow. Pipelines help streamline ML workflows, making them more organized and easier to manage.
*   **Datasets:** scikit-learn provides utility functions to load sample datasets, which are useful for learning and experimentation (e.g., `sklearn.datasets.load_iris()`, `sklearn.datasets.load_boston()`).

**Basic Workflow in scikit-learn:**

1.  **Load and prepare data:** Load your dataset into NumPy arrays or Pandas DataFrames. Preprocess data if needed (handle missing values, scale features, etc.).
2.  **Split data:** Split your data into training and testing sets using `sklearn.model_selection.train_test_split()`. Train set is used to train the model, and test set is used to evaluate its performance on unseen data.
3.  **Choose a model:** Select an appropriate estimator (algorithm) for your task (classification or regression).
4.  **Train the model:** Create an instance of the estimator and train it using the training data with `.fit(X_train, y_train)`.
5.  **Make predictions:** Use the trained model to make predictions on the test data using `.predict(X_test)`.
6.  **Evaluate the model:** Evaluate the performance of your model using appropriate metrics (accuracy, precision, recall, F1-score for classification; R-squared, Mean Squared Error for regression) from `sklearn.metrics`.

## Classification Algorithms: Logistic Regression, Support Vector Machines

Let's explore two common classification algorithms in scikit-learn: Logistic Regression and Support Vector Machines (SVM).

**1. Logistic Regression:**

Logistic Regression is a linear model for binary or multi-class classification. Despite its name, it's used for classification, not regression. It models the probability of a data point belonging to a particular class.

```python
# Code cell
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
from sklearn.datasets import load_iris # Example dataset

# Load Iris dataset (for classification)
iris = load_iris()
X, y = iris.data, iris.target # Features (X) and target labels (y)

# Split data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42) # 30% test set, random seed for reproducibility

# Initialize Logistic Regression classifier
logreg_classifier = LogisticRegression(max_iter=1000) # Increase max_iter for convergence

# Train the classifier on training data
logreg_classifier.fit(X_train, y_train)

# Make predictions on test data
y_pred_logreg = logreg_classifier.predict(X_test)

# Evaluate accuracy
accuracy_logreg = accuracy_score(y_test, y_pred_logreg)
print("Logistic Regression Accuracy:", accuracy_logreg) # Output: (accuracy score)
```

**2. Support Vector Machines (SVM):**

Support Vector Machines (SVMs) are powerful and versatile algorithms for both classification and regression. SVMs aim to find an optimal hyperplane that separates different classes in the feature space with the largest possible margin.

```python
# Code cell
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC # Support Vector Classifier
from sklearn.metrics import accuracy_score
from sklearn.datasets import load_iris

# Load Iris dataset (same as before)
iris = load_iris()
X, y = iris.data, iris.target

# Split data into training and testing sets (same split as before for comparison)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Initialize Support Vector Classifier (SVC)
svm_classifier = SVC(kernel='linear') # Linear kernel SVM

# Train the classifier
svm_classifier.fit(X_train, y_train)

# Make predictions on test data
y_pred_svm = svm_classifier.predict(X_test)

# Evaluate accuracy
accuracy_svm = accuracy_score(y_test, y_pred_svm)
print("Support Vector Machine (SVM) Accuracy:", accuracy_svm) # Output: (accuracy score)
```

**Choosing between Logistic Regression and SVM:**

*   **Logistic Regression:** Simpler, faster to train, good for linear decision boundaries, interpretable coefficients.
*   **SVM:** More powerful for complex, non-linear decision boundaries (especially with non-linear kernels like RBF), can handle high-dimensional data well, but can be slower to train, less interpretable.

## Regression Algorithms: Linear Regression, Decision Trees

Now, let's look at two regression algorithms: Linear Regression (again, but for regression this time) and Decision Trees for regression.

**1. Linear Regression (for Regression):**

Linear Regression, in its regression form, models the relationship between input features and a continuous target variable as a linear equation.

```python
# Code cell
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.datasets import load_boston # Example dataset for regression

# Load Boston Housing dataset (for regression)
boston = load_boston()
X, y = boston.data, boston.target # Features (X) and target variable (y) - house prices

# Split data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Initialize Linear Regression regressor
linear_regressor = LinearRegression()

# Train the regressor
linear_regressor.fit(X_train, y_train)

# Make predictions on test data
y_pred_linear_reg = linear_regressor.predict(X_test)

# Evaluate regression performance
mse_linear_reg = mean_squared_error(y_test, y_pred_linear_reg) # Mean Squared Error
r2_linear_reg = r2_score(y_test, y_pred_linear_reg) # R-squared

print("Linear Regression Mean Squared Error:", mse_linear_reg) # Output: (MSE value)
print("Linear Regression R-squared:", r2_linear_reg) # Output: (R-squared value)
```

**2. Decision Tree Regression:**

Decision Trees can also be used for regression tasks. Decision Tree Regressors build tree-like models to predict continuous target variables by partitioning the feature space into regions and assigning a constant prediction value within each region.

```python
# Code cell
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeRegressor
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.datasets import load_boston

# Load Boston Housing dataset (same as before)
boston = load_boston()
X, y = boston.data, boston.target

# Split data into training and testing sets (same split as before)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Initialize Decision Tree Regressor
tree_regressor = DecisionTreeRegressor(max_depth=5) # Limit tree depth to prevent overfitting

# Train the regressor
tree_regressor.fit(X_train, y_train)

# Make predictions on test data
y_pred_tree_reg = tree_regressor.predict(X_test)

# Evaluate regression performance
mse_tree_reg = mean_squared_error(y_test, y_pred_tree_reg)
r2_tree_reg = r2_score(y_test, y_pred_tree_reg)

print("Decision Tree Regression Mean Squared Error:", mse_tree_reg) # Output: (MSE value)
print("Decision Tree Regression R-squared:", r2_tree_reg) # Output: (R-squared value)
```

**Choosing between Linear Regression and Decision Tree Regression:**

*   **Linear Regression:** Assumes a linear relationship, simple, interpretable, fast, may not capture non-linear relationships well.
*   **Decision Tree Regression:** Can capture non-linear relationships, more flexible, can handle both categorical and numerical features, can be prone to overfitting (especially with deep trees), less interpretable than linear regression.

This chapter provides a starting point for your machine learning journey with scikit-learn. You've learned about supervised vs. unsupervised learning, key scikit-learn concepts, and implemented basic classification (Logistic Regression, SVM) and regression (Linear Regression, Decision Tree) algorithms. In the following chapters, we'll delve deeper into model evaluation, selection, advanced ML techniques, and applications in physics and data science.

**In this chapter, we've covered:**

*   Introduction to Machine Learning concepts: Supervised vs. Unsupervised Learning.
*   Introduction to scikit-learn (sklearn): Estimators, Transformers, Pipelines.
*   Basic ML workflow: data splitting, model training, prediction, evaluation.
*   Classification algorithms: Logistic Regression, Support Vector Machines (SVM).
*   Regression algorithms: Linear Regression, Decision Tree Regression.

In the next chapter, we'll focus on model evaluation and selection techniques to build more robust and effective machine learning models.
