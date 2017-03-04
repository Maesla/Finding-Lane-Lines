#**Finding Lane Lines on the Road** 



[//]: # (Image References)

[pipeline1]: ./result_images/Original.jpg "Original"
[pipeline2]: ./result_images/Grayscale.jpg "Grayscale"
[pipeline3]: ./result_images/Gaussian_Blur.jpg "Gaussian Blur"
[pipeline4]: ./result_images/Canny.jpg "Canny"
[pipeline5]: ./result_images/Region_of_interest.jpg "Region"
[pipeline6]: ./result_images/Hough.jpg "Hough"
[pipeline7]: ./result_images/Hough_Extrapolating.jpg "Extrapolating"
[pipeline8]: ./result_images/Result.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 7 steps:

1. I convert the images to grayscale.
2. I apply a Gaussian blur
3. Then, I apply Canny
4. After applying Canny, I crop the image. I get a triangle. The lower corners are the image bottom corners. The upper corner is positioned approximately at 0.5 width and 0.6 height, with 0,0 in the upper corner.
5. I apply a Hough algorithm to the cropped image. 
    - This is a modification of Hough. The first part is a common Hough. The second part is a modification of draw_lines. I will explain at the end, in **Drawing a single line** section.
6. I apply the same cropping to the result, because the calculated lines are drawn in all the image.
7. Finally, in the last step, I blend the result with the original

####Example pipeline
![alt text][pipeline1]

![alt text][pipeline2]

![alt text][pipeline3]

![alt text][pipeline4]

![alt text][pipeline5]

![alt text][pipeline6]

![alt text][pipeline7]

![alt text][pipeline8]


#### Drawing a single line
In order to draw a single line, I use these steps:

1. I get the lines from Hough
2. I calculate the slope, with the formula slope = (y2-y1)/(x2-x1)
3. If the slope is greater than 0, is a left line. Otherwise, is a right one.
4. With the slope, and the one of the two points, I calculate the b, in the equation y = m*x + b
5. So, I have m and b. The idea is to calculate the average of all the lines.
6. When I have calculated the average m and b, I draw the line. 
7. For drawing the line, I need to calculate two points, so I calculate y1 for x1 = 0 and y2 for x2 = width.
8. With the new P1 and P2, I draw the line with cv2.line
9. To avoid the problem of having left and right variables in the function, I call the method twice with a sign argument. In this way, I can use the same method twice, one for the right lines and one for the left lines.


###2. Identify potential shortcomings with your current pipeline

I highlight three main shortcomings:

1. Intermittent lines. I have noticed that there are a few frames without lines detected.
2. Infinite slopes. Sometimes, the slope is NaN because **equals(x2, x1) == true**
3. Curved lanes. In curved lanes, like the challenge one, is algorithm does not work very well.


###3. Suggest possible improvements to your pipeline

1. Using the Hough space for the single line algorithm. Using Cartesian coordinates bring known problems, like the problem pointed before in 2.2
2. Using the arithmetic mean does not seem to be the better way to get the slope of a set of lines. Arithmetic mean is very sensible to extreme values.
3. I think a better way to get the main line should be based in the Hough algorithm. Passing the line to polar coordinates, then to hough space, and then, finding the lines in a cell with similar ρ and θ, and using this as the main line, not with an arithmetic mean.
4. I use twice the **finding a single line algorithm**. One for the left one and other for the right one. I think this is cleaner with the actual implementation, but slower. Probably a better way should be find the both lines in one pass. Even better, using the paradigm described in the previous point is even better, because left and right lines should group together and with one pass we could have them both.
