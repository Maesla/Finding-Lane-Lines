#**Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

The Self-Driving Car Nanodegree Lesson2 project is submitted.
In order to keep the original files, a few copies have been made.

#Code
The code can be found in  [mywork.ipynb](mywork.ipynb). It has been tested with jupyter and it runs completely.

There are three main blocks:

1. My methods or helpers methods. They are not main methods but helpers methods, Like **PlotImage**. In this block has been developed **draw\_lines\_extrapolate**. This method is used to find one line that groups all the lines returned by Hough algorithm.
2. # Pipeline. In this block is developped the entire pipeline for finding lane lines.
3. Pipeline example. This block is for plotting, testing and saving the pipeline

#Report
The full report can be found in [writeup_report.md](writeup_report.md)

#Result
The result images can be found in the [result_images](result_images) folder.

The result videos can be found in white.mp4, yellow.mp4 and extra.mp4

 <video width="320" height="240" controls>
  <source src="white.mp4" type="video/mp4">
</video> 
 <video width="320" height="240" controls>
  <source src="yellow.mp4" type="video/mp4">
</video> 
 <video width="320" height="240" controls>
  <source src="extra.mp4" type="video/mp4">
</video> 

