# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report



[image1]: ./test_images_output/solidYellowCurve2.jpg "result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used Canny edge detection with two thresholds after I applied gaussian blur to the images. I got images with edges detected all over the places. Because camera has a fixed mount on the car and the car usually stays in lane, the positions of lanes we want to detect usually fall into a fixed region in the images. Therefore, a masked wedge-shape region is used to filter out the edges in the region of the current driving lane. After that, I applied hough transformation to fit straight lines that represent the lane markings of the current lane. These lines are later drawn in the original images to visualize the lane finding results.

Here is the example lane finding result:
![alt text][image1]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by using the slope of the straight lines to seperate out left lane and right lane. For the lines that are part of left lane, I find the bottom left and top right points in the image plane. For the lines that are part of right lane, I find the bottom right and top left points in the image plane. Those points are used to represent left lane and right lane respectively.



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the car is driving one curved road, my method can only fit straight lanes to the detected edges. 

Another shortcoming could be the lighting condiction varies when the car drives, it's hard to reliably detect the lane edges with fixed threshold.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a quadratic function to fit the detected edge so that the lane markings don't have to be straight. 

Another potential improvement could be to use some statistics of the image, for example brightness, to inform the the thresholds on Canny edge detection.
