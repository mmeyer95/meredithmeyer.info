---
layout: page
title: Lane Finding
permalink: /Lanes/
---

This project focused on advanced image manipulation in order to calculate the lane curvature and vehicle positioning within the lane. It required initial camera calibration, and then a series of processing steps for each frame.

Camera calibration essentially requires calculating the transformation required to undistort an image. This is easily done with a picture of a checkboard, and with helpful functions from OpenCV for python:   
<pre><code>new_image = cv2.drawChessboardCorners(calibration_image, (nx,ny), corners, ret)

ret, mtx, dist, rvecs, tvecs = cv2.calibrateCamera(objpoints, imgpoints, gray.shape[::-1],None, None)</code></pre>

The vectors found using `cv2.calibrateCamera` are subsequently used to undistort images. During camera calibration, the corners of the chessboard are found:
<center><a data-flickr-embed="true"  href="https://www.flickr.com/photos/169500224@N07/46645486945/in/dateposted-public/" title="checkerboard b4"><img src="https://live.staticflickr.com/7922/46645486945_9594ff6bc2.jpg" width="378" height="223" alt="checkerboard b4"></a><a data-flickr-embed="true"  href="https://www.flickr.com/photos/169500224@N07/33684284938/in/dateposted-public/" title="corners"><img src="https://live.staticflickr.com/7862/33684284938_a6c97706ae.jpg" width="378" height="223" alt="corners"></a></center>

<br>For real video footage captured from a vehicle's dash, I applied steps of:
1. **Undistorting each image.** <br>
    Undistorting each image uses information from the camera calibration, and is as simple as `undist = cv2.undistort(image, mtx, dist, None, mtx)` after he mtx and dist matrices are calculated initially, above.
2. **Applying a binary threshold.** <br>
    Thresholding is the most important part of this process. The output of this step must make the lane lines as clearly visible as possible. Through experimentation as well as knowledge of the technique, I decided to combine thresholding methods. After converting to gray scale, I used a Sobel function in the x direction. Sobel is a gradient, so it allows us to see where pixels next to each other are very different. Because lane lines are white or yellow lines on a dark pavement, they are identified by this gradient. I am interested in the gradient in the x direction only, because lane lines will run top to bottom. The output of Sobel threshold is:
    
    <center><img src="https://live.staticflickr.com/7840/33719747158_12dc879ecf.jpg" width="378" height="235" alt="Sobel"><br>
    The Sobel function does a good job of identifying the outline of lane lines. I was also interested in the full lanes to have more pixels and therefore more data, so I looked at HLS color space, in order:<br> 
    <center><img src="https://live.staticflickr.com/7819/47543696102_1a9f9d9208_n.jpg" width="300" height="186" alt="H_channel"><img src="https://live.staticflickr.com/7887/46872660974_c15e49b028_n.jpg" width="300" height="186" alt="L_channel"><img src="https://live.staticflickr.com/7825/47596785451_3ec64ca282_n.jpg" width="300" height="186" alt="S_channel"></center><br> As you can see, the S channel does the best job of highlighting lane lines. The pixels where both of these (Sobel x & S channel) thresholds are reached have the highest likelihood of containing the lane lines. I created a binary image by defining the lane pixels for each image as 1, and all else as 0. The binary image output looks as such:

    <center><img src="https://live.staticflickr.com/7865/46645486985_71e24c7a19.jpg" width="378" height="223" alt="binary threshold2"></center>

    You can see that some other pixels, including what looks like a neighboring car, were identified. The next step only looks at a certain location of the image, so these fale-positive will not be a problem.
3. **Computing a perspective transform (to birds' eye view).** <br>
    The goal of the perspective transform is to map straight lines to a rectangle in an image. Through trial and error on a control image, which yielded the following transformation:
    <center><img src="https://live.staticflickr.com/7892/46837284414_53f6ebd159.jpg" width="378" height="223" alt="persp xform"><img src="https://live.staticflickr.com/7833/33684284668_5c05c6d0e9.jpg" width="378" height="223" alt="persp xform2"></center>
4. **Detecting the lane lines.** <br>
    With the perspective transform of the binary threshold, it was then time to detect the position of the lane lines. I found the positions of the pixels corresponding to the lane lines, and then used a polynomial fit to define those lanes with a single line. I determined the road curvature by converting to real world units based on standard lane width in the US. I calculated the final value with:
    <center><pre><code>R_curve=((1+(2Ay+B)^2)^(3/2))/∣2A∣</code></pre></center>
    where A and B are the first and second coefficients of a quadratic polynomial.
5. **Calculating lane curvature and offset.** <br>
    Assuming the dash cam is centered to the car, the distance offset is the difference between the center of the lanes closest to the car, and the center of the image, converted to "real world" units.
6. **Visualizing the lanes and curvature information on top of the video.** <br>
     To visualize all this information, I output new frames with the lanes shown in green and the calculations overlain:
<center><img src="https://live.staticflickr.com/7818/46645486905_58ec24bc52.jpg" width="378" height="223" alt="example_image"></center>You can see there is a large radius of curvature for a road with only a small amount of curve.

View the full video here:
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/b9hYK5LCyrs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

<a href="https://github.com/mmeyer95/Advanced-Lane-Finding">GitHub Repo</a>
<br>[Back to Portfolio](https://meredithmeyer.info/)
<br>
<center>Contact me (below) for more information.</center>
