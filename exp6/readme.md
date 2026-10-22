import cv2
from google.colab.patches import cv2_imshow
if 'image' not in globals() or image is None:
    image = cv2.imread("Screenshot 2025-12-10 221357.png")
if image is None:
    print("Error: No image found. Please upload or provide a valid image first.")
else:
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    print("Original Image:")
    cv2_imshow(image)
    print("\nGrayscale Image:")
    cv2_imshow(gray_image)
