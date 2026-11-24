import cv2
from google.colab.patches import cv2_imshow

def segment_image(image_path, threshold_value=127):
    # Read the input image in grayscale
    image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
    if image is None:
        print(f"Error: Could not load image from {image_path}")
        return

    # Apply thresholding for binary segmentation
    _, segmented_image = cv2.threshold(image, threshold_value, 255, cv2.THRESH_BINARY)

    # Display the results using Colab-safe viewer patch
    print("Original Grayscale Image:")
    cv2_imshow(image)
    print("Segmented Image (Threshold = " + str(threshold_value) + "):")
    cv2_imshow(segmented_image)

# Run the segmentation on your uploaded image
segment_image("/content/images (1).jfif", 127)
