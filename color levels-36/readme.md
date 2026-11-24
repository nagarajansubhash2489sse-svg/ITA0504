import numpy as np
import cv2
from google.colab.patches import cv2_imshow

def subtract_background(image_path, lower_color, upper_color):
    # Read the image
    image = cv2.imread(image_path)
    if image is None:
        print(f"Error: Could not load image from {image_path}")
        return

    # Convert to HSV color space
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # Define lower and upper range for background color
    lower_bound = np.array(lower_color, dtype=np.uint8)
    upper_bound = np.array(upper_color, dtype=np.uint8)

    # Create mask for background removal
    mask = cv2.inRange(hsv, lower_bound, upper_bound)

    # Invert mask to keep the foreground
    mask_inv = cv2.bitwise_not(mask)

    # Extract the foreground
    foreground = cv2.bitwise_and(image, image, mask=mask_inv)

    # Display results safely using Colab patches
    print("Original Image:")
    cv2_imshow(image)
    print("Background Subtracted Image:")
    cv2_imshow(foreground)

# Configure the parameters to use your selected image and a default color threshold
image_path = "/content/images (1).jfif"
lower_color = [0, 0, 200]    # Adjustable lower bound (defaults targeting lighter backgrounds)
upper_color = [180, 50, 255] # Adjustable upper bound

subtract_background(image_path, lower_color, upper_color)
