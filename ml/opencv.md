# OpenCV

## Overview
OpenCV is a library for computer vision and image processing.

## Basic Usage
```python
import cv2

# Read image
img = cv2.imread('image.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Resize
resized = cv2.resize(img, (300, 300))

# Edge detection
edges = cv2.Canny(gray, 100, 200)

# Face detection
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
faces = face_cascade.detectMultiScale(gray, 1.1, 4)

# Video capture
cap = cv2.VideoCapture(0)
while True:
    ret, frame = cap.read()
    cv2.imshow('Frame', frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
```

## Resources
- OpenCV Documentation
