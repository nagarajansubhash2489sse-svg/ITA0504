import cv2
import numpy as np
from google.colab.patches import cv2_imshow
image = cv2.imread("image.jpg")
if image is None:
    print("Error: 'image.jpg' not found. Please upload your photo first.")
else:
    rows, cols, ch = image.shape
    pts1 = np.float32([[50, 50], [200, 50], [50, 200]])
    pts2 = np.float32([[10, 100], [200, 50], [100, 250]])
    matrix = cv2.getAffineTransform(pts1, pts2)
    transformed_image = cv2.warpAffine(image, matrix, (cols, rows))
    print("Original Image:")
    cv2_imshow(image)
    print("\nAffine Transformed Image:")
    cv2_imshow(transformed_image)
    cv2.imwrite("affine_transformed.jpg", transformed_image)
    print("\nSaved output as 'affine_transformed.jpg'")
