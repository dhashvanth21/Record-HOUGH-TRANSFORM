#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Developed By

* **Name:**   DHASHVANTH B
* **Register No:** 212224230064
 
---

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
# Read the image using OpenCV

###
# Your Code Here
###

image = cv2.imread('Qn_7_.jpg')
```

---

###  Step 3: Convert to Grayscale

```python
# Convert to grayscale.

###
# Your Code Here
###

gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

---

###  Step 4: Display Images

```python
plt.figure(figsize=(10,5))

###
# Your Code Here
###

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray_image, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```

---

###  Step 5: Thresholding

```python
# Apply thresholding

threshold = cv2.threshold(
    gray_image,
    127,
    255,
    cv2.THRESH_BINARY
)[1]

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```

---

###  Step 6: Region of Interest (ROI)

```python
# ROI masking already provided
height, width = threshold.shape

# Define a broad polygonal region of interest
roi_vertices = np.array([[
    (0, height),
    (0, int(height * 0.45)),
    (width, int(height * 0.45)),
    (width, height)
]], dtype=np.int32)

roi_mask = np.zeros_like(threshold)
cv2.fillPoly(roi_mask, roi_vertices, 255)
roi_image = cv2.bitwise_and(threshold, roi_mask)
```

---

### Step 7: Edge Detection (Canny)

```python
# Perform Edge Detection

###
# Your Code Here
###

edges = cv2.Canny(
    gray_image,
    50,
    150
)

plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```

---

###  Step 8: Gaussian Blur

```python
# Apply Gaussian Blur

###
# Your Code Here
###

blurred = cv2.GaussianBlur(
    edges,
    (5, 5),
    0
)

plt.imshow(blurred, cmap="gray")
plt.title("Smoothed Image")
plt.axis("off")
plt.show()
```

---

###  Step 9: Hough Transform

```python
# Detect lines using Hough Transform

###
# Your Code Here
###

lines = cv2.HoughLinesP(
    blurred,
    1,
    np.pi / 180,
    threshold=100,
    minLineLength=50,
    maxLineGap=10
)
```

---

### Step 10: Lane Detection Logic

```python
# Already implemented
# Step 5: Detect lines using HoughLinesP
lines = cv2.HoughLinesP(
    edges,
    1,
    np.pi / 180,
    100,
    minLineLength=50,
    maxLineGap=10
)
# Step 6: Using a for loop, draw the lines on the original image using the detected coordinates
# The lines variable contains the endpoints of the detected lines
if lines is not None:
    print(lines.shape)
    print(lines[:5])
    for line in lines:
        x1, y1, x2, y2 = line
        cv2.line(image, (x1, y1), (x2, y2), (0, 255, 0), 2)
# Display the result of Hough Transform (Image with lines)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Image with lines drawn
plt.title("Result of Hough Transform")
plt.axis('off')

```

---

##  Expected Output

* Original image

<img width="268" height="410" alt="download" src="https://github.com/user-attachments/assets/00913c16-84ac-4bf6-b139-9b07d11a1053" />


* Grayscale image

<img width="268" height="410" alt="download" src="https://github.com/user-attachments/assets/9c193f4d-72b1-4185-b33c-d10db4e33623" />


* Thresholded image

<img width="268" height="410" alt="download" src="https://github.com/user-attachments/assets/aca804f2-14a6-4e9c-9f66-c31c95e720c9" />


* ROI masked image

<img width="268" height="410" alt="download" src="https://github.com/user-attachments/assets/cdf6ed27-eb9a-439a-9264-24eb02e7dd29" />


* Smoothed image

* 
<img width="268" height="410" alt="download" src="https://github.com/user-attachments/assets/4f5b7ea4-c701-4f34-94dd-8b4992074447" />


* Final lane detection output

<img width="268" height="410" alt="download" src="https://github.com/user-attachments/assets/9e7baec2-dc9a-46b6-87e2-eb9f054ddee1" />



---


## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---
