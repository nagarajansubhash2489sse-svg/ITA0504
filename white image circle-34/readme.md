import numpy as np
import cv2
from google.colab.patches import cv2_imshow

def create_circle_image(image_size):
    height, width = image_size  # Extract height and width
    # Create a white image (3D array of ones scaled to 255 for BGR)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    
    # Define the circle properties
    center = (width // 2, height // 2)        # Center of the image
    radius = min(width, height) // 4          # Radius is 1/4th of the smallest dimension
    
    # Draw the circle (color: Red in BGR is (0, 0, 255), thickness: 2)
    cv2.circle(image, center, radius, (0, 0, 255), 2)
    
    # Display the result safely in Colab
    print(f"Generated image of size {width}x{height} with centered circle:")
    cv2_imshow(image)

# Standard dimensions set directly to ensure reliable non-interactive execution
user_width = 400
user_height = 400

create_circle_image((user_height, user_width))
