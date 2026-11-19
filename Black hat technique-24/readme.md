import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image in grayscale
image = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)

# Define a 5x5 structuring element (kernel)
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))

# Apply the Black Hat transformation (Closing minus Original)
blackhat = cv2.morphologyEx(image, cv2.MORPH_BLACKHAT, kernel)

# Set up matplotlib subplot for safe inline visualization
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

# Plot original grayscale image
axes[0].imshow(image, cmap='gray')
axes[0].set_title('Original Grayscale Image')
axes[0].axis('off')

# Plot Black Hat image
axes[1].imshow(blackhat, cmap='gray')
axes[1].set_title('Black Hat Image')
axes[1].axis('off')

plt.tight_layout()
plt.show()

# Save the result
cv2.imwrite("black_hat_image.jpg", blackhat)
