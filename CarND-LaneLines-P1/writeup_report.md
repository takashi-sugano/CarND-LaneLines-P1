# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/whiteCarLaneSwitch.jpg "Detected Lanes"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used the gaussian smoothing/blurring filter to smooth the grayscale images. Next, I detected edges in the images using Canny algorithm, then I masked the edge degected images with a four sided trapezoid polygon. Finally I run hough transfer algorithm and detect lane makers.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculate slopes and intercepts of lanes using weighted average of segment lines. The weight are normalized with length of segment lines. I consider that a more long segment line is more precise line.

I also modified draw function. I wanted to check the segment lines. So, the lines are drawed as green lines and detected lane markers are draws red lines. The example is shown as follows.

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the vehicle is going on a following conditions.

(1) hill. I think the mask might not match the lane shape since the mask parameter is constant.
(2) tight curve. Average of segment line parameter become incorrect because of changing direction even if on a same lane.
(3) brightness road. The edge of lanes could not be detected with constant canny parameters.


### 3. Suggest possible improvements to your pipeline

(1) A possible improvement would be to detect the horizon and decide the mask vertices using the horizon line.
Another potential improvement could be to check the distance of the top of 2 lane markers. And top vertices postion of the mask modified to up position when the distance is too short.

(2) A possible improvement would be to use quadratic function or cubic function on hough line and/or draw_line().

(3) A possible improvement would be to change the brightness and luminance the image. These parameter should be changed using the average of the image before converting to grayscale.