---
layout: page
title: Step Counting and Orientation Determination of a Wrist-Worn Device
permalink: /Steps/
---

The goal of this project was to imitate basic functionality found in smartwatches. The 2 main objectives were to:
* Accurately count number of steps
* Determine when the device is raised for the purpose of displaying information

For this exercise, I chose to use an [Adafruit MMA8451 accelerometer breakout board](https://learn.adafruit.com/adafruit-mma8451-accelerometer-breakout):

<center><img src="https://live.staticflickr.com/65535/49156247981_da3a5fcdda_n.jpg" width="320" height="179" alt="MMA8451"></center>

It is a 3-Axis, 14-bit accelerometer safe to use with either 3V or 5V logic. I used an Arduino UNO development board. In order to create a wristwatch-like setup, I affixed the sensor to a bracelet at the same position as a watch face.

<center><img src="https://live.staticflickr.com/65535/49155796588_d3bb36bf6f_n.jpg" width="162" height="320" alt="IMG-7214"><img src="https://live.staticflickr.com/65535/49156504252_5b7f5a7e4d_n.jpg" width="161" height="320" alt="IMG-7215"></center>

### Step Counting in Normal Conditions
I recorded sequences of walking for 10-15 seconds. The raw acceleromater data, as well as the vector sum acceleration, over time are shown below.

<center><img src="https://live.staticflickr.com/65535/49156247971_90caf8056f_n.jpg" width="320" height="228" alt="Raw_Accelerometer_Data"></center>

Accelerometer data is inherently noisy, and in order to count steps, I need to ignore the noise. My walking sessions were at a normal, relaxed pace. According to the [New York Times](https://www.nytimes.com/2018/06/27/well/walk-health-exercise-steps.html), a brisk walk is 100 steps per minute: 100/60 ~= 1.66 Hz. Since walking, running etc. are quite low in frequency compared to noise and other signals, I chose to use a low-pass filter. I chose a cutoff frequency of 2.00 Hz to account for faster-than-brisk walking speeds. Since the wrist could theoretically be in any position while walking, I chose to use the vector sum of acceleration as my raw signal. Applying the filter yields:

<center><img src="https://live.staticflickr.com/65535/49156597582_137c97c1d9_n.jpg" width="320" height="230" alt="LowPass_VectorSum2"></center>

As you can see, this creates a smooth curve, which looks like an ideally imagined signal from walking. Now I determined the count step by identifying and counting the peaks in the filtered signal:

<center><img src="https://live.staticflickr.com/65535/49156468782_50feedb19f_n.jpg" width="320" height="230" alt="Step_Counts"></center>

The peak locations and count is what one might expect when looking at the signal with a human eye. It is also interesting to point out that the peak acceleration value alternates cyclically, in what would appear to be a difference between a step taken with the left foot (watch side) and a step taken with the right foot (opposite of watch side). The step count also matches what was counted during data collection.

### Step Counting with Altered Arm Position

I also wanted to test that my algorithm could correctly count steps when the arms are not freely swinging by the sides. To test it, I recorded another session of walking, during which an object was held in the "watch" arm, and the elbow was bent at approximately 90 degrees. The raw data is shown below.

<center><img src="https://live.staticflickr.com/65535/49156468832_f59ab9b239_n.jpg" width="320" height="228" alt="Raw_Data_ArmBent"></center>

As you can see, the raw values of the signal have changed drastically for the X and Y axes. Additionally, the cyclic nature of walking is more clearly shown in the X-axis signal, whereas in the other samples, the Y-axis signal displayed the steps more clearly. However, because the algorithm focuses on the vector sum signal, steps were accurately identified and counted under these circumstances as well:

<center><img src="https://live.staticflickr.com/65535/49156468917_d4b371e10a_n.jpg" width="320" height="230" alt="Filter_Vector_Sum_ArmBent"><img src="https://live.staticflickr.com/65535/49155761338_b67a0837cf_n.jpg" width="320" height="223" alt="Steps_ArmBent"></center>

### Rest State Identification

Another feature I wanted to demonstrate was identification of intervals when the "watch" is being looked at by the user. I recorded some ~30 second-long intervals of alternating between "resting" (device not being looked at) and "reading" (device being looked at). The raw signal is shown below.

<center><img src="https://live.staticflickr.com/65535/49156410981_ea420b6e67_n.jpg" width="320" height="226" alt="RawData_PeriodicLift"></center>

The states of resting and reading are most clearly shown in the X-axis data. This makes sense, as when the wrist is in the position to read from the position of a watch face, the x-axis of the accelerometer is parallel to the world z-axis. After again applying a low-pass filter, and defining the transition to an "on" state as the value of the x-axis acceleration approaching -9.8 m/s^2, I was able to categorize the state as expected. Shown below in red is the state, where 0 if "off"/"resting" and 1 is "on"/"reading".

<center><img src="https://live.staticflickr.com/65535/49156468797_c28aa85541_n.jpg" width="320" height="207" alt="Screen_Lit_State"></center>

This is an ongoing project in which I hope to explore both improvements to the algorithms used and additional functionality.

[GitHub Repo](https://github.com/mmeyer95/Smartwatch)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
