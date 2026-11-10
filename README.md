# EX. NO. 04

# GEOMETRIC TRANSFORMATIONS USING OPENCV

---

## AIM

To write a Python program using OpenCV to perform various geometric transformations on an image.

The program performs the following operations:

- Image Translation
- Image Scaling (Resizing)
- Image Shearing
- Image Reflection (Flipping)
- Image Rotation

---

## SOFTWARE REQUIRED

1. Anaconda – Python
2. Jupyter Notebook / VS Code
3. OpenCV (`cv2`)
4. NumPy
5. Matplotlib

---

## ALGORITHM

### Step 1: Import Required Libraries

Import OpenCV, NumPy, and Matplotlib libraries.

### Step 2: Read the Input Image

Read the input image in color mode using `cv2.imread()` and check whether the image is loaded successfully.

### Step 3: Image Translation

- Get the height and width of the image.
- Create a translation matrix.
- Move the image 50 pixels to the right and 80 pixels down.
- Apply the transformation using `cv2.warpAffine()`.
- Display the original and translated images.

### Step 4: Image Scaling

- Resize the image to 0.5× (downscaling).
- Resize the image to 2× (upscaling).
- Use `cv2.resize()` to perform scaling.
- Display the original, downscaled, and upscaled images.

### Step 5: Image Shearing

- Create a transformation matrix for horizontal shearing.
- Create a transformation matrix for vertical shearing.
- Apply the transformations using `cv2.warpAffine()`.
- Display the original and sheared images.

### Step 6: Image Reflection

Perform image flipping using `cv2.flip()`:

- Horizontal reflection.
- Vertical reflection.
- Reflection along both axes.

Display all reflected images.

### Step 7: Image Rotation

- Find the center of the image.
- Create rotation matrices for 45° and 90°.
- Use `cv2.getRotationMatrix2D()` to create rotation matrices.
- Apply transformations using `cv2.warpAffine()`.
- Display the original and rotated images.

---

## PROGRAM

### Developed By:

**Name:** Mohammed Ameer F
### Register Number:

212225040248

**Note:** Keep the input image named `input.jpg` in the same folder as the Jupyter Notebook.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image
img = cv2.imread("input.jpg")

if img is None:
    raise FileNotFoundError("Image not found!")

# Convert BGR to RGB
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

height, width = img.shape[:2]

# 1. IMAGE TRANSLATION

translation_matrix = np.float32([
    [1, 0, 50],
    [0, 1, 80]
])

translated = cv2.warpAffine(
    img, translation_matrix, (width, height)
)

translated_rgb = cv2.cvtColor(translated, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(translated_rgb)
plt.title("Translated Image")
plt.axis("off")

plt.tight_layout()
plt.show()


# 2. IMAGE SCALING

downscaled = cv2.resize(
    img, None, fx=0.5, fy=0.5
)

upscaled = cv2.resize(
    img, None, fx=2, fy=2
)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(downscaled, cv2.COLOR_BGR2RGB))
plt.title("Downscaled Image (0.5x)")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(upscaled, cv2.COLOR_BGR2RGB))
plt.title("Upscaled Image (2x)")
plt.axis("off")

plt.tight_layout()
plt.show()


# 3. IMAGE SHEARING

horizontal_shear_matrix = np.float32([
    [1, 0.5, 0],
    [0, 1, 0]
])

vertical_shear_matrix = np.float32([
    [1, 0, 0],
    [0.5, 1, 0]
])

horizontal_sheared = cv2.warpAffine(
    img, horizontal_shear_matrix, (width, height)
)

vertical_sheared = cv2.warpAffine(
    img, vertical_shear_matrix, (width, height)
)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(horizontal_sheared, cv2.COLOR_BGR2RGB))
plt.title("Horizontal Shearing")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(vertical_sheared, cv2.COLOR_BGR2RGB))
plt.title("Vertical Shearing")
plt.axis("off")

plt.tight_layout()
plt.show()


# 4. IMAGE REFLECTION

horizontal_flip = cv2.flip(img, 1)
vertical_flip = cv2.flip(img, 0)
both_flip = cv2.flip(img, -1)

plt.figure(figsize=(15, 5))

plt.subplot(1, 4, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 4, 2)
plt.imshow(cv2.cvtColor(horizontal_flip, cv2.COLOR_BGR2RGB))
plt.title("Horizontal Flip")
plt.axis("off")

plt.subplot(1, 4, 3)
plt.imshow(cv2.cvtColor(vertical_flip, cv2.COLOR_BGR2RGB))
plt.title("Vertical Flip")
plt.axis("off")

plt.subplot(1, 4, 4)
plt.imshow(cv2.cvtColor(both_flip, cv2.COLOR_BGR2RGB))
plt.title("Both Axes Flip")
plt.axis("off")

plt.tight_layout()
plt.show()


# 5. IMAGE ROTATION

center = (width // 2, height // 2)

rotation_matrix_45 = cv2.getRotationMatrix2D(
    center, 45, 1.0
)

rotation_matrix_90 = cv2.getRotationMatrix2D(
    center, 90, 1.0
)

rotated_45 = cv2.warpAffine(
    img, rotation_matrix_45, (width, height)
)

rotated_90 = cv2.warpAffine(
    img, rotation_matrix_90, (width, height)
)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(rotated_45, cv2.COLOR_BGR2RGB))
plt.title("Rotated Image (45 Degrees)")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(rotated_90, cv2.COLOR_BGR2RGB))
plt.title("Rotated Image (90 Degrees)")
plt.axis("off")

plt.tight_layout()
plt.show()
```

---

## OUTPUT

### i) Image Translation

- Original image is displayed.
  <img width="631" height="367" alt="image" src="https://github.com/user-attachments/assets/2614c314-9e56-4301-ae31-db3105e40093" />

- Translated image shifted 50 pixels to the right and 80 pixels down is displayed.
  <img width="1306" height="387" alt="image" src="https://github.com/user-attachments/assets/ff62e367-c119-4756-b680-547af4aab1aa" />


### ii) Image Scaling

- Original image is displayed.
  <img width="432" height="247" alt="image" src="https://github.com/user-attachments/assets/a9bb8af4-7384-4a87-8369-591fab5f42a4" />


- Downscaled image (0.5×) is displayed.
  <img width="408" height="252" alt="image" src="https://github.com/user-attachments/assets/83d1e81d-44d2-440c-8f40-5fbdc39b83d5" />

- Upscaled image (2×) is displayed.
  <img width="421" height="267" alt="image" src="https://github.com/user-attachments/assets/fab20eba-b6fe-4f74-b80a-2fdd17d9f8fd" />


### iii) Image Shearing

- Original image is displayed.
  <img width="432" height="253" alt="image" src="https://github.com/user-attachments/assets/d43389cf-ff92-4705-94a3-8e8edc2368a0" />

- Horizontally sheared image is displayed.
  <img width="417" height="252" alt="image" src="https://github.com/user-attachments/assets/f4bc0a7a-8c5c-4f6a-b8cb-f59b08db56d8" />

- Vertically sheared image is displayed.
  <img width="430" height="255" alt="image" src="https://github.com/user-attachments/assets/b5d00332-8873-4d2e-ab46-bfade6da16cf" />


### iv) Image Reflection

- Original image is displayed.
  <img width="430" height="250" alt="image" src="https://github.com/user-attachments/assets/34df7ae2-75a8-45ea-8030-b6e2faec14f0" />

- Horizontally flipped image is displayed.
  <img width="330" height="182" alt="image" src="https://github.com/user-attachments/assets/4d7d5d8f-6961-41b1-bc7a-26c47b49a6b9" />

- Vertically flipped image is displayed.
  <img width="315" height="190" alt="image" src="https://github.com/user-attachments/assets/e752b8a1-24d9-44d5-8a28-1006bfc08bfd" />

- Both-axis flipped image is displayed.
  <img width="320" height="223" alt="image" src="https://github.com/user-attachments/assets/1397ea24-5369-4ac0-acae-7db6f15955cf" />


### v) Image Rotation

- Original image is displayed.
  <img width="321" height="203" alt="image" src="https://github.com/user-attachments/assets/4aa5db39-3ee7-426e-8b74-0ae42affc051" />

- Image rotated by 45° is displayed.
  <img width="415" height="252" alt="image" src="https://github.com/user-attachments/assets/0b24b09d-6d08-4b2f-a3af-61a724fee8a1" />

- Image rotated by 90° is displayed.
  <img width="425" height="266" alt="image" src="https://github.com/user-attachments/assets/24976a7b-0b97-46d8-861f-18deaec81e6b" />


---

## RESULT

Thus, various geometric transformations such as translation, scaling, shearing, reflection, and rotation are successfully performed on an image using OpenCV. These transformations demonstrate how images can be spatially manipulated for different computer vision applications.
