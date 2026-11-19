import cv2
import numpy as np
import matplotlib.pyplot as plt
import os

# Check if user image exists; if not, generate a synthetic test image
image_path = "image.jpg"
if not os.path.exists(image_path):
    print(f"'{image_path}' not found. Generating a synthetic test image...")
    # Create a 400x400 black image with some shapes
    synthetic_img = np.zeros((400, 400, 3), dtype=np.uint8)
    cv2.rectangle(synthetic_img, (80, 80), (320, 320), (255, 255, 255), -1)
    cv2.circle(synthetic_img, (200, 200), (80), (100, 100, 100), -1)
    cv2.imwrite(image_path, synthetic_img)

# Read the input image
image = cv2.imread(image_path)

# Convert the image to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply Sobel filter in X and Y directions
sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3) # Gradient in X direction
sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3) # Gradient in Y direction

# Convert gradients to absolute scale
sobel_x = cv2.convertScaleAbs(sobel_x)
sobel_y = cv2.convertScaleAbs(sobel_y)

# Combine the gradients
sobel_combined = cv2.addWeighted(sobel_x, 0.5, sobel_y, 0.5, 0)

# Display images inline using matplotlib
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Convert original BGR image to RGB for correct colors in matplotlib
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

axes[0, 0].imshow(image_rgb)
axes[0, 0].set_title("Original Image")
axes[0, 0].axis('off')

axes[0, 1].imshow(sobel_x, cmap='gray')
axes[0, 1].set_title("Sobel X")
axes[0, 1].axis('off')

axes[1, 0].imshow(sobel_y, cmap='gray')
axes[1, 0].set_title("Sobel Y")
axes[1, 0].axis('off')

axes[1, 1].imshow(sobel_combined, cmap='gray')
axes[1, 1].set_title("Sobel Combined")
axes[1, 1].axis('off')

plt.tight_layout()
plt.show()

# Save the results
cv2.imwrite("sobel_x.jpg", sobel_x)
cv2.imwrite("sobel_y.jpg", sobel_y)
cv2.imwrite("sobel_combined.jpg", sobel_combined)
