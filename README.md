# STURDY OCTO DISCO – SUNGLASSES OVERLAY USING OPENCV

## Aim
To overlay sunglasses on a face image using Python and OpenCV image processing techniques.

## Description
Sturdy Octo Disco is a fun image processing project that adds sunglasses to individual passport-size photos. It uses image resizing, masking, and arithmetic blending techniques to place sunglasses over the eye region.

## Features
- Loads and displays a face image.
- Loads sunglasses with an alpha channel.
- Resizes sunglasses according to the eye region.
- Separates color and alpha channels.
- Applies image masking techniques.
- Combines the face and sunglasses using arithmetic operations.
- Displays the original and final images.

## Technologies Used
- Python
- OpenCV
- NumPy
- Matplotlib
- Jupyter Notebook

## Input Images
- `Image.png` – Original face image.
- `sunglass-png-trendy-sunglasses-prescription-sunglasses-1024.png` – Sunglasses image.

## Implementation
## NAME: Rubasri R
## REG NO: 212224240139
### 1. Import Libraries
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### 2. Load the Face Image
```python
faceImage = cv2.imread('Image.png')
plt.imshow(faceImage[:,:,::-1])
plt.title("Face")
```

### 3. Load the Sunglasses Image
```python
glassPNG = cv2.imread('sunglass-png-trendy-sunglasses-prescription-sunglasses-1024.png', -1)
```

### 4. Resize the Sunglasses
```python
glassPNG = cv2.resize(glassPNG, (360, 140))
```

### 5. Separate Color and Alpha Channels
```python
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

### 6. Apply Sunglasses to the Face
```python
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[390:530, 350:710] = glassBGR
```

### 7. Apply Alpha Masking
```python
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))
glassMask = glassMask.astype(np.float32) / 255.0

glassBGR = glassBGR.astype(np.float32)
eyeROI = faceImage[390:530, 350:710].astype(np.float32)

maskedEye = cv2.multiply(eyeROI, (1 - glassMask))
maskedGlass = cv2.multiply(glassBGR, glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
```

### 8. Display the Final Output
```python
faceWithGlassesArithmetic = faceImage.copy()
faceWithGlassesArithmetic[390:530, 350:710] = np.uint8(eyeRoiFinal)

plt.figure(figsize=[20,20])

plt.subplot(121)
plt.imshow(faceImage[:,:,::-1])
plt.title("Original Image")

plt.subplot(122)
plt.imshow(faceWithGlassesArithmetic[:,:,::-1])
plt.title("With Sunglasses")

plt.show()
```

## Output
<img width="370" height="455" alt="image" src="https://github.com/user-attachments/assets/ce8c7051-4ccb-4c25-a60e-afd4d4588af0" />

<img width="379" height="446" alt="image" src="https://github.com/user-attachments/assets/dacd6b21-b5fe-4a05-b62e-48f70febb310" />

<img width="1103" height="195" alt="image" src="https://github.com/user-attachments/assets/e67a27b7-983d-408b-b48b-d156755549c4" />

<img width="608" height="264" alt="image" src="https://github.com/user-attachments/assets/4d65164b-3296-4ef8-aba6-fd3127142cbe" />

<img width="1081" height="177" alt="image" src="https://github.com/user-attachments/assets/90949551-514e-48d0-8a30-cbc968bc5075" />

## Applications
- Digital image processing.
- Face image augmentation.
- Computer vision learning.
- Photo editing and enhancement.
- Image masking and blending practice.

## Conclusion
The project successfully demonstrates sunglasses overlay on a face image using OpenCV, NumPy, and Matplotlib. It helps understand image resizing, alpha masking, and arithmetic blending techniques.
