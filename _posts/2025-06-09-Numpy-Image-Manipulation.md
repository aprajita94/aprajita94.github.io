---
layout: post
title: Manipulating an image using Numpy 
image: "/posts/camaro.jpg"
tags: [Python, Image, Numpy]
---
In this post, I am going to show a few different image manipulation tricks. It is fun to see that any colored image can be represented by a 3-dimensional matrix. Each index with row and column number corresponds to a pixel point and each dimension corresponds to a color channel - red, green or blue. We remember that these are the primary colors that make all the other colors. So, one can think of each pixel in an image to be made of a certain combination of red, green and blue color. Therefore, we can think of an image in terms of a Numpy array that we can perform a whole lot of operations on!    

Let's get into it!

---

First, let’s start by importing the packages and modules. We import the Numpy package to work with the image array. We also import the “io” package from scikit-image to read and write images and the matplotlib package to plot the images. 

```python
import numpy as np
from skimage import io
import matplotlib.pyplot as plt
```

We now bring in the image that we want to work with. The image is camaro.jpg. We read the image into a variable and print it. Lo and behold! As expected, our variable is a 3D array. We can verify this using the shape function. 

```python
camaro = io.imread("camaro.jpg")
print(camaro)
camaro.shape
```

Here is what the image looks like:

<br>
![alt text](/img/posts/camaro.jpg "Camaro image")
<br>


The shape is returned to be 1200 by 1600 by 3. We see that the image variable has 3 dimensions and that it is wider than it is tall. The value of 3 in the third dimension corresponds to the three channels - red, green and blue.  

# Cropping the image
Let’s first start by cropping the image. Let’s say we only want some part of the top of the image. So we do the following:

```python 
cropped = camaro[0:500,:,:] # Crop along the y-axis
plt.imshow(cropped)
plt.show()
```
<br>
![alt text](/img/posts/camaro_bottom_cropped.png "Bottom of the image cropped out of the original image")
<br>

Let’s do something similar, let’s crop out the right hand side of the image as such:
```python
cropped = camaro[:,400:1000,:] # Crop along the x-axis
plt.imshow(cropped)
plt.show()
```
We get the following:
<br>
![alt text](/img/posts/camaro_side_cropped.png "Side of the image cropped out of the original image" )
<br>
That looks like it worked! 
Let us now crop the camaro out of its environment!

```python
cropped = camaro[350:1100,200:1400,:] # Crop out the car
plt.imshow(cropped)
plt.show()
io.imsave("camaro_cropped.jpg", cropped)
```
That gives us the following image:
<br>
![alt text](/img/posts/camaro_cropped.jpg "Camaro cropped out of the original image")
<br>
The final command in the above code snippet is used to save the image file. 

# Flipping the image
 
In this section, let us try flipping our image.  Let us first flip the image vertically:

```python
# Vertical flip
vertical_flip = camaro[::-1,:,:] # Uses the start, stop, step logic (step = -1)
plt.imshow(vertical_flip)
plt.show()

io.imsave("Camaro_vertical_flip.jpg", vertical_flip)
```
<br>
![alt text](/img/posts/Camaro_vertical_flip.jpg "Camaro image flipped vertically")
<br>

Let us now flip the image horizontally:

```python
# Horizontal flip
horizontal_flip = camaro[:,::-1,:] 
plt.imshow(horizontal_flip)
plt.show()

io.imsave("Camaro_horizontal_flip.jpg", horizontal_flip)
```
<br>
![alt text](/img/posts/Camaro_horizontal_flip.jpg "Camaro image flipped horizontally")
<br>

# Color channels
Let us start by getting out the red color channel from the image. 

```python
red = np.zeros(camaro.shape, dtype = "uint8")
red[:,:,0] = camaro[:,:,0]
plt.imshow(red)
plt.show()
```
When we run the above code, we get the following plot. 
<br>
![alt text](/img/posts/camaro_red_channel.png "Camaro Red Channel")
<br>
Let us now extract the green channel from our image. Since the green channel is given by the index 1 for the third dimension, we can obtain it using the following code. 
```python
green = np.zeros(camaro.shape, dtype = "uint8")
green[:,:,1] = camaro[:,:,1]
plt.imshow(green)
plt.show()
```
Here is the result! 
<br>
![alt text](/img/posts/camaro_green_channel.png "Camaro Green Channel")
<br>
We can do the same for the blue channel using index value 2 for the 3rd dimension. 

```python
blue = np.zeros(camaro.shape, dtype = "uint8")
blue[:,:,2] = camaro[:,:,2]
plt.imshow(blue)
plt.show()
```
We obtain the blue channel as such:

 <br>
![alt text](/img/posts/camaro_blue_channel.png "Camaro Blue Channel")
<br>

To see all the 3 channels together will be even more amazing! Let's do that using the following set of codes. 

```python
camaro_rainbow = np.vstack((red,green,blue))
plt.imshow(camaro_rainbow)
plt.show()

io.imsave("camaro_rainbow.jpg", camaro_rainbow)

```
The final statement helps us save the image in a jpg format. Here we go! 

<br>
![alt text](/img/posts/camaro_rainbow.jpg "Rainbow camaro - All three channels")
<br>


