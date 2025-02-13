# Chapter 3: Machine Learning Algorithms

## Supervised learning

Supervised learning involves training a model on labeled data to predict a target variable. The target variable can be either continuous (regression) or categorical (classification).

**Regression Algorithms:**

*   **Linear Regression:** A simple algorithm that models the relationship between the input features and the target variable as a linear equation.
*   **Polynomial Regression:** An extension of linear regression that allows for non-linear relationships between the input features and the target variable.
*   **Support Vector Regression (SVR):** A powerful algorithm that can model complex non-linear relationships between the input features and the target variable.

**Classification Algorithms:**

*   **Logistic Regression:** A linear model for binary classification problems.
*   **Decision Trees:** A tree-based model that partitions the data based on the values of the input features.
*   **Random Forests:** An ensemble of decision trees that improves accuracy and reduces overfitting.
*   **Support Vector Machines (SVM):** A powerful algorithm that can model complex non-linear relationships between the input features and the target variable.

Each algorithm has its own advantages and disadvantages. Linear regression is simple and easy to interpret, but it may not be suitable for non-linear relationships. Decision trees are easy to understand and can handle both numerical and categorical data, but they can be prone to overfitting. Random forests are more accurate than decision trees and less prone to overfitting, but they are more difficult to interpret. SVMs are very powerful and can model complex relationships, but they can be computationally expensive.

## Unsupervised learning

Unsupervised learning involves training a model on unlabeled data to discover patterns and relationships.

**Clustering Algorithms:**

*   **K-Means Clustering:** A simple and efficient algorithm that partitions the data into K clusters, where each data point belongs to the cluster with the nearest mean (centroid).
*   **Hierarchical Clustering:** An algorithm that builds a hierarchy of clusters, starting with each data point as its own cluster and then merging the closest clusters until a single cluster is formed.
*   **DBSCAN (Density-Based Spatial Clustering of Applications with Noise):** An algorithm that groups together data points that are closely packed together, marking as outliers points that lie alone in low-density regions.

**Dimensionality Reduction Techniques:**

*   **Principal Component Analysis (PCA):** A technique that reduces the dimensionality of the data by projecting it onto a set of orthogonal axes (principal components) that capture the most variance in the data.
*   **t-Distributed Stochastic Neighbor Embedding (t-SNE):** A technique that reduces the dimensionality of the data while preserving the local structure of the data.

K-means clustering is simple and efficient, but it requires specifying the number of clusters in advance. Hierarchical clustering does not require specifying the number of clusters in advance, but it can be computationally expensive. DBSCAN can discover clusters of arbitrary shape and is robust to outliers, but it requires tuning the parameters carefully. PCA is a linear technique that is easy to compute, but it may not be suitable for non-linear data. T-SNE is a non-linear technique that can capture complex relationships in the data, but it is computationally expensive and can be sensitive to the choice of parameters.

## Model selection and evaluation

Model selection and evaluation are crucial steps in the ML process. Model selection involves choosing the best model for a given task, while model evaluation involves assessing the performance of a model on a separate dataset.

**Model Selection Techniques:**

*   **Cross-Validation:** A technique that involves splitting the data into multiple folds and training and evaluating the model on different combinations of folds. This helps to estimate the model's performance on unseen data.
*   **Grid Search:** A technique that involves training and evaluating the model on a grid of hyperparameter values. This helps to find the best combination of hyperparameters for the model.

**Evaluation Metrics:**

*   **Regression:**
    *   **Mean Squared Error (MSE):** A measure of the average squared difference between the predicted and actual values.
    *   **R-Squared:** A measure of the proportion of variance in the target variable that is explained by the model.
*   **Classification:**
    *   **Accuracy:** A measure of the proportion of correctly classified instances.
    *   **Precision:** A measure of the proportion of positive predictions that are actually positive.
    *   **Recall:** A measure of the proportion of actual positive instances that are correctly predicted as positive.
    *   **F1-Score:** A harmonic mean of precision and recall.
    *   **AUC (Area Under the Curve):** A measure of the model's ability to distinguish between positive and negative instances.

**Bias-Variance Tradeoff:**

The bias-variance tradeoff is a fundamental concept in ML. Bias is the error due to the model's inability to capture the underlying patterns in the data. Variance is the error due to the model's sensitivity to the training data. A model with high bias is said to be underfitting, while a model with high variance is said to be overfitting. The goal is to find a model that has low bias and low variance.
