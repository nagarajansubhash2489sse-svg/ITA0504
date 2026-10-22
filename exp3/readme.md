import cv2
from google.colab.patches import cv2_imshow
if 'image' not in globals() or image is None:
    image = cv2.imread("Screenshot 2025-12-10 221357.png")
if image is None:
    print("Error: No image found. Please run the upload cell first.")
else:
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    edges = cv2.Canny(gray_image, 100, 200)
    print("Original Image:")
    cv2_imshow(image)
    print("\nEdge Detected Image:")
    cv2_imshow(edges)
    cv2.imwrite("edges_output.jpg", edges)
    print("\nEdges successfully detected and saved as 'edges_output.jpg'.")
