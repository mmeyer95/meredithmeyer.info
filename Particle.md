---
layout: page
title: Localization of a Car Using a Particle Filter
permalink: /Locate
---

The project involved implementation of Particle Filter equations in C++ code. Particle filters use a set of initially randomized particles that each represent a potential location (x,y) and heading direction (theta). Based on the likelihood that the particle represents the localized object's true location, it is given a weight (essentiall a probability). The probability that a particle represents the truth is determined by sensor data (usually LiDAR or RADAR) of the direction distances to nearby object. Knowledge of the map space is required.

Implementation of a particle filter involves 4 basic steps:
1. Initialization
2. Measurement update
3. Weight update
4. Resampling

A simulator was used to help visualize the filter and its performance. The green lines represent spacial data from the sensor of relative distances to nearby landmarks (the "x"s).See the filter in action:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/9hujlEV-CDU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub Repo](https://github.com/mmeyer95/Kidnapped_Vehicle)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
