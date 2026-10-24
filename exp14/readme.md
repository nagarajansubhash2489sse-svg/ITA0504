import cv2
import numpy as np
from google.colab.patches import cv2_imshow
image = cv2.imread("image.jpg")
if image is None:
    print("Error: 'image.jpg' not found. Please upload your image first.")
else:
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3) # Gradient in X direction
    sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3) # Gradient in Y direction
    sobel_x = cv2.convertScaleAbs(sobel_x)
    sobel_y = cv2.convertScaleAbs(sobel_y)
    sobel_combined = cv2.addWeighted(sobel_x, 0.5, sobel_y, 0.5, 0)
    print("Original Image:")
    cv2_imshow(image)   
    print("\nSobel X (Horizontal Edges):")
    cv2_imshow(sobel_x)
    print("\nSobel Y (Vertical Edges):")
    cv2_imshow(sobel_y)
    print("\nSobel Combined:")
    cv2_imshow(sobel_combined)
    cv2.imwrite("sobel_x.jpg", sobel_x)
    cv2.imwrite("sobel_y.jpg", sobel_y)
    cv2.imwrite("sobel_combined.jpg", sobel_combined)
    print("\nResults saved as 'sobel_x.jpg', 'sobel_y.jpg', and 'sobel_combined.jpg'.")
