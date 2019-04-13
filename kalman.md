---
layout: page
title: Kalman Filters for Radar and Lidar
permalink: /Kalman/
---

The project involved implementation of Kalman Filter equations in C++ code. The basic Kalman filter equations used are:

<center><img src="https://live.staticflickr.com/7815/32653506937_652eecb4df.jpg"></center>

Where **x** is the state matrix, **P** is the process covariance matrix, **Q** is the measurement noise matrix, **F** is the state transiton matrix, and **H** is the measurement matrix. Kalman Filters are cyclic; A measurement step and prediction step are performed for each data point.

Since radar measurements are in polar coordinates, the state vector must be converted to polar coordinates in order to compare the current state to a new radar measurement:

<center><img src=""https://live.staticflickr.com/7817/46680354765_b6c4b7939f.jpg"></center>

and the prediction error, **y,** must instead be calculated as:

<center><img src=""></center>

Also, since radar comes in polar coordinates, it is not linear. Kalman Filters demand linearity. To account for the non-linearity, we use a Jacobian matrix for **H** in the measurement step for radar.

A simulator was used to visualize the data points and print root-mean-square error (RMSE). The simulator shows the locations of the readings from Lidar (blue), from Radar (red), and the predicted position incorporating both data types (green).

<center><a data-flickr-embed="true"  href="https://www.flickr.com/photos/169500224@N07/33699311738" title="Kalman_ZoomIn"><img src="https://live.staticflickr.com/7896/33699311738_1b4a15439e.jpg" width="387" height="223" alt="Kalman_ZoomIn"></a></center>

With my implemented filter, I was able to smoothly measure and track the location of the object (approximated as green) throughout travel in a figure 8:

<center><a data-flickr-embed="true"  href="https://www.flickr.com/photos/169500224@N07/47520637392/in/photostream/" title="Kalman_ZoomOut"><img src="https://live.staticflickr.com/7902/47520637392_273dac5236.jpg" width="500" height="300" alt="Kalman_ZoomOut"></a></center>

The filter also works on another data set, which begins travel in the opposite direction and initializes with radar data, rather than lidar data:

<center><img src=""></center>

[GitHub Repo]()
<br> Contact me (below) for more information.


