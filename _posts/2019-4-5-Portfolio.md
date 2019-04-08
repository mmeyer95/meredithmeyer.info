---
layout: page
title: Portfolio
permalink: /
---
***
Below is a high-level overview of many of the projects I have worked on recently. For more information, visit my GitHub profile, or contact me directly (see footer).

## Lane Finding
#### Skills: Computer Vision, OpenCV, Python, Camera Calibration, Video Processing, Jupyter Notebooks

Using Canny edge detection for a grayscale image, followed by a Hough Line Transform, I was able to identify lane lines on images captured from a vehicle dash.

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/b9hYK5LCyrs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

This project focused on more advanced image manipulation in order to calculate the lane curvature and vehicle positioning within the lane. For real video footage captured from a vehicle's dash, I applied steps of:
1. Undistorting each image
2. Applying a binary threshold
3. Compute a perspective transform (to birds' eye view)
4. Detecting the lane lines
5. Calculating lane curvature and offset
6. Visualizing the lanes and curvature information on top of the video

## Street Sign Classification
#### Skills: Computer Vision, Neural Networks, CNNs, Deep Learning, Python, Jupyter Notebooks 

## Autonomous Driving
#### Skills: Collecting training data, Deep Learning, CNNs, C++

## Kalman Filters
#### Skills: Kalman Filters, Sensor Fusion, C++

## Voila: Fitness Data Hub
#### Skills: Java, Sensors, Arduino, Laser Cutting, CAD

The motivation for this project path came from a shared group interest in personal health and happiness. As busy individuals with many smartphone apps and notifications, we all envisioned a way to make health tracking both simpler and more insightful.

Our dream for this project was to make the technology seem as amiable as possible. One of the ways we sought to do this is by using smooth edges- circles rather than rectangles- in the overall design. We were limited in budget and supplies, so we adapted a rectangular screen to become multiple circular screens.

The final device was created through myriad cycles of 3D printing pieces. The hardware includes a Pico Pro microcontroller and screen, accelerometer, LED strip, motion sensor, and Bluetooth Low Energy (BLE) connection. Refer to the video below to see how this technology works, and what it's all about.

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/73sUKSZ9bQc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## WorkOutimal: Smart Exercise Bike
#### Skills: Automation, Arduino, Hardware, Sensing, Project Management

A play on the words "workout" and "optimal", WorkOutimal was my Capstone project in the M.Eng. program at UC Berkeley. The goal of the project was to create a cardio machine, in our case a bicycle, that is able to guide the user through an efficient workout. Efficient, for our purposes, means maximum calorie expenditure for a given time. This is possible because power output, which is the product of force and velocity, is a nonlinear function for a human.

For the project, our team decided to change a previously-existing stationary exercise bike. The bike, pictured stripped-down, is a basic Loctek desk bike which uses a magnet and flywheel to manipulate the resistance to pedaling.

As part of the hardware duo, my responsibility is to actually create a working product. We are using a 12 volt linear actuator to manipulate the position of the magnet, and thus the resistance on the bike. I will be using an arduino to gauge the speed of pedalling and also to control the linear actuator. So, the first round of the product will be an add-on item to a stationary bicycle.

The assembly is shown (left). In order to measure the pedal velocity, I created a low-fidelity encoder using a single LED and photoresistor. The gaps in the wheel change the reading on the photoresistor, which I then used to calculate the rotations of the flywheel, and then the rotations of the pedals. Both the velocity measurement system and linear actuator are controlled using an Arduino Uno.

View a teaser for this project:
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/F1LDj81z75A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

## Text Entry
#### Skills: Java, Android Studio, Laser Cutting, Soldering

As an introduction to Android, I created a low fidelity prototype of a text entry device, including software.
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/T63Gp9oZcBs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>
