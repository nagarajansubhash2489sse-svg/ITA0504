import cv2
from google.colab.patches import cv2_imshow
image = cv2.imread("Screenshot 2025-12-10 221357.png")
if image is None:
    print("Error: Could not load the image. Please verify your filename.")
else:
    rotated_img = cv2.rotate(image, cv2.ROTATE_90_CLOCKWISE)
    print("Original Image:")
    cv2_imshow(image)
    print("\nRotated Image (90 Degrees Clockwise):")
    cv2_imshow(rotated_img)
    cv2.imwrite("rotated_output.jpg", rotated_img)
    print("\nImage successfully rotated and saved as 'rotated_output.jpg'.")
