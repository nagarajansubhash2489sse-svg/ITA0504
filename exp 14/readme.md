import cv2
import numpy as np
from google.colab.patches import cv2_imshow
image = cv2.imread("image.jpg")
if image is None:
    print("Error: 'image.jpg' not found. Please upload your image first.")
else:
    rows, cols, ch = image.shape
    pts1 = np.float32([[50, 50], [400, 50], [50, 400], [400, 400]])
    pts2 = np.float32([[10, 100], [300, 50], [100, 300], [350, 350]])
    matrix = cv2.getPerspectiveTransform(pts1, pts2)
    transformed_image = cv2.warpPerspective(image, matrix, (cols, rows))
    print("Original Image:")
    cv2_imshow(image)
    print("\nPerspective Transformed Image:")
    cv2_imshow(transformed_image)
    cv2.imwrite("perspective_transformed.jpg", transformed_image)
    print("\nSaved output as 'perspective_transformed.jpg'")
