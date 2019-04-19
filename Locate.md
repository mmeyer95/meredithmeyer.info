---
layout: page
title: Localization of a Car Using a Particle Filter
permalink: /Locate
---

The project involved implementation of Particle Filter equations in C++ code. Particle filters use a set of initially randomized particles that each represent a potential location (x,y) and heading direction (theta). Based on the likelihood that the particle represents the localized object's true location, it is given a weight (essentiall a probability). The probability that a particle represents the truth is determined by sensor data (usually LiDAR or RADAR) of the direction distances to nearby object. Knowledge of the map space is required.

Implementation of a particle filter involves 4 basic steps:
1. Initialization
2. Measurement Update
3. Weights Update
4. Resampling

Initialization is completed once, while steps 2-4 are computed cyclically, once for each time step.

1. **Initialization**

    First, a set of particles needs to be created. One initial measurement is needed to initialize, as well as the number of particles. More particles means it's more likely that a particle will be at the right location, but it also slows down processing time, which is not ideal for real-time applications (like self-driving cars). I chose 100 particles for this project.

2. **Measurement Update**

3. **Weights Update**

4. **Resampling**
    
    Particles are resampled from the distribution of particles with weights calculated in step 3. The particles are modeled as a discrete distribution. Resampling will result with the same number of particles as initialized, but with more particles clustered around the points where the car is most likely located.

A simulator was used to help visualize the filter and its performance. The green lines represent spacial data from the sensor of relative distances to nearby landmarks (the "x"s).See the filter in action:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/9hujlEV-CDU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub Repo](https://github.com/mmeyer95/Kidnapped_Vehicle)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
