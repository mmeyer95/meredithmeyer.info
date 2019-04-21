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

    The prediction step uses knowledge of the localized object's motion model in order to predict the next position. The motion model used for this project is of a constant yaw rate (AKA delta_theta) between time steps. In practice learning, a more simplified motion model was used, where heading direction is constant between time steps, like travelling only along spokes of a wheel. In a car, we are likely to have access to its current velocity (spedometer) and steering angle (internal mechanics). Therefore, this project is based on a motion model of constant velocity and delta theta (corresponding to steering angle) between time steps. The equations used to define new position and heading direction are:
    
    <center><img src="https://live.staticflickr.com/65535/32713252657_e4923fb27f_b.jpg" width="869" height="354" alt="motion"></center>
    
    The goal of particle filters is to find the particle that represents the vehicle's actual position. Therefore, whatever the car does, we assume each particle does as well. For the prediction step, I simple apply the same motion to each particle as the car performed.
    
3. **Measurement and Weights Update**

    At the time of the next measurement coming in, we can compare the predictions to the actual measurements. This involves some coordinate system conversions and Gaussian distributions. Since the new measurements are given in terms of distance from the car to a nearby landmark, we have to convert to the corresponding map coordinates for those measurements. The hypothesis for each particle is that it represents the true location of the car, so for each particle I converted the vector measurement originating from the car's coordinate system to the corresponding cartesian coordinate on the map. The coordinate conversion equations are:
    
    <center><img src="https://live.staticflickr.com/65535/46931923854_e688c58e5a_b.jpg" width="764" height="182" alt="Coordinate transform"></center>
    where subscript **c** corresponds to the **c**ar's sensor measurements, **p** to the **p**articles position, and **m** to the **m**ap coordinates. **Theta** is the angle of rotation between the particle's coordinate system and the map's coordinate system. Since the particle's heading direction is defined by the map's X axis, **theta** is the particle's heading direction.
    
    After determining the location of "sensed" landmarks on the map, we have to determine which real landmark was sensed. I did this using the **nearest neighbor** technique. Essentially, whatever landmark is closest to the sensed observation becomes paired to that measurement. For this project, the sensor range was taken into account, and landmarks outside of a 50 meter range were not considered for association to a measurement.
    
    After associating each measurement with a landmark, there is enough information to update the particle weights. Remember, a particle's weight represents the probability of that particle representing the car's actual location. The weight is calculated as the product of multivariate Gaussians. The number of factors is equal to the number of landmarks sensed. The multivariate Gaussian distributions determine the probability that a measurement value for a landmark would actually be sensed based on its distance from the true landmark in 2D space. Visualization of a multivariate Gaussian is shown below, where the most likely location is in the center (i.e. the landmarks actual location), and the probability decreases radially.
    
    <center><img src="https://live.staticflickr.com/65535/40689431453_8f4a633400.jpg" width="259" height="194" alt="gaussian"></center>
    
    The calculation of each probability was done as follows:
    
    <center><img src="https://live.staticflickr.com/65535/46931923484_1a9dd3ffe6_b.jpg" width="862" height="180" alt="Particle weight"></center>
    where **x** and **y** are the sensed locations, **μ** x & y are the actual locations, and **σ** are the standard deviations of the sensor in each axial direction. A particle's weight is the product of the above equation for each measurement.
    
4. **Resampling**
    
    Particles are resampled from the distribution of particles with weights calculated in step 3. The particles are modeled as a discrete distribution, and each particle's probability of being picked is directly related to its weight. Resampling will result with the same number of particles as initialized, but with more particles clustered around the points where the car is most likely located.

**Examples:**

For a simple particle filter with constant heading direction and low standard deviation, the "car's" position is located in one iteration of the filter.

<center><img src="https://live.staticflickr.com/65535/40689318473_f366e6837f.jpg" width="500" height="316" alt="1000world_10000parts_init_low_noise"><img src="https://live.staticflickr.com/65535/40689318423_cba2c41123.jpg" width="500" height="322" alt="1000world_10000parts_low_noise_1itr"></center>
<center>(The blue "X" represents the car, red "*"s the particles, and green *^*s the landmarks)</center>

If the standard deviation of measurements is high (representing a low precision sensor), a particle filter cannot do as good of a job with pinpointing location, but can still find the general area. After 5 iterations of the filter for high standard deviation, we get something like this:

<center><img src="https://live.staticflickr.com/65535/40689318123_034d0f76c7.jpg" width="500" height="326" alt="lots_of_noise_100"></center>

If the moves are large (representing an incredible fast vehicle, or low sampling rate sensor), the particle filter can lose track of the vehicle after it's already been located:

<center><img src="https://live.staticflickr.com/65535/46931923834_86ff6dcf9a.jpg" width="500" height="319" alt="Big_moves_lose_track"></center>

It takes multiple iterations for the particles' heading directions to converge to that of the car. Another phenomenon to note is that with greater numbers of landmarks, the particle filter is also less likely to be accurate. Two processes lead to this. First, with nearest neighbor association, the sensor measurement is not always paired to the correct landmark. Secondly, and closely related, the more landmarks there are, the more likely another landmark is nearby that could instead be associated with a measurement. You can see the many landmark hinders localization:

<center><img src="https://live.staticflickr.com/65535/40689318233_4815bc012c.jpg" width="500" height="311" alt="lots_of_landmarks_and_noise">></center>
    
For this project, I used a provided simulator to help visualize the filter and evaluate its performance. The green lines represent spacial data from the sensor of relative distances to nearby landmarks (the "x"s).See the filter in action:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/9hujlEV-CDU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub Repo](https://github.com/mmeyer95/Kidnapped_Vehicle)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
