if image is None:
    print("Error: 'image.jpg' not found. Please upload your photo first.")
else:
    flipped_image = cv2.flip(image, 1)
    rotated_image = cv2.rotate(flipped_image, cv2.ROTATE_90_COUNTERCLOCKWISE)
    print("Original Image:")
    cv2_imshow(image) 
    print("\nRotated 270-degree Clockwise Along Y-axis (Flipped + ROTATE_90_COUNTERCLOCKWISE):")
    cv2_imshow(rotated_image)
    cv2.imwrite("rotated_image_270.jpg", rotated_image)
    print("\nSaved output as 'rotated_image_270.jpg'")
