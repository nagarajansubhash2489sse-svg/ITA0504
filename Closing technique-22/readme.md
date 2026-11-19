import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image
image = cv2.imread('image.jpg') # Uses your uploaded image

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Define a 5x5 structuring element (kernel)
kernel = np.ones((5,5), np.uint8)

# Apply Morphological Closing (Dilation followed by Erosion)
closed_image = cv2.morphologyEx(gray_image, cv2.MORPH_CLOSE, kernel)

# Set up matplotlib subplot for safe inline visualization
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

# Convert BGR original to RGB for correct colors in matplotlib
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Plot original image
axes[0].imshow(image_rgb)
axes[0].set_title('Original Image')
axes[0].axis('off')

# Plot closed image
axes[1].imshow(closed_image, cmap='gray')
axes[1].set_title('Closed Image (Morphological Closing)')
axes[1].axis('off')

plt.tight_layout()
plt.show()

# Save the result
cv2.imwrite("closed_image.jpg", closed_image)
