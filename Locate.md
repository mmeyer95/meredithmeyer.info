---
layout: page
title: Localization of a Car Using a Particle Filter
permalink: /Locate
---

The project involved implementation of Particle Filter equations in C++ code. Particle filters use a set of initially randomized particles that each represent a potential location (x,y) and heading direction (theta). Based on the likelihood that the particle represents the localized object's true location, it is given a weight (essentiall a probability). The probability that a particle represents the truth is determined by sensor data (usually LiDAR or RADAR) of the direction distances to nearby object. Knowledge of the map space is required.

Implementation of a particle filter involves 4 basic steps:
1. Initialization
2. Prediction
3. Measurement and Weights Update
4. Resampling

Initialization is completed once, while steps 2-4 are computed cyclically, once for each time step.

1. **Initialization**

    First, a set of particles needs to be created. The number of particles is key to initialization. More particles means it's more likely that a particle will be at the right location, but it also slows down processing time, which is not ideal for real-time applications (like self-driving cars). In the project, I initialized 100 particles based on a Gaussian distribution around the first measurement. Since we have one measurement to start with, which is realatively accurate (GPS), we do not need to have as many particles. In learning about particle filters, I practiced with using a small "world" and randomly initializing particles. You'll see what that looks like later.

2. **Prediction**

    The prediction step uses knowledge of the localized object's motion model in order to predict the next position. The motion model used for this project is of a constant yaw rate (AKA delta_theta) between time steps. In practice learning, a more simplified motion model was used: pick an angle from +x axis and travel a distance "X" in the direction, like travelling only along spokes of a wheel. In a car, we are likely to have access to its current velocity (spedometer) and steering angle (internal mechanics). Therefore, this project is based on a motion model of constant velocity and steering angle between time steps. The equations used to define new position and heading direction are:
    
    The goal of particle filters is to find the particle that represents the vehicle's actual position. Therefore, whatever the car does, we assume each particle does as well. For the prediction step, I simple apply the same motion to each particle as the car performed.
    
3. **Measurement and Weights Update**

    At the next measurement coming in, we can compare the predictions to the actual measurements. This involves some coordinate system conversions and Gaussian distributions.
    
4. **Resampling**
    
    Particles are resampled from the distribution of particles with weights calculated in step 3. The particles are modeled as a discrete distribution. Resampling will result with the same number of particles as initialized, but with more particles clustered around the points where the car is most likely located.

A simulator was used to help visualize the filter and its performance. The green lines represent spacial data from the sensor of relative distances to nearby landmarks (the "x"s).See the filter in action:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/9hujlEV-CDU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub Repo](https://github.com/mmeyer95/Kidnapped_Vehicle)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
