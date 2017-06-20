# Finding Lane Lines on the Road

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[weighted_image]: ./test_images_output/whiteCarLaneSwitch_output.jpg "Lines drawn over test images using improved draw\_lines() function"

[stuck]: ./left_line_stuck.png "Line stuck at the bottom of the video"

[errors]: ./errors.png "Errors calculated from the test images"

---

## Reflection

### 1. Description

The basic pipeline consisted of a conversion to grayscale, a Canny edge transform, mask on the image, hough lines and finally the weighted image which is the original image with the hough lines drawn over it. In the beginning it was possible to play a bit with the parameters to achieve good lines when testing using the images, but when going to the video, I had to modify the draw\_lines() function so it could average all the lines calculated in order to have just one line, and this line was extrapolated to the size of the mask used over the frame. This process of averaging and extrapolating was then tested on the images as shown below:

![alt text][weighted_image]

I used global variables which kept the slopes and biases of the last two lines (left and right) drawn. This way I could certify that I would only take into account lines with slopes within an error from the past line drawn to calculate the next line. Using the test images given, I was able to have an idea of where in the image the lane lines would be in the beginning and with this idea I set initial values for the global variables. The test images also helped me to define what the error was going to be. Since one of the biases had a value very close to zero and the other had a value bigger than 500, it didn't make sense to use percent values for the errors. Also, the absolute values (see on the image below) were very close and this way I was able to define one error for both sides.

![alt_text][errors]

After the average slopes and biases was calculated, this parameters were then used to extrapolate the line and find the x-axis coordinates given that the y-axis coordinates used were yt and yb, the y from the top of the masked image and the y from the bottom of the image, respectively.

That approach successfully met the projects expectations for the required videos. For the challenge video however the pipeline didn't work for reasons explained next.

### 2. Potential Shortcomings

I definetly had trouble handling the case where no lines were found for a long time. On the challenge video for example, where the light changes a lot and the road surface changes color, my pipeline broke.

Afraid of not finding lines for a given frame, I set a high error margin. This made the pipeline find some lines on the image that were nowhere close to the lane lines and get stuck there as shown below.

![alt text][stuck]

### 3. Possible Improvements

If I could do something with the average so it resists better to changes on the road the pipeline would improve a lot. Also the camera changes position on each video. On the challenge video even a part of the car appears. For that reason, setting an initial slope was definetely not a ideal solution since I don't know where the line will be. Overall, the pipeline needs to be more robust.
