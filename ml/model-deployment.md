# Model Deployment

## Overview
Strategies for deploying ML models to production.

## Flask API
```python
from flask import Flask, request, jsonify
import joblib

app = Flask(__name__)
model = joblib.load('model.pkl')

@app.route('/predict', methods=['POST'])
def predict():
    data = request.json
    prediction = model.predict([data['features']])
    return jsonify({'prediction': prediction.tolist()})
```

## Docker
```dockerfile
FROM python:3.9
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

## Best Practices
1. Version your models
2. Monitor performance
3. A/B testing
4. Handle failures gracefully
