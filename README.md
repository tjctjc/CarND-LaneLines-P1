# **Finding Lane Lines on the Road** 

<img src="images/screenshot.png" width="640" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

### To Run the project
Step 1. Clone this project
  git clone https://github.com/tjctjc/CarND-LaneLines-P1

Step 2. Run Jupyter Notebook

Step 3. Click on P1.ipynb to launch the project code

### Reflection
### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
- Convert RGB image to Gray scale image
- Blur the image to remove some of the noise before further processing the image
- Apply Canny Edge filter on the image to get edges
- Because the way the camera is mounted in the car, we can assume the region of our interests.  Thus, we can only use the region of interests for further processing
- I use Hough Transform algorithm to find line segments in the region.
- Then I average the lines to get slopes and extrapolate to get traight lines for each lane.
  I split the lane lines into left and right by their slopes, respectively. If the slope is negative I assigned it to the right line and if the slope is positive I assigned it to the left line. I added a moving average over the slopes in order to include only the points that fell within certain level. Also, if two lines overlapping, I recalculate the slope and points to draw short lines.

### 2. Identify potential shortcomings with your current pipeline
- If there's obsticles just in front of camera, the pipeline might detect those as lanes
- In conditions such as night time, snowy and etc, the pipeline might not be able to detect lanes


### 3. Suggest possible improvements to your pipeline
- Based on some parameters which could be changing based on scene conditions(such as darkness/brightness/whether/etc), using those parameters we could develop an algorithm to change parameters for Hough Transform/Canny/etc algorithm so that it can dynamically be changing basedon road/scene condition.


