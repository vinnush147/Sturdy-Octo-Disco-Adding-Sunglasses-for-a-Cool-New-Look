# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:

### Developed by: Vinnush Kumar LS
### Register Number: 212223230244

```
import cv2
import matplotlib.pyplot as plt
import numpy as np
faceImage = cv2.imread('passport.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="425" height="435" alt="download" src="https://github.com/user-attachments/assets/df5b1238-b97e-4909-96b9-694fac306bf5" />

```

glassPNG = cv2.imread('glasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="542" height="435" alt="download" src="https://github.com/user-attachments/assets/c03fd0dd-3e64-4026-bae5-e761e9b1fd7f" />

```
glassPNG = cv2.resize(glassPNG,(200,120))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1218" height="383" alt="download" src="https://github.com/user-attachments/assets/fa30fca9-9c5c-49cb-bd4c-cfb3374b5593" />

```
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[135:255, 116:316] = glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="425" height="418" alt="download" src="https://github.com/user-attachments/assets/49457a44-1979-40b2-80ff-b36453d37a60" />

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI= faceWithGlassesArithmetic[135:255, 116:316]
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
maskedGlass = cv2.multiply(glassBGR,glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
<img width="1606" height="339" alt="download" src="https://github.com/user-attachments/assets/b17e63af-26fb-41ff-81b3-08bd875f7114" />

```
faceWithGlassesArithmetic[135:255, 116:316]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

<img width="1606" height="770" alt="download" src="https://github.com/user-attachments/assets/3a67a40c-80c9-4a24-9178-e73e984ff525" />

Feel free to fork, contribute, or customize this project for your creative needs!
