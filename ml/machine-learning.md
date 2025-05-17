# Machine Learning Fundamentals

## Overview
Machine Learning is a subset of AI that enables systems to learn from data and improve from experience.

## Types of ML
1. **Supervised Learning**: Labeled data (Classification, Regression)
2. **Unsupervised Learning**: Unlabeled data (Clustering, Dimensionality Reduction)
3. **Reinforcement Learning**: Learn through rewards

## Workflow
```python
# 1. Load data
import pandas as pd
data = pd.read_csv('data.csv')

# 2. Preprocess
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# 3. Split
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# 4. Train
from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier()
model.fit(X_train, y_train)

# 5. Evaluate
from sklearn.metrics import accuracy_score
predictions = model.predict(X_test)
accuracy = accuracy_score(y_test, predictions)
```

## Common Algorithms
- **Linear Regression**: Continuous output
- **Logistic Regression**: Binary classification
- **Decision Trees**: Rule-based
- **Random Forest**: Ensemble of trees
- **SVM**: Margin maximization
- **Neural Networks**: Deep learning

## Metrics
- **Classification**: Accuracy, Precision, Recall, F1, AUC-ROC
- **Regression**: MSE, RMSE, MAE, R²

## Best Practices
1. **Understand your data** first
2. **Handle missing values**
3. **Feature engineering** matters
4. **Cross-validate** results
5. **Avoid data leakage**

## Resources
- scikit-learn Documentation
- Hands-On Machine Learning (book)
