# **Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve"

---
### Reflection

### 1. My Pipeline and modification of the draw_lines() function.

My pipeline consisted of 6 steps.
  1. I converted the images to grayscale
  2. I ran the gaussian blur function.
  3. I ran the canny function on the images.
  4. I found the region of interest using estimated vertices.
  5. I ran the hough lines function
    - This created lines on a blank image.
    - This called the draw lines function
  6. I ran the weighed function
    - This mapped the lines onto the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
- Calculating the slope. If the slope is positive, and is on the right side of the image, the line belongs on the right. however, if the slope is negative, and on the left side of the image, it belongs on the left.
- Finding the average slope of left lines, and right lines. I also calculated the average x point and average right point, since the average of these two points would be an intercept of the average line.
- Finding the intercept of the bottom most point in the image(for both left and right side lanes), and the intercept of the top most point where the street lines can be read.


Here is an example of my calculated image lines: you can find all of them in the **test_images_output** folder.

![alt text][image1]

### 2. Pipeline issues and improvements

I noticed that my pipeline solution flickers quite a bit compared to the example provided.
I believe this is due to issues with finding average (which can cause divide by zero exceptions), which in turn skip a few frames of the video. I also ran into this issue when lines had close to no slope. Perhaps this can be improved by comparing the previous frame's lanes and finding an average between the new frame, in order to smoothen out the sudden change.
