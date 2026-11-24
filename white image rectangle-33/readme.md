import numpy as np
import cv2
from google.colab.patches import cv2_imshow

def create_rectangle_image(image_size):
    height, width = image_size  # Extract height and width
    # Create a white image (3D array of ones scaled to 255 for RGB/BGR)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    
    # Define rectangle coordinates (centered in the image)
    top_left = (width // 4, height // 4)
    bottom_right = (3 * width // 4, 3 * height // 4)
    
    # Draw the rectangle (color: Blue in BGR is (255, 0, 0), thickness: 2)
    cv2.rectangle(image, top_left, bottom_right, (255, 0, 0), 2)
    
    # Display the result safely in Colab
    print(f"Generated image of size {width}x{height} with centered rectangle:")
    cv2_imshow(image)

# Standard dimensions set directly to ensure reliable non-interactive execution
user_width = 400
user_height = 400

create_rectangle_image((user_height, user_width))
