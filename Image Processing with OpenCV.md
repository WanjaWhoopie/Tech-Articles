# Introduction

The history of image processing dates back to the 1960s with people doing research at Bell Technologies, Jet Propulsion Laboratory, Massachusetts Institute of Technology, University of Maryland, and a few other research facilities. In 1966 English molecular biologist Aaron Klug at the University of Cambridge formulated a method for digital image processing of two-dimensional images. In this article we will learn the basics of image processing with OpenCV. We shall assume that you know the basics of Python and have already installed it on your computer. 

To install OpenCV write the following command:


```python
In windows:
pip install opencv-python

In linux:
sudo apt-get install libopencv-dev python-opencv

In mac:
brew install opencv3 --with-contrib --with-python3
```

After the installation is done we need to import the CV2 module in our project as shown. If you get no errors then you are good to go.



```python
import cv2
```

# Read the Image

We will use the imread() method to read the image. The syntax is: *cv2.imread(path, flag).* There are three types of flags. The first is cv2.IMREAD_COLOR which species that the image should be read in color and any transparency is neglected. Instead of writing the whole word you can just use the number 1. The second is cv2.IMREAD_GRAYSCALE which can be replaced by 0 and specifies that the image loaded should be in gray scale. The third one is cv2.IMREAD_UNCHANGED whose alternative is -1. It specifies to load an image as it is including its alpha channel. An alpha channel is essentially the component in color that defines opacity by determining how a pixel is rendered when blended with another. If you do not set up a flag the default is 1.  

Store the image read in a variable to be able to access it easily. The variable is now a matrix. You can view it by printing the variable. If the image is not found or the format is invalid it will return an empty matrix. 


```python
img = cv2.imread("image 1.jpg")
print (img)
```

    [[[251 250 246]
      [251 250 246]
      [251 250 246]
      ...
     [[ 21  19  18]
      [ 23  21  20]
      [ 20  19  15]
      ...
      [ 38  30  23]
      [ 38  30  23]
      [ 38  30  23]]]


To view the image we will use imshow(). On the waitkey  method you enter the waiting time in milliseconds. This is the time you need the image to show before it disappears. If you use 0, you will need to cancel the image display manually.


```python
cv2.imshow('My Image', img) 

cv2.waitKey(0)
```

# Crop Image

We will now learn how to crop an image. First we find the dimensions of the image. This helps know the height and width of the image so that we fit the dimensions of the new image within a useful range. You will see that with the use of a variable we do not need to keep reading the image again to perform a new action.


```python
print(img.shape)
```

    (3963, 5000, 3)


The three digits represent the height, width and channels respectively. Do note that, if the image was in grayscale, the tuple returned would contain only the number of rows and columns. The cropping is performed in the form of slicing. The cropping starts from a position x,y to another position h,w. This is the syntax: *croppedImage = img[startRow:endRow, startCol:endCol]*


```python
y=1000
x=1000
h=2000
w=2000

img_cropped = img[x:w, y:h]

cv2.imshow('Cropped Image', img_cropped) 

cv2.waitKey(0)
```

# Resize Image

We shall use the function cv2.resize() in this next task. In the example we are going to give we will not pay attention to aspect ratio but just randomly change the height and width. It is possible to change height only or width only.

The syntax is as follows: *cv2.resize(src, d[, dst[, fx[, fy[, interpolation]]]])*. The first two arguments are required. This is what the different parameters represent:
'src' shows the path to the image
'd' stands for the desired size or dimensions
'fx' shows scale factor on the horizontal axis
'fy' shows scale factor on the y axis
'interpolation' is used for image decimation 

(Could be INTER_NEAREST – a nearest-neighbor interpolation, INTER_LINEAR – a bilinear interpolation (used by default), INTER_AREA – resampling using pixel area relation, INTER_CUBIC – a bicubic interpolation over 4×4 pixel neighborhood, INTER_LANCZOS4 – a Lanczos interpolation over 8×8 pixel neighborhood.)


```python
width = 3000
height = 2000
d = (width, height)

img_resized = cv2.resize(img, d, interpolation = cv2.INTER_AREA)

cv2.imshow('Resized Image', img_resized) 

cv2.waitKey(0)
```

# Make Image Blurry

 Contrary to popular opinion, noise isn't always so bad. A lot of photographers documenting something like war use noise to add some bit of character. Noises makes an image look blurry.

There are many ways of blurring an image. The default one is called averaging and the method used takes in the image source and kernel size as parameters. There are other types of blurring like gaussian blurring, bilateral filtering, and median blurring which we won't dive into at the moment. 


```python
img_averaging = cv2.blur(img,(100,100))

cv2.imshow('Resized Image', img_averaging) 

cv2.waitKey(0)
```

# Reduce Noise from Image

Sometimes you may have an image that is grainy and not so clear. We can use openCV to help reduce noise on the image.  You have to note though that too much noise reduction will end up with a plastic like image that is far worse than an image that is a little grainy. Let us see how to remove noise for when the need arises.

In applications like image segmentation, image classification, image registration and many others, denoising plays a big role. It helps remove unwanted and unavoidable noise. The main types of noise are salt and pepper and gaussian. We will perform an implementation of Non-local Means Denoising algorithm. 

In OpenCV there are four variations of this technique:
1. cv.fastNlMeansDenoising() - works with a single grayscale images
2. cv.fastNlMeansDenoisingColored() - works with a color image.
3. cv.fastNlMeansDenoisingMulti() - works with image sequence captured in short period of time (grayscale images)
4. cv.fastNlMeansDenoisingColoredMulti() - same as above, but for color images.

This is how the method is defined:
 *cv2.fastNlMeansDenoisingColored(src[, dst[, h[, hColor[, templateWindowSize[, searchWindowSize]]]]])*

We shall explain the parameters. 
'src' -image we seek to denoise
'dst' -defines output image with the same size and type as what we have in src
'h' -determines filter strength. The higher it is the more noise can be removed but on the downside the more detail that can be removed from the image
'hColor' -same as h but for color components only
'templateWindowSize' -size of template patch used to compute weights that is written in odd numbers
'searchWindowSize' -also an odd number, used to compute average of given pixel



```python
img2 = cv2.imread("image 2.jpg")
dst = cv2.fastNlMeansDenoisingColored(img2,None,10,10,7,21)

cv2.imshow('Denoised Image', img2) 

cv2.waitKey(0)
```

# Conclusion

We now have a few tricks up our sleeves when it comes to OpenCV and image manipulation. I hope this tutorial has given you a good basic foundation and tickled your curiosity enough that you are going to check out more advanced things you can do with OpenCV. Practice more to understand the why of anything you input. Happy coding.
