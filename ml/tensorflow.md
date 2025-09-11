# TensorFlow

## Overview
TensorFlow is Google's end-to-end machine learning platform.

## Keras API
```python
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(128, activation='relu', input_shape=(784,)),
    keras.layers.Dropout(0.2),
    keras.layers.Dense(10, activation='softmax')
])

model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

model.fit(x_train, y_train, epochs=10, validation_split=0.2)
model.evaluate(x_test, y_test)
model.save('model.h5')
```

## Resources
- TensorFlow Documentation
