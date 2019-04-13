---
layout: page
title: Kalman Filters for Radar and Lidar
permalink: /Kalman/
---

The project involved implementation of Kalman Filter equations in C++ code. The basic Kalman filter equations used are:

<center><img src="https://live.staticflickr.com/7815/32653506937_652eecb4df.jpg"></center>

Where **x** is the state matrix, **P** is the process covariance matrix, **Q** is the measurement noise matrix, **F** is the state transiton matrix, and **H** is the measurement matrix. Kalman Filters are cyclic; A measurement step and prediction step are performed for each data point.

Since radar measurements are in polar coordinates, the state vector {X,Y,Vx,Vy} must be converted to polar coordinates in order to compare the current state to a new radar measurement:

<center><img src="https://live.staticflickr.com/7817/46680354765_b6c4b7939f.jpg"></center>

and the prediction error, **y,** must instead be calculated as:

<center><img src="https://live.staticflickr.com/7920/46680566005_3043f35646_m.jpg"></center>

Also, since radar comes in polar coordinates, it is not linear. Kalman Filters demand linearity. To account for the non-linearity, we use a Jacobian matrix for **H** in the measurement step for radar:

<center><img src="https://live.staticflickr.com/7898/47543136112_d9b9b53130_o.png" width="1079" height="379" alt="Jacobian"></center>

A simulator was used to visualize the data points and print root-mean-square error (RMSE). The simulator shows the locations of the readings from Lidar (blue), from Radar (red), and the predicted position incorporating both data types (green).

<center><img src="https://live.staticflickr.com/7896/33699311738_1b4a15439e.jpg" width="387" height="223" alt="Kalman_ZoomIn"></center>

With my implemented filter, I was able to smoothly measure and track the location of the object (approximated as green) throughout travel in a figure 8:

<center><img src="https://live.staticflickr.com/7902/47520637392_273dac5236.jpg" width="500" height="300" alt="Kalman_ZoomOut"></center>

RMSE for the first data set was as low as {0.97.0.91,0.45,0.45}.<br>
The filter also works on another data set, which begins travel in the opposite direction and initializes with radar data, rather than lidar data, with improved RMSEs of {0.078,0.087,0.44, 0.43}. See the filter in action:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/893XY_uEn8k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub Repo](https://github.com/mmeyer95/KalmanFilters)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
