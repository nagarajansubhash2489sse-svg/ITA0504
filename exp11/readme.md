import cv2
import os
import numpy as np
from google.colab.patches import cv2_imshow
image_path = 'image.jpg'
if not os.path.exists(image_path) and os.path.exists('experiment.jpg'):
    os.rename('experiment.jpg', image_path)
image = cv2.imread(image_path)
if image is None:
    print("Could not find your uploaded image. Creating a temporary demonstration image...")
    image = np.zeros((300, 300, 3), dtype=np.uint8)
    for i in range(300):
        image[:, i] = [255 - i * 255 // 300, 0, i * 255 // 300]
    cv2.putText(image, "F", (100, 200), cv2.FONT_HERSHEY_SIMPLEX, 5, (255, 255, 255), 10)
flipped_image = cv2.flip(image, 1)
rotated_image = cv2.rotate(flipped_image, cv2.ROTATE_180)
print("Original Image:")
cv2_imshow(image)
print("\nRotated 180-degree Clockwise Along Y-axis:")
cv2_imshow(rotated_image)
cv2.imwrite("rotated_image.jpg", rotated_image)
print("\nTransformation complete! Saved output as 'rotated_image.jpg'.")
