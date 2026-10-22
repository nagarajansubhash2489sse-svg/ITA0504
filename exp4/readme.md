import cv2
from google.colab.patches import cv2_imshow
if 'image' not in globals() or image is None:
    image = cv2.imread("Screenshot 2025-12-10 221357.png")
if image is None:
    print("Error: No image found. Please upload or provide a valid image first.")
else:
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    equalized_image = cv2.equalizeHist(gray_image)
    print("Original Grayscale Image:")
    cv2_imshow(gray_image)
    print("\nHistogram Equalized Image:")
    cv2_imshow(equalized_image)
    cv2.imwrite("equalized_output.jpg", equalized_image)
    print("\nHistogram equalization completed successfully and saved as 'equalized_output.jpg'.")
