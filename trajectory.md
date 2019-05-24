---
layout: page
title: Behavior Planning & Trajectory Generation
permalink: /trajectory/
---
The goal of this project was to safely navigate a 3-lane highway in simulation, without colliding with other cars or exceeding the speed limit of 50 mph. Lane changes should only be made when they are both safe and help the car progress through traffic. Acceleration should remain under 10 m/s^2, and jerk under 10 m/s^3. The main task of the project can be split into 2 parts: behavior planning, and trajectory generation.

### Behavior Planning
The output of my behavior planning step was the determination of a target lane (1, 2, or 3) and speed (<50 mph). Breaking this down into 2 steps, behavior planning involved polling for and determining nearby object (i.e. Sensor Fusion), and deciding on a move. 
Using the sensor fusion data, I decided whether a car would be present in any of the 3 lanes within a target area at the end of this move. I also kept track of the closest car to the ego car in each of the lanes: its velocity, and its relative distance to my travel. Below is a graphic defining positions where vehicles are found in a lane (colored blocks), and their distance to the ego car at the end of the move (in meters).

Once I defined the presence of other cars, I decided on a move and car speed. A move to another lane was only allowed if the following conditions are met:
*There is another lane in that direction I can move to (the move wouldn’t pull me off the road or into opposing traffic)
*There is no car in that lane OR the car in that lane is moving faster than the car in my lane, and it is at least 20 m away from me

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


[GitHub Repo](https://github.com/mmeyer95/Highway_Driving)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
