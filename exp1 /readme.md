import cv2
from google.colab import files
from google.colab.patches import cv2_imshow
uploaded = files.upload()
filename = next(iter(uploaded))
image = cv2.imread(filename)
if image is None:
    print("Error: Unable to read the image.")
else:
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    print("Original Image:")
    cv2_imshow(image)
    print("Grayscale Image:")
    cv2_imshow(gray_image)
    cv2.imwrite("grayscale_output.jpg", gray_image)
    print("Grayscale conversion completed.")
