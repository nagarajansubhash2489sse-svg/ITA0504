import cv2
from google.colab.patches import cv2_imshow
image = cv2.imread("Screenshot 2025-12-10 221357.png")
if image is None:
    print("Error: Could not load the image. Please verify your filename.")
else:
    bigger_image = cv2.resize(image, None, fx=2, fy=2, interpolation=cv2.INTER_LINEAR)
    smaller_image = cv2.resize(image, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)
    print("Original Image:")
    cv2_imshow(image)
    print("\nBigger Image (2x Scale):")
    cv2_imshow(bigger_image)
    print("\nSmaller Image (0.5x Scale):")
    cv2_imshow(smaller_image)
    cv2.imwrite("bigger_output.jpg", bigger_image)
    cv2.imwrite("smaller_output.jpg", smaller_image)
    print("\nImages successfully resized and saved.")
