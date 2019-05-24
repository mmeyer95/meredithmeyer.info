---
layout: page
title: Behavior Planning & Trajectory Generation
permalink: /trajectory/
---
The goal of this project was to safely navigate a 3-lane highway in simulation, without colliding with other cars or exceeding the speed limit of 50 mph. Lane changes should only be made when they are both safe and help the car progress through traffic. Acceleration should remain under 10 m/s^2, and jerk under 10 m/s^3. 

<center><img src="https://ibb.co/Hpg0dwL"></center>
<center>A screenshot of the simulator. Calculated trajectory points are shown in green.</center>

The process for successful implementation of a self-driving car consists of many steps happening at overlapping times, as displayed by the below graphic.

<center><img src="https://ibb.co/VwjgF01"></center>
<center>Diagram of process flow from Udacity.com</center>

Sensor fusion, localization, and motion control are each completed in a separate project. For this purposes of this project, these 3 steps are already accounted for.
Therefore, the main task of the project can be split into 3 parts: prediction, behavior planning, and trajectory generation. It was accomplished in C++.

### Prediction
Prediction uses sensor fusion data to identify nearby cars and predict where they will be in the future. For the prediction step, since the simulation is run on a highway, I did not have to account for turns. Also, for the purpose of this project I assumed I would not have to account for sudden stops. The sensor fusion data includes the cars' x and y positions, in map coordinate, as well as the x and y components of their velocities. I used simple kinematics to calculate a predicted position and velocity for the other cars on the road at a future time t. Since I pass 1 second of trajectory data to the simulator at a time, t is less than or equal to 1 second (depending on how much time passes between execution of the code). It was also helpful in this step to use a different coordinate system, s & d. 

The output of the prediction step is used in the next step, behavior planning.

### Behavior Planning
The goal of the behavior planning step for this project is the determination of a target lane (1, 2, or 3) and speed (<50 mph). 

Once I defined the presence of other cars, I decided on a move and car speed. A move to another lane was only allowed if the following conditions are met:
*There is another lane in that direction I can move to (the move wouldn’t pull me off the road or into opposing traffic)
*There is no car in that lane OR the car in that lane is moving faster than the car in my lane, and it is at least 20 m away from me

<center><img src="https://ibb.co/bm1FvMK"></center>

Red spaces in the above graphic indicate positions of neighboring cars which would make a left or right lane shift not allowed. The target speed is ideally that of either: the car in front of me, or the maximum speed allowed. However, to avoid sudden large accels or decels, I only incremented the velocity, rather than setting it to the nearby car’s speed immediately.

### Trajectory Generation
After determining a behavior as a goal lane and move speed, the trajectory generation step determines the actual X & Y values for the trajectory of the car. To do so, I:

1. Find 5 points that the car will visit as it travels down the road towards its goal position
2. Define the 5 points in relative time and extrapolate those points with a spline function
3. Send the simulator the x & y points for each time step of 0.02 seconds

These steps are described below.

1. The 5 points used as car visit points consist of 2 previous points and 3 future points. The previous points are the last x & y points from the previous path, if there are unprocessed points. If there is no previous path, likely just at the start of the simulator, the previous points are the car’s current x & y plus one point behind the car’s current s value, in the same lane. The 3 future x & y points I defined as 30, 60, and 90 meters down the road in the middle of the target lane.
2. The timing of the previous 2 points in straight-forward. The most recent point is time 0, while one step prior is -0.02 second, since each trajectory point is always 0.02 seconds apart. The timing of the next 3 points must be based upon the car’s commanded velocity. I calculate the time stamp from the distance between the two points and the velocity at which the car should be travelling, based on: Time = Distance/ Speed. With all visit points defined, I calculated 2 splines: one for x vs. time, one for y vs. time.
3. Finally, I send the x & y points to the simulator. First, I fill the vectors with any remaining, un-processed points from the previous move. I always send the simulator 1 second, or 50 points, of data. Therefore, any open spots after the remaining points are added I fill with points from the splines calculated in step 2

You can see from the screenshots that the car decides to switch lanes when it makes sense.
<center><img src="https://ibb.co/xMR47Qr"><img src="https://ibb.co/ZLTFY8F"></center>

[GitHub Repo](https://github.com/mmeyer95/Highway_Driving)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
