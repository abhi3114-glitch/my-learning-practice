# scikit-learn

## Overview
scikit-learn is a Python machine learning library providing simple and efficient tools for data analysis and modeling.

## Common Usage
```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train model
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train_scaled, y_train)

# Predict and evaluate
predictions = model.predict(X_test_scaled)
print(accuracy_score(y_test, predictions))
print(classification_report(y_test, predictions))
```

## Resources
- scikit-learn Documentation
