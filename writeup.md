# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of these steps:
* Gaussian blur
* Canny edge detection
* Masking to a trapezoid-shaped region
* Finding lines with Hough transform
* Drawing the lines

Initially I also grayscaled the image as a first step. I opted not to do that after working on the challenge as it reduced contrast of the lines against light concrete.

The draw_lines function divides lines into left and right, calculates their slope, filters outlier lines, and averages the slope to calculate a line. It initially removes lines that have a slope under a certain threshold, as in noisy sections (shadow, transition from black to light road) these lines are over-represented.

During work on the challenge, I was unable to tune the Canny edge detection to find the lane lines during the light concrete bridge section. After reading in #p-lane-lines I took Alex Popovici's suggestion to use a window to guess the lines during these gaps.

### 2. Identify potential shortcomings with your current pipeline

This solution and its various settings are specific to the videos included. 

It doesn't work well in low contrast situations. Driving over a section of road with low contrast lane lines and shadows, especially for a prolonged period, would mean the pipeline couldn't find or guess where the lines were. 

Other objects in the current lane would also break the pipeline. Cracks in the road, especially in the center of the lane, might throw off the line detection. Another vehicle in the same lane might also throw off the lane detection.

### 3. Suggest possible improvements to your pipeline

The challenge video showed other improvements. The camera was slightly off center, so the original region of interest was offset. In a more robust version of this pipeline, that would be more configurable. Similarly, the hood area of the car should be removed from that region.

The windowing led to some other odd side effects. Given more time, I would have worked to make more modular data structures for use in draw_lines/windowing and a less hacky approach there.

