import cv2
import matplotlib.pyplot as plt
import random
import os

# List of available processed image files in the current workspace
processed_images = [
    "/content/image.jpg",
    "/content/opened_image.jpg",
    "/content/closed_image.jpg",
    "/content/top_hat_image.jpg",
    "/content/black_hat_image.jpg",
    "/content/sobel_combined.jpg"
]

# Filter to keep only the files that actually exist in the workspace
existing_images = [img for img in processed_images if os.path.exists(img)]

if existing_images:
    # Randomly select one image
    selected_image_path = random.choice(existing_images)
    
    # Read and display the selected image
    img = cv2.imread(selected_image_path)
    
    plt.figure(figsize=(8, 6))
    if len(img.shape) == 2 or img.shape[2] == 1:
        # Grayscale
        plt.imshow(img, cmap='gray')
    else:
        # Convert BGR to RGB
        img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
        plt.imshow(img_rgb)
        
    plt.title(f"Randomly Selected: {os.path.basename(selected_image_path)}")
    plt.axis('off')
    plt.show()
else:
    print("No processed images found in the workspace to select from.")
