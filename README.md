# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** [Your Name Here]  
- **Register Number:** [Your Register Number Here]

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
img_bgr=cv2.imread("Eagle_in_Flight.jpg",1)
```

#### 2. Print the image width, height & Channel.
```python
img_bgr.shape
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img_bgr[:,:,::-1])
plt.title("Eagle")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("Eagle_in_Flight.png", img_bgr)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img_png = cv2.imread("Eagle_in_Flight.png")
img_rgb = cv2.cvtColor(img_png, cv2.COLOR_BGR2RGB)

img_bgr.shape
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img_bgr[:,:,::-1])
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
cropped_reg=img_bgr[20:420,150:600]
plt.imshow(cropped_reg[:,:,::-1]);
```

#### 8. Resize the image up by a factor of 2x.
```python
img_resized = cv2.resize(img_bgr, None, fx=2, fy=2)

plt.imshow(img_resized[:,:,::-1])
plt.title("Resized Image (2x)")
plt.axis("off")
plt.show()

```

#### 9. Flip the cropped/resized image horizontally.
```python
img_flipped = cv2.flip(img_resized, 1)

plt.imshow(img_flipped[:,:,::-1])
plt.title("Flipped Image (Horizontal)")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
img_bgr2 = cv2.imread("Apollo-11-launch.jpg")
img_bgr2.shape
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN
font_scale = 2
thickness = 2
color = (255, 255, 255)  
h, w = img_bgr2.shape[:2]
(text_width, text_height), _ = cv2.getTextSize(text, font_face, font_scale, thickness)

x = (w - text_width) // 2
y = h - 20  
cv2.putText(img_bgr2, text, (x, y), font_face, font_scale, color, thickness)

import matplotlib.pyplot as plt
plt.imshow(img_bgr2[:,:,::-1])
plt.axis("off")
plt.title("Apollo 11 Launch with Text")
plt.show()
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
# rect_color = magenta
rect_color = (255, 0, 255)
top_left = (200, 50)
bottom_right = (600, 700)

cv2.rectangle(img_bgr2, top_left, bottom_right, rect_color, 3)
```

#### 13. Display the final annotated image.
```python
plt.imshow(img_bgr2[:,:,::-1]) 
plt.title("Final Annotated Image")
plt.axis("off")
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
img_bgr3 = cv2.imread("boy.jpg")
img_bgr3.shape
```

#### 15. Adjust the brightness of the image.
```python
# Create a matrix of ones (with data type float64)
# matrix_ones = 
brightness = 50 
img_bright = cv2.convertScaleAbs(img_bgr3, alpha=1, beta=brightness)

plt.imshow(img_bright[:,:,::-1])
plt.title("Brightened Image")
plt.axis("off")
plt.show()
```

#### 16. Create brighter and darker images.
```python
#img_brighter = cv2.add(img, matrix)
#img_darker = cv2.subtract(img, matrix)
img_bright = cv2.convertScaleAbs(img_bgr3, alpha=1, beta=50)
img_dark = cv2.convertScaleAbs(img_bgr3, alpha=1, beta=-50)
plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(img_bright[:,:,::-1])
plt.title("Brighter Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(img_dark[:,:,::-1])
plt.title("Darker Image")
plt.axis("off")

plt.show()
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(15,5))

# Original Image
plt.subplot(1,3,1)
plt.imshow(img_bgr3[:,:,[2,1,0]])
plt.title("Original Image")
plt.axis("off")

# Darker Image
plt.subplot(1,3,2)
plt.imshow(img_dark[:,:,[2,1,0]])
plt.title("Darker Image")
plt.axis("off")

# Brighter Image
plt.subplot(1,3,3)
plt.imshow(img_bright[:,:,[2,1,0]])
plt.title("Brighter Image")
plt.axis("off")

plt.show()
```

#### 18. Modify the image contrast.
```python
# Create two higher contrast images using the 'scale' option with factors of 1.1 and 1.2 (without overflow fix)
matrix1 = np.ones(img_bgr3.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_bgr3.shape, dtype="float32") * 1.2

img_higher1 = img_bgr3 * matrix1
img_higher2 = img_bgr3 * matrix2
```
#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
matrix_low = np.ones(img_bgr3.shape, dtype="float32") * 0.8
img_lower = (img_bgr3 * matrix_low).astype('uint8')

matrix_high = np.ones(img_bgr3.shape, dtype="float32") * 1.2
img_higher = (img_bgr3 * matrix_high).astype('uint8')
plt.figure(figsize=(12,5))

plt.subplot(1,3,1)
plt.imshow(img_bgr3[:,:,::-1])
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(img_lower[:,:,::-1])
plt.title("Lower Contrast")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(img_higher1[:,:,::-1])   
plt.title("Higher Contrast")
plt.axis("off")

```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img_bgr3)

plt.figure(figsize=(12,5))

plt.subplot(1,3,1)
plt.imshow(b, cmap='gray')
plt.title("Blue Channel")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(g, cmap='gray')
plt.title("Green Channel")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(r, cmap='gray')
plt.title("Red Channel")
plt.axis("off")

plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
b, g, r = cv2.split(img_bgr3)
img_merged = cv2.merge([b, g, r])

plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(img_bgr3[:,:,::-1])
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(img_merged[:,:,::-1])
plt.title("Merged Image")
plt.axis("off")

plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
img_hsv = cv2.cvtColor(img_bgr3, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(img_hsv)
plt.figure(figsize=(12,5))

plt.subplot(1,3,1)
plt.imshow(h, cmap='gray')
plt.title("Hue (H)")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(s, cmap='gray')
plt.title("Saturation (S)")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(v, cmap='gray')
plt.title("Value (V)")
plt.axis("off")

plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
img_hsv = cv2.cvtColor(img_bgr3, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(img_hsv)
img_hsv_merged = cv2.merge([h, s, v])
img_bgr_restored = cv2.cvtColor(img_hsv_merged, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(img_bgr3[:,:,::-1])
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(img_bgr_restored[:,:,::-1])
plt.title("Merged HSV Image")
plt.axis("off")

plt.show()
```

## Output:
- **i)** Read and Display an Image.  
- **ii)** Adjust Image Brightness.  
- **iii)** Modify Image Contrast.  
- **iv)** Generate Third Image Using Bitwise Operations.
- 
## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

