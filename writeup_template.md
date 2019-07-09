# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### Pipeline:

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I passed the images to Gaussian filter in order to remove unwanted noise. The Gaussian blurred images were then passed to Canny edge detector to detect edges based on specified lower and upper threshold. Then a specific region of interest was selected such that only lane edges are detected in the images and nothing else. After that  Hough transform was applied to obtain the x and y points in order to draw the lane lines.

### draw_lines() function:

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the slope and intercepts from the points obtained from Hough Transform. The line points were separated into left and right line points based on the slope i.e. if the slope > 0.0 then consider the points to be of left line and otherwise. This way all the left (x,y) points, left slope values, right (x,y) points and right slope values were stored in a separate lists. Then the mean for each list was taken and those respective mean values were then used to calculate the left and right intercepts for left and right lines repectively using (b = y - mx) formula. Now I had mean slope value and mean intercept value for both left and right lines. So, in order to use slope intercept form y values were set i.e. y_max was set to y axis of the image and y_min was set to somewhere near the middle position of the image (0.6 times y axis). Based on those y values and using slope intercept equation left and right x values were calculated. And the respective x and y values for left and right lines were given to cv2.line() to draw the lines. 



### 2. Potential Shortcomings with the current pipeline


One potential shortcoming would be what would happen when the lanes instead being straight are curved. Then it would be difficult for this algorithm to detect curved lines and may detect random straight lines within region of interest. 

Another shortcoming could be the illumination. What if this algorithm is tested on different illumination then it may detect some unwanted lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to incorporate algorithms that can detect any sort of lines.

Another potential improvement could be to test and improve algorithm based on illumination.
