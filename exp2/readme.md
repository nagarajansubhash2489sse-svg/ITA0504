import cv2
from google.colab.patches import cv2_imshow
if 'image' not in globals() or image is None:
    image = cv2.imread("Screenshot 2025-12-10 221357.png")
if image is None:
    print("Error: Image not found. Please upload or provide a valid image first.")
else:
    blurred_image = cv2.GaussianBlur(image, (15, 15), 0)
    print("Original Image:")
    cv2_imshow(image)
    print("\nBlurred Image:")
    cv2_imshow(blurred_image)
    cv2.imwrite("blurred_output.jpg", blurred_image)
    print("\nImage successfully blurred and saved as 'blurred_output.jpg'.")
