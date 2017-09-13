# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[whiteCarLaneSwitch]: ./test_images_output/whiteCarLaneSwitch.jpg "Hough transform"
[HoughsolidWhiteRight]: ./test_images_output/HoughsolidWhiteRight.jpg "Final lane"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I blurred them to smooth the image, after that I applied
Canny edge detection and filtered the result with a region of interest. Lastly I used the Hough probabilistic transform to get the lines
representing each lane line and painted them to the input image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function
to separate lines by slope (<0 for left side, >0 for right side). Then I filter lines for each half of the region of interest if they don't
have a similar slope as they're supposed to (lines on the left should all have slope<0). I also tried calculating the median slope for each side
and use it as a threshold for slopes within a certaing range of the median, although the method was theoretically sound
it was unable to remove outliers when applied.
Once I have filtered the lines, I fitted a new line for each side using all the points of the lines retained and calculate the two points defining
the new lines.

![alt text][whiteCarLaneSwitch]
![alt text][HoughsolidWhiteRight]


### 2. Identify potential shortcomings with your current pipeline


Several potential shortcomings would be what would happen when the car goes up or downhill or if there are too many cars/obstacles or poor lighting conditions
to see the lane painting.

Another shortcoming would be if the camera's position changes and it's not calibrated again.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a more robust approach to remove artifacts that do not belong to actual lane lines.
Implementing a dynamic region of interest in case the camera accidentally moves. Better image preprocessing whit poor lightning conditions (use HSV color space).

Another possible improvement would be to implement second/thrid degree polynomials with polyfit to adjust better when driving on roads with curves.