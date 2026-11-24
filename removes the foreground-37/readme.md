import numpy as np
import cv2
from google.colab.patches import cv2_imshow

def subtract_foreground(image_path, lower_color, upper_color):
    # Read the image
    image = cv2.imread(image_path)
    if image is None:
        print(f"Error: Could not load image from {image_path}")
        return

    # Convert to HSV color space
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # Define lower and upper range for foreground color (to remove)
    lower_bound = np.array(lower_color, dtype=np.uint8)
    upper_bound = np.array(upper_color, dtype=np.uint8)

    # Create mask for the foreground color to remove
    mask = cv2.inRange(hsv, lower_bound, upper_bound)
    
    # Create inverse mask to extract only the background
    background_mask = cv2.bitwise_not(mask)

    # Extract the background
    background = cv2.bitwise_and(image, image, mask=background_mask)

    # Display results safely using Colab patches
    print("Original Image:")
    cv2_imshow(image)
    print("Foreground Subtracted Image (Only Background):")
    cv2_imshow(background)

# Configure parameters to use your selected image
image_path = "/content/images (1).jfif"
lower_color = [0, 50, 50]     # Example lower bound for foreground color
upper_color = [120, 255, 255] # Example upper bound for foreground color

subtract_foreground(image_path, lower_color, upper_color)
