# Chapter 11: Model Evaluation and Selection

In the previous chapter, we introduced basic machine learning algorithms using scikit-learn. However, simply training a model is not enough. We need to evaluate its performance rigorously and select the best model for our task. This chapter focuses on model evaluation and selection techniques, which are crucial for building robust and effective machine learning models.

## Metrics for Classification and Regression

Model evaluation relies on metrics that quantify how well a model is performing. Different metrics are used for classification and regression tasks.

**1. Classification Metrics:**

*   **Accuracy:** The most basic metric, representing the percentage of correctly classified instances. However, accuracy can be misleading for imbalanced datasets.
*   **Confusion Matrix:** A table that summarizes the performance of a classification model by showing counts of true positives, true negatives, false positives, and false negatives.
*   **Precision:**  Out of all instances predicted as positive, what proportion is actually positive? (Precision = True Positives / (True Positives + False Positives)). High precision means low false positive rate.
*   **Recall (Sensitivity or True Positive Rate):** Out of all actual positive instances, what proportion is correctly predicted as positive? (Recall = True Positives / (True Positives + False Negatives)). High recall means low false negative rate.
*   **F1-Score:** The harmonic mean of precision and recall, providing a balanced measure of a model's performance, especially useful when classes are imbalanced. (F1-Score = 2 * (Precision * Recall) / (Precision + Recall)).
*   **AUC-ROC (Area Under the Receiver Operating Characteristic curve):**  For binary classification, ROC curve plots the True Positive Rate against the False Positive Rate at various threshold settings. AUC-ROC measures the area under this curve, with a higher AUC-ROC indicating better performance in distinguishing between classes.
*   **Classification Report:** scikit-learn provides `classification_report()` to generate a comprehensive report including precision, recall, F1-score, and support for each class.

**Example: Classification Metrics in scikit-learn**

```python
# Code cell
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report, roc_auc_score
from sklearn.datasets import load_iris

# Load Iris dataset
iris = load_iris()
X, y = iris.data, iris.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
logreg_classifier = LogisticRegression(max_iter=1000)
logreg_classifier.fit(X_train, y_train)
y_pred_logreg = logreg_classifier.predict(X_test)
y_prob_logreg = logreg_classifier.predict_proba(X_test)[:, 1] # Probabilities for positive class (for AUC-ROC in binary case, adjust for multi-class)


# Calculate metrics
accuracy = accuracy_score(y_test, y_pred_logreg)
conf_matrix = confusion_matrix(y_test, y_pred_logreg)
class_report = classification_report(y_test, y_pred_logreg)
# auc_roc = roc_auc_score(y_test, y_prob_logreg) # AUC-ROC - applicable for binary classification, needs adjustment for multi-class

print("Accuracy:", accuracy)
print("\nConfusion Matrix:\n", conf_matrix)
print("\nClassification Report:\n", class_report)
# print("\nAUC-ROC:", auc_roc) # AUC-ROC - for binary classification
```

**2. Regression Metrics:**

*   **Mean Squared Error (MSE):** The average squared difference between predicted and actual values. Lower MSE indicates better performance. Sensitive to outliers due to squared errors.
*   **Root Mean Squared Error (RMSE):** The square root of MSE, providing an error metric in the same units as the target variable, making it more interpretable.
*   **Mean Absolute Error (MAE):** The average absolute difference between predicted and actual values. Less sensitive to outliers than MSE/RMSE.
*   **R-squared (Coefficient of Determination):** Measures the proportion of variance in the dependent variable that is predictable from the independent variables. R-squared ranges from 0 to 1, with higher values indicating a better fit. Can be negative for very poor models.
*   **Adjusted R-squared:**  Adjusts R-squared for the number of predictors in the model, useful when comparing models with different numbers of features.

**Example: Regression Metrics in scikit-learn**

```python
# Code cell
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
from sklearn.datasets import load_boston

# Load Boston Housing dataset
boston = load_boston()
X, y = boston.data, boston.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
linear_regressor = LinearRegression()
linear_regressor.fit(X_train, y_train)
y_pred_linear_reg = linear_regressor.predict(X_test)

# Calculate metrics
mse = mean_squared_error(y_test, y_pred_linear_reg)
rmse = mean_squared_error(y_test, y_pred_linear_reg, squared=False) # squared=False for RMSE
mae = mean_absolute_error(y_test, y_pred_linear_reg)
r2 = r2_score(y_test, y_pred_linear_reg)

print("Mean Squared Error (MSE):", mse)
print("Root Mean Squared Error (RMSE):", rmse)
print("Mean Absolute Error (MAE):", mae)
print("R-squared:", r2)
```

## Cross-Validation Techniques

To get a more reliable estimate of a model's performance and prevent overfitting, we use cross-validation. Cross-validation involves splitting the data into multiple folds, training the model on some folds, and evaluating it on the remaining fold(s), repeating this process multiple times and averaging the results.

**Common Cross-Validation Techniques:**

*   **K-Fold Cross-Validation:** The data is divided into k folds. In each iteration, k-1 folds are used for training, and the remaining fold is used for validation. This is repeated k times, with each fold used as validation once. The performance metrics are averaged over all k iterations.
*   **Stratified K-Fold Cross-Validation:** Similar to K-Fold, but ensures that each fold contains approximately the same proportion of instances of each target class, especially important for imbalanced classification datasets.
*   **Leave-One-Out Cross-Validation (LOOCV):** Each data point is used as a validation set, and the model is trained on the rest of the data. Can be computationally expensive for large datasets.

**Cross-Validation in scikit-learn:**

scikit-learn provides `cross_val_score()` for performing cross-validation and getting performance scores for each fold.

**Example: K-Fold Cross-Validation with `cross_val_score()`**

```python
# Code cell
from sklearn.model_selection import cross_val_score, KFold
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris

# Load Iris dataset
iris = load_iris()
X, y = iris.data, iris.target

# Initialize Logistic Regression classifier
logreg_classifier_cv = LogisticRegression(max_iter=1000)

# Define K-Fold cross-validator (e.g., 5 folds)
kf = KFold(n_splits=5, shuffle=True, random_state=42) # shuffle data before splitting

# Perform K-Fold cross-validation and get accuracy scores for each fold
cv_scores = cross_val_score(logreg_classifier_cv, X, y, cv=kf, scoring='accuracy') # cv=kf for KFold, scoring='accuracy' for classification accuracy

print("Cross-validation scores (Accuracy for each fold):", cv_scores)
print("Mean cross-validation accuracy:", cv_scores.mean()) # Average accuracy across folds
print("Standard deviation of cross-validation accuracy:", cv_scores.std()) # Standard deviation of accuracy
```

## Hyperparameter Tuning: Grid Search, Random Search

Machine learning models often have hyperparameters that are not learned from data but set before training (e.g., `C` and `kernel` in SVM, `max_depth` in Decision Trees). Hyperparameter tuning involves finding the optimal combination of hyperparameters that results in the best model performance.

**Common Hyperparameter Tuning Techniques:**

*   **Grid Search:** Exhaustively searches through a predefined grid of hyperparameter values. It tries all possible combinations of hyperparameters in the grid and evaluates the model's performance for each combination using cross-validation.
*   **Random Search:** Randomly samples hyperparameter combinations from predefined ranges or distributions. Often more efficient than Grid Search, especially when some hyperparameters are less important than others.

**Hyperparameter Tuning in scikit-learn:**

scikit-learn provides `GridSearchCV` and `RandomizedSearchCV` for hyperparameter tuning using cross-validation.

**Example: Grid Search with `GridSearchCV`**

```python
# Code cell
from sklearn.model_selection import GridSearchCV, train_test_split
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score
from sklearn.datasets import load_iris

# Load Iris dataset
iris = load_iris()
X, y = iris.data, iris.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Define hyperparameter grid to search
param_grid = {
    'C': [0.1, 1, 10, 100], # Different values for C hyperparameter
    'kernel': ['linear', 'rbf', 'poly'], # Different kernels to try
    'gamma': ['scale', 'auto', 0.1, 1] # Different gamma values (for rbf and poly kernels)
}

# Initialize GridSearchCV
grid_search = GridSearchCV(SVC(), param_grid, cv=3, scoring='accuracy', verbose=2) # cv=3 for 3-fold CV, scoring='accuracy'

# Perform Grid Search (fit on training data)
grid_search.fit(X_train, y_train)

# Best model and best hyperparameters found by Grid Search
best_svm_model = grid_search.best_estimator_
best_hyperparameters = grid_search.best_params_
best_accuracy = grid_search.best_score_

print("Best Hyperparameters found by Grid Search:", best_hyperparameters)
print("Best Cross-validation Accuracy:", best_accuracy)

# Evaluate best model on test set
y_pred_best_svm = best_svm_model.predict(X_test)
test_accuracy_best_svm = accuracy_score(y_test, y_pred_best_svm)
print("Test set accuracy of best model:", test_accuracy_best_svm)
```

**Example: Random Search with `RandomizedSearchCV`**

```python
# Code cell
from sklearn.model_selection import RandomizedSearchCV, train_test_split
from sklearn.ensemble import RandomForestRegressor # Example regressor
from sklearn.metrics import mean_squared_error
from sklearn.datasets import load_boston
from scipy.stats import randint, uniform # For defining hyperparameter distributions

# Load Boston Housing dataset
boston = load_boston()
X, y = boston.data, boston.target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Define hyperparameter distributions for Random Search
param_distributions = {
    'n_estimators': randint(50, 500), # Randomly sample n_estimators from 50 to 500
    'max_depth': randint(3, 15), # Randomly sample max_depth from 3 to 15
    'min_samples_split': uniform(0.01, 0.1) # Randomly sample min_samples_split from 0.01 to 0.1 (as a fraction)
}

# Initialize RandomizedSearchCV
random_search = RandomizedSearchCV(RandomForestRegressor(random_state=42), # Base estimator - RandomForestRegressor
                                   param_distributions=param_distributions,
                                   n_iter=10, # Number of random combinations to try
                                   cv=3, # 3-fold cross-validation
                                   scoring='neg_mean_squared_error', # Scoring metric for regression (negative MSE for maximization)
                                   verbose=1,
                                   random_state=42)

# Perform Random Search (fit on training data)
random_search.fit(X_train, y_train)

# Best model and best hyperparameters found by Random Search
best_rf_model = random_search.best_estimator_
best_hyperparameters_random = random_search.best_params_
best_neg_mse = random_search.best_score_ # Note: negative MSE because GridSearchCV maximizes score

print("Best Hyperparameters found by Random Search:", best_hyperparameters_random)
print("Best Cross-validation Negative MSE:", best_neg_mse) # Negative MSE value

# Evaluate best model on test set
y_pred_best_rf = best_rf_model.predict(X_test)
test_mse_best_rf = mean_squared_error(y_test, y_pred_best_rf)
print("Test set MSE of best model:", test_mse_best_rf)
```

**Choosing between Grid Search and Random Search:**

*   **Grid Search:** Suitable when the hyperparameter search space is relatively small and well-defined. Exhaustive search, guarantees finding the best combination within the grid, but can be computationally expensive for large grids.
*   **Random Search:** More efficient for larger search spaces, especially when some hyperparameters are less important. Explores a wider range of hyperparameter values, but doesn't guarantee finding the absolute best combination within the entire search space.

## Bias-Variance Tradeoff

Model evaluation and selection are closely related to the bias-variance tradeoff, a fundamental concept in machine learning.

*   **Bias:** The error introduced by approximating a real-world problem, which may be complex, by a simplified model. High bias models tend to underfit the training data (oversimplify). Example: Linear regression on non-linear data.
*   **Variance:** The sensitivity of a model to fluctuations in the training dataset. High variance models are very sensitive to training data and tend to overfit (model training data too closely, including noise). Example: Deep decision trees.

**Bias-Variance Tradeoff:**

*   **Simple models (e.g., Linear Regression):** High bias, low variance. They are less flexible, may underfit complex data, but are less sensitive to training data variations.
*   **Complex models (e.g., Deep Decision Trees, High-degree Polynomial Regression):** Low bias, high variance. They are more flexible, can fit complex data well, but are more prone to overfitting and sensitive to training data variations.

**Goal:** Find a model with a good balance between bias and variance, achieving good generalization performance on unseen data (test data).

**Techniques to manage Bias-Variance Tradeoff:**

*   **Model selection:** Choose a model with appropriate complexity for the data (e.g., simpler model if data is linear, more complex model if data is non-linear).
*   **Hyperparameter tuning:** Regularization techniques (e.g., L1, L2 regularization in linear models, pruning in decision trees) can help reduce variance and control model complexity.
*   **Cross-validation:** Helps estimate generalization performance and detect overfitting (high variance) or underfitting (high bias).
*   **Ensemble methods (later chapters):** Combine multiple models to reduce variance and improve robustness (e.g., Random Forests, Gradient Boosting).

Understanding and managing the bias-variance tradeoff is crucial for building machine learning models that generalize well to new, unseen data.

**In this chapter, we've covered:**

*   Metrics for classification (accuracy, confusion matrix, precision, recall, F1-score, AUC-ROC) and regression (MSE, RMSE, MAE, R-squared).
*   Cross-validation techniques (K-Fold, Stratified K-Fold) for robust model evaluation.
*   Hyperparameter tuning using Grid Search and Random Search with scikit-learn.
*   Introduction to the bias-variance tradeoff and its importance in model selection.

In the next chapter, we'll explore more advanced topics in data science, including dimensionality reduction techniques.
