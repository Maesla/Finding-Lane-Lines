#**Finding Lane Lines on the Road** 


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
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

My pipeline consists of 7 steps. 
1. I convert the images to grayscale.
2. I apply a gaussian blur
3. Then, I apply Canny
4. After applying Canny, I crop the image. I get a triangle. The lower corners are the image bottom corners. The upper corner is positioned approximaly at 0.5 width and 0.6 heght, with 0,0 in the upper corner.
5. I apply a hough algorith to the crop image. This is a version of Hough. The first part is a common Hough. The second part is a modification of draw_lines. I will explain at the end.
6. I apply the same crop to the result, because the calculated lines are drawn in all the image.
7. Finally, in the last step, I blend the result with the original

![alt text][pipeline1]
![alt text][pipeline2]
![alt text][pipeline3]
![alt text][pipeline4]
![alt text][pipeline5]
![alt text][pipeline6]
![alt text][pipeline7]
![alt text][pipeline8]



In order to draw a single line, I use these steps:
1. I get the lines from Hough
2. I calculate the slope, with the formula slope = (y2-y1)/(x2-x1)
3. If the slope is greater than 0, is a left line. Otherwise, is a right one.
4. With the slope, and the one of the two points, I calculate the b, in the ecuation y = m*x + b
5. So, I have m and b. The idea is to calculate the average of all the lines.
6. When I have calculated the average m and b, I draw the line. 
7. For drawing the line, I need to calculate to points, so I calcuate y1 for x1 = 0 and y2 for x2 = width.
8. With the new P1 and P2, I draw the line with cv2.line
9. To avoid the problem of having left and right, I call the method twice with a sign argument. In this way, I can use the same method twice, one for the right lines and one for the left lines
My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
