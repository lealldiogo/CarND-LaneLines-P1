#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[testimage]: ./test_images/solidWhiteCurve.jpg "testing"

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]
![alt text][testimage]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...


# Finding Lane Lines on the Road

## 1. Description

The basic pipeline was run on an image and consisted of a conversion to grayscale, a Canny edge transform, mask on the image, hough lines and finally the weighted image which is the original image with the hough lines drawn over it. In the beginning it was possible to play a bit with the parameters to achieve good lines, but when going to the video, I had to modify the draw\_lines() function so it could average all the lines calculated so I would have just one, and this line was extrapolated to cut all the mask I used. I used a global variable which kept the last average. This way I could certify that I used only lines within a margin of error of x% from the last average were taken into account to calculate the next line. This line was then extrapolated using its slope and bias, and the yt yb which are the y from the top of the image and the y form the bottom of the image respectively.

## 2. Potential Shortcomings

I definetly had trouble handling the case where no lines were found for a long time. On the challenge video for example, where the light changes a lot and the road changes color(?), my pipeline broke. So my pipeline was not robust enough.

## 3. Possible Improvements

If I could do something with the average so it resists better changes in the road, I mean make it more robust, that would be better. Set an initial slope I also think is not the ideal solution.