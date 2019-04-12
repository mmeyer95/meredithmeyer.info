---
layout: page
title: Lane Finding
permalink: /Lanes/
---
This project focused on advanced image manipulation in order to calculate the lane curvature and vehicle positioning within the lane. It required initial camera calibration, and then a series of processing steps for each frame.

Camera calibration essentially requires calculating the transformation required to undistort an image. This is easily done with a picture of a checkboard, and with helpful functions from OpenCV for python:
```new_image = cv2.drawChessboardCorners(calibration_image, (nx,ny), corners, ret)

ret, mtx, dist, rvecs, tvecs = cv2.calibrateCamera(objpoints, imgpoints, gray.shape[::-1],None, None)
```

The vectors found using `cv2.calibrateCamera` are subsequently used to undistort images. During camera calibration, the corners of the chessboard are found:
<center><a data-flickr-embed="true"  href="https://www.flickr.com/photos/169500224@N07/46645486945/in/dateposted-public/" title="checkerboard b4"><img src="https://live.staticflickr.com/7922/46645486945_9594ff6bc2.jpg" width="378" height="223" alt="checkerboard b4"></a><a data-flickr-embed="true"  href="https://www.flickr.com/photos/169500224@N07/33684284938/in/dateposted-public/" title="corners"><img src="https://live.staticflickr.com/7862/33684284938_a6c97706ae.jpg" width="378" height="223" alt="corners"></a></center>

<br>For real video footage captured from a vehicle's dash, I applied steps of:
1. Undistorting each image
2. Applying a binary threshold
3. Compute a perspective transform (to birds' eye view)
4. Detecting the lane lines
5. Calculating lane curvature and offset
6. Visualizing the lanes and curvature information on top of the video
<p>

1. Undistorting each image uses information from the camera calibration, and is as simple as `undist = cv2.undistort(image, mtx, dist, None, mtx)`
2. Thresholding is the most important part of this process. The output of this step must make the lane lines as clearly visible as possible. Through experimentation as well as knowledge of the technique, I decided to use a Sobel gradient threshold in the x direction, in combination with a threshold of the S channel in HLS color space. The pixels where both of these thresholds are reached have the highest likelihood of containing the lane lines. The binary image output looks as such:

<center><img src="https://live.staticflickr.com/7865/46645486985_71e24c7a19.jpg" width="378" height="223" alt="binary threshold2"></center>

You can see that some other pixels, including what looks like a neighboring car, were identified. The next step only looks at a certain location of the image, so these fale-positive will not be a problem.
3. The goal of the perspective transform is to map straight lines to a rectangle in an image. Through trial and error on a control image, which yielded the following transformation:
<center><img src="https://live.staticflickr.com/7892/46837284414_53f6ebd159.jpg" width="378" height="223" alt="persp xform"><img src="https://live.staticflickr.com/7833/33684284668_5c05c6d0e9.jpg" width="378" height="223" alt="persp xform2"></center>
4. With the perspective transform of the binary threshold, it was then time to detect the position of the lane lines.
5. Assuming the dash cam is centered to the car, the distance offset is the difference between the center of the lanes closest to the car, and the center of the image, converted to "real world" units.
6. To visualize all this information, I output new frames with the lanes shown in green and the calculations overlain:
<center><img src="https://live.staticflickr.com/7818/46645486905_58ec24bc52.jpg" width="378" height="223" alt="example_image"></center>
You can see there is a large radius of curvature for a road with only a small amount of curve.

View the full video here:
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/b9hYK5LCyrs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub](https://github.com/mmeyer95/Advanced-Lane-Finding) <br>
Contact me (below) for more information.

