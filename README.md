#**Finding Lane Lines on the Road** 

##Project Overview

###This project is focused on finding lanes within both images and videos using OpenCV. The approach is based on Canny function and Hough Transform find the edges related to the lanes and connect them to form the lanes.

---

[image1]: ./examples/grayscale.jpg "Grayscale"

[image2]: ./test_images/solidWhiteRight_WithLines.jpg "Lane_Detection"

![alt text][image1] ![alt text][image2]

---

### Reflection

##Pipeline:

###1. The pipeline consists of the following path:

1) Convert image to gray scale
2) Apply Gaussian smoothing method to smooth out the image and remove noises.
3) Use Canny to identify the edges in the image
4) Use fillPoly to choose the region of interest in the image. This allows the program to focus on where we are looking for the lanes.
5) Use Hough Transform to find lines and connect the identified edges in the image.
6) Use the update draw lines function to show the identified lanes in the oroginal image. Note that the draw_lines function is updated (called "draw_lines_update") to extend the line to the top and bottom of the region of interest. For this purpose, the average slop is calculated based on the slopes of lines in left and right hand sides. One point is selected from each side and the line equation has been calculated using the average slope and the selected point (y - y0 = m(x - x0), where (x0,y0) are the coordinates of the selected point and m is the average slope). The intersection of the line with the bounderis of the region of interest is identified and two lines are plotted in red color to show the lanes.

###2. Identify potential shortcomings with your current pipeline

The key shortcoming of this approach is its sensitivity to the model parameters (both Canny and Hough Transform). 

Another shortcoming of this approach is predefined bounderies of the region of interest. This is particularly important in dealing with sharp curves.

I tested few of my dashcam videos, and this approach (when designed for homogenous light conditions) is incapable of dealing with inhomogenous light (e.g., existing of shadows)


###3. Suggest possible improvements to your pipeline

An optimization based system can be used to find the optimized paramters based on comparing the selected lines with the actual lanes. This cound be a challenging task, but can create more accurate outcome.

Adding more edges to the region of interest can solve the curve issue and defining a piecewise linear function instead of a single line can help moving around the curvature.

The image can be divided into different lighting conditinos and each section analyzed seperately.

