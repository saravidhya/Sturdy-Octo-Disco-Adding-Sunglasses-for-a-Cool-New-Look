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

## Program:

```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceimage=cv2.imread("C:\Bhuvaneshwaran important details\SCL_0648 copy (1).jpg")
plt.imshow(faceimage[:,:,::-1]);plt.title("face")
```

```
faceimage.shape
```
![image](https://github.com/user-attachments/assets/febca43a-bfce-4a1f-9156-d61ffae88f9c)

```
#resized_faceImage.shape
faceimage.shape
```
![image](https://github.com/user-attachments/assets/9fb44966-74d3-4331-a9fc-121f1e8fdaf7)

```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glasspng=cv2.imread('sun.png',-1)
plt.imshow(glasspng[:,:,::-1]);plt.title("GLASSPNG")
```
![image](https://github.com/user-attachments/assets/aff8067f-c4ab-482e-a025-f602f343cd1a)
```
# Resize the image to fit over the eye region
glasspng=cv2.resize(glasspng,(170,80))
print("image Dimension={}".format(glasspng.shape))
```
![image](https://github.com/user-attachments/assets/74977477-d7c9-4add-9f28-f4cb78ad1be4)
```
# Separate the Color and alpha channels
glassbgr=glasspng[:,:,0:3]
glassmask1=glasspng[:,:,3]
```
```
# Display the images for clarity
plt.figure(figsize=[10,10])
plt.subplot(121);plt.imshow(glassbgr[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassmask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![image](https://github.com/user-attachments/assets/71ca3793-e675-4f63-a707-1f68f60dc5ee)
```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
facewithglassesnaive=faceimage.copy()
```
```
# Replace the eye region with the sunglass image
facewithglassesnaive[150:230, 125:295]=glassbgr
plt.imshow(facewithglassesnaive[...,::-1])
```
![image](https://github.com/user-attachments/assets/cd87fab1-126c-463b-b94e-cbf7256259d0)
```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassmask=cv2.merge((glassmask1,glassmask1,glassmask1))
```
```
# Make the values [0,1] since we are using arithmetic operations
glassmask=np.uint8(glassmask/255)

# Make a copy
facewithglassesarithmetic=faceimage.copy()

# Get the eye region from the face image
eyeroi=facewithglassesarithmetic[150:230,125:295]
maskedeye=cv2.multiply(eyeroi,(1-  glassmask))

# Use the mask to create the masked eye region
maskedglass=cv2.multiply(glassbgr,glassmask)

# Use the mask to create the masked sunglass region
eyeroifinal=cv2.add(maskedeye,maskedglass)

# Display the intermediate results
plt.figure(figsize=[10,10])
plt.subplot(131);plt.imshow(maskedeye[...,::-1]);plt.title("masked eye region")
plt.subplot(132);plt.imshow(maskedglass[...,::-1]);plt.title("masked sunglass region")
plt.subplot(133);plt.imshow(eyeroifinal[...,::-1]);plt.title("augmented eye and sunglass")
```
![image](https://github.com/user-attachments/assets/7ca473b0-ae23-45b4-95bc-8a30eaa0541e)
```
# Replace the eye ROI with the output from the previous section
facewithglassesarithmetic[150:230,125:295]=eyeroifinal

# Display the final result
plt.figure(figsize=[10,10]);
plt.subplot(121);plt.imshow(faceimage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(facewithglassesarithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
![Screenshot 2025-04-29 093129](https://github.com/user-attachments/assets/8079b407-d52e-4420-9309-9dc8f9801fc3)


## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!
