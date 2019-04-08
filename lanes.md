---
layout: page
title: Lane Finding
permalink: /Lanes/
---
This project focused on advanced image manipulation in order to calculate the lane curvature and vehicle positioning within the lane. It required initial camera calibration, and then a series of processing steps for each frame.
<br>For real video footage captured from a vehicle's dash, I applied steps of:
1. Undistorting each image
2. Applying a binary threshold
3. Compute a perspective transform (to birds' eye view)
4. Detecting the lane lines
5. Calculating lane curvature and offset
6. Visualizing the lanes and curvature information on top of the video
