# Part 2
## Student Information

**Project:** Applied AI & ML Essentials Capstone Project  
**Part:** Part 2 – Supervised Machine Learning

---

# Dataset

This part uses the cleaned dataset produced in Part 1.

```
BHP_cleaned.csv
```

---

# Objective

The objective of this part is to build and evaluate:

- A Regression model for predicting house prices.
- A Classification model for predicting whether a house price is above or below the median price.

---

# Python Libraries Used

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

---

# Target Variables

## Regression Target

The regression target is:

```
price
```

This is a continuous numerical variable representing the selling price of a property.

---

## Classification Target

The classification target was created by converting the price column into a binary label.

```python
(price > price.median()).astype(int)
```

Meaning:

- 1 = Price above the median
- 0 = Price at or below the median

---

# Feature Encoding

The dataset contains several categorical variables.

Since these variables have no natural ordering, One-Hot Encoding was used.

```python
pd.get_dummies(drop_first=True)
```

Using one-hot encoding prevents the model from incorrectly assuming that one category has a greater numerical value than another.

The first dummy variable was dropped to reduce multicollinearity.

---

# Train-Test Split

The data was split into training and testing datasets using:

```python
train_test_split()
```

Parameters used:

- Test Size = 20%
- Random State = 42

---

# Feature Scaling

StandardScaler was applied **only on the training data** before transforming the testing data.

This prevents **data leakage**.

If the scaler were fitted using the entire dataset, information from the test set would influence the training process, producing overly optimistic evaluation results.

---

# Linear Regression

A Linear Regression model was trained using the scaled training data.

Evaluation metrics:

- Mean Squared Error (MSE)
- R² Score

The model coefficients were printed to determine which features had the strongest influence on predicted house prices.

Large positive coefficients indicate that increasing the feature increases the predicted house price.

Large negative coefficients indicate that increasing the feature decreases the predicted house price.

---

# Ridge Regression

A Ridge Regression model with:

```python
alpha = 1.0
```

was trained using the same training data.

The MSE and R² values were compared against Linear Regression.

Ridge Regression adds L2 regularization, which reduces excessively large coefficients and helps improve model generalization when features are highly correlated.

The alpha parameter controls the amount of regularization.

---

# Logistic Regression

A Logistic Regression classifier was trained to classify whether a property price is above or below the median.

The model produced:

- Confusion Matrix
- Accuracy
- Precision
- Recall
- F1 Score
- ROC Curve
- AUC Score

---

# Precision and Recall

Precision is calculated as:

```
Precision = TP / (TP + FP)
```

Recall is calculated as:

```
Recall = TP / (TP + FN)
```

For this project, **Recall** is considered slightly more important because identifying expensive houses correctly is generally more useful than incorrectly classifying a few lower-priced houses.

---

# ROC Curve and AUC

The ROC curve illustrates the trade-off between the True Positive Rate and False Positive Rate.

The Area Under the Curve (AUC) measures how well the classifier separates the two classes.

An AUC closer to 1 indicates better classification performance.

---

# Decision Threshold Analysis

The default classification threshold of 0.5 was compared with thresholds ranging from:

- 0.30
- 0.40
- 0.50
- 0.60
- 0.70

For each threshold, Precision, Recall, and F1-score were calculated.

The threshold with the highest F1-score was identified as the best balance between Precision and Recall.

---

# Logistic Regression Regularization

A second Logistic Regression model was trained using:

```
C = 0.01
```

The results were compared with the default model:

```
C = 1.0
```

The parameter **C** controls the strength of regularization.

A smaller C value increases regularization, which reduces model complexity but may also reduce predictive performance.

---

# Bootstrap Confidence Interval

To compare both Logistic Regression models, 500 bootstrap samples were drawn from the testing dataset.

For each sample:

- ROC AUC was calculated for both models.
- The AUC difference was computed.

Finally:

- Mean AUC Difference
- 2.5 Percentile
- 97.5 Percentile

were reported to construct a 95% confidence interval.

If the confidence interval excludes zero, the performance difference between the two models is considered reliable.

---

# Summary

In this part, both regression and classification models were successfully developed using the cleaned housing dataset.

The data was encoded, scaled correctly, and split without introducing data leakage.

Model performance was evaluated using multiple regression and classification metrics, allowing a comparison between standard models and their regularized versions.
