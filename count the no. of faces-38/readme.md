import sys
import os

# 1. Address NumPy 2.x and OpenCV compatibility issues by installing stable 1.x versions
try:
    import cv2
    import numpy as np
except (ImportError, AttributeError):
    print("Dependencies incompatible. Upgrading/downgrading packages for compatibility...")
    !pip install --quiet "numpy<2" "opencv-python-headless==4.8.0.76"
    print("Restarting kernel to apply package changes...")
    os.kill(os.getpid(), 9)

import cv2
from google.colab.patches import cv2_imshow
import urllib.request

def count_faces(image_path):
    # Load the image
    image = cv2.imread(image_path)
    if image is None:
        # Download a fallback sample if face_image.jpg does not exist
        if image_path == "face_image.jpg":
            print("face_image.jpg not found. Downloading a sample image...")
            sample_url = "https://raw.githubusercontent.com/opencv/opencv/master/samples/data/lena.jpg"
            urllib.request.urlretrieve(sample_url, "face_image.jpg")
            image = cv2.imread(image_path)
        
        if image is None:
            print(f"Error: Could not load image from {image_path}")
            return 0

    # Convert image to grayscale
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Load the pre-trained Haar cascade face detection model
    face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')

    # Detect faces in the image
    faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))

    # Count the number of faces
    face_count = len(faces)
    print(f"Number of faces detected: {face_count}")

    # Draw rectangles around detected faces
    for (x, y, w, h) in faces:
        cv2.rectangle(image, (x, y), (x + w, y + h), (0, 255, 0), 2)

    # Display the image with detected faces safely using the Colab patch
    cv2_imshow(image)
    return face_count

# Example usage with download-fallback check
image_path = "face_image.jpg"
count_faces(image_path)
