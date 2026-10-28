# Geometric Transformations Using OpenCV

---

## Aim

To write a Python program using OpenCV to perform various geometric transformations on an image.

The program performs the following operations:

- Image Translation  
- Image Scaling (Resizing)  
- Image Shearing  
- Image Reflection (Flipping)  
- Image Rotation  

---

##  Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

##  Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the input image in color mode.

### Step 3: Image Translation
- Create a translation matrix to shift the image  
- Move the image 50 pixels to the right and 80 pixels down  
- Apply transformation using `cv2.warpAffine()`  
- Display original and translated images  

### Step 4: Image Scaling
- Resize the image to 0.5× (downscale)  
- Resize the image to 2× (upscale)  
- Use `cv2.resize()`  
- Display original, downscaled, and upscaled images  

### Step 5: Image Shearing
- Create transformation matrices for:
  - Horizontal shearing  
  - Vertical shearing  
- Apply transformations using `cv2.warpAffine()`  
- Display original and sheared images  

### Step 6: Image Reflection
- Perform flipping using `cv2.flip()`:
  - Horizontal reflection  
  - Vertical reflection  
  - Both axes  
- Display all reflected images  

### Step 7: Image Rotation
- Create rotation matrices for:
  - 45° rotation  
  - 90° rotation  
- Use `cv2.getRotationMatrix2D()` and `cv2.warpAffine()`  
- Display original and rotated images  

---

##  Program
```

import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 1: Read the input image
img = cv2.imread("parrot.jpg")

if img is None:
    print("Error: parrot.jpg not found!")
    print("Keep parrot.jpg in the same folder as geo.py")
    raise SystemExit

# Convert BGR to RGB for correct display
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

height, width = img.shape[:2]


# Step 2: Image Translation
translation_matrix = np.float32([
    [1, 0, 50],
    [0, 1, 80]
])

translated = cv2.warpAffine(
    img, translation_matrix, (width, height)
)


# Step 3: Image Scaling
downscaled = cv2.resize(
    img, None, fx=0.5, fy=0.5
)

upscaled = cv2.resize(
    img, None, fx=2, fy=2
)


# Step 4: Image Shearing
horizontal_matrix = np.float32([
    [1, 0.5, 0],
    [0, 1, 0]
])

vertical_matrix = np.float32([
    [1, 0, 0],
    [0.5, 1, 0]
])

horizontal_shear = cv2.warpAffine(
    img, horizontal_matrix,
    (int(width * 1.5), height)
)

vertical_shear = cv2.warpAffine(
    img, vertical_matrix,
    (width, int(height * 1.5))
)


# Step 5: Image Reflection
horizontal_flip = cv2.flip(img, 1)
vertical_flip = cv2.flip(img, 0)
both_flip = cv2.flip(img, -1)


# Step 6: Image Rotation
center = (width // 2, height // 2)

rotation_45_matrix = cv2.getRotationMatrix2D(
    center, 45, 1.0
)

rotation_90_matrix = cv2.getRotationMatrix2D(
    center, 90, 1.0
)

rotated_45 = cv2.warpAffine(
    img, rotation_45_matrix, (width, height)
)

rotated_90 = cv2.warpAffine(
    img, rotation_90_matrix, (width, height)
)


# Step 7: Function to display images neatly
def show_images(title, images):
    count = len(images)

    fig, axes = plt.subplots(
        1, count, figsize=(5 * count, 5)
    )

    fig.suptitle(
        title, fontsize=18, fontweight="bold"
    )

    if count == 1:
        axes = [axes]

    for ax, (image, label) in zip(axes, images):
        ax.imshow(image)
        ax.set_title(label, fontsize=12)
        ax.axis("off")

    plt.tight_layout(rect=[0, 0, 1, 0.90])
    plt.show()


# 1. Original Image
show_images("1. Original Image", [
    (img, "Original")
])


# 2. Image Translation
show_images("2. Image Translation", [
    (img, "Original"),
    (translated, "Translated")
])


# 3. Image Scaling
show_images("3. Image Scaling", [
    (img, "Original"),
    (downscaled, "Downscaled 0.5x"),
    (upscaled, "Upscaled 2x")
])


# 4. Image Shearing
show_images("4. Image Shearing", [
    (img, "Original"),
    (horizontal_shear, "Horizontal Shearing"),
    (vertical_shear, "Vertical Shearing")
])


# 5. Image Reflection
show_images("5. Image Reflection", [
    (img, "Original"),
    (horizontal_flip, "Horizontal Flip"),
    (vertical_flip, "Vertical Flip"),
    (both_flip, "Both Axes Flip")
])


# 6. Image Rotation
show_images("6. Image Rotation", [
    (img, "Original"),
    (rotated_45, "Rotation 45 Degrees"),
    (rotated_90, "Rotation 90 Degrees")
])
```

### Developed By:
**Name:** Dharshini V 

### Register No:212225100010
____________________________  

---

##  Output

### Image Translation
- Original image is displayed  
- Translated image (shifted right and down) is displayed  
<img width="1917" height="1032" alt="image" src="https://github.com/user-attachments/assets/9bfa90ec-2335-4d41-9cec-195d5e106df5" />

### Image Scaling
- Original image is displayed  
- Downscaled image (0.5×) is displayed  
- Upscaled image (2×) is displayed  
<img width="1917" height="1025" alt="image" src="https://github.com/user-attachments/assets/d39c5743-c4dc-4e98-8da3-f37247489122" />

### Image Shearing
- Original image is displayed  
- Horizontally sheared image is displayed  
- Vertically sheared image is displayed  
<img width="1872" height="1023" alt="image" src="https://github.com/user-attachments/assets/49619c01-be41-46a9-a3da-b2d027ddbe6c" />

### Image Reflection
- Original image is displayed  
- Horizontally flipped image is displayed  
- Vertically flipped image is displayed  
- Both-axis flipped image is displayed
- <img width="1917" height="1025" alt="image" src="https://github.com/user-attachments/assets/f17a954c-c860-479d-9c50-b2f054d48c9e" />


### Image Rotation
- Original image is displayed  
- 45° rotated image is displayed  
- 90° rotated image is displayed  
![Uploading image.png…]()

---

##  Result

Thus, various geometric transformations such as translation, scaling, shearing, reflection, and rotation are successfully performed using OpenCV. These transformations demonstrate how images can be spatially manipulated for different computer vision applications.
